# git filter-repo (推荐)
- [文档参考地址](https://htmlpreview.github.io/?https://github.com/newren/git-filter-repo/blob/docs/html/git-filter-repo.html#EXAMPLES)
- [源项目地址](https://github.com/newren/git-filter-repo)
- [github 操作文档sample](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

# git filter-branch (不推荐)
## step 1:
```
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA-File" \
  --prune-empty --tag-name-filter cat -- --all

git filter-branch --force --index-filter \
  "git rm -r --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-Data-Directory" \
  --prune-empty --tag-name-filter cat -- --all
 
```
## step 2:(Optional)
```
echo "YOUR-FILE-WITH-SENSITIVE-DATA" >> .gitignore
git add .gitignore
git commit -m "Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore"
```

## step 3:
```
强推替换所有的branch分支
git push origin --force --all
```
## step 4:
```
强推替换所有tag分支
git push origin --force --tags
```

## step 5:
```
#After some time has passed and you're confident that git filter-branch had no unintended side effects, 
#you can force all objects in your local repository to be dereferenced and garbage collected with
#the following commands (using Git 1.8.5 or newer)
git for-each-ref --format="delete %(refname)" refs/original | git update-ref --stdin
git reflog expire --expire=now --all
git gc --prune=now
```

[github参考地址](https://help.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository)
