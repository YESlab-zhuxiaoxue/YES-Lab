# YES-Lab# ROS Noetic 安装报告

**GitHub 用户名**：YESlab-zhuxiaoxue

## 一、 安装步骤简述
1. 安装 VMware Workstation Pro 虚拟机，并下载 Ubuntu 20.04 (Focal Fossa) 镜像完成系统安装。
2. 配置系统环境与软件源：
   - 更新系统并安装必要工具：`sudo apt install curl gnupg2 lsb-release -y`
   - 添加 ROS 官方密钥与软件源（由于网络原因，最终使用清华镜像源：`https://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/`）。
3. 安装 ROS Noetic 桌面完整版：
   - 执行命令：`sudo apt install ros-noetic-desktop-full -y`
4. 初始化 rosdep 及环境配置：
   - 配置环境变量：`echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc && source ~/.bashrc`
   - 安装构建工具：`sudo apt install python3-rosinstall python3-rosinstall-generator python3-wstool build-essential -y`

## 二、 遇到的问题及解决办法
在安装过程中遇到了以下问题，经过排查后均成功解决：

1. **问题：`sudo apt update` 报错 404 Not Found (涉及中科大镜像源)。**
   - **原因**：配置的源路径失效（`/ros2/ubuntu` 路径不存在），且与 ROS 1 的源产生冲突。
   - **解决**：删除所有错误的源文件（`sudo rm -rf /etc/apt/sources.list.d/*ros*`），替换为清华镜像源，再执行 `sudo apt update` 即可。
2. **问题：`rosdep update` 网络连接超时 (socket.timeout)。**
   - **原因**：国内网络环境限制，无法访问 GitHub 相关资源。
   - **解决**：由于该工具非核心运行必需品，暂时跳过。后续使用国内一键配置工具（如小鱼工具）修复了该网络问题。
3. **问题：运行 `turtlesim` 后，键盘方向键无法控制小海龟移动。**
   - **原因**：终端窗口焦点丢失，`turtle_teleop_key` 节点只接收焦点所在窗口的按键。
   - **解决**：鼠标点击 `rosrun turtlesim turtle_teleop_key` 所在的终端窗口，确保光标闪烁，再按方向键即可正常控制。

## 三、 运行结果
已成功配置 ROS Noetic 环境，并通过 `roscore`、`turtlesim_node` 及 `turtle_teleop_key` 完成了小海龟的运动测试，各项功能运行正常。
## 四、 附件
- 版本截图及小海龟录屏：请见本仓库根目录下的附件文件。
