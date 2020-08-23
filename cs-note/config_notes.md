# 远程登录

## 背景
用的Mac，平时需要通过跳板机去登录多个线上机器，而跳板机的登录是需要token的。
## 工具
1. iTerm2。
2. tmux。

## 配置
1. 首先解决每次登录跳板机需要密码的问题。在`~/.ssh/config`的文件中如下配置：
```
Host [跳板机的ip地址]
ServerAliveInterval 10
ControlMaster auto
ControlPath ~/.ssh/%r@%h:%p
User [用户名]
Port [端口]
```
其中：
`ServelAliveInterval`定时发送心跳包
`ContolMaster和ControlPath`会话共享
这样的配置使得首次登录跳板机后不再需要密码。可以使用命令`ssh -fN [ip地址]`来进行后台首次登录。

2. 确保跳板机上安装了tmux，希望登录跳板机后创建或选择tmux会话来登录各个远程服务器。新建一个脚本文件如`~/.ssh/ssh_tmux`:
```
ssh [跳板机的ip地址] "tmux ls" & read session && ssh [跳板机的ip地址] -t "tmux attach -t ${session:-default} || tmux new -s ${session:-default}"
```
该脚本首先列出跳板机上的tmux seeion，然后从终端读入一个session名称，试图attach或创建一个新的session。可以在iterm2的Profiles配置快捷键，快速调用该脚本。
3. 在跳板机上编写选择远程机器的脚本，如下：
```
#!/bin/bash
ips=([user@ip] #常用需要登录的ip地址
[user@ip]
)

echo "Choose a machine which you want to login: "
select var in "${ips[@]}";do
break;
done
printf "\ropitpm"
printf "\r######" #后面会解释.
echo
echo "ssh ${val}"
cmd="ssh ${val}"
${cmd}
```
配置文件中的`opitpm`是为了让iterm2捕获这个字符串然后弹出password manager，可以在Profiles中Triggers进行相关配置。其中使用printf是为了用`######`快速覆盖`opitpm`这个字符串，不让iterm2每次捕获过时的`opitpm`就弹出password manager。接着在password manager上填上日常使用的密码。运行该脚本可以配置快捷键入alias kl='bash xxx'

4. 最后日常的登陆步骤就是这样：运行`ssh -fN ...`首次登录跳板机，然后调用`~/.ssh/ssh_tmux`脚本进入跳板机上的一个tmux会话，使用kl快捷键选择要登录的远程服务器地址，然后会弹出password manager，选择密码登录即可。