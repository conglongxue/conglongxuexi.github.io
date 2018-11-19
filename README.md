# git语法总结
##一、git的初始化
使用Git的第一件事就是设置你的名字和email,这些就是你在提交commit时的签名，每次提交记录里都会包含这些信息。使用git config命令进行配置：

$ git config --global user.name ""

$ git config --global user.email "“
##二、创建版本库
命令: mkdir learntGit

 在当前目录下创建learntGit文件夹

 cd learnGit 

进入learnGit文件夹中

 pwd

 查看当前路径

 git init

 将当前目录变成Git可以管理的仓库

 git add + 文件名

 将文件添加到仓库，可多次提交（添加成功，没有任何显示）

 git commit -m + 

提交说明 把文件提交到版本库
##三、Git开发常用命令

###1.查看版本状态


命令: 

git  status

 查看当前版本库的状态


git  diff  

  查看当前相对上一次提交修改的内容

###2.版本回退

命令:

 git log

 显示从最近到最远的提交日志

 git log --pretty== oneline 

显示log,但是不显示很多凌乱的信息 q 显示log版本信息有很多，使用q键停止查看

 git reset —hard head^

 回退到上一个版本

 git reset —hard head^^ 

回退到上上个版本 

git reset —hard head~100

 回退到之前100个版本

 git reset —hard +commit_id 

回到某个版本号的版本 


###3.工作区与暂存区


git  add   :

  添加文件，是将文件修改添加到暂存区。


git commit : 

 提交更改，实际是把暂存区的所有内容提交到当前分支

###4.管理修改

问题说明:
我们修改一个文件，第一次修改之后执行git add ，第二次修改不执行git add ,然后我们执行git commit并使用git status查看状态，可以发现第二次的修改并未提交。这是因为Git跟踪修改，如果不add到暂存区就不会加入到commit。


解决方案：继续执行git add，再git commit，也可以别着急提交第一次修改，先add第二次修改再commit

###5.撤销修改

情况一: 文件修改后还没被放到暂存区，


情况二: 文件修改后已经被添加到暂存区，然后又做了修改。又修改部分被撤销，


解决方案：


git checkout --  + 文件名    将文件在工作区的修改全部撤销。


执行结果:


情况一：执行撤销就回到和版本库一模一样的状态。


情况二：文件会恢复到上次添加到暂存区的状态，即使多次使用也只能回到最近一次暂存区状态。


情况一和情况二，总之都是让文件回到最近一次git commit或者add时的状态


情况三：想要撤销的部分已经add到暂存区，但是还没有被commit


解决方案：


1.使用git reset HEAD +文件名    把暂存区的修改撤销，重新放回到工作区。


2.根据情况1和情况2的方法撤销修改


情况四：想要撤销的部分已经提交到版本库中，但是还没有push到远程仓库


解决方法：使版本回退的方法

###6.删除文件


命令： rm + 文件名     删除文件

##四、远程仓库

###1.本地仓库与远程仓库之间的传输设置


本地仓库Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以需要一点设置：


第一步：创建SSH Key。


1.在用户的主目录下，查看是否有.ssh目录.


2.如果有，再看看这个目录有没有 id_rsa和id_rsa.pub这两个文件。


3.如果有，可直接跳到下一步。


4.如果没有，打开Shell(Window下打开Git Bash),创建SSH Key。


5.使用命令创建SSH Key： ssh -keygen -t rss -C  + github邮箱地址


第二步：设置远程仓库的key(以GitHub为例)


1.登陆GitHub，打开“Account Setting” ->“SSH Keys”页面。


2.点击”Add SSH Key”, 填上任意Title, 在key文本框中粘贴id_rsa.pub文件的内容。


3.点击"Add key”，确认添加了公钥

###2.将本地仓库与远程仓库关联同步
命令: 


git remote add origin +远程仓库地址 

  将本地仓库关联远程仓库
git push -u origin master       

   第一次推送master分支的所有内容到远程仓库
git push origin master      

   本地推送到远程(第一次之后）

##五、分支管理

###创建与合并分支
命令: 


git  checkout  +  分支名       

 切换分支


git  checkout  -b  dev        

 git checkout命令加上-b参数表示创建并切换分支


git  branch                   

 查看当前分支,会显示所有分支，并在当前分支前加*号


git  merge  +  分支名           

合并分支，指定分支名的分支合并到当前分支。
git  branch +  分支名           

创建分支


git  branch  -d  + 分支名     

  删除指定分支名的分支

##六、标签管理

命令： 

git tag + <tag名> 

创建一个标签 

git tag 

查看所有标签 

git tag + <tag名> + commitID 

通过git log查看提交过的版本Id,可以为曾经某个commit时刻的版本打上标签 

git show + <tagname> 

查看标签信息，可以看到tag的说明（如果创建的时候带有说明），可以看到PGP签名信息

 git tag -a + <tagname> -m + <tagDescription>

 创建带有说明的标签，用-a指定标签名，-m指定说明文字

 git tag -s + <tagname> -m + <tagDescription> 

通过-s用私钥签名一个标签，使用PGP签名，不过必须安装
gpg(GunPG)，没有gpg秘钥对会报错 

git tag -d + <tagname>

 删除标签 

git push origin + <tagname>

 推送某个标签到远程 

git push origin -- tags

 一次性推送全部尚未推送到远程的本地标签

 git push origin :refs/tags/<tagname>

 删除一个远程标签，登陆远程可查看删除标签效果。 




