- [【Apollo自动驾驶源码解读】车道线的感知和高精地图融合 - 铃灵狗 - 博客园 (cnblogs.com)](https://www.cnblogs.com/linglingdog/p/15990056.html)

## 1 模式选择

在modules/map/relative_map/conf/relative_map_config.pb.txt文件中对模式进行修改：

```
lane_source: OFFLINE_GENERATED
```

存在两种模式：`OFFLINE_GENERATED 和 PERCPTION`
当使用前者时 高精地图和感知进行融合
使用后者时 只是用感知生成相对地图
本文只讨论前者

## 2 函数入口

文件路径：`modules/map/relative_map/navigation_lane.cc`
函数名：`ool NavigationLane::GeneratePath() `这个是重点分析的函数
下面进入这个函数

## 3 逻辑分析

在这里进行了模式检查：

```
if (config_.lane_source() == NavigationLaneConfig::OFFLINE_GENERATED && navigation_line_num > 0)
```

现在进入这个if中

```java
for (int i = 0; i < navigation_line_num; ++i) {
    auto current_navi_path = std::make_shared<NavigationPath>();
    auto *path = current_navi_path->mutable_path();
    if (ConvertNavigationLineToPath(i, path)) {
        current_navi_path->set_path_priority(
            navigation_info_.navigation_path(i).path_priority());
        navigation_path_list_.emplace_back(
            i, default_left_width_, default_right_width_, current_navi_path);
    }
}
```

这里根据导航数据对 navigation_path_list_ 进行了填充 接下来马上进行判断：

```
if (navigation_path_list_.empty()) {
      generate_path_on_perception_func();
      return true;
    }
```

如果没有数据 只能使用感知了
如果数据不为空 我们继续
这里对导航路线进行排序 还有设置当前车辆所在路径
其中 `current_navi_path_tuple_ `这个变量记录了当前车所在的道路的索引 **下面我们将这个变量称为当前车道**

```java
//根据车的方向 将导航路线从左到右排序
navigation_path_list_.sort(
    [](const NaviPathTuple &left, const NaviPathTuple &right) {
        double left_y = std::get<3>(left)->path().path_point(0).y();
        double right_y = std::get<3>(right)->path().path_point(0).y();
        return left_y > right_y;
    });

// Get which navigation path the vehicle is currently on.
double min_d = std::numeric_limits<double>::max();
for (const auto &navi_path_tuple : navigation_path_list_) {
    int current_line_index = std::get<0>(navi_path_tuple);
    ADEBUG << "Current navigation path index is: " << current_line_index;
    double current_d = std::numeric_limits<double>::max();
    auto item_iter = last_project_index_map_.find(current_line_index);
    if (item_iter != last_project_index_map_.end()) {
        current_d = item_iter->second.second;
    }
    if (current_d < min_d) {
        min_d = current_d;
        //设置当前车辆所在路径
        current_navi_path_tuple_ = navi_path_tuple;
    }
}
```

接下来 将**当前车道**进行融合 而不是将所有车道进行融合！

```
//融合感知和导航车道线
    // Merge current navigation path where the vehicle is located with perceived
    // lane markers.
    auto *path = std::get<3>(current_navi_path_tuple_)->mutable_path();
    MergeNavigationLineAndLaneMarker(std::get<0>(current_navi_path_tuple_),
                                     path);
```

进入融合函数

```
void NavigationLane::MergeNavigationLineAndLaneMarker(const int line_index, common::Path *const path) 
```

进入之后直接进行判断
如果点的数量少于2 则首先生成导航的车道线

```
if (path->path_point_size() < 2) {
    path->Clear();
    ConvertNavigationLineToPath(line_index, path);
  }
```

如果还是点的数量过少 那只能使用感知的了 并直接return 不用融合了

```java
//如果路径点还是小于2 则根据感知生成导航车道线
// If the size of "path" points is still smaller than 2, just generate a
// navigation path based on perceived lane markers.
if (path->path_point_size() < 2) {
    path->Clear();
    ConvertLaneMarkerToPath(perception_obstacles_.lane_marker(), path);
    return;
}

common::Path lane_marker_path;
ConvertLaneMarkerToPath(perception_obstacles_.lane_marker(),
                        &lane_marker_path);

// If the size of lane marker path points is smaller than 2, merging is not
// required.
if (lane_marker_path.path_point_size() < 2) {
    return;
}
```

下面进行融合

前提是只对当前车道进行车道线的融合 因为传入的就只是当前车道

融合原理大概是预先设置一个权重 目前感觉这个权重应该是不变的 这里存个疑

然后遍历导航中这条线每个点 在导航中找到这个点对应的点 根据权重进行融合

代码展示

```java
int lane_marker_index = 0;
double navigation_line_weight = 1.0 - config_.lane_marker_weight();
for (int i = 0; i < path->path_point_size(); ++i) {
    auto *point = path->mutable_path_point(i);
    double s = point->s();
    //计算s距离之后的匹配点 并返回匹配点的索引
    //lane_marker_path为感知发来的道路
    auto lane_maker_point = GetPathPointByS(lane_marker_path, lane_marker_index,
                                            s, &lane_marker_index);
    // For the beginning and ending portions of a navigation path beyond the
    // perceived path, only the y-coordinates in the FLU coordinate system are
    // used for merging.
    const int marker_size = lane_marker_path.path_point_size();
    if (lane_marker_index < 0 || lane_marker_index > (marker_size - 1)) {
        point->set_y(navigation_line_weight * point->y() +
                     (1 - navigation_line_weight) * lane_maker_point.y());
        lane_marker_index = 0;
        continue;
    }
    *point = common::util::GetWeightedAverageOfTwoPathPoints(
        *point, lane_maker_point, navigation_line_weight,
        1 - navigation_line_weight);
}
```

然后回到之前的函数

下面就是各种设置宽度了

先提取了感知的道路宽度

遍历导航中所有的道路（这里不仅仅是处理当前道路）

如果遍历到了当前道路 就设置为感知到的道路宽度

代码展示

```java
//设置导航道路的宽度
// Set the width for the navigation path which the vehicle is currently on.
//注意感知车道线宽度是在这里储存的
double left_width = perceived_left_width_ > 0.0 ? perceived_left_width_
    : default_left_width_;
double right_width = perceived_right_width_ > 0.0 ? perceived_right_width_
    : default_right_width_;
if (!IsFloatEqual(left_width, default_left_width_) &&
    !IsFloatEqual(right_width, default_right_width_)) {
    left_width = left_width > default_left_width_ ? left_width - min_d
        : left_width + min_d;
    right_width = right_width > default_right_width_ ? right_width - min_d
        : right_width + min_d;
}

ADEBUG << "The left width of current lane is: " << left_width
    << " and the right width of current lane is: " << right_width;

std::get<1>(current_navi_path_tuple_) = left_width;
std::get<2>(current_navi_path_tuple_) = right_width;
auto curr_navi_path_iter = std::find_if(
    std::begin(navigation_path_list_), std::end(navigation_path_list_),
    [this](const NaviPathTuple &item) {
        return std::get<0>(item) == std::get<0>(current_navi_path_tuple_);
    });
if (curr_navi_path_iter != std::end(navigation_path_list_)) {
    std::get<1>(*curr_navi_path_iter) = left_width;
    std::get<2>(*curr_navi_path_iter) = right_width;
}
// Set the width between each navigation path and its adjacent path.
// The reason for using average of multiple points is to prevent too much
// interference from a singularity.
// If current navigation path is the path which the vehicle is currently
// on, the current lane width uses the perceived width.
//设置每个导航路径与其相邻路径之间的宽度。
//使用多个点的平均值是为了防止奇点产生过多干扰。
//如果当前导航路径是车辆当前所在的路径，则当前车道宽度使用感知宽度。
int average_point_size = 5;
for (auto iter = navigation_path_list_.begin();
     iter != navigation_path_list_.end(); ++iter) {
    const auto &curr_path = std::get<3>(*iter)->path();

    // Left neighbor
    auto prev_iter = std::prev(iter);
    if (prev_iter != navigation_path_list_.end()) {
        const auto &prev_path = std::get<3>(*prev_iter)->path();
        average_point_size = std::min(
            average_point_size,
            std::min(curr_path.path_point_size(), prev_path.path_point_size()));
        double lateral_distance_sum = 0.0;
        for (int i = 0; i < average_point_size; ++i) {
            lateral_distance_sum +=
                fabs(curr_path.path_point(i).y() - prev_path.path_point(i).y());
        }
        double width = lateral_distance_sum /
            static_cast<double>(average_point_size) / 2.0;
        width = common::math::Clamp(width, config_.min_lane_half_width(),
                                    config_.max_lane_half_width());

        auto &curr_left_width = std::get<1>(*iter);
        auto &prev_right_width = std::get<2>(*prev_iter);
        if (std::get<0>(*iter) == std::get<0>(current_navi_path_tuple_)) {
            prev_right_width = 2.0 * width - curr_left_width;
        } else {
            curr_left_width = width;
            prev_right_width = width;
        }
    }
    // Right neighbor
    auto next_iter = std::next(iter);
    if (next_iter != navigation_path_list_.end()) {
        const auto &next_path = std::get<3>(*next_iter)->path();
        average_point_size = std::min(
            average_point_size,
            std::min(curr_path.path_point_size(), next_path.path_point_size()));
        double lateral_distance_sum = 0.0;
        for (int i = 0; i < average_point_size; ++i) {
            lateral_distance_sum +=
                fabs(curr_path.path_point(i).y() - next_path.path_point(i).y());
        }
        double width = lateral_distance_sum /
            static_cast<double>(average_point_size) / 2.0;
        width = common::math::Clamp(width, config_.min_lane_half_width(),
                                    config_.max_lane_half_width());

        auto &curr_right_width = std::get<2>(*iter);
        auto &next_left_width = std::get<1>(*next_iter);
        if (std::get<0>(*iter) == std::get<0>(current_navi_path_tuple_)) {
            next_left_width = 2.0 * width - curr_right_width;
        } else {
            next_left_width = width;
            curr_right_width = width;
        }
    }
```

## 4 总结

如果权重是动态变化的还请大家评论纠正我
感觉apollo的车道线也就是高精地图和感知通过权重进行融合 没有很特别很精妙的算法 