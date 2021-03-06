## 1 功能简介

车头AI特征识别摄像机应用于地面道路、城市快速路、高速公路等各种道路，抓拍车头方向，采用深度学习算法，对场景中所有出现的车辆进行准确的检测后，运用基于深度学习的小目标检测算法检测车头的各类特征，具备车牌号码、车牌颜色、车身颜色、车辆品牌等车辆基本特征检测功能。

| 摄像机类型 | 支持型号 | 所属版本 | 最大分辨率 | 最大监测车道数 | 主要功能                                                     |
| ---------- | -------- | -------- | ---------- | -------------- | ------------------------------------------------------------ |
| 摄像机     |          |          | 900万像素  | 3车道          | 1卡口（车头）2遮阳板检测3细分车型检测4纸巾盒检测5挂饰检测6天窗检测7后视镜检测8前车灯检测9前雾灯检测 |

## 2 技术指标

针对该算法，当前规格指标情况如下，针对车辆检测及车牌检测：

| 类别     | 捕获率 | 检测准确率 | 场景使用条件                                                 |
| -------- | ------ | ---------- | ------------------------------------------------------------ |
| 号牌检测 | ≥99%   | ≥98%       | 1、 车牌像素水平方向不小于120像素点；2、 车牌倾斜角度小于5度3、 图像特征部分清晰度达到人工可分辨 |

针对该算法，各种AI特征检测精度在标准场景下的指标如下：

| 检测功能 | 检测准确率（标准场景下） |
| -------- | ------------------------ |
| 遮阳板   | 白天：≥95% 夜间：≥90%    |
| 细分车型 | 白天：≥90% 夜间：≥80%    |
| 纸巾盒   | 白天：≥80% 夜间：≥70%    |
| 挂饰     | 白天：≥85% 夜间：≥75%    |
| 天窗     | 白天：≥95% 夜间：≥90%    |
| 后视镜   | 白天：≥95% 夜间：≥90%    |
| 前车灯   | 白天：≥95% 夜间：≥90%    |
| 前雾灯   | 白天：≥95% 夜间：≥90%    |

