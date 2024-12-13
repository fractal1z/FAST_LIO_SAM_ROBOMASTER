# FAST_LIO_SAM_ROBOMASTER

## Front_end : fastlio2      Back_end : lio_sam   robomaster 2025

<p align='center'>
    <img src="./FAST_LIO_SAM/pic/cover2.png " alt="drawing" width="200" height ="200"/>
    <img src="./FAST_LIO_SAM/pic/cover4.png" alt="drawing" width="200" height =200/>
    <img src="./FAST_LIO_SAM/pic/cover3.png" alt="drawing" width="200" height =200/>
    <img src="./FAST_LIO_SAM/pic/cover1.png" alt="drawing" width="200" height =200/>
</p>


## Related worked 

1.[FAST-LIO2](https://github.com/hku-mars/FAST_LIO)为紧耦合的lio slam系统，因其缺乏前端，所以缺少全局一致性，参考lio_sam的后端部分，接入GTSAM进行后端优化。

2.[FAST_LIO_SLAM](https://github.com/gisbi-kim/FAST_LIO_SLAM)的作者kim在FAST-LIO2的基础上，添加SC-PGO模块，通过加入ScanContext全局描述子，进行回环修正,SC-PGO模块与FAST-LIO2解耦，非常方便，很优秀的工作。

3.[FAST_LIO_LC](https://github.com/yanliang-wang/FAST_LIO_LC)的作者yanliang-wang,在FAST_LIO_SLAM的基础上添加了：1.基于Radius Search 基于欧式距离的回环检测搜索，增加回环搜索的鲁棒性；2.回环检测的优化结果，更新到FAST-LIO2的当前帧位姿中，幷进行ikdtree的重构，进而更新submap。

4.[FAST_LIO_SAM](https://github.com/kahowang/FAST_LIO_SAM)的作者kahowang,对比FAST_LIO_SLAM 与 FAST_LIO_LC 使用外部接入的PGO回环检测模块进行后端优化 ，FAST_LIO_SAM 将LIO-SAM的后端GTSAM优化部分移植到FAST-LIO2的代码中，数据传输处理环节更加清晰。
## Contributions  
本仓库基于dji ROBOMASTER 2025修改，使用九轴imu自带orientation与GPS的XYZ时间对齐后进行位姿先验因子约束。添加了初始位姿优化对齐lidar启动坐标系与世界系，可选择从当前lidar启动坐标系更新位姿，或是从世界系给出绝对位姿。



## Prerequisites

- Ubuntu 18.04 and ROS Melodic
- PCL >= 1.8 (default for Ubuntu 18.04)
- Eigen >= 3.3.4 (default for Ubuntu 18.04)
- GTSAM >= 4.0.0(tested on 4.0.0-alpha2)

## Build

```shell
cd YOUR_WORKSPACE/src
git clone  xxx
cd ..
catkin_make
```



## Attention:

1.FAST-LIO2中对pose姿态是使用so3表示，而gtsam中，输入的relative_pose姿态是Euler RPY形式表示，需要使用罗德里格斯的公式进行转换更新。

2.参考yanliang-wang [FAST-LIO-LC](https://github.com/yanliang-wang/FAST_LIO_LC)中的iktree  reconstruct 




6.LIO-SAM 中使用**ekf_localization_node**这个ROS Package 把GPS的WGS84 坐标系 转到 World系下，FAST-LIO-SAM考虑到尽量与外部的ROS package 解耦，调用 **GeographicLib**进行坐标转换。本项目直接使用IntelligentUAVChampionshipSimulator的GPS数据与九轴imu orientation。



## some problems:






​																																													
