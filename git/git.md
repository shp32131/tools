## 配置SSH  
- 大部分git服务器使用SSH公钥来进行授权，所以系统中每个用户都要提供一个公钥用于授权  
- 1.在自己电脑端生成一个密钥和一个公钥,使用工具 `ssh_keygen`   
  - `linux`系统  
    + SSH公钥默认储存在用户家目录下 `\~/.ssh` 目录   
    + 目录中有两个文件分别是 `id_rsa` 密钥 和 `id_rsa.pub` 公钥   
  - `window`系统
    + SSH密钥默认保存在 `c:\user\liuqinglin\.ssh `  
    + `ssh-keygen -t rsa -C 'yourEmail'`  
      - `-t` 指定密钥类型,默认生成用于SSH-2的RSA密钥  
      - `-C` 指定添加密钥中的注释  
- 2.复制 `id_rsa.pub` 文件内的公钥到托管平台,比如 `github -> setting -> SSH Keys`  

## git 配置
- git有三个配置文件,后面的配置会覆盖前面的配置  
  + `/etc/gitconfig` 操作指令  `git config --system`   
  + `~/.gitconfig`  操作指令   `git config --global`  
  + `.git/config`  操作指令   
- 查看配置信息，有重名的，默认使用的是最后一个配置  
  + `git --version` 查看版本 
  + `git config --list` 查看配置信息 
  + `git config user.name` 查看配置值  

- 配置 `git`
  + 配置用户名和邮箱,每次提交都会用这两个信息标记是谁提交了更新,随更新内容一起纳入历史记录  
    - `git config --global user.name 'your name'`
    - `git config --global user.email your email`
  + 配置默认编辑器  
    - `git config --global core.editor vim `

## git 基本管理
### git三大概念 工作区 暂存区 版本库  
![git](./imgs/git01.jpg)

- 1.工作区: 就是我们电脑中的项目的目录树  
  + `git clean`指令用来从工作目录中删除所有没有跟踪`tracked`过的文件  
    - `git clean -n` 告诉你哪些文件将会被删除(没有tracked的文件)  
    - `git clean -f` 删除当前目录下没有`tracked`过的文件,不会删除`.gitignore`指定的文件 
    - `git clean -df` 删除当前目录下没有被`tracked`过的文件和文件夹  

- 2.暂存区: 由`git init`指令生成的`.git`目录(版本库)中,标记为 `stage` 或 `index`的目录树,是暂存区  
  + 执行`git add`时,将工作区的修改更新到`stage`暂存区中,同时将修改的内容写到`objects`对象库中  
    - `git add .` 提交所有修改和新增的文件 
    - `git add -u` 只提交修改文件,不提交新增文件  
    - `git checkout .` 放弃没有提交的所有修改  
    - `git checkout xx.js` 放弃指定文件的修改  
    - `git ls-files -s` 查看暂存区文件列表 
    - `git cat-file -p 6e9a94` 查看暂存区文件内容   
  + `git rm --cached <file>`时,直接从`stage`暂存区删除文件,工作区没影响  
  + `git commit`时,将`stage`目录树写到`objects`对象库中`master`分支相应更新  
    - 即提交时`master`分支的目录树是暂存区的目录树  
  + `git checkout <file>`时，危险操作,用`stage`暂存区文件替换工作区文件 
    - 会清除掉工作区中未添加到`stage`暂存区的改动  
  + `git checkout HEAD <file>`时,危险操作,用`HEAD`指向的`master`分支中的文件替换暂存区和工作区的文件
    - 会清除工作区中和暂存区中未提交的改变   

- 3.版本库: 由`git init`指令生成的`.git`目录,是`git`的版本库   
  + 版本库中`HEAD`指向的是一个`master`分支目录树  
  + 版本库中，`objects`标识的是`git`的对象库，位于`.git/objects`目录下，包含各种创建对象和内容  
  + `git reset HEAD`时，`stage`暂存区的目录树重写为`master`分支的目录树,工作区没影响  
  + 使用`reset`恢复到历史提交点,重置暂存区与工作区的内容  
    - `git reset --hard` 清空工作区和暂存区的改动 
    - `git reset --hard HEAD^^^` 恢复前三个版本  
    - `git reset --hard b7b73147ca8d6fc20e451d7b36` 恢复到指定提交版本  
      + 先由`git log`指令获取版本号 
    - `git reset --soft` 保留工作区的内容,把文件差异放进暂存区  
### 分支管理 
- 分支说明: 
  + `master` 主分支,有且只有一个  
  + `release` 是线上版本分支,线上版本发布后,会将`release`合并到`master`  
  + `develop` 开发分支,通常给测试部署环境或打包的分支,每个成员在自己分支开发完成后,向`develop`分支合并   
  + `feature` 功能分支或个人分支,有多个,`merge`完成后会删除   

### 日志查看 

### 效率提升 

## git 使用  
- 1.创建本地仓库并完成初始提交 
  + 新建项目并添加`README.md`文件 
  + `git init` 
  + `git add README.md`
  + `git commit -m "first commit"`

- 2.添加远程仓库 
  + `git remote add origin https://github.com/shp32131/hansan.git` 

- 3.查看远程仓库 `git remote -v`

- 4.推送数据到远程仓库 `git push -u origin master`
  + `git pull origin master` 当`hint: not have locally...`
  + `git pull --allow-unrelated-histories` 当`refusing to merge unrelated histories...`

- 5.删除远程仓库关联 `git remote rm origin`

### 自动部署 
