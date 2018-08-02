记录文件的更新
在某一阶段工作结束后，有一系列文件，新增加的，修改的需要提交到git 仓库，所有的文件不外乎两类，一类为已跟踪状态，一种为未跟踪状态，已跟踪状态的文件是已经提交到git仓库中的文件，未跟踪的文件从没有提交到git仓库过，已跟踪状态的文件又有三种状态：未修改状态，已修改状态，已暂存状态，类型如下的结构
所有文件状态:
	已跟踪状态
		未修改状态
		已修改状态
		已暂存状态
	未跟踪状态

未跟踪文件经过提交操作后变为已跟踪文件，已跟踪文件经过修改，提交到暂存区，提交到仓库过程后拥有了新的版本代号，所有的文件都依次进行此过程不断进行下去

查询状态
提交前希望查看一下当前工作目录下所有文件的状态：
git status

跟踪新文件
处于未跟踪状态的文件用下面的命令执行想要跟踪新文件的意图
git add newfilename

将修改的文件提交到暂存区
git add modifiedfile

上面的演示中，git add命令理解为将文件添加到下一次提交中更好，因为即可以将旧的修改文件添加到暂存区，也可以将新的文件使其处于跟踪状态。

git status只显示的是文件级别的状态变化，也就是整个仓库中文化状态变化的宏观表现，如果还想再看更细致的文件内容级别的变化，用git diff命令
git diff : 显示的是工作目录中的文件状态与暂存区中的文件不一致的地方，而不是自上次提交以来所有文件变化内容的地方
git diff --staged：显示的是暂存区中的文件与上次提交后仓库中的文件不一致的地方

提交命令
git commit -m "commit subject"
用来提交暂存区的内容到git仓库，记住，是暂存区中的内容到仓库，不是工作内容的文件内容到仓库，没有加入到暂存区的文件是不会被提交的，忘记的只好下次再提交了。

移除文件
git 仓库不想再跟踪某文件时，这时，需要运行git rm 命令来从暂存区中移除对文件的跟踪，在下次运行git commit命令后记录进行git 仓库，从此不再跟踪删除文件的更新
git rm filename
git commit -m "rm filename"
git rm filename的运行结果：删除在本地磁盘上的文件，再从暂存区移除此对此文件的跟踪
如果filename已经修改过且提交至暂存区了，上述命令执行不成功，如果仍然想要执行成功，需要加上-f参数：git rm filename -f
如果只想不再跟踪filename文件，但是不想把filename从本地磁盘上删除，那么需要用下列的两个命令：
git rm --cached filename
git commit -m "xxxxx"
这样后，filename将不会再被跟踪了，但是仍然在磁盘上，如果此文件没有在.gitignore列表中，那么此文件会处于未跟踪状态，如果处于.gitignore列表中，则在运行git status命令时，不会显示在未跟踪文件列表中。

更改文件名
git mv file_from file_to
git commit *****
可选择的另外一种操作模式： 先copy文件，修改copy后的文件名到理想的文件名，删除old文件，add new文件，最后再提交

查看提交历史
git log ：提交历史大致示意图
git log -p ：提交历史及对应修改的内容
git log -2： 最近两次的提交


撤消操作
如果提交后想修改最近一次提交的注释，可以用下面的命令来执行：
git commit --atend
如果提交后有未提交到暂存区的已修改文件，用下面的过程来执行：
git add forggtenfile
git commit --atend 
在输入新的提交信息后，后面一次提交的注释信息会覆盖掉前一次的提交注释信息。

撤消暂存区中的文件
git reset HEAD filename： filename是处于暂存状态，执行完成后，filename处于修改但未暂存状态

撤消修改文件但是未提交状态的文件修改：
git checkout filename

打标签
为什么需要打标签？
因为在某些情况下，我们需要一些标识来标识某些重要的阶段性成果会对重要的东西做标记，比如，在重大版本发布功能开发完成后，需要对此版本进行一个标识，标识V1.0类似的功能。也可能是重要的bug修复，进行备忘，所以，需要有打标签的功能。

git 标签有两类：一类是附注标签，一类是轻标签，轻标签就是一个某次提交的sha引用，而附注标签则可以进行多方面的信息记录，一般建议打附注标签

查看当前仓库中有哪些标签？
git tag

在当前位置新建附注标签
git tag -a v1.0 -m "version 1.0"

在当前位置建立新轻量标签
git tag v2.0

查看标签的具体信息
git show tag-name

后期打标签，也就是在过去提交的记录中想打标签，如何操作？
git log --pretty=oneline
67940cd6f8f8c5ce8bd6cb855a0afe26f6a0210c git reset and git checkout command
6ce5d1912b4306a90cbff472c7352e58f4266fa4 modify gitbasiccommand.md
cdaf2c78a8596841f014e41d07ff4ec1b8a059b1 git log command and add project.md file
a15cdab387391f4b1fa5041e3320c5f0a55ebff5 add project file
00c06d14eb448eb02601558f588e789d2606480c git rm and git mv command
9907968c5210dc2da80d9608658abc750dd47320 modify file name
e01d8062735d4c77593e82cdcd19ddaec427a441 test git rm --cached command
4f62681838aa51f5a4df36a82fe56c47ee25c9a9 add project.md file
3cfffdf986232fec53f3b3f3d145c093e3da1dbd delete project.md
33bad872ff5641e6ff653a26888ce5e2de741a48 add project.md file
ee5fa80767e97c38adcb3ca64fd2439640d3509f git commit command
a7558775140784b8bb088a435aa060d3083c1e37 git add and git diff command
44abdbbb6916fc1479b87c3de88eb315731807ea add ignore file
203737a76cd360dfc81ff0d76c92d4996f2b5b05 git basic concept

在git basic concept位置打版本v0.1标签
git tag -a v0.1 203737 -m "init version of git learning"

推送标签到远程仓库
push操作并不会推送tag到远程仓库，需要用命令来操作
推送某版本的tag到远程仓库
git push origin v1.0
推送所有标签到远程仓库
git push origin --tags
检出标签
git checkout -b version1.0 v1.0

同步本地仓库到远程仓库
添加远程仓库
git remote add origin https://github.com/ChenCaiHust/LearnGit.git
origin是远程仓库的别名，一般默认为origin，https://github.com/ChenCaiHust/LearnGit.git是远程仓库的地址
推送到远程仓库：
git push -u origin master

注意：如果是git init初始化一个本地仓库，那么一般需要先设定好远程仓库的地址，初始化一个新的仓库，里面是空的，对于用github作为远程仓库而言，新建一个仓库时全部用默认的内容就可以了，不要加readme.md和licence.txt等文件，否则执行上述两个命令不会成功，会出问题。

查看远程仓库
git remote： 会显示简单的信息
git remote -v : 会显示更具体的信息
