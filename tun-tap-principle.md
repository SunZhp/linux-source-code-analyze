# TUN/TAP设备原理与实现

`TUN/TAP设备` 是Linux下的一种虚拟设备，相对虚拟设备来说，一般计算机所使用的网卡就是物理设备。物理设备有发送和接收网络数据包的能力，而虚拟设备的作用就是模拟物理设备，提供特殊的发送和接收功能。

由于 `TUN/TAP设备` 是虚拟的设备，所以不能像网卡一样从网络中接收数据包，那么 `TUN/TAP设备` 从哪里读取数据，又把数据发送到哪里去呢？下面通过一张图来阐述 `TUN/TAP设备` 的工作方式 (图片来源于https://www.ibm.com/developerworks/cn/linux/l-tuntap/index.html )：

![TUN/TAP](https://www.ibm.com/developerworks/cn/linux/l-tuntap/images/image002.jpg)

上图的右下角是物理网卡设备，它能从 `物理链路` 读取和发送数据。

而左下角是 `TUN/TAP设备`，可以看出 `TUN/TAP设备` 连接着 `字符驱动` 和 `TCP/IP协议栈`，这就是说可以通过 `read()` 和 `write()` 系统调用来对 `TUN/TAP设备` 进行数据的读写操作，而读写的数据会经过 `TCP/IP协议栈`。

其实 `TUN/TAP设备` 并没有对外网发送数据这个功能，如果需要对外网发送数据，必须通过路由转发才能实现。也就是通过构建发送到外网的数据包，然后通过路由转发来发送出去。

## TUN/TAP设备使用

