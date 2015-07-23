<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Git 命令详解](#git-%E5%91%BD%E4%BB%A4%E8%AF%A6%E8%A7%A3)
  - [Git 帮助（Git Help）](#git-%E5%B8%AE%E5%8A%A9%EF%BC%88git-help%EF%BC%89)
  - [Git 配置（Git Config）](#git-%E9%85%8D%E7%BD%AE%EF%BC%88git-config%EF%BC%89)
  - [配置GitHub信息](#%E9%85%8D%E7%BD%AEgithub%E4%BF%A1%E6%81%AF)
  - [Git 基本操作](#git-%E5%9F%BA%E6%9C%AC%E6%93%8D%E4%BD%9C)
    - [初始化仓库](#%E5%88%9D%E5%A7%8B%E5%8C%96%E4%BB%93%E5%BA%93)
    - [添加文件到暂存区](#%E6%B7%BB%E5%8A%A0%E6%96%87%E4%BB%B6%E5%88%B0%E6%9A%82%E5%AD%98%E5%8C%BA)
    - [提交文件到提交区](#%E6%8F%90%E4%BA%A4%E6%96%87%E4%BB%B6%E5%88%B0%E6%8F%90%E4%BA%A4%E5%8C%BA)
    - [删除文件](#%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6)
    - [对比](#%E5%AF%B9%E6%AF%94)
    - [撤销修改](#%E6%92%A4%E9%94%80%E4%BF%AE%E6%94%B9)
  - [分支操作](#%E5%88%86%E6%94%AF%E6%93%8D%E4%BD%9C)
    - [切换分支](#%E5%88%87%E6%8D%A2%E5%88%86%E6%94%AF)
    - [恢复分支](#%E6%81%A2%E5%A4%8D%E5%88%86%E6%94%AF)
  - [保存现场](#%E4%BF%9D%E5%AD%98%E7%8E%B0%E5%9C%BA)
    - [恢复分支现场](#%E6%81%A2%E5%A4%8D%E5%88%86%E6%94%AF%E7%8E%B0%E5%9C%BA)
  - [分支合并](#%E5%88%86%E6%94%AF%E5%90%88%E5%B9%B6)
  - [标签](#%E6%A0%87%E7%AD%BE)
  - [版本回退](#%E7%89%88%E6%9C%AC%E5%9B%9E%E9%80%80)
  - [远程服务器](#%E8%BF%9C%E7%A8%8B%E6%9C%8D%E5%8A%A1%E5%99%A8)
  - [问答](#%E9%97%AE%E7%AD%94)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Git 命令详解

### Git 帮助（Git Help）

- `git help <command>`    
- `git <command> -h`    
- `git <command> --help`     
- `man git -<command>` 均可查询某个命令的帮助文档。

### Git 配置（Git Config）

语法：`git config <scope> <setting>` 

- `<scope>` 有三个配置级别，分别是：`--local`, `--global`, `--system`
	- --local (默认)具有最高优先级，只影响本仓库。对应的配置文件： `.git/config`
	- --global 中级优先级，影响到所有当前用户的仓库。对应的配置文件：`~/.gitconfig`
	- --system 最低优先级，影响到全系统的仓库。对应的配置文件： `/etc/gitconfig`
- `<setting>` 代表具体的设置命令

**配置Git信息**

```bash
git config --global user.name "your name"
git config --global user.email "your name"
```
NOTE：这里的name和email并非一定要设置成与GitHub中的一样，你可以设置不同的名字和邮箱。但是建议成一样的，避免混淆。

**配置别名**

`git config --global alias.st status`      

配置一个名为st的别名，对应status

`git config --global alias.unstage "reset HEAD"`   

配置一个名为unstage的别名，对应reset HEAD

NOTE：如果你使用 Mac OS X 可以尝试使用 [Oh My Zsh](http://ohmyz.sh)
其中已经预先设置好了非常多常用别名。

**配置输出显示显示不同颜色**

`git config --global color.ui true`

### 配置GitHub信息

**获取Github秘钥**

`ssh-keygen -t rsa -C "youremail@example.com"`

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

之后在GitHub的"Accout Settings"中的"SSH Keys"中添加id_rsa.pub中的内容

### Git 基本操作

#### 初始化仓库

**初始化一个裸中央服务器**

`git init <path> --bare`   

如：`git init ~/git-server --bare`

**初始化一个本地仓库服务器**

`git init <path>`

如：`git init ~/MyGitHub`

NOTE：在初始化仓库后会出现一个隐藏的目录 `.git`，其中包括了所有的当前仓库的版本信息和本地设置文件(`.git/config`)

#### 添加文件到暂存区

**将文件添加到暂存区**

`git add <file>` 

如：`git add readme.md`  

**批量添加本目录下地文件到暂存区**

`git add .`

**将工作区修改直接提交到版本库**

`git commit -a -m "message"`

如：`git commit -a -m "Resolve Bugs"`

#### 提交文件到提交区

**将暂存区内容提交到提交区**

`git commit -m "message"`

如：`git commit -m "Login Feature."`

#### 删除文件

**将文件从暂存区删除**

`git rm --cached <file>`

如：`git rm --cache readme.md`

**将文件从工作区和暂存区删除**

`git rm <file>`

如：`git rm readme.md`

**删除所有被跟踪但在工作区已经被删除的文件**

`git rm $(git ls-files --deleted)` 

**查询状态**

`git status`

#### 对比

**查询工作区与暂存区的所有差异**

`git diff`

**查询工作区与暂存区某个文件的差异**

`git diff <file>` 

如：`git diff readme.md`

**查询工作区与某次版本库差异**

- `git diff 48x3847` 显示工作目录与48x3847提交的差异 

**查询暂存区与上次提交的差异**

`git diff --cached`

**查询暂存区与某次提交的差异**

`git diff --cached <reference>` 

如：`git diff --cached 827x80`

**查询提交历史记录**

- `git log` 显示历史记录

- `git log --oneline`  每条历史记录用一行显示

#### 撤销修改

**撤销某个文件在工作区修改（从暂存区复制）**

`git checkout -- <file>`

相当于将文件从暂存区复制到工作目录（此方法会丢弃工作区修改且**不可恢复**）

如：`git checkout -- readme.md`

**撤销某个文件在工作区的修改（从提交区复制）**

`git checkout HEAD -- <FILE>`

相当于直接将提交区的最新内容复制到工作区

如：`git checkout HEAD -- readme.md`

**撤销某个文件在暂存区的修改（从提交区复制）**

`git reset HEAD <file>` 

相当于将提交区的最新内容复制到暂存区

如：`git reset HEAD readme.md`

**查询所有运行过的命令**

`git reflog`

**忽略文件**

`.gitignore` 可以在添加至仓库时忽略匹配的文件，但仅作用于*未跟踪*的文件。

NOTE：GitHub 为各个类型项目和操作系统提供了忽略文件模板，可以在[这里](https://github.com/github/gitignore)找到。

### 分支操作

**创建分支**

`git branch <branchName>` 

**删除分支**

`git branch -d <branchName>` 

**强行删除分支**

`git branch -D <branchName>` 

**显示所有分支信息**

`git branch -v`

#### 切换分支

**切换分支**

`git checkout <branchName>`

**创建分支并切换到此分支**

`git checkout -b <branchName>` 

NOTE：等于 git branch + git checkout

#### 恢复分支

**恢复到上一个分支**

`git checkout`

**切换到任何一个版本**

`git checkout <commitId | tag>`

### 保存现场

**查看保存的分支现场**

`git stash list`

**保存分支现场**

`git stash`

**保存现场操作（并输入描述信息）**

`git stash save "message"` 

NOTE：`git stash`操作相当于将工作区和暂存区的修改存进stash区里

#### 恢复分支现场

**恢复最近一次保存的分支现场（删除stash记录）**

`git stash pop` 

NOTE：stash pop = stash apply + stash drop

**恢复最近一次保存的分支现场（不删除stash记录）**

`git stash apply` 

**恢复特定的分支现场**

`git stash apply <stashId>`

如：`git stash apply stash@{0}`

**删除最近一次保存的stash记录**

`git stash drop`

### 分支合并

**显示分支的父节点信息**

`git cat-file -p HEAD` 

**合并分支到当前分支**

`git merge <branchName>` 

**不使用fast-forward方式合并**

`git merge next --no-ff`

### 标签

**查看所有标签**

`git tag`

**查看标签信息**

`git show v1.0`

**往commit上打标签**

`git tag -a v1.0 202x38 -m "version 1.0 release"`

NOTE：往202x38的commit上打标签，如果不指定，则默认为HEAD（即最近一次的提交）

**删除标签**

`git tag -d v1.0`

**推送标签到远程**

`git push origin v1.0`

**一次性推送所有未推送到远程的本地标签**

`git push origin --tags`

**删除已经推送到远程的标签**

```
git tag -d v1.0
git push origin :refs/tags/v1.0
```

### 版本回退

**完全回退**

**回退到上个版本**

`git reset --hard HEAD^` 

**回退到上上个版本**

`git reset --hard HEAD^^` 

**回退到上100个版本**

`git reset --hard HEAD~100` 

**回退到特定版本**

`git reset --hard commit_id` 

如：`git reset --hard 28yc83`

### 远程服务器

**创建一个裸中央服务器**

`git init ~/git-server --bare` 

**将本地仓库与远程仓库关联**

`git remote add <lias> <remoteGitAddr>`

如：`git remote add origin bookshop@github.com`

**查看远程仓库信息**

`git remote -v` （信息保存在：`.git/config`）

**直接将分支推送到远程分支**

`git push <remoteServer> <localBranch>`

如：`git push -u /User/leeluo/git-server master`

NOTE：-u参数会把本地的master分支和远程的master分支关联起来

**将分支推送到远程分支（设置别名后）**

`git push origin master`

**同步远程仓库的提交历史（git push）**

`git fetch origin master`

NOTE：fetch之后，如果有冲突，按下列步骤解决：

1. 先用`git merge origin/master`合并远程分支，运行命令后会提示自动合并失败，这时需要你手动解决出现冲突的文件。
2. 解决冲突后，用`git add <file>` `git commit <file>`方式提交存在冲突的文件
3. 最后，用`git push <remoteAddr> <localAddr>`推送分支

NOTE：关于git pull，如果中央仓库修改的内容与你本地的没有冲突，那么git pull会自动合并两份。但是如果有冲突，git pull就会执行失败，而提示你先用git fetch取出冲突，解决冲突后再提交。   而用git fetch进行更新的话，如果中央仓库修改的内容与你本地的没有冲突，你也需要用`git merge origin/master`命令将分支合并。   所以一般情况下，都是直接用git pull更新，如果没有冲突的话，那么版本就会自动合并。 如果有冲突，那么你就需要先git fetch，然后解决冲突，再git add + git commit，之后在git push.


**同步远程仓库的提交历史（git pull）**

git pull = git fetch + git merge

NOTE：git pull不同于git push的区别之一就是git pull会自动合并冲突分支，不是很灵活。运行git pull之前需要先指定本地dev分支与远程origin/dev分支的链接

`git branch --set-upstream dev origin/dev`

**创建与远程分支对应的分支**

`git checkout -b branch-name origin/branch-name` 

如：`git checkout -b dev origin/dev`

**从远程库克隆**

`git clone git@github.com:michaelliao/gitskills.git`


### 问答

1. git pull除了会直接获取远程历史，还会与你本地版本的历史进行合并？

答：是的

2. git checkout 和 git reset 都可以使HEAD指向发生改变

答：是的。[MARK]


