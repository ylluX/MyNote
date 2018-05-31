# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [常见问题](#常见问题)
      * [参考资料](#参考资料)
      * [修改远端仓库的标签](#修改远端仓库的标签)
      * [push到Github每次都要输入密码](#push到github每次都要输入密码)
      * [一台电脑同时使用GitLab和GitHub仓库](#一台电脑同时使用gitlab和github仓库)
   * [ssh-keygen](#ssh-keygen)

<!-- Added by: luyl, at: 2018-05-31T09:38+08:00 -->

<!--te-->

----

# 常见问题



## 参考资料

[Pro Git中文版](http://iissnan.com/progit/)

[GitHub详细教程 - 后山人的专栏 - CSDN博客](https://blog.csdn.net/lishuo_os_ds/article/details/8078475)

[]()



## 修改远端仓库的标签

```
# 创建该远成库：git remote add 远程库名 远程库地址
git remote add origin git@github.com:ylluX/hello-word.git
git remote add neworigin https://github.com/ylluX/hello-word.git

# 删除该远程库：git remote remove 远程库名
git remote remove origin

# 改变远程库的名字
git remote rename 旧名称 新名称
git remote rename origin origin1
```




## push到Github每次都要输入密码

[push到Github每次都要输入密码](https://blog.csdn.net/wozaixiaoximen/article/details/49487285)

[初次安装git配置用户名和邮箱](https://www.cnblogs.com/superGG1990/p/6844952.html)

push 到 Github 每次都要输入密码，原因是使用了 Https 的方式添加远程仓库

`git remote add origin https://github.com/weiheli/UCenter.git`

查看 push 和 fetch 方式

```
git remote -v 
```

结果：

```
origin	https://github.com/ylluX/python_script.git (fetch)
origin	https://github.com/ylluX/python_script.git (push)
```

可以使用ssh解决

创建SSH Key，把id_rsa.pub中的内容添加到 Github 的Deploy keys

首先，生成密钥对，可以用 ssh-keygen 来创建：

```
ssh-keygen -t rsa -C "your_email@youremail.com"
```

填写密钥的保存位置（默认~/.ssh）和密码，就生成了密钥（id_rsa）和公钥（id_rsa.pub）

然后，添加公钥到你的远程仓库（github）

登陆你的github帐户。点击你的头像，然后 Settings -> 左栏点击 SSH and GPG keys -> 点击 New SSH key

然后你复制上面的公钥内容，粘贴进“Key”文本域内。 title域，自己随便起个名字。

点击 Add key。

完成以后，验证下这个key是不是正常工作：

```
ssh -T git@github.com
```

最后，修改git的remote url

```
git remote rm origin
git remote add origin git@github.com:ylluX/python_script.git
```

之后，你就可以愉快的使用git fetch, git pull , git push，再也不用输入烦人的密码了




## 一台电脑同时使用GitLab和GitHub仓库

[一台电脑同时使用GitLab和GitHub仓库](https://blog.csdn.net/KingBoyWorld/article/details/69221031?locationNum=1&fps=1)



# ssh-keygen

* [SSH配置以及多个SSH & config文件](https://blog.csdn.net/wiki_su/article/details/50247551)
* [在Windows下清除ssh-key私钥访问密码](https://www.jianshu.com/p/3543f71dca9a)
* [ssh-keygen之后，生成的密码都叫id_rsa.pub，我想改名不行吗？](https://segmentfault.com/q/1010000005698184)
