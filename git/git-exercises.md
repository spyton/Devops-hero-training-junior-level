# git exercises

无论是dev还是devops只要是涉及代码管理和版本控制, 都需要熟练掌握git, 可以说没有git, 你写的代码“寸步难行”. 甚至有些团队内部会有git故事会, 在代码评审中, 每一个commit都需要独立讲出它的背景,用法,目的等等.将commit贡献作为KPI考核. 不过在有些devops的招聘简介里面, HR有时不会把git写为能力要求, 有时会造成求职者忽视git的精进用法,在面试和工作中无法和团队高效沟通和协作. 这就是git hero场景训练的目的之一, 让大家重视git, 把它作为devops learnig path中重要的基础一环, 为devops打下坚实的基础.&#x20;

## git config&#x20;

在project文件夹内启动虚拟机, 关于vagrant的安装请看vagrant setup.
```
vagrant up
```
进入虚拟机后, 首先列出git所有配置参数
```
vagrant@ubuntu-bionic:~$ git config -l
core.editor=vim
```
由于在虚拟机配置文件vagrantfile里我们初始化git的编辑器配置为vim, 所以此命令会显示core.editor配置
然后列出所有配置文件位置(path)以及范围(scope)
```
vagrant@ubuntu-bionic:~$ git config --list --show-origin --show-scope
system  file:/etc/gitconfig     core.editor=vim
```
这里可以看到系统git配置文件存储在/et/gitconfig, 然后我们可以打开此文件并配置用户名和邮箱
{% hint style="info" %}
/etc/gitconfig需要sudo权限才能修改
{% endhint %}
添加以下部分进入/etc/gitconfig
```
[user]
        email = training@devops.com
        name  = training
```
重新查看所有git配置会发现新的user配置加入到了系统范围中(scope), 进入git\_commands\_training文件夹并执行git\_config.sh脚本, 之后发现git用户名由training变为training\_home.&#x20;
```
vagrant@ubuntu-bionic:~/git_commands_training$ sh git_config.sh
vagrant@ubuntu-bionic:~/git_commands_training$ git config --get user.name
training_home
```
{% hint style="info" %}
这里可以根据git的3层配置文件来理解此处git用户名的变化
{% endhint %}