#### git不同端开发的fileMode，LF,CRLF的问题
- [LF,CRLF文章链接](https://blog.csdn.net/kikitious_du/article/details/79603444)
- [filemode文章链接](https://blog.csdn.net/ai2000ai/article/details/79628896)
```
MAC:
git config --add core.filemode false
git config --global core.autocrlf input
WINDOW:
git config --global core.autocrlf false
```
