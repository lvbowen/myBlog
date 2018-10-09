## git常用命令 

新建代码库：  
```
git init    //在当前目录新建一个Git代码库  
git init [project-name]     //新建一个目录，将其初始化为Git代码库  
git clone [url]     //下载一个项目和它的整个代码历史  
```
增加/删除文件：  
```
git add [file1] [file2] ...     //添加指定文件到暂存区  
git add [dir]     //添加指定目录到暂存区，包括子目录  
git add .     //添加当前目录的所有文件到暂存区  
git rm [file1] [file2] ...      //删除工作区文件，并且将这次删除放入暂存区  
git rm --cached [file]      //停止追踪指定文件，但该文件会保留在工作区  
git mv [file-original] [file-renamed]     //改名文件，并且将这个改名放入暂存区
```
代码提交：  
```
git commit -m [message]     //提交暂存区到仓库区  
git commit [file1] [file2] ... -m [message]     //提交暂存区的指定文件到仓库区  
git commit -v     //提交时显示所有diff信息  
git commit --amend -m [message]     //使用一次新的commit，替代上一次提交,改写提交信息  
git commit -a -m [message]          //一句命令将modified的文件提交到暂存区再到仓库区，如果有新文件还是需要先git add 
```
分支：
```
git branch      //列出所有本地分支  
git branch -r     //列出所有远程分支  
git branch -a     //列出所有本地分支和远程分支  
git branch [branch]      //新建一个分支，但依然停留在当前分支   
git branch [branch] [commit]      //新建一个分支，指向指定commit  
git branch --track [branch] [remote-branch]     //新建一个分支，与指定的远程分支建立追踪关系  
git branch --set-upstream [branch] [remote-branch]      //建立追踪关系，在现有分支与指定的远程分支之间  
git branch -d [branch]     //删除本地分支  
git branch -m [oldBranchName] [newBranchName]   //修改本地分支名称
git checkout [branch]     //切换到指定分支，并更新工作区; 若该指定分支本地没有而远程有，则会新建一个分支并切换过去且与远程同名分支建立追踪关系  
git checkout -b [branch]      //新建一个分支，并切换到该分支   
git checkout -      //切换到上一个分支   
git merge [branch]      //合并指定分支到当前分支  
git cherry-pick [commit]      //选择一个commit，合并进当前分支  
git push origin --delete [branch]       //删除远程分支  
git branch -dr [remote/branch]      //删除远程分支  
```
其他：  
 ```
 git remote -v      //查看项目的远程地址
 ``` 

扩展阅读：<a href="http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html" target="_blank" style="margin-right:10px;">常用git命令清单</a>       [git远程操作](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
































