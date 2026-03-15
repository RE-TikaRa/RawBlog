---
title: Vmware系列-Ubuntu断网修复指南
thumbnail: 'https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png'
excerpt: 对于VMware下Ubuntu断网的几种修复方式
banner: 'https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png'
password: ''
abstract: '有东西被加密了, 请输入密码查看.'
message: '您好, 这里需要密码.'
wrong_pass_message: '抱歉, 这个密码看着不太对, 请再试试.'
wrong_hash_message: '抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.'
expires: '10000-01-01 07:59:59'
tags:
  - VMware
  - Ubuntu
categories:
  - VMware
abbrlink: '40349006'
date: 2026-02-12 20:50:43
sticky:
---

## 写在最前

- **宿主机**：是指安装了 VMware 软件并运行虚拟机的物理计算机（通常是您的 Windows 电脑）。
- **虚拟机**：是指在 VMware 中运行的操作系统环境（本文特指您遇到断网问题的 Ubuntu 系统）。

在开始任何复杂操作之前，请务必执行以下步骤，以减少不必要的麻烦：

1.  **关闭防火墙与安全软件**：建议暂时关闭 **宿主机** 的 Windows Defender 以及其他第三方杀毒软件。防火墙有时会拦截虚拟机的网络连接或 DHCP 请求，这是导致断网的常见原因。
2.  **创建快照备份**：在进行任何配置修改之前，强烈建议使用 VMware 的“快照”功能备份当前状态。如果修改导致问题恶化，您可以随时一键还原。

## 实践建议

如果虚拟机出现网络图标消失或无法联网的情况，建议优先排查**情况一**（Windows 服务状态）。这是最常见且修复成本最低的问题。

如果服务正常，请依次尝试**情况二**（NetworkManager 配置）和**情况三**（VMware 桥接网络）。

若按照前三种情况均无法修复，请将 **虚拟机**（Ubuntu）的网络配置回退至**情况三**之前的状态，然后尝试**情况四**（路由表）或**情况五**（NAT 模式）。

## 工具准备

### 基础网络工具

我们将需要使用 `net-tools` (提供 `ifconfig` 命令) 或 `iproute2` (提供 `ip` 命令) 来查看网络状态。这两者功能类似，您可以根据习惯选择其一。

#### net-tools (使用 ifconfig)

```bash
sudo apt update
sudo apt install net-tools
```

如果 **虚拟机** 无法联网，可在 **宿主机** 下载源码包（[net-tools 项目页](https://sourceforge.net/projects/net-tools/)），传输至虚拟机后编译安装：

```bash
cd ~/下载
tar -xf net-tools-2.10.tar.xz
cd net-tools-2.10
./configure
make
sudo make install
```

#### iproute2 (使用 ip addr)

建议确认 `iproute2` 工具可用，现代 Linux 发行版通常预装此工具。

```bash
sudo apt update
sudo apt install iproute2 iputils-ping
```

如果无法联网，可在 **宿主机** 下载 `iproute2` 与 `iputils-ping` 的 `.deb` 安装包，拷贝到虚拟机后执行安装：

```bash
cd ~/下载
sudo dpkg -i ./*.deb
sudo apt -f install
```

## 情况一：宿主机服务未启动

很多时候“断网”仅仅是因为 VMware 的后台服务被关闭了。请首先在 **宿主机**（Windows）上进行检查。

1.  按下 `Win + R` 键，输入 `services.msc` 并回车。
2.  在服务列表中找到并检查 `VMware DHCP Service` 和 `VMware NAT Service`。
3.  确保这两个服务的状态为 **正在运行**。
4.  建议将这两个服务的启动类型设置为 **自动**，以免下次重启后再次失效。

![windows服务](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/refs/heads/main/image-20260213010000011.png)

## 情况二：NetworkManager 未接管

如果服务正常但 Ubuntu 仍不显示有线连接图标，常见原因是 NetworkManager 服务未正确接管网卡。

![问题示例](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/refs/heads/main/20260212224250931.png)

### 启用 NetworkManager 管理接口

编辑前建议先备份配置文件：

```bash
sudo cp /etc/NetworkManager/NetworkManager.conf /etc/NetworkManager/NetworkManager.conf.bak
sudo vim /etc/NetworkManager/NetworkManager.conf
```

确保文件中包含以下内容：


```ini
[ifupdown]
managed=true
```

![NetworkManager 配置](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260212225114347.png)

### 检查全局设备管理配置

编辑全局配置文件：

```bash
sudo vim /usr/lib/NetworkManager/conf.d/10-globally-managed-devices.conf
```

确保有线网卡（`ethernet`）未被排除在管理之外。如果存在 `unmanaged-devices` 字段，需确保其允许 `ethernet` 设备。

![全局设备配置](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260212225528115.png)

### 重启 NetworkManager

重启网络管理服务：

```bash
sudo systemctl restart NetworkManager
```

按照以下命令检查网络状态：

```bash
ip -br addr
ip route
```

### 若仍未恢复，清理状态缓存后重启

执行以下命令重置状态并重启系统：

```bash
sudo systemctl stop NetworkManager
sudo rm -f /var/lib/NetworkManager/NetworkManager.state
sudo systemctl start NetworkManager
sudo reboot
```

{% notel blue 情况解析：NetworkManager 未接管 %}
问题的核心在于让 NetworkManager 重新接管虚拟以太网卡并重建设备状态。很多“断网”现象并非驱动失效，而是网络接口被错误标记为“不受管理”（unmanaged），导致 DHCP 获取 IP 与路由下发流程无法执行。
{% endnotel %}

## 情况三：配置静态 IP (桥接模式)

如果系统未分配 IP 地址且任务栏不显示网络图标，请按以下步骤操作。

### 查看当前网络状态

查看 IP 地址：

```bash
ifconfig
# 或者使用
ip addr
```

### 重置 NetworkManager 服务

在终端依次执行以下命令（推荐使用 systemctl）：

```bash
sudo systemctl stop NetworkManager
sudo rm /var/lib/NetworkManager/NetworkManager.state
sudo systemctl start NetworkManager
sudo reboot
```

### 配置 VMware 桥接网络

系统重启后，需要确保 VMware 的网络配置为桥接模式，并正确桥接到 **宿主机** 的物理网卡（通常是无线网卡或有线网卡）。

**简述**：桥接模式下，虚拟机相当于局域网中的独立设备。

操作路径：

```text
VMware 菜单 -> 编辑 -> 虚拟网络编辑器
```

将虚拟机的网络适配器设置为桥接模式。**宿主机** 网卡的具体名称取决于您的实际硬件，请参考下图确认您的 **宿主机** 网卡以及 **宿主机** IP 地址。

![image-20260213004531438](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213004531438.png)

![image-20260213003948349](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213003948349.png)

![image-20260213004142505](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213004142505.png)

![image-20260213004416178](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213004416178.png)

### 进入 Ubuntu 网络设置

打开 **虚拟机** 的系统网络设置界面，准备手动配置 IP。

![image-20260213004735588](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213004735588.png)

### 设置静态 IP 地址

将网络配置为手动（静态 IP），并确保 IP 地址与 **宿主机** 处于同一网段，且该 IP 未被局域网内其他设备占用。

配置示例：

- **网关**：192.168.1.1（请填写 **宿主机** 所在局域网的真实网关）
- **子网掩码**：255.255.255.0
- **IPV4 地址**：192.168.1.X（X 为同网段下未使用的地址。**提示**：您可以在 **宿主机** 终端中 `ping 192.168.1.X`，如果显示“无法访问目标主机”或“请求超时”，说明该 IP 基本可用。）

![image-20260213004921221](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213004921221.png)

### 应用配置并验证

点击应用后，在终端再次执行：

```bash
ifconfig
```

检查 IP 地址是否已更新。如果仍显示旧地址，请尝试关闭并重新开启网络连接开关，再次检查。

### 连通性测试

静态 IP 配置成功后，进行以下测试：

- **宿主机** 是否可以 ping 通 **虚拟机**（Ubuntu）。
- **虚拟机**（Ubuntu）是否可以访问互联网。

如果 **宿主机** 能 ping 通 **虚拟机** 但虚拟机无法上网，需进一步检查路由表配置。

## 情况四：路由表异常

如果配置了静态 IP 仍无法访问网络，可能是路由表存在异常。

### 查看路由表

在终端执行：

```bash
route
```

### 清空主路由表

```bash
sudo ip route flush table main
```

### 重新添加默认路由

```bash
sudo route add default gw 192.168.1.100
sudo route add default gw 192.168.1.1
```

说明：

- `192.168.1.100`应替换为您之前设置的 **虚拟机静态 IP**。
- `192.168.1.1` 应替换为 **宿主机** 所在局域网的网关地址。

完成后重新测试网络连接。

## 情况五：虚拟机 NAT 网络配置

如果桥接模式无法使用（例如在校园网等复杂认证环境下），可尝试使用 NAT 模式。

**简述**：NAT 模式下，虚拟机通过宿主机共享网络，兼容性最好。

### 虚拟机网络模式设置

在 VMware 虚拟机设置中，将网络适配器模式修改为 **NAT 模式**。

![image-20260213005113744](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213005113744.png)

### 配置 VMware 虚拟网络

打开 VMware 菜单：

```text
编辑 -> 虚拟网络编辑器
```

在列表中选择 **VMnet8（NAT 模式）**，点击 **更改设置**（需要管理员权限）。

![image-20260213005221650](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213005221650.png)

在 VMnet8 的配置界面中，确保勾选以下选项：

- [x] NAT 模式
- [x] 将主机虚拟适配器连接到此网络
- [x] 使用本地 DHCP 服务将 IP 地址分配给虚拟机

记录下方的 **子网 IP** 地址，例如：

```text
192.168.137.0
```

此地址段在后续配置中需保持一致。

![image-20260213005258404](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213005258404.png)

![image-20260213005414247](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213005414247.png)

### 配置宿主机网络共享

在 **宿主机**（Windows）中打开：

```text
控制面板 -> 网络和 Internet -> 网络连接
```

您通常会看到：

- `VMnet1`：仅主机模式适配器
- `VMnet8`：NAT 模式适配器

找到 **宿主机** 当前正在使用的物理网络适配器（例如 `WLAN` 或 `以太网`），右键点击选择 **属性** -> **共享** 选项卡。

勾选 **“允许其他网络用户通过此计算机的 Internet 连接进行连接”**，并在家庭网络连接中选择 **VMnet8**。

![image-20260213005530143](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213005530143.png)

![image-20260213005554134](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213005554134.png)

系统会提示本地 LAN 适配器将被设置为某个 IP（通常是 `192.168.137.1`）。

![image-20260213005626479](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213005626479.png)

### 验证 VMnet8 地址

在 **宿主机** 网络连接界面，右键点击 **VMnet8** -> **状态** -> **详细信息**，确认 IPv4 地址是否已自动配置为网关地址（例如 `192.168.137.1`）。

![image-20260213005732455](https://raw.githubusercontent.com/RE-TikaRa/ImgHosting/main/image-20260213005732455.png)

### 启动虚拟机测试网络

启动 **虚拟机**（Ubuntu），系统应自动获取 IP 并连接至互联网。可打开浏览器进行测试。

### 注意：子网地址一致性

VMnet8 的地址可以根据需要调整，但必须保证以下通过 **宿主机** 和 **VMware** 设置的地址处于同一网段：

1.  VMware 虚拟网络编辑器中的 **子网 IP**。
2.  **宿主机** 上 VMnet8 适配器的 **IPv4 地址**。

例如：
- 宿主机 VMnet8：`192.168.137.1`
- VMware 子网 IP：`192.168.137.0`

### 重启后无法联网排查

如果 **宿主机** 重启后虚拟机无法联网，请再次检查 **情况一** 中提到的 Windows 服务状态，或尝试重新安装VMware。
