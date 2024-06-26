---
date:
  created: 2023-06-01
tags:
  - Yanshee
  - AI
  - robotics
  - competition
  - optimization
  - system
  - Raspberry Pi
categories:
  - Robotics
  - Yanshee
comments: true
---

# 关于我和 Yanshee 的那些事 - 系统优化篇

关于系统优化，在之前的文章中已经涉及一部分。这篇文章主要是为了补上一些其他方面的注意事项。<!-- more -->如果有一些其他方面的问题，欢迎在讨论区提出。

## 系统安全 {#Safety}

Yanshee 机器人的系统安全自然没有那么重要，但**防人之心不可无**嘛，这里最好提及一下。

### 重设密码 {#Setpasswd}

机器人出厂时设置了统一密码，可能会带来安全隐患（正如警告窗口所提出的），并且这个密码默认情况下是 ssh 服务、VNC 所共用的。为了避免自己的机器人被他人操控，建议设置一个安全的密码：

```sh
sudo passwd
```

!!! info inline end "提示"

    Yanshee 的 `sudo` 指令，`pi` 用户可以直接使用，输入新密码即可。

## 优化调节 {#Optimize}

### 配置程序 {#Confprog}

Yanshee 机器人系统自带了优化程序（`首选项` -> `Raspberry Pi Configuration`），可以按上面的说明自行调节。

!!! warning "注意"

    不建议调节 `Camera` `SSH` `VNC` 的开关。除非确定不会使用，否则会造成很大的麻烦。

### 软件包管理 {#Pkgs}

另外，如果觉得机器人安装的软件太多（或太少），可以自己打开终端，做一些想要的改动。这里推荐安装一个命令行管理软件：`aptitude`，比用 `apt` 管理软件要稍微方便一些。

```sh
sudo apt install aptitude
```

!!! warning "注意"

    不推荐升级，由于一些软件源的签名问题，以及依赖问题，强制升级会破坏你的机器人！

## 救急方案 {#Rescue}

如果我一不小心搞坏了自己的机器人（指的是：桌面无法正常出现，这样软件上的问题），该怎么办？

- 首先，可以试试用 SSH 连接机器人，看看是否正常进入 Shell。
- 如果可以进入，则最好看一下系统日志 (`journalctl -xr`)，具体是哪方面的问题。
- 如果你记得在出现问题前做了些什么，或许可以手动恢复。（比如，禁用的服务，安装/移除的软件包等等）
- 如果误删了文件或是根本无法进入系统，建议送交专业人员进行处理。
