## git典型的工作流程及对应的命令

### 克隆远程仓库到本地仓库
* git clone https://github.com/ChenCaiHust/LearnGit.git

### 进入工作目录
* cd LearnGit

### 需要有新的工作需要做，确保本地master分支跟踪到远程origin/master分支最新位置
* git pull

### 在新的分支上开始我们的工作
* git checkout -b fix001bugs

### 在fix001bugs上开始工作，多次执行下面的两步循环提交工作成果
* git add filename
* git commit -m "some text"

### 开发工作完成时，再次git pull下让本地master flow origin/master
* git pull
* 如果自动获取与合并失败，需要在本地先解决掉冲突

### 切换到master分支
* git checkout master

### 在本地合并fix001bugs到master分支
* git merge fix001bugs

### 推送本地更新到远程仓库
* git push -u origin master


如果merge权限不是作者，那么一般需要将新的分支合并请求推送到远程仓库


