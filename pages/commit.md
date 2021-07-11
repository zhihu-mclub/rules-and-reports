# 如何提交更改

这个仓库的VCS基于Git。

### 何为Git？
>Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.  
> 
>Git is easy to learn and has a tiny footprint with lightning fast performance. It outclasses SCM tools like Subversion, CVS, Perforce, and ClearCase with features like cheap local branching, convenient staging areas, and multiple workflows.  --摘自git-scm.com

### 如何提交文件？
**强烈建议你先不要拿这个仓库练手，先新建一个仓库，谢谢**  
首先，在Github首页点击`New`，创建一个新仓库。

<img src="https://cdn.jsdelivr.net/gh/zhihu-mclub/rules-and-reports@gh-pages/img/new-repo.png">

接下来，你大概会看到这样子的界面：

<img width="800px" height="500px" src="https://cdn.jsdelivr.net/gh/zhihu-mclub/rules-and-reports@gh-pages/img/repo.png">

然后在按照你的情况填写即可。不要勾任何一个复选框，点击`Create repository`，然后你应该能看到如下界面：

<img width="800px" height="500px" src="https://cdn.jsdelivr.net/gh/zhihu-mclub/rules-and-reports@gh-pages/img/repo-details.png">

去 [git官方网站](https://git-scm.com/) 下载一个Git。
下载后双击运行，一路next，安装完成后在任一资源管理器中右键，你应该可以看到`Git Bash Here`这个菜单，点击它。  
接着会出来一个Unix风格的命令行窗口，回到浏览器，复制`Quick setup — if you’ve done this kind of thing before`下面的框里的内容。
输入以下命令(注意Git默认的复制方式是Ctrl+Ins，粘贴方式是Shift+Ins)：
```
git init
git remote add origin 你复制的链接
```
接下来新建一个txt文件，命名为`test.txt`，写入以下内容：
```
Hello World
```
然后Ctrl+S保存，在进到命令行，输入以下内容：
```
git add test.txt
git commit -m "my first commit!"
git push -u origin master
```
至此，你已经完成了一次Git的版本推送。下面是一个简单的示例以获得`rules-and-reports`仓库的内容：
```
git clone https://github.com/zhihu-mclub/rules-and-reports.git
```
然后在你修改完仓库内容后(本文假设你更改了main分支的内容)，输入以下命令：
```
git add .
git commit -m "你的对这次提交的描述 不要删引号"
git pull origin main
git push origin main
```
如果你在gh-pages分支更改了内容，那么你应该输入以下命令：
```
git checkout gh-pages
git add .
git commit -m "你的对这次提交的描述 不要删引号"
git pull origin gh-pages
git push origin gh-pages
```