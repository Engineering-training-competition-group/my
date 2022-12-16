# 工训赛无人机

## 启动指令

时间对齐

```
sudo ptpd -M -i enp88s0 -C
```

启动mavros

```
roslaunch mavros px4.launch
```

查IMU的频率是否接近200

```
rostopic hz /mavros/imu/data
```

开启雷达

```
roslaunch livox_ros_driver livox_lidar_msg.launch
```

启动fast_lio

```
roslaunch fast_lio mapping_avia.launch
```

连接slam,里程计和飞控

```
roslaunch px4_realsence_bridge bridge.launch
```

## 安装

###  imu内参

安装code_utils需要安装ceres库

首先安装code_utils库

安装依赖

```
sudo apt-get install libdw-dev
```

在src中下载code_utils

```
git clone https://github.com/gaowenliang/code_utils
```

在工作空间中编译

```
cd catkin_ws
catkin_make
```

编译中可能遇到问题，库路径不对和OPENCV版本问题

### 雷达和imu的外参

使用官方的标定包

## 调参

### imu内参

录包

```
rosbag record -O imu_bagname /mavros/imu/data_raw 
```

#TODO

### 雷达和imu的外参

#TODO

## 修改及原因

## 当前问题

### 11月20日

#### 起飞不稳

做了imu和雷达标定后，所有部分正常开启，SlAM非常稳定，启动OFFBOARD代码后，无人机会朝着左后方撞击。

终端出现如下报错

PositionTargetGlobal failed because no origin

![](C:\Users\31919\Desktop\97e2819a442b4a0eab68ec156f99983.jpg)

`未解决`

#### 降落时会直接断电摔下

手飞时会突然断电摔下，自动飞时调到land模式会直接摔下

![](C:\Users\31919\Desktop\21ae85ee3be1f1ca41b53c594284908.jpg)

![](C:\Users\31919\Desktop\277ed1547a81aa4ab8e8964f1e94320.jpg)

![](C:\Users\31919\Desktop\374084be271cd2244e3524cec6183bb.jpg)

上图可见油门值和电机的输出值，在一瞬间突然掉零。该问题导致一电机烧毁，解决办法需要和电机的商家沟通

#### 