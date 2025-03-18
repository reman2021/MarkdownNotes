### 网络代理

#### 配置网络代理

```shell
//全局代理
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
//只对github.com使用代理
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
git config --global https.https://github.com.proxy socks5://127.0.0.1:1080
```

代理IP和PORT可在代理工具中查看。

#### 查看网络代理

```
env | grep -I proxy
```

#### 取消网络代理

```shell
git config --global --unset http.proxy
git config --global --unset https.proxy

git config --global --unset http.https://github.com.proxy
git config --global --unset https.https://github.com.proxy
```

