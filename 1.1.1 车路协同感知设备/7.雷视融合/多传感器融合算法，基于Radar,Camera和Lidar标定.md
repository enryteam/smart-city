- [多传感器融合算法，基于Radar,Camera和Lidar标定](https://blog.csdn.net/nh54zyt/article/details/112134514)

传感器设备的标定
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/1ef8ce5499d942c286eee98f03caed95.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_18,color_FFFFFF,t_70,g_se,x_16#pic_center)

## 1：单目标定

单目标定opencv不稳定,matlab更好
 Ubuntu下matlab安装方法
 https://blog.csdn.net/m0_38087936/article/details/103342731
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104162847959.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104162847822.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104162847765.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)

但是得注意参数：

```cpp
cameraParams.IntrinsicMatrix:
3293.35909906506 fc1	0	0
-4.35172616366572	3293.54167494101fc2	0
1537.90640626082 vo	1049.28114385394 v1	1


cameraParams.RadialDistortion:  k1 k2 k5
-0.0777901104375618	0.174514579680910	-0.0774194053626076


cameraParams.TangentialDistortion:  k3 k4
-0.000207967884843062	-0.00215186224296790
在使用opencv中的undistort进行畸变矫正时，需要使用8个参数即fc1, fc2, cc1, cc2, kc1, kc2, kc3, kc4;
RadialDistorion中的参数分别是：kc1,kc2,kc5(不常用)
TangentialDistortion中的参数分别是：kc3,kc4
IntrinsicMatrix中的参数分别是：
fc1 不用 0
不用 fc2 0
cc1 cc2 1
opencv的畸变矫正程序如下：
double fc1, fc2, cc1, cc2, kc1, kc2, kc3, kc4;
fc1 = ;
fc2 = ;
cc1 = ;
cc2 = ;
kc1 = ;
kc2 = ;
kc3 =;
kc4 =;
Mat intrinsic_matrix = (Mat_(3, 3) << fc1, 0, cc1, 0, fc2, cc2, 0, 0, 1);
Mat distortion_coeffs = (Mat_(1, 4) << kc1, kc2, kc3, kc4);
```

## 2：双目标定

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104163359574.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104163359874.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104163359483.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 经过双目标定得到摄像头的各项参数后，
 采用OpenCV中的stereoRectify(立体校正)得到校正旋转矩阵R、投影矩阵P、重投影矩阵Q，
 再采用initUndistortRectifyMap函数得出校准映射参数，然后用remap来校准输入的左右图像。

双目标定参考文档（英文）：https://ww2.mathworks.cn/help/vision/ug/stereo-camera-calibrator-app.html

## 3：单目与Radar毫米波标定

**方法一：**![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302190113886.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

> 方法一：以图像坐标系为准，根据投影点图像像素坐标和前方车辆的宽度、距离信息在 图像上建立感兴趣区域ROI。
>
> 方法二：以毫米波雷达坐标系为准，将摄像头坐标系进行旋转和平移，并与毫米波雷达坐标系对齐。对摄像头的原始图像进行逆透视变换时，选取的地面特征点均以毫米波雷达为原点，并测量其在世界坐标系（毫米波雷达坐标系）下的坐标。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104150002277.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104150002155.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 **方法二：**![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104150024346.gif#pic_center)
 https://blog.csdn.net/leonardohaig/article/details/88724365
 **方法三：**![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104112404150.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)
 **方法四：**
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210325105947800.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210325105900726.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210325110141184.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

> 水平摆放https://blog.csdn.net/weixin_42631693/article/details/90042530
>
> 倾斜摆放
>  Radar坐标系俯仰角和偏航角到世界坐标系转换
>  [Radar](https://blog.csdn.net/leonardohaig/article/details/88724365)

## 4：Lidar与Radar标定![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104145923670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104145923655.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)

radar lidar camera分别检测跟踪，融合跟踪
 [radar_lidar](https://github.com/JunshengFu/tracking-with-Extended-Kalman-Filter)

## 5：同步

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302164845573.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302164845562.png)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302190355127.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

## 6：ADAS radar和camera

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302191359686.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302191359646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)

可以简单的将车作为中间变量

> 即求Radar到Car，Camera到Car

那么Radar到Car：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302190825756.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)
 那么Car到camera：

> 方法：
>  利用世界坐标系中的一系列的已知的点相对车体坐标系的三维点
>  及YXZ三维坐标（距离Car圆心）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302191754911.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

整体的公式如下：![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302191002747.png#pic_center)

|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||

## 方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/55e77ff86383403997551d5d0009d69e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_18,color_FFFFFF,t_70,g_se,x_16#pic_center)

## 7： PNP

如下5种PNP求解方法：
 https://www.cnblogs.com/yepeichu/p/12670818.html
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/055930d18d334b9fa8ec569a314f7208.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

例如求激光和图像标定外参

https://blog.csdn.net/qq_37394634/article/details/104430656
 直接法：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/6ab256f7b06643848278c466bd15292a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/e8dee4497d6a4ab09faf87a1e598a57b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/f247e3c772a643f39c222642dd1e2c0b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_17,color_FFFFFF,t_70,g_se,x_16#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/100a006a6316416fb476945055f4a64f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_13,color_FFFFFF,t_70,g_se,x_16#pic_center)
 例如，如下代码：

先使用OpenCV的solvePnP()求解出运动，
 然后再使用高斯牛顿法进行BA优化。

```cpp
#include<iostream>
#include "common.h"
#include <Eigen/Core>
#include <g2o/core/base_vertex.h>
#include <g2o/core/base_unary_edge.h>
#include <g2o/core/block_solver.h>
#include <g2o/core/optimization_algorithm_levenberg.h>
#include <g2o/solvers/csparse/linear_solver_csparse.h>
#include <g2o/types/sba/types_six_dof_expmap.h>


// BA求解
void bundleAdjustment(vector<Point3f> points_3d, vector<Point2f> points_2d, const Mat &K, Mat &R, Mat &t);


/**
 * 本程序演示了PnP求解相机位姿,BA优化位姿与3D空间点坐标
 * @param argc
 * @param argv
 * @return
 */
int main(int argc, char **argv) {

    if (argc != 4) {
        cout << "usage: pose_estimation_3d2d img1 img2 depth1" << endl;
        return 1;
    }
    //-- 读取图像
    Mat img_1 = imread(argv[1], CV_LOAD_IMAGE_COLOR);
    Mat img_2 = imread(argv[2], CV_LOAD_IMAGE_COLOR);

    vector<KeyPoint> key_points_1, key_points_2;
    vector<DMatch> matches;
    find_feature_matches(img_1, img_2, key_points_1, key_points_2, matches);
    cout << "一共找到" << matches.size() << "组匹配点" << endl;

//    建立3D点,深度图为16位无符号,单通道
    Mat d1 = imread(argv[3], CV_LOAD_IMAGE_UNCHANGED);
    Mat_<double> K(3, 3);
    K << 520.9, 0, 325.1, 0, 521.0, 249.7, 0, 0, 1;
    vector<Point3f> pts_3d;
    vector<Point2f> pts_2d;
    for (auto &match : matches) {
        ushort d = d1.ptr<unsigned short>(int(key_points_1[match.queryIdx].pt.y))
        [int(key_points_1[match.queryIdx].pt.x)];
        if (d == 0)
            continue;
        double dd = d / 1000.0;
        Point2d p1 = pixel2cam(key_points_1[match.queryIdx].pt, K);
        pts_3d.push_back(Point3d(p1.x * dd, p1.y * dd, dd));
        pts_2d.push_back(key_points_2[match.trainIdx].pt);
    }
    cout << "3d-2d pairs: " << pts_3d.size() << endl;

    Mat r, t;
//    调用OpenCV的PnP求解
    solvePnP(pts_3d, pts_2d, K, Mat(), r, t, false, cv::SOLVEPNP_EPNP);
    Mat R;
//    通过罗德里格斯公式将旋转向量转为旋转矩阵
    cv::Rodrigues(r, R);
    cout << "R=\n" << R << endl;
    cout << "t=\n" << t << endl;
//    BA
    bundleAdjustment(pts_3d, pts_2d, K, R, t);
    return 0;
}


/**
 * BA求解
 * @param points_3d
 * @param points_2d
 * @param K
 * @param R
 * @param t
 */
void bundleAdjustment(vector<Point3f> points_3d, vector<Point2f> points_2d,
                      const Mat &K, Mat &R, Mat &t) {
//    初始化g2o,pose维度为6,landmark维度为3
    typedef g2o::BlockSolver<g2o::BlockSolverTraits<6, 3>> Block;
    Block::LinearSolverType *linearSolver = new g2o::LinearSolverCSparse<Block::PoseMatrixType>();
    auto *solver_ptr = new Block(linearSolver);
    auto *solver = new g2o::OptimizationAlgorithmLevenberg(solver_ptr);
    g2o::SparseOptimizer optimizer;
    optimizer.setAlgorithm(solver);

//    vertex
    auto *pose = new g2o::VertexSE3Expmap();
    Eigen::Matrix3d R_mat;
    R_mat << R.at<double>(0, 0), R.at<double>(0, 1), R.at<double>(0, 2),
            R.at<double>(1, 0), R.at<double>(1, 1), R.at<double>(1, 2),
            R.at<double>(2, 0), R.at<double>(2, 1), R.at<double>(2, 2);
    pose->setId(0);
    pose->setEstimate(g2o::SE3Quat(R_mat, Eigen::Vector3d(t.at<double>(0, 0), t.at<double>(1, 0), t.at<double>(2, 0))));
    optimizer.addVertex(pose);
//    landmarks
    int index = 1;
    for (const Point3f &p:points_3d) {
        auto *point = new g2o::VertexSBAPointXYZ();
        point->setId(index++);
        point->setEstimate(Eigen::Vector3d(p.x, p.y, p.z));
        point->setMarginalized(true);
        optimizer.addVertex(point);
    }

//    parameter: camera intrinsics
    g2o::CameraParameters *camera = new g2o::CameraParameters(
            K.at<double>(0, 0), Eigen::Vector2d(K.at<double>(0, 2), K.at<double>(1, 2)), 0);
    camera->setId(0);
    optimizer.addParameter(camera);

//    edges
    index = 1;
    for (const Point2f &p:points_2d) {
        auto *edge = new g2o::EdgeProjectXYZ2UV();
        edge->setId(index);
        edge->setVertex(0, dynamic_cast<g2o::VertexSBAPointXYZ *>(optimizer.vertex(index)));
        edge->setVertex(1, pose);
        edge->setMeasurement(Eigen::Vector2d(p.x, p.y));
        edge->setParameterId(0, 0);
        edge->setInformation(Eigen::Matrix2d::Identity());
        optimizer.addEdge(edge);
        index++;
    }

    auto t1 = chrono::steady_clock::now();
    optimizer.setVerbose(true);
    optimizer.initializeOptimization();
    optimizer.optimize(100);
    auto t2 = chrono::steady_clock::now();
    auto time_used = chrono::duration_cast<chrono::duration<double >>(t2 - t1);
    cout << "optimization costs time: " << time_used.count() << " seconds." << endl;
    cout << "\nafter optimization:\n" << "T=\n" << Eigen::Isometry3d(pose->estimate()).matrix() << endl;
}
```