

## 项目子工程

> 主工程安装子工程

```bash
## <repository-url> 目标子工程仓库地址
## <path>           目标子工程配置在主工程的路径地址
git submodule add <repository-url> <path>

## eg: 
# git submodule add git@github.com:fengye3306/CloudCompare.git ./3rdparty/CloudCompare
```

> 拷贝&更新子工程

```bash
# 对于默认拷贝（git clone）的一个项目，默认拷贝主工程而不带子工程
# 使用submodule update 更新子模块
git submodule update --init --recursive
```

## github拉取error

> Failed to connect to github.com port 443

fatal: unable to access 'https://github.com/fengye3306/Node_FengYe.git/': Failed to connect to github.com port 443 after 21052 ms: Could not connect to server

开启翻墙且浏览器打得开github页面,本地拉取代码时发生error，问题本质是git工具没有走翻墙。   

```ssh
# 以实际代理ip:port为准

# 配置socks5代理 
git config --global http.proxy socks5 127.0.0.1:7890
git config --global https.proxy socks5 127.0.0.1:7890
# 配置http代理
git config --global http.proxy 127.0.0.1:7890
git config --global https.proxy 127.0.0.1:7890
```
本质是要使得git走代理，即（127.0.0.1）是使用的代理的主机号，7890是数据转发端口。     


**扩展**   
```ssh
# 查看代理命令
git config --global --get http.proxy
git config --global --get https.proxy  
# 取消代理命令
git config --global --unset http.proxy
git config --global --unset https.proxy
```
