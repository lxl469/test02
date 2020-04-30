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
       * 若是输出 绿色 modified abc.txt,则表示 进行到第一步，该文件放到仓储门口
       * 若是输出 