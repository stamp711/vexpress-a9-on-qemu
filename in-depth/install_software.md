# 安装所需的软件

在虚拟机桌面中，按 `Ctrl + Alt + T` 打开终端。

## 更改 APT 的源为清华大学 TUNA 镜像源

为了获得更快的下载速度，我们更改 APT 的源为清华大学 TUNA 镜像源:

```bash
# 先备份一个
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bakup
```

> `sudo` 表示以 root 权限来执行后面的命令，你需要具有管理员权限的账户才能使用 `sudo`。使用 `sudo` 时，你需要输入密码；输入密码后，在一段时间内再次使用 `sudo` 将不需要输入密码。

```bash
# 然后替换一下地址...
sudo sed -i "s|//.*archive.ubuntu.com|//mirror.tuna.tsinghua.edu.cn|" /etc/apt/sources.list
```

> 上面的命令所做的事情是：在 `/etc/apt/sources.list` 中每一行搜索 `//*archive.ubuntu.com`，并将搜索到的第一个结果替换成 `//mirror.tuna.tsinghua.edu.cn`。
>
> 这么干并不能替换列表中所有的软件源地址（不符合 `http(s)://*archive.ubuntu.com` 形式的地址），不过之后需要进行大量下载的源已经被替换了。

更新软件源列表：

```bash
sudo apt-get update
```

## 安装虚拟机附加程序（如果你还没有安装的话）

如果你使用的是 VirtualBox，并且还没有安装虚拟机附加程序，可以：

```bash
sudo apt-get install virtualbox-guest-additions-iso
```

如果你使用的是 VMware Workstation，并且还没有安装虚拟机附加程序，可以：

```bash
sudo apt-get install open-vm-tools
```

## 安装实验所要用到的的软件

安装一些要用到的东西

```bash
sudo apt-get -y install libncurses5-dev curl git
```

> `libncurses5-dev` 是 `menuconfig` 时显示菜单的依赖库，`curl` 是网络传输工具（可以用来下载文件），`git` 是版本管理工具。

安装交叉编译器：

```bash
# -y 表示无需确认
sudo apt-get install -y gcc-arm-linux-gnueabi g++-arm-linux-gnueabi
```

> `gcc` 是 C 编译器，`g++` 是 C++ 编译器。

安装 QEMU：

```bash
sudo apt-get install -y qemu
```

> 安装 QEMU 时，`qemu-system` 和 `qemu-utils` 会被自动安装，所以不需要手动输入。