# git 命令
## 基本命令
* git init
    * 初始化一个仓库,创建后会在目录中生成.git文件
* git add filename
    * 将文件添加到缓冲区
* git rm filename
    * 删除文件
* git commit -m '提交说明'
    * 一次性提交缓冲区中所有的修改到远程仓库(没有被添加到缓冲区的是不会被提交的)
* git status
    * 查看git库的状态,会显示已提交和未提交的文件
* git diff filename
    * 比较文件修改前后的差异(还没提交前)
* git log
    * 查看日志
* git reset
    * 版本回退
    * 用法1:  git reset --hard HEAD^
        * 回退到上一个版本（HEAD代表当前版本，有一个^代表上一个版本，以此类推）
    * 用法2:  git reset --hard d7b5
        * 回退到指定版本(其中d7b5是想回退的指定版本号的前几位)
* git reflog
    * 查看仓库操作历史
## git分支管理
* git branch
    * 创建分支
* git checkout 分支名
    * 切换到指定分支
* git checkout -b 分支名
    * 创建并切换到指定的分支
* git merge 分支名
    * 合并某分支内容到当前分支
* git branch -d 分支名
    * 删除分支
* git log --graph
    * 查看分支合并图

[参考](https://blog.csdn.net/lxw198902165221/article/details/89228458?ops_request_misc=&request_id=&biz_id=102&utm_term=git%20%E5%91%BD%E4%BB%A4&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-89228458)