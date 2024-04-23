# Git 基础



## 参考文档

[Git官方文档](https://git-scm.com/doc)

[菜鸟教程](https://www.runoob.com/git/git-basic-operations.html "命令速查")

[Pro Git](https://git-scm.com/book/en/v2)



## 设置命令别名

打开当前用户的主目录`C:\Users\yourUserNmae\`

打开.bashrc文件

`alias 别名='具体命令'`



## Git的Vim设置

修改vim配置文件

位置：git安装目录\etc\vimrc



## 修改用户名和邮箱

> 查看用户名和邮箱

~~~git
git config user.name
git config user.email
~~~

> 修改用户名和邮箱

~~~git
git config --global user.name "runoob"
git config --global user.email test@runoob.com
~~~

如果用了 **--global** 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的项目都会默认使用这里配置的用户信息。

如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。



## 初始化仓库

> 执行该命令之后，就可以在当前目录下生成.init文件夹，并且会默认生成一个master分支。

~~~git
git init 
~~~

> 该命令从URL指向的远程仓库拷贝一份到当前目录

~~~git
git clone [url]
~~~



## Git工作流

![img](C:\Users\86187\Desktop\instructions\Git使用说明.assets\git-command.jpg)



![The lifecycle of the status of your files](C:\Users\86187\Desktop\instructions\Git使用说明.assets\lifecycle.png)

## Git status

**git status** 是一个用于查看 Git 仓库当前状态的命令。

**git status** 命令可以查看在你上次提交之后是否有对文件进行再次修改，以及是否新增加了文件。

~~~git
git status [-s]
~~~

-s 选项打印简化结果



## Git add

**git add** 命令可将该文件的修改添加到暂存区。



add、stage、commit、modified这些概念易混淆，具体介绍[see here](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)



新建文件是untracked, add之后变为staged

staged做改动, 变为Unstaged

Unstaged add变为staged



> Track one or more files.

~~~
git add [file1] [file2] ...
~~~

> Track all untracked files in workspace to staging area.

~~~
git add .
~~~



## Git diff

比较==暂存区和工作区的差异==(modified but Unstaged)

~~~
git diff [file]
~~~



比较==暂存区和HEAD的差异==(staged but not committed)

```
$ git diff --cached [file]
或
$ git diff --staged [file]
```



比较==工作区和HEAD的差异==

~~~
git diff HEAD
~~~





## Git commit

git commit 命令将暂存区内容添加到本地仓库中。

> 提交全部

~~~
git commit -m [message]
~~~

> 提交指定文件

~~~
git commit [file1] [file2] ... -m [message]
~~~

commit只会将当前暂存区里的文件提交到版本库

- 如果文件未跟踪，用add将其加入暂存区，再使用commit提交
- 如果文件已跟踪，但被修改，要先使用add将更新修改到暂存区，再提交



有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 `--amend` 选项的提交命令来重新提交：

```console
$ git commit --amend
```

这个命令会将暂存区中的文件提交。 如果自上次提交以来你还未做任何修改（例如，在上次提交后马上执行了此命令）， 那么快照会保持不变，而你所修改的只是提交信息。



## Git标签

[here](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)





## 查看历史



### git log

~~~
git log  //查看历史提交记录
~~~



选项

 - `--oneline`：以简洁的一行格式显示提交信息。
 - `--graph`：以图形化方式显示分支和合并历史。
 - `--decorate`：显示分支和标签指向的提交。
 - `--author=<作者>`：只显示特定作者的提交。
 - `--since=<时间>`：只显示指定时间之后的提交。
 - `--until=<时间>`：只显示指定时间之前的提交。
 - `--grep=<模式>`：只显示包含指定模式的提交消息。
 - `--no-merges`：不显示合并提交。
 - `--stat`：显示简略统计信息，包括修改的文件和行数。
 - `--abbrev-commit`：使用短提交哈希值。
 - `--pretty=<格式>`：使用自定义的提交信息显示格式。

 ==已设置别名==

~~~
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
~~~



### [git blame](https://www.runoob.com/git/git-commit-history.html#git-blame)

~~~
git blame <file>  //逐行显示指定文件的每一行代码是由谁在什么时候引入或修改的。
~~~

<del>到底是谁干的！狠狠地blame</del>



## 删除文件

git rm 命令用于删除文件。

[refrerence](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#_removing_files)

> 将文件从暂存区和工作区中删除：

```
git rm <file>
```



> If you modified the file ==or== had already added it to the staging area, you must force the removal with the `-f` option.

~~~
git rm -f <file>
~~~



Another useful thing you may want to do is to keep the file in your working tree but remove it from your staging area. In other words, you may want to keep the file on your hard drive but not have Git track it anymore. This is particularly useful if you forgot to add something to your `.gitignore` file and accidentally staged it, like a large log file or a bunch of `.a` compiled files. To do this, use the `--cached` option:

```console
$ git rm --cached README  //只从暂存区删除
```



## 撤销操作



### reset

[撤销操作](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C)

[原理](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset)

1. **Soft Reset**  撤销commit

   ```
   git reset --soft <commit>
   ```

   仅移动 HEAD 指针到指定的提交，不修改暂存区和工作目录内容。你可以重新提交这些更改。

   

2. **Mixed Reset**(默认)  撤销stage

   ```
   git reset --mixed <commit>
   ```

   移动 HEAD 指针到指定的提交，将暂存区的内容修改为指定提交，但不修改工作目录内容。你需要重新暂存你想要提交的更改。

3. **Hard Reset**  撤销修改

   ```
   git reset --hard <commit>
   ```

   移动 HEAD 指针到指定的提交，重置暂存区和工作目录内容到指定提交的状态。==慎用，会删除工作目录中未提交的更改==。(可以用git reflog查看hash值再跳回去,不过改动会消失)

4. **取消暂存的文件**：

   ```
   git reset HEAD <file>
   ```

   取消暂存指定文件，将其从暂存区移除，但保留在工作目录中。

   比如对a,b两个文件的修改都提交到了暂存区(staged but not commit)

   `git reset HEAD a`可以把 a 变回Unstaged.



与[Git diff](#Git diff)结合可以自由查看各种各样的差异



---

### restore

[restore](https://www.runoob.com/git/git-restore.html)



### rebase

[merge与rebase](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)

[视频参考](【【B站最全Git进阶课程】git rebase:  人生无法重来，但代码可以！】 https://www.bilibili.com/video/BV1Xb4y1773F/?share_source=copy_web&vd_source=b23f8a9cd162ff7a94424d5480360ac9)



## Git mv

[git mv](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#_git_mv)



## Git分支

[Git Branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell#ch03-git-branching)

### 分支简介

为了真正理解 Git 处理分支的方式，我们需要回顾一下 Git 是如何保存数据的。

或许你还记得 [起步](https://git-scm.com/book/zh/v2/ch00/ch01-getting-started) 的内容， Git 保存的不是文件的变化或者差异，而是一系列不同时刻的 **快照** 。

在进行提交操作时，Git 会保存一个提交对象（commit object）。 该提交对象会包含一个指向暂存内容快照的指针。 但不仅仅是这样，该提交对象还包含了作者的姓名和邮箱、提交时输入的信息以及指向本次提交前的一个或多个提交的指针。 首次提交产生的提交对象没有父提交，普通提交操作产生的提交对象有一个父对象， 而由多个分支合并产生的提交对象有多个父对象，

假设现在有一个工作目录，里面有三个文件, 你把它们暂存并提交了上去。 暂存操作会为每一个文件计算校验和（使用我们在 [起步](https://git-scm.com/book/zh/v2/ch00/ch01-getting-started) 中提到的 SHA-1 哈希算法），然后会把当前版本的文件快照保存到 Git 仓库中 （Git 使用 *blob* 对象来保存它们），最终将校验和加入到暂存区域等待提交：

```console
$ git add README test.rb LICENSE
$ git commit -m 'The initial commit of my project'
```

当使用 `git commit` 进行提交操作时，Git 会先计算每一个子目录（本例中只有项目根目录）的校验和， 然后在 Git 仓库中这些校验和保存为树对象。随后，Git 便会创建一个提交对象， 它除了包含上面提到的那些信息外，还包含指向这个树对象（项目根目录）的指针。 如此一来，Git 就可以在需要的时候重现此次保存的快照。

现在，Git 仓库中有五个对象：三个 *blob* 对象（保存着文件快照）、一个 **树** 对象 （记录着目录结构和 blob 对象索引）以及一个 **提交** 对象（包含着指向前述树对象的指针和所有提交信息）。

![A commit and its tree](C:\Users\86187\Desktop\instructions\Git使用说明.assets\commit-and-tree.png)

做些修改后再次提交，那么这次产生的提交对象会包含一个指向上次提交对象（父对象）的指针。

![提交对象及其父对象。](C:\Users\86187\Desktop\instructions\Git使用说明.assets\commits-and-parents.png)

Git 的分支，其实本质上仅仅是指向提交对象的可变指针。 Git 的默认分支名字是 `master`。 在多次提交操作之后，你其实已经有一个指向最后一次提交的 `master` 分支。 `master` 分支会在每次提交时自动向前移动。

![A branch and its commit history](C:\Users\86187\Desktop\instructions\Git使用说明.assets\branch-and-history.png)



### 查看分支

> 查看本地分支

~~~git
git branch
~~~

==本地仓库必须至少有一个commit才会有branch==




> 查看远端分支

~~~git
git branch -r	
~~~

---



### Git stash

[stash](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E8%B4%AE%E8%97%8F%E4%B8%8E%E6%B8%85%E7%90%86#_git_stashing)

有时对本地仓库进行了许多编辑, 突然想要切换到其他分支进行操作, 但这样所有未提交的修改都会消失,可以使用`git stash`将本分支所有未提交的改动存储起来, 处理完其他分支的操作后回到本分支,使用`git stash apply`将之前储存的操作重新应用回来

使用`git stash list`查看保存的修改



### 创建/删除和切换



> 创建分支

~~~
git branch <branchName>
~~~

> 删除分支
~~~
git branch -d <branchName>
~~~

> 切换分支

~~~
git checkout <branchName>
git switch <branchName>
~~~

> 创建并切换到该分支

~~~
git checkout -b <branchName>
git switch -c <branchName>
~~~

> 切换回前一个分支
~~~
git checkout -
git switch -
~~~
---



### 分支合并

> 合并目的分支到当前分支

~~~
git merge <branchName>
~~~

遇到冲突, 到冲突的文件中手动修改, 然后add+commit, 结束本次merge

[分支的合并](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6#_basic_merging)





## Git clone

[clone](https://git-scm.com/docs/git-clone/zh_HANS-CN)

[相关](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E8%BF%9C%E7%A8%8B%E5%88%86%E6%94%AF)

将存储库克隆到新创建的目录中，为克隆存储库中的每个分支创建远程跟踪分支（使用`git branch --remotes`可见），并在根据远程库的HEAD指向在本地创建一个新的分支, 将本地的HEAD指向该分支.



由于远程仓库的HEAD指向一般默认都是master或main, 所以clone之后本地只会有一个分支(master或main), 如果想指定本地分支为远端某一特定分支,使用:

> git clone -b <远端分支名称>

比如:

<img src="C:\Users\86187\Desktop\instructions\Git使用说明.assets\image-20240421000435454.png" alt="image-20240421000435454" style="zoom:50%;" />

远端有两个分支:main edit

使用git clone 在本地创建的分支是main, 如果想创建edit , 使用:

> git clone -b edit <Url>

当然, 即使clone的时候没有指定edit, 也可以之后使用 `git checkout edit` 这样会新创建一个edit分支并跟踪远端的edit.





## Git remote

> 查看远端

~~~
git remote [-v]   //-v选项显示远端地址
~~~

> 添加远端

~~~
git remote add <shortname> <url>
~~~

> 将已配置的远程仓库重命名。

~~~
git remote rename <old_name> <new_name>
~~~

> 从当前仓库中删除指定的远程仓库

~~~
git remote remove <remote_name>
~~~

> 修改指定远程仓库的 URL。

~~~
git remote set-url <remote_name> <new_url>
~~~

> 显示指定远程仓库的详细信息，包括 URL 和跟踪分支。

~~~
git remote show <remote_name>
~~~



### fetch

~~~
git fetch
~~~

这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看。



### pull

**git pull** 命令用于从远程获取代码并合并到本地分支

~~~
git pull <远程主机名> <远程分支名>:<本地分支名>
~~~

如果要合并到当前分支, 则不需要冒号和本地分支名



### push

**git push** 命令用于从将本地的分支版本上传到远程并合并。

```
git push <远程主机名> <本地分支名>:<远程分支名>
```

如果本地分支名与远程分支名相同，则可以省略冒号和远程分支名

如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数



删除主机的分支可以使用 --delete 参数，以下命令表示删除 origin 主机的 master 分支：

```
git push origin --delete master
```









## 分支与远端



同步远端的修改到本地, 假如此时本地在edit分支上

~~~
git fetch origin    //从远端拉取数据,本地就会有远端所有分支的引用
git merge origin/edit   //将远端的edit分支合并到当前分支
~~~



### 本地分支跟踪远端分支

> 使用该命令可以让本地某个分支跟踪远端分支, 跟踪终止后可以直接在本地分支上使用pull和push命令进行自动拉取和推送

~~~
git branch -u <remote>/<remoteBranch> <localBranch>
~~~



> 查看跟踪关系

~~~
git branch -vv
~~~



> 解除本地分支的跟踪

~~~
git branch --unset-upstream <本地分支名>
~~~











# 实践案例





































