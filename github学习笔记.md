# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [常见问题](#常见问题)
      * [push到Github每次都要输入密码](#push到github每次都要输入密码)

<!-- Added by: bmk, at: 2018-04-12T15:54+0800 -->

<!--te-->

----

# 常见问题

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
