# vagrant command

便于顺利进入训练的场景, 保持干净的训练环境, 这里介绍几个常用的vagrant命令.

## vagrant init

在当前文件夹内初始化一个Vagranfile,  可以设定box( config.vm.box ) 和其指定下载的url地址, 常用的flag有-f(强制初始化, overwrite原有的Vagranfile) 和 -m (只保留Vagrantfile内运行的内容, 删除注释提示)&#x20;

```
vagrant init -f -m config.vm.box config.vm.box_url
#例如: 产生一个ubuntu trusty64系统的Vagrantfile
vagrant init -f -m ubuntu/trusty64 app.vagrantup.com/ubuntu/boxes/trusty64
```

## vagrant up&#x20;

当前文件夹内生成Vagrantfile后, 就可以运行Vagranfile配置的虚拟机, 在文件夹内运行

```
vagrant up                                                                 
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'ubuntu/trusty64'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'ubuntu/trusty64' version '20190514.0.0' is up to date...
==> default: Setting the name of the VM: test_default_1679768579200_26726
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default: 
    default: Guest Additions Version: 4.3.40
    default: VirtualBox Version: 6.1
==> default: [vagrant-dns] TLD but no host_name given. No patterns will be configured.
vagrant-dns: trying to stop process with pid 12062 sending TERM and waiting 20s ...
vagrant-dns: process with pid 12062 successfully stopped.
vagrant-dns: process with pid 13179 started.
==> default: Restarted DNS Service
==> default: Mounting shared folders...
```

## vagrant ssh

虚拟机成功运行后, 可以在文件夹内运行vagrant ssh进入虚拟机, 如果Vagrantfile内配置了多个虚拟机(比如定义个一个kubernetes cluster) 可以使用vagrant status先查看虚拟机名称, 单个虚拟机运行时, 默认为default

```
vagrant ssh vm_name
```

## vagrant reload

如果需要更新虚拟机配置, 首先需要对Vagrantfile进行修改, 然后在文件夹内运行

```
vagrant reload
==> default: Attempting graceful shutdown of VM...
==> default: Checking if box 'ubuntu/trusty64' version '20190514.0.0' is up to date...
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
```

可以看到vagrant首先停止当前虚拟机,然后重新启动更新配置后的虚拟机.

## vagrant halt

正常(graceful)停止当前文件夹内vagrantfile配置的虚拟机, 如果当前配置了多个虚拟机,可以使用vagrant status先查看虚拟机的name或者id, 然后使用

> graceful shutdown 虚拟机首先会正常关闭运行中的进程, 然后在关闭虚拟机本身, 而非强制停机, 造成进程关闭错误

```
vagrant halt name 或者 id 
```

## vagrant suspend

如果需要存储当前虚拟机的运行状态, 比如有数据库或者程序运行中, 可以使用suspend命令, 挂起虚拟机, 虚拟机内存会保存在主机的硬盘上, 当再次使用vagrant resume恢复虚拟机时, 虚拟机会快速恢复在suspend时的运行状态, 不会从最开始守护进程重新启动.&#x20;

## vagrant destroy

训练完毕后, 可以使用destroy将虚拟机删除, 不同于halt或者suspend, destroy会将此虚拟机在硬盘产生的内容全部删除, 回到vagrant up前的初始状态.&#x20;

## vagrant box

用来管理vagrant中的虚拟机镜像, 通常使用list来查看本地vagrant管理的镜像. 并使用add和remove进行添加与删除操作.

## vagrant global-status

用来查看vagrant运行的所有虚拟机,运行状态和对应vagrantfile所在文件夹, 在运行较多虚拟机后, 有些虚拟机并未使用halt或destroy关闭, 它们会一直运行在vagrant环境内, 消耗本机后台资源以及电池使用. 是每次训练后非常有用的查看命令.&#x20;

