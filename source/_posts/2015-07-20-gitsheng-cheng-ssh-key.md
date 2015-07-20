---
layout: post
title: "Git生成SSH Key"
date: 2015-07-20 10:37:02 +0800
comments: true
categories: 
---

### 生成 Mac OSX Git SSH Key

[翻译自https://help.github.com/articles/generating-ssh-keys/](https://help.github.com/articles/generating-ssh-keys)
 
 
 
###  步骤 1 检查SSH Key

首先，我们需要检查SSH Key是否在电脑上存在。打开命令行工具，输入：

```
ls -al ~/.ssh
```


检查所列目录是否存在一个public SSH Key.  默认的情况，public ssh key 是以下几种:

```
id_dsa.pub
id_ecdsa.pub
id_ed25519.pub
id_rsa.pub
```

如果你看到存在一对公有，私有的key(比如  id_rsa.pub and id_rsa )，就表明您曾经连接过Github, 这时候你可以选择跳过 第二步直接操作第三步

如果报错，也不用担心，我们将在第二步创建

###  步骤 2  生成新的 SSH key

命令行输入：

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

*然后接着如下操作:*

```
 Enter file in which to save the key (/Users/you/.ssh/id_rsa):    //您直接回车就可以了
 Enter passphrase (empty for no passphrase):  //输入您的密码
 Enter same passphrase again:  //再次输入您的密码
```

*完成后将出现如下输出：*

```
 Your identification has been saved in /Users/you/.ssh/id_rsa.
 Your public key has been saved in /Users/you/.ssh/id_rsa.pub.
 The key fingerprint is:
 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
```

###  步骤 3  添加 key 到 ssh-agent

*命令行输入：*

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```


###  步骤 4 添加你的 SSH key 到你的账户

```
pbcopy < ~/.ssh/id_rsa.pub
```
这样生成的key您就完成了拷贝，然后您在添加到您的Github账户中

###  步骤 5  测试连接
*打开命令行输入：*


```
ssh -T git@github.com
```

当出现：Hi username! You've successfully authenticated, but GitHub does not
 provide shell access. 就表示一切操作成功啦！

