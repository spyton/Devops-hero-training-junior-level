# vagrant setup

既然我们的训练方式是针对特定场景下的, 所以需要使用vagrant搭建和配置虚拟机来获得相应的训练场景,  每个场景的状态都可以用vagrantfile来描述并且能够分享给社区同步配置. 节省每次训练中场景配置的时间, 从而获得更高效的训练成果.&#x20;

## virtualbox 安装

在安装vagrant之前, 首先需要安装virtualbox开源跨平台工具,  支持Linux, Mac os X和windows, 下载安装地址: [http://virtualbox.org](http://virtualbox.org)

## vagrant 安装

vagrant本身也是开源多平台工具, 支持macOS, windows和Linux操作系统, vagrant下载地址: [https://www.vagrantup.com/Downloads](https://www.vagrantup.com/Downloads)

按照提示安装成功后, 在terminal输入 vagrant --version 后会看到安装的版本.&#x20;

```
vagrant --version
Vagrant 2.2.19
```
