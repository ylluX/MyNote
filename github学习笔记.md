# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [基本概念](#基本概念)
   * [常见问题](#常见问题)
      * [参考资料](#参考资料)
      * [修改远端仓库的标签](#修改远端仓库的标签)
      * [push到Github每次都要输入密码](#push到github每次都要输入密码)
      * [一台电脑同时使用GitLab和GitHub仓库](#一台电脑同时使用gitlab和github仓库)
      * [git如何clone所有的远程分支](#git如何clone所有的远程分支)
      * [git本地的撤销修改和删除操作](#git本地的撤销修改和删除操作)
   * [常见操作](#常见操作)
      * [分支(branch)](#分支branch)
      * [log](#log)
      * [标签(tag)](#标签tag)
   * [ssh-keygen](#ssh-keygen)

<!-- Added by: luyl, at: 2018-08-08T14:33+08:00 -->

<!--te-->

----

# 基本概念

* [Git仓库分支(Branch)和标签(Tag)](https://blog.csdn.net/iprettydeveloper/article/details/53944125)
* [GIT分支管理是一门艺术](http://roclinux.cn/?p=2129)

基于我们当前团队的协作能力和提交代码的质量水平，并考虑方便持续集成CI（自动化构建、 
测试、发布），我们约定下列常驻Branch：

* **develop** 分支：顾名思义即持续开发的分支，我们希望每个开发组都在这个分支上保 
持线性的持续小步迭代，正常的CodeReview WorkFlow和开发级的自动CI也在这里进行。 
当开发完一个迭代(Sprint)，开发小组有信心转测时，就将代码合并到 release 分支， 
并要求打一个alpha级的Tag(如5.2.0-alpha)
* **release** 分支：顾名思义即用于发布过程的分支，包括开发转测(实际上我们认为这里的测试集成测试)、测试和BugFix以及发布上线的过程，当发布成功时要打一个发布beta Tag(如 
5.2.1-beta)，并将代码合并到 master 分支
* **master** 分支：即有质量保证的、可安全运行的分支，禁止直接代码提交，避免被污染，仅用 
于代码合并和归集，在这个分支上的代码应该永远是可用的、稳定的。当需要拉一个特别的开发分时， 
应该基于 master。

当需要fix线上的一个问题是，应该基于上线时的那个beta Tag做hotfix。当出现线上Bug需要hotfix时，我们需要在上次上线的Tag处拉一个临时的 hotfix 分支进行 
修正，或者在未被其他开发迭代污染的release分支上直接hotfix上线并合并到master和 
develop，然后打一个新的Tag(如5.2.2-beta）

这个分支体系是我们期望长期持续迭代的分支规划，其它临时分支的删除、创建、命名，都由团队自己 
决定，保持一定的灵活性。但每个团队都应该努力避免对上述常规情况造成破坏的情况发生，如果有特 
殊情况（如有两个并行的开发分支同步进行），需要由各组Leader和QA团队协商提供临时方案，这会 
影响到团队协同中的转测、CI基准分支等。

关于打 Tag 的规则 ：

鼓励开发和QA团队共同对勤于打Tag，这便于真正的版本管理，避免有rollback需要或者需要查看和 
对比历史版本的时候的混乱和低效局面。但同时也要求一定的规范性，让人一看便知。

Tag格式为： MajorVersion.MinorVersion.FixVersion-TypeLabel，其中TypeLabel 
为 alpha、 beta、 devel。具体参见下图举例，其中devel是留给开发过程中 
使用的。

分工上，开发团队负责打 tag-alpha，测试团队负责打 tag-beta。

但是，自己决定并不意味着胡乱命名，大家仍然要以 语义明（白）（准）确 的原则 
来管理自己的分支和标签名，因为所有这些都是为了提高协作效率。


----

# 常见问题


## 参考资料

[Pro Git中文版](http://iissnan.com/progit/)

[GitHub详细教程 - 后山人的专栏 - CSDN博客](https://blog.csdn.net/lishuo_os_ds/article/details/8078475)

[Git命令大全](https://upload-images.jianshu.io/upload_images/290760-e8491f69473bf200.jpg)


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


## git如何clone所有的远程分支

git clone只能clone远程库的master分支，无法clone所有分支，解决办法如下：

1. 找一个干净目录，假设是git_work
2. `cd git_work`
3. `git clone http://myrepo.xxx.com/project/.git` ,这样在git_work目录下得到一个project子目录
4. `cd project`
5. `git branch -a`，列出所有分支名称如下：
	remotes/origin/dev
	remotes/origin/release
6. `git checkout -b dev origin/dev`，作用是checkout远程的dev分支，在本地起名为dev分支，并切换到本地的dev分支
7. `git checkout -b release origin/release`，作用参见上一步解释
8. `git checkout dev`，切换回dev分支，并开始开发。


## git本地的撤销修改和删除操作

[git本地的撤销修改和删除操作](https://www.cnblogs.com/qlqwjy/p/8378851.html)

[廖雪峰-Git教程-撤销修改](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374831943254ee90db11b13d4ba9a73b9047f4fb968d000)

工作区某个修改的文件不想add到暂存区，而是回退到它修改前的状态：`git checkout -- testfile`

如果想要将所有修改的文件都回退到原始状态：`git checkout -- *` 

如果要回退到上个版本： `git reset -hard HEAD^`

如果已经add到暂存区，但还没有commit，想要回退到修改前的状态：`git reset HEAD <file>`


----


# 常见操作

## 分支(branch)

* 查看本地分支： `git branch` 或 `git branch -l`
* 查看远程分支： `git branch -a`
* 切换分支：`git checkout branch2`
* 将远程分支release克隆到本地：`git checkout -b release origin/release`

## log

* 查看log时每行显示一个：`git log --oneline`

## 标签(tag)

* 查看所有tag：`git tag`
* 查看tag信息：`git show tagname`

`git checkout tag1`可以跳到某个标签，但此时HEAD不会指向任何分支,严谨的说是HEAD指向了一个没有分支名字的修订版本，
此时恭喜你,已经处于游离状态了(detached HEAD).这时候我们在进行commit操作不会提交到任何分支上去. 
参考：[git问题记录--如何从从detached HEAD状态解救出来](https://www.jianshu.com/p/ae4857d2f868)


## diff

* 显示出所有有差异的文件列表：`git diff branch1 branch2 --stat`
* 显示指定文件的详细差异：`git diff branch1 branch2 文件名(带路径)`
* 显示出所有有差异的文件的详细差异：`git diff branch1 branch2`


----

# ssh-keygen

* [SSH配置以及多个SSH & config文件](https://blog.csdn.net/wiki_su/article/details/50247551)
* [在Windows下清除ssh-key私钥访问密码](https://www.jianshu.com/p/3543f71dca9a)
* [ssh-keygen之后，生成的密码都叫id_rsa.pub，我想改名不行吗？](https://segmentfault.com/q/1010000005698184)
