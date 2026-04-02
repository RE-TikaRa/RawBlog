---
title: ROS实践系列03-消息与服务
date: 2026-03-15 18:27:11
tags:
  - ROS
  - ROS实践
  - 消息
  - 服务
categories:
  - ROS实践
abbrlink: d418d54e
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
sticky:
excerpt: "详解 ROS 消息与服务机制，实践 .msg/.srv 编写、发布订阅与服务通信"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2028-03-15 18:27:11
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---

# ROS消息与服务基础

## 消息（Message）

- **作用** ：ROS节点间通信的“数据载体”，把数据从一个节点传递到另一个节点（比如控制指令、传感器数据等）。 
- **定义位置** ：写在 **`.msg`文件** 中，例如 `geometry_msgs/Twist` （常用于控制机器人的线速度、角速度）。 
- **数据类型** ：支持基础类型（ `int32` 、 `float64` 、 `string` 等）、 **数组** （如保存多个相同类型的数据）、 **嵌套消息** （自定义消息中嵌套其他消息，形成“结构体”般的复杂结构）。 

## 服务（Service）

- **通信模式** ： **请求 - 响应** 机制，类似“发请求→等待处理→拿结果”的流程（同步通信）。 
- **定义位置** ：写在 **`.srv`文件** 中，例如 `std_srvs/Trigger` （常用于“触发操作并返回状态”，比如让机器人执行某个动作后，返回“成功/失败”）。 
- **结构** ：分为 **请求** （可携带参数，告诉服务端“怎么执行”）和 **响应** （返回操作结果、状态信息，比如成功/失败、错误原因等）。 

##  话题与服务的对比

- **话题（基于消息的通信）** ： 
  - 特点： **异步通信** （“广播式”）。 
  - 场景：适合 **数据流传输** （如摄像头持续发布图像、激光雷达发布点云、传感器持续采集数据），订阅节点按自身节奏处理数据，不强求“实时响应”。 

- **服务** ： 
  - 特点： **同步通信** （“点对点打电话要结果”）。 
  - 场景：适合 **请求 - 响应场景** （如让机械臂运动到目标位置、查询传感器当前状态），必须等“结果返回”后再执行下一步。 

## 核心区别总结

话题像“持续发广播”，适合“数据流式”的持续传输；服务像“打电话问事情”，适合“我要结果再继续”的请求 - 响应场景。两者的 **通信模式** 和 **适用场景** 完全不同，是ROS中实现节点间协作的两大核心机制~

---
# 消息文件.msg的编写

## **消息文件格式规范**  
### **基本结构与数据类型**  
- **字段定义格式** ：  
  `数据类型 变量名` （ **无逗号，空格分隔** ）  
  **✅ 正确** ： `int32 id`  
  **❌ 错误** ： `int32 id,` （类似 C 语法，ROS 不支持）  

- **支持的数据类型** （ROS 内置）：  
  
  | 类型          | 说明                     | 示例               |
  |---------------|--------------------------|--------------------|
  | `bool`        | 布尔值                   | `bool is_active`   |
  | `int8/uint8`  | 8 位整数                 | `int8 age`         |
  | `int16/uint16` | 16 位整数                | `uint16 count`     |
  | `int32/uint32` | 32 位整数                | `int32 id`         |
  | `int64/uint64` | 64 位整数                | `int64 timestamp`  |
  | `float32/float64` | 浮点数                | `float64 value`    |
  | `string`      | 字符串                   | `string name`      |
  | `time`        | 时间戳（ROS 1/2）        | `time timestamp`   |
  | `duration`    | 时长（ROS 1/2）          | `duration timeout` |
  

### **依赖声明（关键修正）**

- **ROS 1** ：  
  **无需在 `.msg` 文件中声明依赖** ！依赖通过 `package.xml` 和 `CMakeLists.txt` 管理。  
  > 示例：若需使用 `std_msgs/String` ，在包的 `package.xml` 中添加 `<depend>std_msgs</depend>` 。

### **注释规范**

- **所有注释以 `#` 开头** ：  
  
  ```msg
  # 人信息消息
  # 作者：ROS Team
  # 日期：2023-10-01
  
  string name  # 姓名（小写+下划线）
  uint8 age    # 年龄（0-255）
  string gender # 性别（"male" / "female"）
  ```

### 命名规范

| 项目         | 规范                          | 示例                     |
|--------------|-------------------------------|--------------------------|
| **消息文件名** | 全小写 + 下划线分隔（ `*.msg` ） | `person.msg`             |
| **字段名**    | 全小写 + 下划线分隔           | `name` , `age` , `gender`  |
| **禁止**      | 首字母大写、驼峰式、数字开头   | ❌ `PersonName` , ❌ `1st_name` |

{% note warning  %}
**为什么？** ROS 严格要求命名规范，避免与 C++/Python 代码冲突，提高可读性。
{% endnote %}

### **关键注意事项**

1. **文件位置** ：  
   
   - 消息文件必须放在 **包的 `msg/` 目录下** （如 `my_package/msg/Person.msg` ）。  
   - 未按此结构放置，ROS 无法编译。
   
2. **字段唯一性** ：  
   
   - 同一消息中 **禁止重复字段名** （如 `int32 id` 和 `int32 id` 重复）。
   
3. **基本类型限制** ：  
   - 不能使用自定义类型（如 `MyCustomType` ），需通过依赖的 `.msg` 文件定义。
   

## 创建msg消息

### 创建消息包
我们将创建一个new_msg包，并且定义新的消息

```bash
   cd ~/Tika_pkg/src  #进入src目录中
   catkin_create_pkg new_msg std_msgs rospy roscpp  #创建功能包
   cd ~/Tika_pkg/src/new_msg/   #进入对应的文件夹内
   mkdir msg  #创建对应文件夹
   echo "int64 num" > msg/num.msg  #将内容写入到文件当中
```
### 修改package.xml
接下来，查看package.xml, 确保它包含一下两条语句:
```bash
   <build_depend>message_generation</build_depend>
   <exec_depend>message_runtime</exec_depend>
```

![image-20251003151037367](https://s2.loli.net/2025/10/03/cVBJ3il4erWxHfF.png)

### 修改CMakeLists.txt

在CMakeLists.txt文件中，利用find_packag函数，增加对message_generation的依赖，这样就可以生成消息了。 你可以直接在COMPONENTS的列表里增加message_generation，就像这样：
```txt
     find_package(catkin REQUIRED COMPONENTS
     roscpp
     rospy
     std_msgs
     message_generation 
   )
```

![image-20251003151537366](https://s2.loli.net/2025/10/03/gwf6SUW5yim9bIc.png)

另外在CMakeLists.txt文件中，继续找到以下代码块，去掉注释符号#用你的.msg文件替代Message*.msg，或者将下面的内容复制粘贴
```txt
     add_message_files(
       FILES
       num.msg
       Message2.msg
     )
```
![image-20251003152109628](https://s2.loli.net/2025/10/03/4Av1ieYWjnrusLP.png)

![image-20251003152155983](https://s2.loli.net/2025/10/03/xLCOqsyPT3iYDw9.png)

![image-20251003152239857](https://s2.loli.net/2025/10/03/i8U2G9EYTVNohIc.png)

接下来，添加generate_messages()函数到如下位置

```txt
    ## Generate actions in the 'action' folder
    # add_action_files(
    #   FILES
    #   Action1.action
    #   Action2.action
    # )
    #######################################原先的代码文件##########################################
    ####################################需要修改的的代码文件########################################

    generate_messages() 

    ####################################需要修改的的代码文件########################################
    #######################################原先的代码文件##########################################
    ## Generate added messages and services with any dependencies listed here
    # generate_messages(
    #   DEPENDENCIES
    #   std_msgs
    # )
```

![image-20251003152716821](https://s2.loli.net/2025/10/03/nYU8JlWI1Bu27ZT.png)

### 编译msg节点

我们回到 ~/Tika_ws下执行编译命令：

```bash
catkin_make -j1
```

预期输出结果如下：

```bash
tika@tika-virtual-machine:~/Tika$ catkin_make -j1
Base path: /home/tika/Tika
Source space: /home/tika/Tika/src
Build space: /home/tika/Tika/build
Devel space: /home/tika/Tika/devel
Install space: /home/tika/Tika/install
####
#### Running command: "cmake /home/tika/Tika/src -DCATKIN_DEVEL_PREFIX=/home/tika/Tika/devel -DCMAKE_INSTALL_PREFIX=/home/tika/Tika/install -G Unix Makefiles" in "/home/tika/Tika/build"
####
-- Using CATKIN_DEVEL_PREFIX: /home/tika/Tika/devel
-- Using CMAKE_PREFIX_PATH: /home/tika/Tika/devel;/opt/ros/noetic
-- This workspace overlays: /home/tika/Tika/devel;/opt/ros/noetic
-- Found PythonInterp: /usr/bin/python3 (found suitable version "3.8.10", minimum required is "3") 
-- Using PYTHON_EXECUTABLE: /usr/bin/python3
-- Using Debian Python package layout
-- Using empy: /usr/lib/python3/dist-packages/em.py
-- Using CATKIN_ENABLE_TESTING: ON
-- Call enable_testing()
-- Using CATKIN_TEST_RESULTS_DIR: /home/tika/Tika/build/test_results
-- Forcing gtest/gmock from source, though one was otherwise available.
-- Found gtest sources under '/usr/src/googletest': gtests will be built
-- Found gmock sources under '/usr/src/googletest': gmock will be built
-- Found PythonInterp: /usr/bin/python3 (found version "3.8.10") 
-- Using Python nosetests: /usr/bin/nosetests3
-- catkin 0.8.12
-- BUILD_SHARED_LIBS is on
-- BUILD_SHARED_LIBS is on
-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-- ~~  traversing 3 packages in topological order:
-- ~~  - hello
-- ~~  - new_msg
-- ~~  - test_pkg
-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
-- +++ processing catkin package: 'hello'
-- ==> add_subdirectory(hello)
-- +++ processing catkin package: 'new_msg'
-- ==> add_subdirectory(new_msg)
-- Using these message generators: gencpp;geneus;genlisp;gennodejs;genpy
-- new_msg: 1 messages, 0 services
-- +++ processing catkin package: 'test_pkg'
-- ==> add_subdirectory(test_pkg)
-- Configuring done
-- Generating done
-- Build files have been written to: /home/tika/Tika/build
####
#### Running command: "make -j1" in "/home/tika/Tika/build"
####
Scanning dependencies of target _new_msg_generate_messages_check_deps_num
[  0%] Built target _new_msg_generate_messages_check_deps_num
Scanning dependencies of target new_msg_generate_messages_py
[ 14%] Generating Python from MSG new_msg/num
[ 28%] Generating Python msg __init__.py for new_msg
[ 28%] Built target new_msg_generate_messages_py
Scanning dependencies of target new_msg_generate_messages_nodejs
[ 42%] Generating Javascript code from new_msg/num.msg
[ 42%] Built target new_msg_generate_messages_nodejs
Scanning dependencies of target new_msg_generate_messages_lisp
[ 57%] Generating Lisp code from new_msg/num.msg
[ 57%] Built target new_msg_generate_messages_lisp
Scanning dependencies of target new_msg_generate_messages_cpp
[ 71%] Generating C++ code from new_msg/num.msg
[ 71%] Built target new_msg_generate_messages_cpp
Scanning dependencies of target new_msg_generate_messages_eus
[ 85%] Generating EusLisp code from new_msg/num.msg
[100%] Generating EusLisp manifest code for new_msg
[100%] Built target new_msg_generate_messages_eus
Scanning dependencies of target new_msg_generate_messages
[100%] Built target new_msg_generate_messages
```

## 使用rosmsg检查

通过rosmsg show命令，检查ROS是否能够识消息。

```
rosmsg show [message type]
```

例如，我将会运行以下命令：

```
rosmsg show new_msg/num
```

你将会看到如下输出

![image-20251003153839402.png](https://s2.loli.net/2025/10/03/CK1DdWxFzVEM3Qo.png)

消息类型由两部分组成：

- **Package名** ：消息所在的包（例如 `new_msg` ）
- **消息名** ：具体消息名称（例如 `num` ）

如果忘记包名，可直接省略包名，使用消息名进行查询：

```bash
rosmsg show num
```

执行后将显示：
```bash
[new_msg/num]:
int64 num
```

![image-20251003154414589.png](https://s2.loli.net/2025/10/03/9hGrziFcu2N3ZVS.png)

---

# 服务文件（.srv）的编写

## 服务文件格式

服务文件分为请求和响应两部分：
- **请求部分** ：定义输入参数
- **响应部分** ：定义输出结果

请求和响应部分字段定义与消息文件类似，支持多种数据类型和数组。

### 示例与规范

#### 示例：AddTwoInts 服务

```text
# 请求部分
int64 a
int64 b

# 响应部分
int64 sum
```

{% note info  %}
**说明** ：定义一个AddTwoInts服务，请求包含两个整数，响应返回它们的和。
{% endnote %}

#### 规范要求

- 服务文件名以小写字母开头
- 请求和响应字段名应清晰描述功能，便于理解和使用
- 例如： `add_two_ints.srv` （文件名）， `a` 、 `b` （请求字段）， `sum` （响应字段）

### 注意事项

1. **字段名唯一性** ：请求和响应部分字段名不能重复，避免冲突，确保服务正常工作。
2. **依赖声明** ：服务文件依赖其他消息类型时，需在 `package.xml` 中正确声明依赖，确保编译通过。
3. **类型支持** ：支持ROS标准数据类型（如 `int32` 、 `float64` 、 `string` 等）及自定义消息类型。
4. **结构清晰** ：服务文件应保持简洁，仅包含必要的请求和响应字段。

## 创建服务文件

在上面msg的package中创建一个服务：

```bash
roscd new_msg
mkdir srv
```

这次我们不再手动创建服务，而是从其他的package中复制一个服务。 roscp是一个很实用的命令行工具，它实现了将文件从一个package复制到另外一个package的功能。

  使用方法:

```bash
roscp [package_name] [file_to_copy_path] [copy_path]
```

现在我们可以从rospy_tutorials package中复制一个服务文件了：

```bash
roscp rospy_tutorials AddTwoInts.srv srv/AddTwoInts.srv
```

## 修改CMakeLists.txt

在CMakeLists.txt文件中增加了对message_generation的依赖。:

```txt
\# Do not just add this line to your CMakeLists.txt, modify the existing line
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
  )
```

{% note info  %}
message_generation 对msg和srv都起作用
{% endnote %}

在上一节创建消息的步骤中已经执行过，所以会有内容。
同样，跟msg文件类似，你也需要在CMakeLists.txt文件中做一些修改。查看上边的说明，增加额外的依赖项。删掉#，去除对下边语句的注释:

```txt
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )
```

用你自己的srv文件名替换掉那些Service*.srv文件:

```txt
## Generate services in the 'srv' folder
  add_service_files(
    FILES
    AddTwoInts.srv
  )
```

如图所示：

![image-20251003161725597](https://s2.loli.net/2025/10/03/DsCjOtNHZvqwAz3.png)

![image-20251003161849522](https://s2.loli.net/2025/10/03/mc2kbYIElwxS8Aa.png)

## 编译srv节点

参考 [2.2.4-编译msg节点](#编译msg节点) 的编译

我们回到 ~/Tika_ws下执行编译命令：

```bash
catkin_make -j1
```

## 使用rossrv检查

通过rosmsg show命令，检查ROS是否能够识该服务。

使用方法:

```bash
rossrv show <service type>
```

例子:

```bash
rossrv show new_msg/AddTwoInts
```

你将会看到:

```bash
int64 a
int64 b
---
int64 sum
```

跟rosmsg类似, 你也可以不指定具体的package名来查找服务文件：

```bash
tika@tika-virtual-machine:~/Tika$ rossrv show AddTwoInts
[rospy_tutorials/AddTwoInts]:
int64 a
int64 b
---
int64 sum

[new_msg/AddTwoInts]:
int64 a
int64 b
---
int64 sum
```

实际操作：

![image-20251003202058180](https://s2.loli.net/2025/10/03/dZ8kwxMtY5HLqXK.png)
---
# 消息的发布与订阅

## 编写发布节点

在我们前几节的功能包（new_msg)中，运行如下命令，创建 `scripts` 来存放我们的python代码

```bash
mkdir scripts
cd scripts
```

然后运行以下命令

```bash
wget https://raw.githubusercontent.com/ros/ros_tutorials/noetic-devel/rospy_tutorials/001_talker_listener/talker.py --no-check-certificate
```

这个命令让我们会下载一份talker.py的文件，这个文件是ros的一个最简单的发布者的示例

然后利用如下命令给这份文件升权

```bash
chmod +x talker.py
```

![image-20251003204237187](https://s2.loli.net/2025/10/03/4BwjzIuRtWgl1sb.png)

然后我们利用VS code打开这份文件

```bash
code talker.py
```

![image-20251003204755322](https://s2.loli.net/2025/10/03/TlZDWIVn7ORska2.png)

图上这些部分是talker.py的核心代码，我写了一份带注释的方便理解

```python
################################################################################
# Simple talker demo that published std_msgs/Strings messages
# to the 'chatter' topic
#
# 功能说明：
# 1. 创建一个ROS节点名为"talker"
# 2. 以10Hz的频率向"chatter"话题发布字符串消息
# 3. 消息内容为"hello world"加时间戳
################################################################################

# 导入ROS Python客户端库
import rospy

# 从标准消息包导入String消息类型
# String消息只包含一个字符串字段"data"
from std_msgs.msg import String

def talker():
    """
    发布者函数，创建一个ROS节点，定期发布消息
    """
    # 创建一个Publisher（发布者）对象
    # 参数1: 话题名称为'chatter'
    # 参数2: 消息类型为String
    # 参数3: 队列大小为10，当消息处理速度跟不上发布速度时，新消息会覆盖旧消息
    pub = rospy.Publisher('chatter', String, queue_size=10)
    
    # 初始化节点，节点名为'talker'
    # anonymous=True 表示允许运行多个同名节点，ROS会自动在名称后添加数字后缀
    rospy.init_node('talker', anonymous=True)
    
    # 设置循环频率为10Hz（每秒10次）
    # Rate对象会自动计算每次循环需要休眠的时间
    rate = rospy.Rate(10) # 10hz
    
    # 循环直到节点被关闭（例如通过Ctrl+C）
    # rospy.is_shutdown() 在节点正常关闭时返回True
    while not rospy.is_shutdown():
        # 构造要发布的消息内容，包含时间戳，这个消息可以改
        hello_str = "hello world This is Tiks's Talker %s" % rospy.get_time()
        
        # 在终端打印消息内容，同时也会记录到ROS日志中
        rospy.loginfo(hello_str)
        
        # 通过Publisher发布消息到'chatter'话题
        pub.publish(hello_str)
        
        # 按照设定的频率休眠
        # 如果代码执行时间超过休眠时间，则不休眠
        rate.sleep()

# Python标准写法，确保只有直接运行此脚本时才执行以下代码
if __name__ == '__main__':
    try:
        # 调用talker函数开始执行节点功能
        talker()
    except rospy.ROSInterruptException:
        # 当节点被Ctrl+C等操作中断时会抛出此异常
        # 这里选择忽略异常，直接退出程序
        pass
```

## 为talker.py修改CMakeLists.txt

将以下内容添加到CMakeLists.txt中。这样可以确保正确安装了python脚本，并使用了正确的python解释器。

```txt
catkin_install_python(PROGRAMS scripts/talker.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
```

![image-20251003210137094](https://s2.loli.net/2025/10/03/8oTfngqcXMuYHi1.png)

## 订阅器节点编写

运行以下命令下载代码，同时对文件进行升权：

```
roscd new_msg/scripts
wget https://raw.githubusercontent.com/ros/ros_tutorials/noetic-devel/rospy_tutorials/001_talker_listener/listener.py --no-check-certificate
chmod +x listener.py
```

同样的，我也对核心代码部分写了注释

```python

################################################################################
# Simple listener demo that listens to std_msgs/Strings published 
# to the 'chatter' topic
#
# 功能说明：
# 这是一个ROS节点，用于订阅"chatter"话题并打印接收到的消息
# 它演示了ROS中订阅者（Subscriber）的基本用法
################################################################################

# 导入ROS Python客户端库
# rospy提供了编写ROS节点所需的所有功能
import rospy

# 从标准消息包中导入String消息类型
# String消息类型用于传输字符串数据
from std_msgs.msg import String

def callback(data):
    """
    回调函数：当有新消息发布到订阅的话题时被调用
    
    参数:
        data: 接收到的消息数据，类型为String
             data.data 包含实际的字符串内容
    
    功能:
        打印接收到的消息内容和节点信息到ROS日志
    """
    # rospy.get_caller_id() 获取当前节点的唯一标识符
    # data.data 包含实际接收到的字符串消息
    # rospy.loginfo() 将消息打印到控制台并记录到日志文件
    rospy.loginfo(rospy.get_caller_id() + ' I heard: %s', data.data)

def listener():
    """
    主要的监听器函数，设置节点并开始监听消息
    
    功能:
        1. 初始化ROS节点
        2. 创建订阅者对象
        3. 保持节点运行以接收消息
    """

    # 初始化ROS节点
    # 参数1: 节点名称为'listener'
    # 参数2: anonymous=True 表示允许同时运行多个该节点实例
    #       ROS会自动为每个实例添加唯一后缀，避免名称冲突
    #       这在测试和调试时很有用
    rospy.init_node('listener', anonymous=True)

    # 创建订阅者对象
    # 参数1: 订阅的话题名称为'chatter'
    # 参数2: 消息类型为String
    # 参数3: 回调函数为callback
    # 当有新消息发布到'chatter'话题时，callback函数会被自动调用
    rospy.Subscriber('chatter', String, callback)

    # 保持节点运行直到被关闭
    # rospy.spin() 进入循环，等待消息到达并调用回调函数
    # 程序会一直阻塞在这里，不会继续执行后续代码
    # 当节点被关闭时（如Ctrl+C），循环结束
    rospy.spin()

# Python标准入口点检查
# 确保只有直接运行此脚本时才执行以下代码
# 如果该文件被其他脚本导入，则不会执行
if __name__ == '__main__':
    # 调用listener函数开始执行节点功能
    listener()

```
listener.py的代码与talker.py相似，不同之处在于，我们引入了一种基于回调的新机制来订阅消息。

```python
rospy.init_node('listener', anonymous=True) 
# 初始化ROS节点，节点名为'listener'，anonymous=True指定节点名后加上一个随机数
rospy.Subscriber("chatter", String, callback) 
# 订阅名为'chatter'的主题，消息类型为String，当有消息发布到该主题时，调用回调函数callback
rospy.spin()
# 进入循环，保持节点的运行
```

这个声明，您的节点订阅的话题是类型的std_msgs.msgs.String。收到新消息时，将以消息作为第一个参数来调用回调。

我们还稍微改变了对rospy.init_node（）的调用。我们添加了anonymous = True关键字参数。ROS要求每个节点都有唯一的名称。如果出现一个具有相同名称的节点，它将碰撞前一个节点。这样一来，故障节点就可以轻松地从网络上踢出去。该匿名=真标志告诉rospy为节点生成一个唯一的名称，以便您可以有多个listener.py节点轻松运行。

最后添加的rospy.spin（）只是使您的节点无法退出，直到该节点已关闭。与roscpp不同，rospy.spin（）不会影响订户回调函数，因为它们具有自己的线程。


## 为listener.py修改CMakeLists.txt

找到我们为talker.py修改CMakeLists.txt的字段

![image-20251003210137094](https://s2.loli.net/2025/10/03/8oTfngqcXMuYHi1.png)

在第一行末尾加上 `scripts/listener.py` ，整个字段的就是

```txt
catkin_install_python(PROGRAMS scripts/talker.py scripts/listener.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
```

![image-20251003211607992](https://s2.loli.net/2025/10/03/1u6RpZAKhgNw7yL.png)

{% note warning  %}
需要注意的是 `scripts/talker.py` 和 `scripts/listener.py` 中间有一个空格
{% endnote %}

## 编译节点

我们使用CMake作为构建系统，即使对于Python节点，也必须使用它。这是为了确保创建用于消息和服务的自动生成的Python代码。因为CMake不直接编译项目，而是通过CMakeLists.txt配置文件生成适用于不同平台的构建文件（如Makefile、Visual Studio工程文件等），这些文件再由实际的编译工具（如make、MSBuild）执行编译过程。

转到根目录并运行catkin_make：

```bash
cd ~/Tika_ws
catkin_make -j1 clean
```

---
# 测试消息发布器和订阅器

我们新建终端，运行如下命令

```bash
cd ~/Tika_ws/
source devel/setup.bash
roscore
```

然后我们再次新建一个终端，在工程根目录下运行如下命令，以启动"talker"的发布器节点

```bash
rosrun new_msg talker.py 
```

会出现如下情况

![image-20251003213223489](https://s2.loli.net/2025/10/03/zOAkjh7bwiZ3a9F.png)

我们编写了一个名为"listener"的订阅器节点。再打开另外一个终端运行：

```bash
rosrun new_msg listener.py
```

运行结果如下，便是成功

![image-20251003213433979](https://s2.loli.net/2025/10/03/9Y2gSkJwfOWHZvt.png)

至此，消息的发布和订阅以全部完成。

---
# ROS服务通信：编写Service和Client

## 创建Server节点

我们将创建一个简单的service节点("server")，该节点将接收到两个整形数字，并返回它们的和。进入前几章的教程中所创建的new_msg包所在的目录，打开一个终端运行：

```bash
cd  ~/Tika_ws/src/new_msg
```

接下来创建server.py，运行如下命令

```bash
cd scripts
touch server.py
code server.py
```

此时我们会打开VS code界面，把如下内容复制进去并保存

```python
#!/usr/bin/env python 
from __future__ import print_function
from new_msg.srv import AddTwoInts,AddTwoIntsResponse
import rospy
def handle_add_two_ints(req):
	print("Returning [%s + %s = %s]"%(req.a, req.b, (req.a + req.b)))
	return AddTwoIntsResponse(req.a + req.b)
def add_two_ints_server():
	rospy.init_node('add_two_ints_server')
	s = rospy.Service('add_two_ints', AddTwoInts, handle_add_two_ints)
	print("Ready to add two ints.")
	rospy.spin()
if __name__ == "__main__":
	add_two_ints_server()
```

方便起见，我依旧是写了一份带注释的版本

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

"""
ROS服务端脚本示例：实现两个整数相加的功能
此脚本演示了如何在ROS中创建一个简单的服务端节点
"""

# 从__future__导入print_function以确保Python 2和3之间的兼容性
from __future__ import print_function

# 导入自定义的服务类型AddTwoInts及其响应类型AddTwoIntsResponse
# 这些类型是在new_msg包的srv模块中定义的
from new_msg.srv import AddTwoInts, AddTwoIntsResponse

# 导入rospy库，这是ROS的Python客户端库
import rospy


def handle_add_two_ints(req):
    """
    处理加法请求的回调函数
    
    当服务接收到请求时，该函数会被调用。它接收一个请求对象，
    执行计算，并返回结果。
    
    参数:
        req: AddTwoIntsRequest类型的对象，包含要相加的两个整数(a和b)
        
    返回:
        AddTwoIntsResponse类型的对象，包含相加的结果
    """
    # 在终端打印请求信息和计算结果，便于调试和监控
    print("Returning [%s + %s = %s]" % (req.a, req.b, (req.a + req.b)))
    
    # 创建并返回响应对象，其中包含两个数相加的结果
    return AddTwoIntsResponse(req.a + req.b)


def add_two_ints_server():
    """
    初始化并运行加法服务服务器
    
    此函数负责初始化节点、创建服务以及保持节点运行
    """
    # 初始化ROS节点，节点名称为'add_two_ints_server'
    # 节点是ROS系统中最基本的执行单元
    rospy.init_node('add_two_ints_server')
    
    # 创建服务端实例
    # 参数说明：
    # 'add_two_ints': 服务名称，客户端将通过此名称调用服务
    # AddTwoInts: 服务类型，定义了请求和响应的数据结构
    # handle_add_two_ints: 回调函数，当接收到请求时会被调用
    s = rospy.Service('add_two_ints', AddTwoInts, handle_add_two_ints)
    
    # 打印提示信息，表明服务已经准备就绪
    print("Ready to add two ints.")
    
    # 保持节点运行直到被手动终止
    # spin()函数会一直阻塞直到节点关闭
    rospy.spin()


# Python的标准写法，确保只有直接运行此脚本时才执行以下代码
# 如果此文件被其他文件导入，则不会执行
if __name__ == "__main__":
    # 调用主函数启动服务
    add_two_ints_server()
```

然后给这份文件升权

```bash
chmod +x server.py
```

## 创建Client节点

运行如下命令

```
roscd new_msg/scripts
touch client.py
code client.py
```

将如下内容粘贴到VS code

```python
#!/usr/bin/env python
from __future__ import print_function
import sys
import rospy
from new_msg.srv import *
def add_two_ints_client(x, y):
	rospy.wait_for_service('add_two_ints')
	try:
		add_two_ints = rospy.ServiceProxy('add_two_ints', AddTwoInts)
		resp1 = add_two_ints(x, y)
		return resp1.sum
	except rospy.ServiceException as e:
		print("Service call failed: %s"%e)
def usage():
	return "%s [x y]"%sys.argv[0]
 
if __name__ == "__main__":
	if len(sys.argv) == 3:
		x = int(sys.argv[1])
		y = int(sys.argv[2])
	else:
		print(usage())
		sys.exit(1)
	print("Requesting %s+%s"%(x, y))
	print("%s + %s = %s"%(x, y, add_two_ints_client(x, y)))
```

同样的，我也写了一份带注释的

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# ROS服务客户端示例：调用两个整数相加的服务
# 此脚本演示了如何在ROS中创建一个服务客户端节点来调用服务

# 从__future__导入print_function以确保Python 2和3之间的兼容性
from __future__ import print_function
# 导入sys模块用于处理命令行参数
import sys
# 导入rospy库，这是ROS的Python客户端库
import rospy
# 从new_msg.srv模块导入所有服务类型
# 注意：这是一种通配符导入，在生产环境中建议明确指定所需的类型
from new_msg.srv import *

# 定义客户端函数，用于调用add_two_ints服务
# 参数x和y是需要相加的两个整数
def add_two_ints_client(x, y):
	# 等待名为'add_two_ints'的服务变为可用状态
	rospy.wait_for_service('add_two_ints')
	try:
		# 创建服务代理对象，用于调用指定的服务
		add_two_ints = rospy.ServiceProxy('add_two_ints', AddTwoInts)
		# 调用服务，传入参数x和y
		resp1 = add_two_ints(x, y)
		# 返回响应中的sum字段
		return resp1.sum
	except rospy.ServiceException as e:
		# 捕获服务调用异常并打印错误信息
		print("Service call failed: %s"%e)

# 定义显示程序使用方法的辅助函数
def usage():
	# 返回程序的基本使用方法
	return "%s [x y]"%sys.argv[0]

# 程序主入口点
if __name__ == "__main__":
	# 检查命令行参数数量是否正确
	if len(sys.argv) == 3:
		# 将命令行参数转换为整数
		x = int(sys.argv[1])
		y = int(sys.argv[2])
	else:
		# 如果参数数量不正确，打印使用说明并退出程序
		print(usage())
		sys.exit(1)
	# 打印即将发送的服务请求信息
	print("Requesting %s+%s"%(x, y))
	# 调用服务客户端函数执行加法运算，并打印结果
	print("%s + %s = %s"%(x, y, add_two_ints_client(x, y)))
```

然后给文件升权

```bash
chmod +x client.py
```

## 为Service和Client修改CMakeLists.txt

确保如下部分是非注释态

![image-20251003223339274](https://s2.loli.net/2025/10/03/AqXpPrbjQhRmEiW.png)

1. **删除重复的 `generate_messages()` 调用**
   - 删除了第 68 行的空调用 `generate_messages()`

2. **添加带依赖声明的 `generate_messages()` 调用**
   - 添加了明确指定依赖项的调用：
   ```cmake
   generate_messages(
     DEPENDENCIES
     std_msgs
   )
   ```

## 修改原因

1. **CMake 规则要求** ：每个 ROS 包中只能调用一次 `generate_messages()` 函数
2. **依赖声明必要性** ：为了正确生成服务代码，需要显式声明对标准消息包 `std_msgs` 的依赖
3. **代码生成** ：只有正确配置后， `catkin_make` 才能生成服务对应的 Python 模块，解决导入错误

## 编译节点

回到我们的工作空间根目录并执行编译

```bash
catkin_make -j1
```

然后更新一下配置文件

```bash
source devel/setup.bash
```



## 测试 Service和Client

首先打开一个终端运行：

```bash
roscore
```

然后再次新建一个终端运行

```bash
cd ~/Tika && source devel/setup.bash && rosrun new_msg server.py
```

![image-20251003225417929](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/nKoQEjkrSI3Bltg.png)

再次新建一个终端，并且运行Client并附带一些参数：

```bash
rosrun new_msg client.py 6 9 
```

出现下图的结果便是整个服务通信已完成

![image-20251003225537231](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/SdskfiWuj6vO3B8.png)

