# git configuration

#### git config 命令行

git的配置首先可以用CLI (command-line interface)来控制和修改, 但是因为git config命令行繁杂且难以记忆, 使用频率偏低, 作为devops在实际工作中都会直接修改gitconfig文件. 值得记忆的命令行其实2个就够了:

查看所有git配置参数,如果不显示,则说明当前没有任何git配置.

```
git config -l
```

查看git配置文件位置以及管理范围(scope).

```
git config --list --show-origin --show-scope
```

{% hint style="info" %}
git 2.23版本后支持--show-scope, 可以通过git --version来查当前版本, 这个命令的好处是所有类型的操作系统(mac os, linux , windows) 都适用 (配置文件位置路径在不同操作系统中是不一样的) .
{% endhint %}

<figure><img src="../.gitbook/assets/Capture d’écran 2023-02-28 à 23.33.11.png" alt=""><figcaption><p>command output</p></figcaption></figure>

#### git的3层配置文件

git分3层逐个顺序读取配置文件: System->Global-> Local , 每遇到**重复的配置**参数都会重载(overwrite)之前一层的参数. 比如如果你在global层定义了一个git user参数, 而且local层定义了另一个git user参数, 最终git会采用最后一个层也就是local层的git user参数.

<figure><img src="../.gitbook/assets/Capture d’écran 2023-02-28 à 23.20.35.png" alt=""><figcaption><p>3 layer configuration file</p></figcaption></figure>

#### git的重要配置参数

git配置文件是ini格式由\[section]和parameter组成, 最主要的几个配置有

<figure><img src="../.gitbook/assets/Capture d’écran 2023-02-28 à 23.49.52.png" alt=""><figcaption><p>git config file</p></figcaption></figure>

* user.name 和 user.email

基础用户配置, 需要用户名(user.name)和用户邮箱(user.email), 否则在commit时git会自动要求配置, 填入后会在commit 的作者(author)栏看到user.name \<user.email>的信息.

* core.editor

git编辑器, 默认从系统环境变量中读取, 用户可以设置为自己喜欢的编辑器, 比如vim, vscode等等

* credential.helper

可以设置为store, 用来在系统硬盘上储存git远程代码仓库的用户名和密码, 在远程连接时自动加载, 避免每次push时手动输入用户名和密码.

{% hint style="info" %}
如果helper设置为store, git会在用户HOME文件下生成一个隐藏文件 .git-credentials, 用户名和personal access token (ghp\_\*\*\*\*\*\*\*)会出现在此文件中, 例如[https://user:pass@example.com](https://user:pass@example.com), 从安全角度讲, 通常此文件只能依赖系统文件权限(默认是600 : 只本用户可读写)对用户名密码进行保护, 所以定期对代码仓的个人personal access token进行更新是很有必要的安全意识.
{% endhint %}
