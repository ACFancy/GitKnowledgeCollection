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
### git 误删分支恢复方法
```
git log -g 找到之前的删掉分支的提交记录（比如commit_xxx）
git branch recover_branch_name commit_xxx
git checkout recover_branch_name
```
### 设置author和email
```
// 设置全局
git config --global user.name "Author Name"
git config --global user.email "Author Email"

// 或者设置本地项目库配置
git config user.name "Author Name"
git config user.email "Author Email"
```
### git修改提交作者和邮箱
```
//只需要最近一次提交
git commit --amend --author="NewAuthor <NewEmail@address.com>"

//如果是多个修改，那么就需要使用到git filter-branch这个工具来做批量修改
<1>
1. git rebase -i HEAD~n 的方式，Pick -> edit, 
2. 再使用git commit --amend --author="NewAuthor <NewEmail@address.com>"
3. git rebase --continue 完成操作
<2>脚本
#!/bin/sh

git filter-branch --env-filter '

an="$GIT_AUTHOR_NAME"
am="$GIT_AUTHOR_EMAIL"
cn="$GIT_COMMITTER_NAME"
cm="$GIT_COMMITTER_EMAIL"

if [ "$GIT_COMMITTER_EMAIL" = "[Your Old Email]" ]
then
    cn="[Your New Author Name]"
    cm="[Your New Email]"
fi
if [ "$GIT_AUTHOR_EMAIL" = "[Your Old Email]" ]
then
    an="[Your New Author Name]"
    am="[Your New Email]"
fi

export GIT_AUTHOR_NAME="$an"
export GIT_AUTHOR_EMAIL="$am"
export GIT_COMMITTER_NAME="$cn"
export GIT_COMMITTER_EMAIL="$cm"
'
```
