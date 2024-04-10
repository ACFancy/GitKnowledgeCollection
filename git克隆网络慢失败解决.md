#### git克隆网络慢失败解决
- It could be an issue with poor internet connection. I had the same issue and resolved it with the below command,
```sh
git config --global http.postBuffer 4096M
```

- I once homebrew installation is successful, reverted back to the default buffer size, which is 1M.
```sh
git config --global http.postBuffer 1M
```
