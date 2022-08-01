## 常用的Linux命令

平时一定要多使用这些基础的命令！

1）、cd : 改变目录。

2）、cd . . 回退到上一个目录，直接cd进入默认目录

3）、pwd : 显示当前所在的目录路径。

4）、ls(ll):  都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。

5）、touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。

6）、rm:  删除一个文件, rm index.js 就会把index.js文件删除。

7）、mkdir:  新建一个目录,就是新建一个文件夹。

8）、rm -r :  删除一个文件夹, rm -r src 删除src目录

```
rm -rf / 切勿在Linux中尝试！删除电脑中全部文件！
```

9）、mv 移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下。

10）、reset 重新初始化终端/清屏。

11）、clear 清屏。

12）、history 查看命令历史。

13）、help 帮助。

14）、exit 退出。

15）、#表示注释



## Git 命令

 通过`git init`命令 把这个目录变成Git可以管理的仓库（会增加一个.git目录）；

用命令`git add`命令 告诉Git，把文件添加到仓库； 

使用命令`git commit -m `，完成；

要随时掌握工作区的状态，使用`git status`命令。

如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。(修改完成之后 还需add commit命令进行添加 提交)。

`cat` +文件名命令 是查看文件内容

`HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。

穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。要重返未来.

用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

`git ls-files`：查看git已经加入本地仓库的文件

#### 分支管理

查看分支：`git branch`

创建分支：`git branch `

切换分支：`git checkout `或者`git switch `

创建+切换分支：`git checkout -b `或者`git switch -c `

合并某分支到当前分支：`git merge `

删除分支：`git branch -d `

修改文件名字：`git mv oldFileName newFileName `(此命令在本地修改后push到GitHub上也会自动修改。)

#### git add 所有文件

`git add xx`命令可以将xx文件添加到暂存区，如果有很多改动可以通过 `git add -A .`来一次添加所有改变的文件。

注意 `-A` 选项后面还有一个句点。 `git add -A`表示添加所有内容， `git add .` 表示添加新文件和编辑过的文件不包括删除的文件; `git add -u` 表示添加编辑或者删除的文件，不包括新添加的文件

#### 当你像删除文件时：

​	 通常直接在文件管理器中把没用的文件删了，或者用`rm`命令删了： `rm fileName` 此时文件在文件已经删除，但是版本库还有

###### 场景一误删： 

因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本： `git checkout -- fileName`

（ `git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。 ）

###### 场景二彻底删除：

 确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`：

1.`git rm fileName`  	

2.`git commit -m "remove fileName"`





#### 当你该乱文件中内容时

场景一当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- filename`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD `，就回到了场景1，第二步按场景1操作。（ `git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。 ）

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)一节，不过前提是没有推送到远程库。



#### 添加远程库

 要关联一个远程库，使用命令  `git remote add origin git@github.com:Orange-es/learngit.git`

 *`关联一个远程库时必须给远程库指定一个名字,`origin`是默认习惯命名；* 

*`Orange-es`是你GitHub名字*

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

#### 删除远程库

如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm `命令。使用前，建议先用`git remote -v`查看远程库信息：

```
$ git remote -v
origin  git@github.com:michaelliao/learn-git.git (fetch)
origin  git@github.com:michaelliao/learn-git.git (push)
```

然后，根据名字删除，比如删除`origin`：

```
$ git remote rm origin
```

此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

