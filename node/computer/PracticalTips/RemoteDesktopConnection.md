
> 本地windows远程桌面同一路由器下的debian


1. 查debian的ip

```sh
# ip列表
ip addr show

# 查看路由器分配的ip
hostname -I
```

2. debian安装xrdp

```sh
# install

sudo apt install xrdp

# 启动并设置为开机启动
sudo systemctl enable xrdp
sudo systemctl start xrdp
```

3. 配置debian防火墙开启默认端口（3389） 

```sh
# 安装ufw
sudo apt update
sudo apt install ufw

# 启用防火墙并允许RDP端口
sudo ufw enable
sudo ufw allow 3389/tcp
sudo ufw status verbose  # 查看规则
```

4. windows链接，使用`win + R` ，后输入 `mstsc`工具远程链接。  

