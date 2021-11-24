# RosTutorial
qtcreator-ros
打开终端快捷键：ctrl+shift+e, ctrl+shift+o




1.创建工程文件目录
mkdir catkin_test1
mkdir catkin_test1/src
2.在catkin_test1目录中make
catkin_make
3.配置环境
source devel/setup.bash
4.创建catkin软件包
cd ~/catkin_ws/src
catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
5.编译
5.1待编译的cpp

           
5.2配置CMakeList.txt


cmake_minimum_required(VERSION 2.8.3)
project(beginner_tutorials)

## Find catkin and any catkin packages
find_package(catkin REQUIRED COMPONENTS roscpp rospy std_msgs message_generation)

## Declare ROS messages and services
add_message_files(
FILES 
Num.msg
)
add_service_files(FILES AddTwoInts.srv)

## Generate added messages and services
generate_messages(DEPENDENCIES std_msgs)
#generate_messages()
#rosbuild_genmsg()

## Declare a catkin package
catkin_package(
CATKIN_DEPENDS message_runtime
)

## Build talker and listener
include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(talker src/talker.cpp)
target_link_libraries(talker ${catkin_LIBRARIES})
add_dependencies(talker beginner_tutorials_generate_messages_cpp)

add_executable(listener src/listener.cpp)
target_link_libraries(listener ${catkin_LIBRARIES})
add_dependencies(listener beginner_tutorials_generate_messages_cpp)

## Build service client and server
# %Tag(SRVCLIENT)%
add_executable(add_two_ints_server src/add_two_ints_server.cpp)
target_link_libraries(add_two_ints_server ${catkin_LIBRARIES})
add_dependencies(add_two_ints_server beginner_tutorials_gencpp)

add_executable(add_two_ints_client src/add_two_ints_client.cpp)
target_link_libraries(add_two_ints_client ${catkin_LIBRARIES})
add_dependencies(add_two_ints_client beginner_tutorials_gencpp)



5.3编译 catkin_make



知识点：
build 目录是构建空间的默认位置，同时cmake和make也是在这里被调用来配置和构建你的软件包。
devel目录是开发空间的默认位置, 在安装软件包之前，这里可以存放可执行文件和库。
Src里面放ros包
Src/rospack/include放头文件
Src/rospack/src放源文件
Xml: 包含软件包元信息

