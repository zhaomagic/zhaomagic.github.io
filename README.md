Git 安装配置指南 （Windows）
赵蕾  2017-4
一、	Git 安装
1	安装Git
由于虚拟机系统版本问题，目前Git支持XP操作系统的最高版本为2.10.0，更高的版本目前虚拟机的操作系统暂不支持，请开发人员下载指定的版本安装。

运行Git-2.10.0-32-bit, 默认安装，一直next 
 

2	安装TortoiseGit
由于虚拟机系统版本原因，目前TortoiseGit支持XP系统的最高版本为1.7.15.0，更高的版本目前虚拟机的操作系统暂不支持，请开发人员下载指定的版本安装。

运行TortoiseGit-1.7.15.0-32bit 默认安装
   
3	配置过程
a)	点击TortoiseGit---Settings
 
b)	设置用户和邮箱信息
 
c)	填写git路径
 
二、	SSHKey 生成
1	点击开始---TortoiseGit----Puttygen
 
2	点击开始---Genernate, 并用鼠标在空白处不停移动，生成随机key
     
3	将公钥上传至gitlab（gitlab用户）
生成后如下图，红色框中的是公钥，需要上传到gitlab上，复制公钥
 
登录gitlab页面，点击用户选择Setting
点击左侧栏SSH Keys，添加复制的公钥信息，点击Add key 保存。

 
4	保存私钥，点击是 将私钥保存为private.ppk
 
5	配置SSH登录密钥
   如图运行TortoiseGit软件包中的Pageant程序
 
点击后，会在windows右下角出现如下图标，双击
 
点击AddKey，将刚才生成的private.ppk添加进来。
 
配置完成

三、	基本使用方法
1	Clone 版本库 
若代码库在gitlab上，登录gitlab，选择project下面的项目，复制对应的ssh路径。
 
Tortoisegit的clone方法如下图，Branch和Origin Name默认不需填写。
 

2	新增修改提交文件
新增文件
 
提交到本地仓库
 
 
拉取远程更新到本地
 

推送到远程仓库
 

 
3	使用TortoiseGit操作分支的创建与合并
第一步：创建本地分支
点击右键选择TortoiseGit，选择Create Branch…，在Branch框中填写新分支的名称（若选中”switch to new branch”则直接转到新分支上，省去第二步），点击OK按钮：
 
  
 
第二步：通过“Switch/Checkout”切换到新创建的分支上，点击OK：
 
  
 
  
第三步：在新分支下执行PUSH操作，在对话框中保持远程分支为空白，点击OK，则将在远程创建了新的分支（在PUSH的时候远程服务器发现远程没有该分支，此时会自动创建一个和本地分支名称一样的分支，并将本地分支的内容上传到该分支）。
 
  
 
 
 
第四步：其他成员切换该新分支：
首先进行pull操作， 然后进行切换分支（如第二步）
 
第五步：分区合并
进行分支合并之前我们需要明确哪个分支将要合并到哪个分支，首先通过“Switch/CheckOut”切换到主干分支（如develop分支）,然后通过“Merge”继进行合并操作，在对话框中选择需要合并的分支。
分支合并成功后，我们即可以通过Commit与PUSH操作将合并上传到中心服务器。
 
  
 
 
第六步：删除分支
       当我们已将新分支合并到主分支后，或者放弃该分支的时候，可以对该分支进行删除操作。
首先通过“CheckOut/Switch”打开对话框，点击Switch to区域中Branch条目后面的更多按钮，打开分支列表对话框，右键点击要删除的分支，选择delete branch进行删除。
  
  
 
注意，在删除远程分支的时候，本地分支并不会删除，这也说明了本地分支与远程分支并无从属关系。

