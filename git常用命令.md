### 查看远程分支和本地分支的对应关系
```
git remote show origin

```

### 从本地删除远程已经删除的分支的tracking(在issue被merge之后，远程分支会被删除，那么相应的本地tracking我们也可以删除掉)
```
git remote prune origin
```

### 从本地删除远程已经删除的分支（merge后可以执行此操作保持工作区的清洁）
```
git fetch -p && for branch in `git branch -vv | grep ': gone]' | awk '{print $1}'`; do git branch -D $branch; done
```

### 删除本地分支
```
git branch -d <branch name>
```

### 删除本地分支
```
git branch -d <branch name>
```

### 删除远程分支
```
git push origin -d <branch name>
```

### 回滚untracked files的修改
```
git clean -fd
```
