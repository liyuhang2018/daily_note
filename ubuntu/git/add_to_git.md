## git常用操作

```shell
git init  
#将此文件夹设置为git仓库
git add .
#表示把该目录下的所有文件加入到本地暂存区中。执行成功后不会有任何提示：
git commit 
#该命令会把本地暂存区中的文件提交到本地历史区，注意只有在本地历史区中的内容才能提交到github。执行该命令后，我们所有的文件都只是在本地。没有github任何关系。如果出现fatal:remote origin already exists
git remote add origin https://github.com/liyuhang2018/multi_agent.git
#该命令是把本地历史区中的文件添加到github服务器的暂存区中。这一步是本地和远程服务器建立联系的一步。执行成功后不会显示任何
git push -u origin master
#这一步是真正向github提交，执行完成后，github上的repository就有和你本地一样的代码文件了。
这些是各种场合常见的 Git 命令：

开始一个工作区（参见：git help tutorial）
   clone      克隆一个仓库到一个新目录
   init       创建一个空的 Git 仓库或重新初始化一个已存在的仓库

在当前变更上工作（参见：git help everyday）
   add        添加文件内容至索引
   mv         移动或重命名一个文件、目录或符号链接
   reset      重置当前 HEAD 到指定状态
   rm         从工作区和索引中删除文件

检查历史和状态（参见：git help revisions）
   bisect     通过二分查找定位引入 bug 的提交
   grep       输出和模式匹配的行
   log        显示提交日志
   show       显示各种类型的对象
   status     显示工作区状态

扩展、标记和调校您的历史记录
   branch     列出、创建或删除分支
   checkout   切换分支或恢复工作区文件
   commit     记录变更到仓库
   diff       显示提交之间、提交和工作区之间等的差异
   merge      合并两个或更多开发历史
   rebase     本地提交转移至更新后的上游分支中
   tag        创建、列出、删除或校验一个 GPG 签名的标签对象

协同（参见：git help workflows）
   fetch      从另外一个仓库下载对象和引用
   pull       获取并整合另外的仓库或一个本地分支
   push       更新远程引用和相关的对象

```

## git的合作

```
1. xianhu在master分支上完成v0.1版本开发，“done demo in master”

2. 发现master分支上有bug，需紧急修复。新建并检出hotfix分支进行bug修复，并merge回master分支，发布版本v0.2。

3. xianhu新建并检出develop分支进行迭代开发，然后在develop分支上检出release01分支，进行发版前测试和bug修复。“fix bugs in release01”，完成后将release01分支merge回develop和master分支，并在master分支上发布版本v0.3。

4. xianhu继续开发develop分支。此时团队成员增加，团队中的每个人都在develop的基础上新建并检出自己的feature分支，开发完成后merge回develop分支。这里利用到了rebase操作和冲突解决等，需要特别注意一点步骤。

5. xianhu在develop分支上检出release02分支，再次进行发版前测试和bug修复，“fix bugs in release02”，完成后将release02分支merge回develop和master分支，并在master分支上发布版本v1.0。
```















