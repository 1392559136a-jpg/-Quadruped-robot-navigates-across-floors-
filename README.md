# -Quadruped-robot-navigates-across-floors-
为解决2维规划不了多楼层问题，提出该解决方案，希望可以点个star，谢谢。(This solution is proposed to address the issue of multi-story buildings not being feasible in 2D planning. I hope you can give it a star, thank you.)
*****
此项目对于PCT_planner（ros2）做了部分修改：
1、增加了三维目标点的选取；
2、优化了路径规划，将多段路径合并成一整段路径，并可以储存下来，随时使用；
3、增加了可通行区域的检测。
*****
*****
此项目对于egoplanner（ros2）做了部分修改：
1、增加了点云过滤的逻辑判断；
2、增加了行为树逻辑判断；
3、适配了机械狗的体积，但并未加入动力学模型优化（如果有大佬愿意帮忙，不胜感激）
*****

*****
此项目对于Fast_lio的修改：
1、增加了点云过滤，将天花板的点云过滤掉，只使用地面和周围点云（逻辑上存在一些问题，如果有大佬愿意帮忙，不胜感激）
*****

本项目是站在巨人的肩膀上，感谢开源生态。本项目支持ros2、ubuntu22.04,其余项目来自各个开源。
此版本为仿真版本，但是实物部署和这个框架差不多，大家可以在此基础上进行优化，使得大家的这个项目更加健壮。
本人第一次开源代码，写得不太规范，如果有大佬愿意帮我完善，感激不尽。

*****
安装rl_sar：
1、安装依赖包：
sudo apt-get install -y  libpcap-dev
sudo apt install nlohmann-json3-dev
sudo apt install libasio-dev
sudo apt install ros-humble-pcl-ros ros-humble-pcl-conversions
sudo apt install ros-humble-libg2o
sudo apt install ros-humble-octomap-ros
sudo apt install ros-humble-cartographer ros-humble-cartographer-ros
sudo apt install ros-humble-nav2-*
sudo apt install -y libyaml-cpp-dev
sudo apt-get install build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt install -y libusb-1.0-0-dev
sudo apt-get install libopencv-dev
2、进入有build.sh的脚本文件夹，然后用./build.sh
*****

*****
运行rl_sar:
1、启动gazebo：ros2 launch rl_sar gazebo.launch.py rname:=b2w（可选机器人类型，然后记得把雷达的配置也移植过去）
2、启动控制器：ros2 run rl_sar rl_sim，然后输入1、0进入运控，再输入n进入导航；
3、启动egoplanner：ros2 launch ego_planner run_in_sim.launch.py     odom_topic:=odom     lidar_cloud_topic:=rslidar_points_odom     drone_id:=0     robot_type:=quadruped     use_dynamic:=False     flight_type:=3
4、启动rviz：ros2 launch ego_planner rviz.launch.py
*****

*****
可选运行：
1、直接在rviz2里面选择目标点，看避障效果；
2、传入pct路进话题，机器人以当前位置作为出发点，进行规划。
*****

*****
安装PCT_planner:
cd planner/
./build_thirdparty.sh
./build.sh
可能会爆内存，如果报已杀死进程，多半是内存爆炸了，这时候一个一个编译即可colcon build --parallel-workers 1
*****

####
使用PCT_planner:
1\python3 tomography.py --scene Spiral
2\python3 plan.py --scene Spiral
缺少了几个步骤，看官方的
####
