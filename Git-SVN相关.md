###项目迁移Svn To Git
#### 参考
- [简书svn2git](https://www.jianshu.com/p/c1cbc5b2826b)
#### cloneSvn 工程
```
1、打开终端 cd 到你想要 clone 的指定目录
$git svn clone Svn项目地址 --no-metadata --trunk=trunk/ --branches=branches --tags=tags --authors-file=./userinfo.txt -s 别名
可选值注解：
-r 可指定开始版本号。
-s指定clone下来的文件夹名
--trunk表示主开发项目
--branches表示分支项目，
--ignore-refs表示不包含后面的分支项目
--tag表示打标签的项目
--authors-file表示svn用户映射到git的用户文件
--no-metadata参数可阻止git导出SVN包含的一些无用信息。后面还可以加文件夹名字作为clone后的目录，如果没有默认是当前路径。
1.1 建立SVN用户到git用户的映射文件userinfo.txt，文件格式如下：
Svn 账户=Git 账户
例如：zhangS = zhangsan<zhangshan@github.com>
```
#### 整理分支和 Tag
```
clone 完成后原代码就以git方式存在了。现在我们看下这个目录下的分支(git branch -a)、Tag（git tag -l）,Log日志（git log）情况。Tag全部变成以分支存在了。本地默认master分支。所以我们需要对这些分支进行整理下以便更规范的管理
1，删除不需要的分支
$rm -Rf .git/refs/你的分支列表中想要删除的分支
2，Tag 移到 Git 真正的 Tag目录
$cp -Rf .git/refs/remotes/origin/tags/* .git/refs/tags/
$rm -Rf .git/refs/remotes/tags/
3, 最后将remote下的分支都移到本地
$cp -Rf .git/refs/remotes/origin/tags/* .git/refs/heads/
$rm -Rf .git/refs/remotes/
note: 也可以将clone好的项目在sourceTree下查看所有分支
```
#### 迁移 到 Git
```
这就到了 Svn To Git 的最后一步了
1，先去 Git 托管平台（如：gitLab） 创建一个空的项目
2，上传刚才整理好的svn 项目
$git remote add origin 创建的git项目地址
$git push -u origin --all
$git push -u origin --tags
```
