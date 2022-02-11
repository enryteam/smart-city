- [多传感器融合算法，基于Lidar,Radar,Camera算法](https://blog.csdn.net/nh54zyt/article/details/115294321)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302185219252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210329100413625.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

## 1：雷达Radar

#### **① 大陆ARS408 参数：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210408105434673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210408105329534.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210408105838630.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210408105602338.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

#### **② livox mid40 参数：**

mid-40的连接使用测试

https://blog.csdn.net/Summer_CX/article/details/116657887

## 2：传统方法融合算法

如apollo
 https://zhuanlan.zhihu.com/p/33852112
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302185933812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302185933768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302185933758.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20210302185407399.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25oNTR6eXQ=,size_16,color_FFFFFF,t_70#pic_center)

## 3：深度学习融合算法

如：
 CenterFusion
 https://arxiv.org/pdf/2011.04841.pdf
 ***难点：***
 为了实现这一点，一种简单的方法是将每个雷达探测点映射到图像平面，并将其与一个对象关联（如果该点映射到该对象的二维边界框内）。这不是一个非常可靠的解决方案，因为雷达探测和目标之间没有一对一的映射。

在图像中，场景中的许多对象生成多个雷达检测，也有一些雷达检测与任何对象都不对应。另外，由于雷达检测的z维不精确（或根本不存在），映射雷达检测可能会在其对应对象的2D边界框之外结束。最后，被遮挡目标的雷达检测将映射到图像中的同一个区域，这使得在二维图像平面上区分它们变得困难。

## 4：多相机的融合，长短焦/双目相机融合

相机到相机标定

基本方法：

根据长焦相机投影到短焦相机的融合图像进行判断，绿色通道为短焦相机图像，红色和蓝色通道是长焦投影后的图像，目视判断检验对齐情况。在融合图像中的融合区域，选择场景中距离较远处（50米以外）的景物进行对齐判断，能够重合则精度高，出现粉色或绿色重影（错位），则存在误差，当误差大于一定范围时（范围依据实际使用情况而定），标定失败，需重新标定（正常情况下，近处物体因受视差影响，在水平方向存在错位，且距离越近错位量越大，此为正常现象。垂直方向不受视差影响）。

结果示例：如下图所示，图2为满足精度要求外参效果，图3为不满足精度要求的现象，请重新进行标定过程。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/2aed76885c974194a03965e79d77fa1d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_11,color_FFFFFF,t_70,g_se,x_16#pic_center)

#### 双目标定RT求解环节，长短焦标定：

最近在做多相机图像拼接，可以将多相机分为多个双目相机来拼接，这里记录一下双目相机标定的一些原理。

基于标定板的两个相机的标定，是基于特征点平面情况。

如图为双目相机与标定板之间的关系。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/12585521a6df4035a05a7ea055ef4c52.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_20,color_FFFFFF,t_70,g_se,x_16)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/7e0f3631e02f49509e17949393db1ce3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_15,color_FFFFFF,t_70,g_se,x_16#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/275f6d20ad124403b8eb5cd1a18a6c7b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_15,color_FFFFFF,t_70,g_se,x_16#pic_center)
 由上关系：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/47f401a24b1f4dc59eda497cd9557612.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

##### 双目之间的位姿（长焦和短焦之间的位姿）：

![在这里插入图片描述](https://img-blog.csdnimg.cn/040b30cfa1724b8ca120cc5dd5a11e1d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_17,color_FFFFFF,t_70,g_se,x_16#pic_center)

视觉slam求位姿：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/6afa19781d5f42d99a15363de54f328a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_17,color_FFFFFF,t_70,g_se,x_16#pic_center)
 基础矩阵和本质矩阵都是3×3的矩阵，它们之间不过是差了个相机内参，因此使用时效果完全一样。

```cpp
void pose_estimation_2d2d ( std::vector<KeyPoint> keypoints_1,
                            std::vector<KeyPoint> keypoints_2,
                            std::vector< DMatch > matches,
                            Mat& R, Mat& t )
{
    // 相机内参,TUM Freiburg2
    Mat K = ( Mat_<double> ( 3,3 ) << 520.9, 0, 325.1, 0, 521.0, 249.7, 0, 0, 1 );

    //-- 把匹配点转换为vector<Point2f>的形式
    vector<Point2f> points1;
    vector<Point2f> points2;

    for ( int i = 0; i < ( int ) matches.size(); i++ )
    {
        points1.push_back ( keypoints_1[matches[i].queryIdx].pt );
        points2.push_back ( keypoints_2[matches[i].trainIdx].pt );
    }

    //-- 计算基础矩阵
    Mat fundamental_matrix;
    fundamental_matrix = findFundamentalMat ( points1, points2, CV_FM_8POINT );
    cout<<"fundamental_matrix is "<<endl<< fundamental_matrix<<endl;

    //-- 计算本质矩阵
    Point2d principal_point ( 325.1, 249.7 );   //相机光心, TUM dataset标定值
    double focal_length = 521;          //相机焦距, TUM dataset标定值
    Mat essential_matrix;
    essential_matrix = findEssentialMat ( points1, points2, focal_length, principal_point );
    cout<<"essential_matrix is "<<endl<< essential_matrix<<endl;

    //-- 计算单应矩阵
    Mat homography_matrix;
    homography_matrix = findHomography ( points1, points2, RANSAC, 3 );
    cout<<"homography_matrix is "<<endl<<homography_matrix<<endl;

    //-- 从本质矩阵中恢复旋转和平移信息.
    recoverPose ( essential_matrix, points1, points2, R, t, focal_length, principal_point );
    cout<<"R is "<<endl<<R<<endl;
    cout<<"t is "<<endl<<t<<endl;
    
}
```

————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

#### 单应性矩阵应用：

长焦和短焦摄像头的组合感知，

长焦小视场角远距离，短焦大视场角短距离。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b3d27d62ff4c4626b5aeabe39dd335f4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/ce96d5718edd40bd852436648bd31edf.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_14,color_FFFFFF,t_70,g_se,x_16#pic_center)
 例如：双目标定方法
 https://blog.csdn.net/plateros/article/details/102665505

可以由单应性矩阵求解出 旋转 平移关系：
 表示就是不同视角的相机的关系；
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/3db0015dfc874c24b3a9acc4f864932b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_15,color_FFFFFF,t_70,g_se,x_16#pic_center)

```cpp
#include <iostream>
#include <opencv2/core/core.hpp>
#include <opencv2/features2d/features2d.hpp>
#include <opencv2/highgui/highgui.hpp>
#include <opencv2/calib3d/calib3d.hpp>
// #include "extra.h" // use this if in OpenCV2 
using namespace std;//标准库　命名空间
using namespace cv; //opencv库命名空间
 
// ./pose_estimation_2d2d 1.png 2.png
/****************************************************
 * 本程序演示了如何使用2D-2D的特征匹配估计相机运动  
 * **************************************************/
//特征匹配 计算匹配点对
void find_feature_matches (
    const Mat& img_1, const Mat& img_2, // & 为引用  直接使用 参数本身 不进行复制  节省时间
    std::vector<KeyPoint>& keypoints_1,// 
    std::vector<KeyPoint>& keypoints_2,
    std::vector< DMatch >& matches );//keypoint Descriptors Match   描述子匹配
//位置估计 计算旋转和平移
void pose_estimation_2d2d (
    std::vector<KeyPoint> keypoints_1,
    std::vector<KeyPoint> keypoints_2,
    std::vector< DMatch > matches,
    Mat& R, Mat& t );
 
// 像素坐标转相机归一化坐标
Point2d pixel2cam ( const Point2d& p, const Mat& K );
 
int main ( int argc, char** argv )
{
    if ( argc != 3 )//命令行参数　 1.png 　2.png
    {
        cout<<"usage: pose_estimation_2d2d img1 img2"<<endl;
        return 1;
    }
    //-- 读取图像
    Mat img_1 = imread ( argv[1], CV_LOAD_IMAGE_COLOR );//彩色图模式
    Mat img_2 = imread ( argv[2], CV_LOAD_IMAGE_COLOR );
 
    vector<KeyPoint> keypoints_1, keypoints_2;//关键点
    vector<DMatch> matches;//特征点匹配对
    find_feature_matches ( img_1, img_2, keypoints_1, keypoints_2, matches );//得到匹配点对
    cout<<"一共找到了"<<matches.size() <<"组匹配点"<<endl;
 
    //-- 估计两张图像间运动
    Mat R,t;//旋转和平移 第一张图 到第二章图的坐标变换矩阵和平移矩阵
    pose_estimation_2d2d ( keypoints_1, keypoints_2, matches, R, t );
 
    //-- 验证E=t^R*scale    变叉乘 为 矩阵乘法   三阶行列式     
    // https://www.cnblogs.com/monoSLAM/p/5349497.html
    //  a   b   c 
    //  d  e    f     = bf - ce , cd - af , ae -bd  =  [0 - c  b; c 0 -a; -b a 0 ] * [ d e f]
    // 向量 t = [ a1 a2 a3] 其
    //  叉乘矩阵 = [0  -a3  a2;
    //                      a3  0  -a1; 
    //                     -a2 a1  0 ]  
    
    Mat t_x = ( Mat_<double> ( 3,3 ) << //t向量的 叉乘矩阵
                0,                      -t.at<double> ( 2,0 ),     t.at<double> ( 1,0 ),
                t.at<double> ( 2,0 ),      0,                      -t.at<double> ( 0,0 ),
                -t.at<double> ( 1.0 ),     t.at<double> ( 0,0 ),      0 );
 
    cout<<"本质矩阵E = t^R= t叉乘矩阵 * R = "<<endl<<t_x*R<<endl;
 
    //-- 验证对极约束
    //相机内参数
    //   [fx 0 cx
    //     0 fy cy
    //     0 0  1]
    Mat K = ( Mat_<double> ( 3,3 ) << 520.9, 0, 325.1, 0, 521.0, 249.7, 0, 0, 1 );// 相机内参,TUM Freiburg2
    for ( DMatch m: matches )//Descriptors Match   描述子匹配
    {
        Point2d pt1 = pixel2cam ( keypoints_1[ m.queryIdx ].pt, K );//像素坐标转相机归一化坐标    x1 =  K逆* p1  x2 =  K逆* p2  相机坐标系下 归一化平面上的点 
        Mat y1 = ( Mat_<double> ( 3,1 ) << pt1.x, pt1.y, 1 );// 归一化平面上的点 齐次表示
        Point2d pt2 = pixel2cam ( keypoints_2[ m.trainIdx ].pt, K );
        Mat y2 = ( Mat_<double> ( 3,1 ) << pt2.x, pt2.y, 1 );
        Mat d = y2.t() * t_x * R * y1;//理论上为 0 
        cout << "epipolar constraint = " << d << endl;
    }
    return 0;
}
 
 
//特征匹配 计算匹配点对 函数
void find_feature_matches ( const Mat& img_1, const Mat& img_2,
                            std::vector<KeyPoint>& keypoints_1,
                            std::vector<KeyPoint>& keypoints_2,
                            std::vector< DMatch >& matches )
{
    //--------------------第0部初始化------------------------------------------------------
    Mat descriptors_1, descriptors_2;//描述子
    //  OpenCV3 特征点检测器  描述子生成器 用法
    Ptr<FeatureDetector> detector = ORB::create();         //特征点检测器    其他 BRISK   FREAK   
    Ptr<DescriptorExtractor> descriptor = ORB::create();//描述子生成器
    // OpenCV2 特征点检测器  描述子生成器 用法
    // Ptr<FeatureDetector> detector = FeatureDetector::create ( "ORB" );
    // Ptr<DescriptorExtractor> descriptor = DescriptorExtractor::create ( "ORB" );
    Ptr<DescriptorMatcher> matcher  = DescriptorMatcher::create ( "BruteForce-Hamming" );//二进制描述子 汉明点对匹配
    
    //------------------第一步:检测 Oriented FAST 角点位置-----------------------------
    detector->detect ( img_1,keypoints_1 );
    detector->detect ( img_2,keypoints_2 );
 
    //------------------第二步:根据角点位置计算 BRIEF 描述子-------------------------
    descriptor->compute ( img_1, keypoints_1, descriptors_1 );
    descriptor->compute ( img_2, keypoints_2, descriptors_2 );
 
    //------------------第三步:对两幅图像中的BRIEF描述子进行匹配，使用 Hamming 距离
    vector<DMatch> match;//Descriptors Match   描述子匹配
    //BFMatcher matcher ( NORM_HAMMING );
    matcher->match ( descriptors_1, descriptors_2, match );//各个特征点描述子之间的汉明距离匹配
 
    //-----------------第四步:匹配点对筛选--------------------------------------------------
    double min_dist=10000, max_dist=0;
    //找出所有匹配之间的最小距离和最大距离, 即是最相似的和最不相似的两组点之间的距离
    for ( int i = 0; i < descriptors_1.rows; i++ )
    {
        double dist = matches[i].distance;
        if ( dist < min_dist ) min_dist = dist;  //最短距离  最相似
        if ( dist > max_dist ) max_dist = dist; //最长距离 最不相似
    }
    printf ( "-- Max dist : %f \n", max_dist );
    printf ( "-- Min dist : %f \n", min_dist );
    //当描述子之间的距离大于两倍的最小距离时,即认为匹配有误.但有时候最小距离会非常小,设置一个经验值30作为下限.
    for ( int i = 0; i < descriptors_1.rows; i++ )
    {
        if ( match[i].distance <= max ( 2*min_dist, 30.0 ) )//最大距离
        {
            matches.push_back ( match[i] );
        }
    }
}
 
// 像素坐标转相机归一化坐标
// 像素坐标转相机归一化坐标    x1 =  K逆* p1  x2 =  K逆* p2  相机坐标系下 归一化平面上的点 
Point2d pixel2cam ( const Point2d& p, const Mat& K )
{
    return Point2d
           (
               ( p.x - K.at<double> ( 0,2 ) ) / K.at<double> ( 0,0 ),// x= (px -cx)/fx
               ( p.y - K.at<double> ( 1,2 ) ) / K.at<double> ( 1,1 )//  y=(py-cy)/fy
           );
}
 
//特征匹配 计算匹配点对 函数   第一张图 到第二章图的坐标变换矩阵和平移矩阵
//对极几何
void pose_estimation_2d2d ( std::vector<KeyPoint> keypoints_1,
                            std::vector<KeyPoint> keypoints_2,
                            std::vector< DMatch > matches,
                            Mat& R, Mat& t )
{
    // 相机内参,TUM Freiburg2
     //相机内参数
    //   [fx 0 cx
    //     0 fy cy
    //     0 0  1]
    Mat K = ( Mat_<double> ( 3,3 ) << 520.9, 0, 325.1, 0, 521.0, 249.7, 0, 0, 1 );
 
    //------------把匹配点转换为vector<Point2f>的形式------------------
    vector<Point2f> points1;
    vector<Point2f> points2;
    for ( int i = 0; i < ( int ) matches.size(); i++ )
    {
        points1.push_back ( keypoints_1[matches[i].queryIdx].pt );
        points2.push_back ( keypoints_2[matches[i].trainIdx].pt );
    }
 
    //-----------计算基础矩阵 F    p2转置*F*p1 = 0   -----------------------------------------------------
    Mat fundamental_matrix;
    fundamental_matrix = findFundamentalMat ( points1, points2, CV_FM_8POINT );//8点发    p2转置*F*p1 = 0 
    cout<<"基础矩阵 fundamental_matrix is "<<endl<< fundamental_matrix<<endl;
 
    //-----------计算本质矩阵 E   x2转置 * E * x1 = 0  ----------------------------------------------------
    Point2d principal_point ( 325.1, 249.7 );	//相机光心, TUM dataset标定值   cx    cy
    double focal_length = 521;			//相机焦距, TUM dataset标定值  fx     fy
    Mat essential_matrix;
    essential_matrix = findEssentialMat ( points1, points2, focal_length, principal_point );// x2转置 * E * x1 = 0  
    cout<<"本质矩阵 essential_matrix is "<<endl<< essential_matrix<<endl;
 
    //-----------计算单应矩阵H    p2 = H *p1  ---------------------------------------------------
    Mat homography_matrix;
    homography_matrix = findHomography ( points1, points2, RANSAC, 3 );
    cout<<"单应矩阵 homography_matrix is "<<endl<<homography_matrix<<endl;
 
    //-- 从本质矩阵中恢复旋转和平移信息. 使用奇异值分解法得到
    recoverPose ( essential_matrix, points1, points2, R, t, focal_length, principal_point );// E = t^R = U C  V   ,U   V 为正交矩阵   C 为奇异值矩阵 C =  diag(1, 1, 0)
    cout<<"R is "<<endl<<R<<endl;
    cout<<"t is "<<endl<<t<<endl;
    
}
```

基本矩阵
 　　什么是基础矩阵？Fundamental matrix
 　　　　基础矩阵，在不同视角下的图像的对应关系，是单应矩阵的一个特例
 单应矩阵
 　　
 　　　　http://blog.itpub.net/31562045/viewspace-2220170/
 　　什么是单应矩阵呢？Homography matrix
 　　
 　　　　同一个平面的点，在不同图像之间的关系
 　　　　这种关系不一定是同一物体，不同视角下的关系。比如我们举例的银行卡
 　　　　但是 我们一般在介绍的时候，都是在说在不同视角下的图像的对应关系，这个时候和基本矩阵的关系是对应的
 　　举例说明
 　　　　银行卡拍摄的时候，可能会有倾斜，这个时候进行数字识别，准确率可能会低
 　　　　经过单应矩阵变换后，将其摆正，然后就有比较高的准确率了。
 　　　　不仅仅是倾斜的银行卡上面某一个点和摆正后的银行卡对应点上，满足单应矩阵的关系；
 　　　　而是倾斜银行卡上面所有点和摆正后的银行卡上所有点都满足单应矩阵关系
 　　　　这里就体现了同一个平面，不同图像之间的观点

至于基础矩阵，实质上是同一个东西，不同的是，本质矩阵的引入是方便利用点P相对于相机坐标系的位置来求解位姿变换矩阵，而基础矩阵的引入是方便利用像素点的位置来求解位姿变换矩阵。点P的绝对坐标和像素点的位置通过相机固有参数联系起来。总结下过程就是：找到相片中的匹配点->计算 和 ->计算本质矩阵->计算位姿矩阵

![在这里插入图片描述](https://img-blog.csdnimg.cn/41cd1255235b48ca99018177fd3ab1bf.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_14,color_FFFFFF,t_70,g_se,x_16#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/bb14b6565d5a4cf8927ca2f2cea251a7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_13,color_FFFFFF,t_70,g_se,x_16#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/8b2062b3ee6f4bed85720c8b1f0f9e75.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_13,color_FFFFFF,t_70,g_se,x_16#pic_center)
  ||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||

#### **基本矩阵、本质矩阵和单应矩阵总结：**

https://blog.csdn.net/kokerf/article/details/72191054
 　
 两幅视图存在两个关系：
 　
 　 第一种，通过对极几何一幅图像上的点可以确定另外一幅图像上的一条直线；
 　 另外一种，通过上一种映射，一幅图像上的点可以确定另外一幅图像上的一个点，这个点是第一幅图像通过光心和图像点的射线与一个平面的交点在第二幅图像上的影像。
 　 第一种情况可以用基本矩阵来表示，
 　 第二种情况则用单应矩阵来表示。而本质矩阵则是基本矩阵的一种特殊情况，是在归一化图像坐标下的基本矩阵。
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/14a2f439da2545ed801f786deeab11b7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_16,color_FFFFFF,t_70,g_se,x_16#pic_center)

单应性拼接应用：

```cpp
#include<opencv2/opencv.hpp>
#include "opencv2/imgproc/imgproc.hpp"
#include "opencv2/highgui/highgui.hpp"
#include "opencv2/features2d.hpp"
#include "opencv2/calib3d.hpp"
#include "opencv2/core.hpp"
#include<iostream>
#include<math.h>

using namespace cv;
using namespace std;

void stitchimg(Mat &src,Mat &warp,int midline);
void stitch(int, void*);
Mat crop(Mat &result);

Mat img[100];
int maxx[100],minx[100],maxy[100],miny[100];

int picturenum=0;


cv::Point2f convert_pt(cv::Point2f point,int w,int h)
{
    //center the point at 0,0
    cv::Point2f pc(point.x-w/2,point.y-h/2);

    //these are your free parameters
    float f = -w/2;
    float r = w;

    float omega = w/2;
    float z0 = f - sqrt(r*r-omega*omega);

    float zc = (2*z0+sqrt(4*z0*z0-4*(pc.x*pc.x/(f*f)+1)*(z0*z0-r*r)))/(2* (pc.x*pc.x/(f*f)+1)); 
    cv::Point2f final_point(pc.x*zc/f,pc.y*zc/f);
    final_point.x += w/2;
    final_point.y += h/2;
    return final_point;
}

Mat cylin(int pictureindex){
    int width=img[pictureindex].cols;
    int height=img[pictureindex].rows;
    Mat tmpimg(img[pictureindex].size(),CV_8U);

	// initial
	maxx[pictureindex]=width/2;
	minx[pictureindex]=width/2;
	maxy[pictureindex]=height/2;
	miny[pictureindex]=height/2;
    for(int y = 0; y < height; y++)
    {
        for(int x = 0; x < width; x++)
        {
            cv::Point2f current_pos(x,y);
            current_pos = convert_pt(current_pos, width, height);

            cv::Point2i top_left((int)current_pos.x,(int)current_pos.y); //top left because of integer rounding

            //make sure the point is actually inside the original image
            if(top_left.x < 0 ||
            top_left.x > width-2 ||
            top_left.y < 0 ||
            top_left.y > height-2)
            {
                continue;
            }

            //bilinear interpolation
            float dx = current_pos.x-top_left.x;
            float dy = current_pos.y-top_left.y;

            float weight_tl = (1.0 - dx) * (1.0 - dy);
            float weight_tr = (dx)       * (1.0 - dy);
            float weight_bl = (1.0 - dx) * (dy);
            float weight_br = (dx)       * (dy);

            uchar value =   weight_tl * img[pictureindex].at<uchar>(top_left) +
			weight_tr * img[pictureindex].at<uchar>(top_left.y,top_left.x+1) +
			weight_bl * img[pictureindex].at<uchar>(top_left.y+1,top_left.x) +
			weight_br * img[pictureindex].at<uchar>(top_left.y+1,top_left.x+1);

			if(value>0){
				maxx[pictureindex]=max(maxx[pictureindex],x);
				minx[pictureindex]=min(minx[pictureindex],x);
				maxy[pictureindex]=max(maxy[pictureindex],y);
				miny[pictureindex]=min(miny[pictureindex],y);
			}

            tmpimg.at<uchar>(y,x) = value;
        }
    }

	return tmpimg;
}

Mat findtranslation(vector<Point2f> r,vector<Point2f> l){

	/*
		Htmp: 
		[1 , 0 , tx]
		[0 , 1 , ty]
	*/
	Mat Htmp(2,3,CV_64F,Scalar(0));
	Htmp.ptr<double>(0)[0]=1;
	Htmp.ptr<double>(1)[1]=1;

	int matchnum=0;
	// choose some match point
	for(int i=0;i<min(100,int(r.size()));i++){
		double tx,ty;
		tx=l[i].x-r[i].x;
		ty=l[i].y-r[i].y;
		int sum=0;
		/*
			1.calculate this match point translation matrix
			2.use this matrix to translate other point
			3.calculate the error
		*/
		for(int j=0;j<r.size();j++){   
			double difx=double(r[j].x)+tx-double(l[j].x);
			double dify=double(r[j].y)+ty-double(l[j].y);
			if(difx<0){
				difx*=(-1);
			}
			if(dify<0){
				dify*=(-1);
			}
			if(difx+dify<3){ // error < threshold 
				sum++;
			}
		}
		// sum bigger mean this translation matrix is better 
		if(sum>matchnum){
			matchnum=sum;
			Htmp.ptr<double>(0)[2]=tx;
			Htmp.ptr<double>(1)[2]=ty;
		}

	}
	return Htmp;
}


void stitch(int, void *)
{
	double start,end;

	start=clock();

	Ptr<ORB> detector = ORB::create(400);
    Ptr<FastFeatureDetector> fast = FastFeatureDetector::create();  

	vector<KeyPoint> keypoints_img[picturenum],keypoint_result;
	Mat descriptor_img[picturenum],descriptor_result;

	FlannBasedMatcher fbmatcher(new flann::LshIndexParams(20, 10, 2));
	vector<DMatch> matches;

	// find keypoint and descriptor
	for(int i=0;i<picturenum;i++){
		resize(img[i],img[i],Size(img[i].cols/3,img[i].rows/3));
		cvtColor(img[i],img[i],CV_BGR2GRAY);
		copyMakeBorder(img[i],img[i],100,100,100,100,BORDER_CONSTANT);

		// cylindrical projection
    	img[i]=cylin(i);
		img[i]=img[i](Range(miny[i],maxy[i]),Range(minx[i],maxx[i]));

		// use fast algorithm to find keypoint
		fast->detect(img[i],keypoints_img[i],Mat());

		// limit keypoint number
		KeyPointsFilter::retainBest(keypoints_img[i],500);
		
		// use orb to find descriptor
		detector->compute(img[i],keypoints_img[i],descriptor_img[i]);

	}

	Mat result=img[0];
	int movex=0,movey=0;

	for(int k=0;k<picturenum-1;k++){

		// use flann to find match
		fbmatcher.match(descriptor_img[k], descriptor_img[k+1], matches);
		double minDist = 1000;

		vector<DMatch> goodmatches;

		for (int i = 0; i < descriptor_img[k].rows; i++)
		{
			double dist = matches[i].distance;
			if (dist < minDist)
			{
				minDist=dist ;
			}
		}
		/*
			dist smaller is better
			choose some good match to find transation matrix
		*/
		for (int i = 0; i < descriptor_img[k].rows; i++)
		{
			double dist = matches[i].distance;
			if (dist < max(5 * minDist, 0.02))
			{
				goodmatches.push_back(matches[i]);
			}
		}

		vector<Point2f> keypointsl,keypointsr;
		for(int i=0;i<goodmatches.size();i++){
			keypointsr.push_back(keypoints_img[k+1][goodmatches[i].trainIdx].pt);
			keypointsl.push_back(keypoints_img[k][goodmatches[i].queryIdx].pt);
		}
		/*
			H =
			[1 , 0 , tx],
			[0 , 1 , ty]

			tx = x direction length that right picture need to move
			ty = y direction length that right picture need to move
		*/
		Mat H=findtranslation(keypointsr,keypointsl);

		/*
			assume that H12 tx = 5
			it mean that image2 is on the right side of image1 , and distance = 5 pixels

			H23 tx = 3
			it mean that image3 is on the right side of image2 , and distance = 3 pixels

			so image3 is on the right side of image1 , and distance = 5 + 3 = 8 pixels
		*/
		H.ptr<double>(0)[2]+=movex;
		H.ptr<double>(1)[2]+=movey;
		movex=H.ptr<double>(0)[2];
		movey=H.ptr<double>(1)[2];

		// if ty < 0 , it will be wrong
		// you can change the code by yourself to fix it
		int mRows=max(result.rows,img[k+1].rows+int(H.ptr<double>(1)[2]));
		int mCols=img[k+1].cols+int(H.ptr<double>(0)[2]);

		// calculate the midline of region that two picture overlapping 
		int midline=(result.cols+int(H.ptr<double>(0)[2]))/2;

		Mat stitchedImage = Mat::zeros(mRows,mCols,CV_8UC1);

		// use affine translation
		warpAffine(img[k+1],stitchedImage,H,Size(mCols,mRows));

		// stitch two picture
		stitchimg(result,stitchedImage,midline);

		// result = new stitching picture
		result=stitchedImage;
	}
	Mat final=crop(result);
	end=clock();
	cout<<end-start<<endl;

	imshow("result",final);
	imwrite("result.jpg",result);

}

void stitchimg(Mat &src,Mat &warp,int midline){
	// stitch two picture in pixels
	for(int i=0;i<src.rows;i++){
		for(int j=0;j<src.cols;j++){
			// both of two picture are black
			if(warp.ptr<uchar>(i)[j]==0 && src.ptr<uchar>(i)[j]==0){
				warp.ptr<uchar>(i)[j]=0;
			}
			else{
				// right picture is black and left picture is not black , choose left picture
				if(warp.ptr<uchar>(i)[j]==0){
					warp.ptr<uchar>(i)[j]=src.ptr<uchar>(i)[j];
				}
				else{
					// blending
					if(j>midline-20 && j<midline+20){
						float ratio=float((j-midline+20))/40;
						warp.ptr<uchar>(i)[j]=warp.ptr<uchar>(i)[j]*ratio+src.ptr<uchar>(i)[j]*(1-ratio);
					}
					// if pixel is at the left side of blending region , choose left picture
					// else choose right picture 
					if(j<=midline-20){
						warp.ptr<uchar>(i)[j]=src.ptr<uchar>(i)[j];
					}
				}

			}
		}
	}
}

Mat crop(Mat &result){
	int top=0,bottom=result.rows;
	for(int i=0;i<result.cols;i++){
		for(int j=0;j<result.rows;j++){
			if(result.ptr<uchar>(j)[i]!=0){
				top=max(top,j);
				break;
			}
		}
	}
	for(int i=0;i<result.cols;i++){
		for(int j=result.rows-1;j>=0;j--){
			if(result.ptr<uchar>(j)[i]!=0){
				bottom=min(bottom,j);
				break;
			}
		}
	}
	return result(Range(top,bottom),Range(0,result.cols));
}

int main(int argc, char** argv)
{
	// change to your picture number
	picturenum=9;

	img[0]=imread("pond/1.jpg");
	img[1]=imread("pond/2.jpg");
	img[2]=imread("pond/3.jpg");
	img[3]=imread("pond/4.jpg");
	img[4]=imread("pond/5.jpg");
	img[5]=imread("pond/6.jpg");
	img[6]=imread("pond/7.jpg");
	img[7]=imread("pond/8.jpg");
	img[8]=imread("pond/9.jpg");

	// img[0]=imread("ocean/1.jpg");
	// img[1]=imread("ocean/2.jpg");
	// img[2]=imread("ocean/3.jpg");
	// img[3]=imread("ocean/4.jpg");
	// img[4]=imread("ocean/5.jpg");
	// img[5]=imread("ocean/6.jpg");
	// img[6]=imread("ocean/7.jpg");
	// img[7]=imread("ocean/8.jpg");
	// img[8]=imread("ocean/9.jpg");
	// img[9]=imread("ocean/10.jpg");
	
	stitch(0,0);
	waitKey(0);
	return 0;

}
```

求解单应性矩阵非线性解法：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/30ad145e55574b83b00d97e18a1828ec.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_15,color_FFFFFF,t_70,g_se,x_16#pic_center)
 本质矩阵求解方法：
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/12769ec21d934e8eaba0b174e3486d7d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAU2Vuc29yRnVzaW9u,size_13,color_FFFFFF,t_70,g_se,x_16#pic_center)

## 5：多RADAR