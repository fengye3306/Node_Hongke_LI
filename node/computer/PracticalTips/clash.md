

## clash-for-linux-install

*clash-for-linux-install是github上的一个开源项目，其可以快速在debian&ubuntu系统上开启clash*  
```path
https://github.com/nelvko/clash-for-linux-install?tab=readme-ov-file
```


> tun模式

*TUN 模式 = 在 Linux 内核里创建一个“虚拟网卡”，把系统所有 IP 流量强制导入 Clash，再由 Clash 决定如何转发。这叫 透明代理（Transparent Proxy）。*

实际上存在clash已经正常起飞，但是浏览器等工具任然无法访问外网。此时应该考虑开启tun模式。     

```shell
# -验证是否已经起飞-
# 7890为转发端口，应该根据配置 设置
curl -x http://127.0.0.1:7890 https://www.google.com -I
#能返回 HTTP 200 / 301 / 302 → Clash + 机场 完全正常
```

> 常用指令集快速查询

* `clashctl on` 开启代理
* `clashctl off` 关闭代理
* `clashtun on` 关闭tun模式
* `clashtun off` 关闭tun模式




