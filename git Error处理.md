## Git Error
-  Git error: Encountered 7 file(s) that should have been pointers, but weren't
   ```shell
   #Clear the cache and do a hard reset:
     git rm --cached -r .
     git reset --hard
     git add --renormalize .
   ```
- Since git lfs 2.5.0, there is a new command available that makes this easier [doc](https://github.com/git-lfs/git-lfs/blob/main/docs/man/git-lfs-migrate.1.ronn#import-no-rewrite)
  ```shell
  git lfs migrate import --no-rewrite "broken file.jpg" "another broken file.png" ...
  # This "migrates" files to git lfs which should be in lfs as per .gitattributes, but aren't at the moment (which is the reason for your error message).
  # --no-rewrite prevents git from applying this to older commits, it creates a single new commit instead.
  # Use -m "commitmessage" to set a commitmessage for that commit.
  ```
## Git lfs相关
- 单单修改 .gitattributes文件内容还不够，还需要执行下面的命令行，以更正追踪的文件
  ```shell
  git add --renormalize .
  ```
