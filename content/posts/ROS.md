+++
date = '2025-02-24T15:57:47+08:00'
draft = true
title = 'ROS'
+++

# 正文内容
1. 启动 rosmaster 所有节点的管理器（负责管理通信，名称解析等）[相当于银行]
roscore # 会创建/rosout节点
2. 启动 “功能包” 里的 “节点”（会启动小乌龟）[相当于运钞车]
语法：rosrun “功能包” “节点”
rosrun turtlesim turtlesim_node
3. 启动 “功能包” 里的 “节点”（允许键盘控制乌龟）[相当于取钱的用户]
rosrun turtlesim turtle_teleop_key

rqt_graph # rqt_XXX:基于qt的可视化工具，这里是显示节点图

测试代码高亮及代码块
python
```python
def hello():
    print("Hello Hugo")
```
C++
```cpp
#include <ros/ros.h>  // 头文件着色
class DemoNode { // 类名高亮
public:
  void callback(const std_msgs::String& msg);  // 函数参数着色
};
```
ROS
```roslaunch
<launch>
  <node pkg="turtlesim" type="turtlesim_node" name="turtle1"/> <!-- XML语法高亮 -->
</launch>
```
bash
```bash
rostopic pub /turtle1/cmd_vel geometry_msgs/Twist \  # 管道符着色
  "linear: {x: 2.0, y: 0.0, z: 0.0}"  # JSON结构高亮
```


打印所有节点
```ROS
rosnode list
```

rosnode info 功能包 #  打印功能包信息（发布、订阅、服务、id）
rostopic list      # 打印所有话题
rostopic pub 话题名 数据消息结构 "具体数据信息"       # 通过指令给话题发布数据
rostopic pub 话题名 数据消息结构 "具体数据信息" -r 10 # 指定发送频率

rosmsg show 某种数据类型 # 打印数据类型，支持话题、服务、节点等

rosservice list # 打印服务内容
rosservice call /spawn "x:0.0 y:0.0 theta: 0.0 name: 'turtle2'" # 添加新的海龟

rosbag record -a -O cmd_record # 记录当前话题所有数据并保存到/home文件夹下
rosbag play cmd_record.bag # 回放以前记录的数据，会严格复现全过程，特别适合在真实设备上采集数据，然后将数据用于仿真训练，避免直接用真实设备训练

