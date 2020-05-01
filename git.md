# git的说明文档
## 使用前提
前提：要在需要操作的文件目录下打开 Git Bash Here，在里面进行操作
## 具体使用方法
- git初始化--建立仓储
    + `$ git init` 完成git隐藏目录的建立，即文件备份存放位置
    
- git设置个人信息--用以区分文件备份的不同的操作者
    + `$ git config --global user.name '姓名'`
    + `$ git config --global user.email '邮箱'` （邮箱可以不真实，但必须符合邮箱格式）
    
- 将文件备份需要两步（以文件abc.txt为例）
    + 一是将当前目录下的文件abc.txt放到仓储的大门口 `$ git add ./abc.txt`
    + 二是将仓储门口的文件abc.txt放到仓储房间中 `$ git commit -m '当前文件的说明'`
    + 注意： 可以将当前目录下所有子文件一次性都进行备份，即 `$ git add ./`
    
- 查询文件备份的状态--即判断是进行到第一步还是第二步或者一步都未进行
    + `$ git status` 
       * 若是输出 绿色 modified abc.txt,则表示 进行完第一步，该文件放到仓储门口
       * 若是输出  working tree clean，则表示 进行完第二步，文件已经被仓储房间中
       * 若是输出 红色 modified abc.txt,则表示 一步都未进行，文件被修改后未被备份
       
- 查询之前备份的历史版本 
    + `$ git log` ---- 输出历史版本的具体信息（包括最终备份时间、作者、版本号）
    + `$ git log --oneline` ---- 输出历史版本的简略信息（仅有版本号）
    
- 版本回退--当需要回退到某一个版本使用
    + `$ git reset --hard Head~0(1,2,3...)` ---0表示回退到最新备份的版本，1表示最新备份的上一个备份版本，2...
    + '$ git reset --hard 版本号' --- 回退到具体版本号，版本号通过 `$ git log --oneline`查询
    + 注意：当回退到某一版本之前，在用 `$ git log --oneline`查询时，会发现之后的版本不会再显现，其是并不是没用了，而要用 `$ git reflog`进行查询

- 创建分支及分支合并 --- 当开发某个功能到某种程度，因名字原因需要备份，但是备份到 主线分支会出现 别人调用该功能出现错误（因为该功能未完成），因此需要创建分支，将该残缺功能备份到分支中去，在该功能开发完成后，再将该分支合并到主线分支 master 中去，从而在主线分支中可以调用该功能
    + `$ git branch dev` ---- 创建分支dev,其中dev是分支名字，同时该分支其他用户访问不到
    + `$ git branch` ---- 查询当前所有的分同时查询当前所处的分支环境，默认是主线分支 master，其中 * 分支名字 就表示当前所处的分支环境
    + `$ git checkout 分支名字` ----表示切换到具体分支
    + `$ git merge dev` ----将分支dev合并到当前分支，注意的是合并dev分支时，当前所处的分支环境必须是其他分支（如：master），否则会报错
    + 注意: 在某子分支（如：dev）中查询 历史本分版本是可以查询到包含主线分支（master）和自身分支中的所有版本信息的，但是在主线分支中查询历史备份版本时（子分支未合并前）只能查询到主线分支中的 所有历史版本信息
    
- 代码上传服务器-----为了团队内成员代码共享，不通过文件发送和U盘传送，成员直接从GitHub（当做git的服务器）的仓储中下载备份的文件,文件上传 gitHub 的步骤：
    + 第一种上传方式：
        * 登录gitHub账户，右上角点击 '+'号，点击 New repository
        * 创建仓储来存储文件，在跳转的页面内的 repository name 中写入仓储名，description中写入仓储描述（可选），选择公开public,最后 create repository
        * 复制跳转页面中HTTPS框内的链接 `https://github.com/lxl469/test01.git`
        * 在需要上传的文件的父级目录下打开 `Git Bash Here`，在里面键入 `$ git push https://github.com/lxl469/test01.git master`
        * 注意：这种上传方式会在第一次上传文件时要验证GitHub的账号和密码，存在风险
    + 第二种上传方式
        * 在任意目录下打开 `Git Bash Here`,在里面创建公钥和私钥，将公钥在GitHub中设置传递，私钥自己留着，在文件上传是会自动进行公钥和私钥之间关系验证，从而避免输入账号和密码
        * 键入 `$ ssh -keygen -t sra -C '邮箱（随意，但要满足邮箱格式）'`,直接一路enter，生成公钥和私钥
        * 打开C://Users/Administrtor/ssh,然后打开新生成的文件 `id_sra.pub`，复制里面的内容， `ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDGqgvw1D84qC0tsFMsSc1U4ddLFbc8riuZoOO1D44mztnusuC+ALiseZsFOyJHVNQePUvbACxcC9WJcbl8x9MxPmpKWTyyoN02JNM/cLKGqzdCArAkfsRJVHFoZveX2mZlUA5spU+ki0BYFWwEkfKp131mqPyGGk1QzbLjw5W8ztkJckJhdE5BBkU6BpWXZPTRzXnjl2g4lE7VQCy3YV2W+gOXyE4yAwcgB6nzEiNt6I3sryMvIMXjNOMN66CKKPiula7MTmk3hJss7Gvsi7K/EzFeSQdZ2Sc88od0lgmY4RusP/2QfRA2BzDv+SaDiqM+hnA9GTOVB339ZMukPEcr lxl@qq.com
`
        * 打开gitHub，点击右上角 '+'号右边的图标中的settings,选中其中的 `SSH and GPG keys`,在点击 `New SSH key`，填写title，将上面的公钥内容复制到key框中，点击 Add,成功完成设置
        * 接下来创建gitHub仓储的步骤与之前的一致，但是上传的时候，复制SSH的链接地址，在要备份的文件复父级目录打开 `git Bash Here`中 键入 `$ git push SSH链接地址 master`
  
- 从GitHub的仓储中下载文件
    + 打开文件将存放目录，左击打开 `Git Bash Here`，在里面初始化一个仓储用来存放即将下载的文件
    + 键入 `$ git pull 链接地址 master`,链接地址可以是 HTTPS链接，也可以是 SSh链接
    
-上传文件和下载文件的一个简单地方法
    + 可以将链接地址 变成变量，这样不必要每次都要复制链接地址，但是只在当前目录下 `Git Bash Here`中可以使用，其他目录下要使用必须重新定义
        * `$ remote add 变量名 链接地址`，这样在后面上传或下载时，直接用 变量名将 链接地址取代