## Git 分支管理

git 分支管理原理：git每次提交会有一个提交对象，提交对象会存储当前提交的快照对象，提交注释等信息，还有一个指向上一次提交的提交对象（父提交对象），每一次提交都会将当前提交对象指向其父对象，所谓的分支只是一个指向提交对象的指针，还有一个HEAD指针，指向当前所在工作的分支，如下图所示：

### 新建立分支
* git branch newbranchname : 在当前提交对象上创建新的分支
* git branch : 查看当前本地的分支，当前所在的分支前面有×号

### 切换分支
* git checkout newbranchname : 切换HEAD指针指向newbranchname,且将工作目录切换到分支newbranchname所在的状态，如果git不能干净地完成此任务，那么切换会失败，如当前分支有内容提交的暂存区但没有提交的git仓库等情况

### 新建分支且切换到此分支
* git checkout -b problem323

### 合并分支
* git merge branchname: 合并branchname到当前工作的分支

### 分支管理
* git branch : 查看所有的分支，当前检出的分支前面有*号
* git branch -v : 查看所有分支最后一次提交
* git branch --merged : 查看合并到当前分支的分支
* git branch --no-merged : 查看尚未合并到当前分支的分支
* git branch -d branchname: 删除某个分支 -D表示强制删除
