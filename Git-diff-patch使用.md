### 创建patch 文件的常用命令行
```
# n指从sha1 id对应的commit开始算起n个提交
git format-patch 【commit sha1 id】-n
# 某个提交的patch
git format-patch 【commit sha1 id】 -1
# 某两次提交之间的所有patch
git format-patch 【commit sha1 id】..【commit sha1 id】
```

### 创建diff文件的常用方法
```
git diff  【commit sha1 id】 【commit sha1 id】 >  【diff文件名】
# 使用SourceTree
选中要目标commit ,右击，选择create patch

```

### 应用patch 和 diff
- 检查patch/diff是否能正常打入:
```
git apply --check 【path/to/xxx.patch】
git apply --check 【path/to/xxx.diff】
```
- 打入patch/diff:
```
git apply 【path/to/xxx.patch】
git apply 【path/to/xxx.diff】
# 或者
git  am 【path/to/xxx.patch】
```
### 冲突解决
- 首先使用 以下命令行，自动合入 patch 中不冲突的代码改动，同时保留冲突的部分
```
git  apply --reject  xxxx.patch
同时会生成后缀为 .rej 的文件，保存没有合并进去的部分的内容，可以参考这个进行冲突解决
```
- 解决完冲突后删除后缀为 .rej 的文件，并执行git add.添加改动到暂存区
- 着执行git am --resolved或者git am --continue
- 在打入patch冲突时，可以执行git am --skip跳过此次冲突，也可以执行git am --abort回退打入patch的动作，还原到操作前的状态
### 参考
- [参考链接](https://juejin.im/post/5b5851976fb9a04f844ad0f4)
