### 1 查看虚拟机ip
```bash
ifconfig 
# 需安装 net-tools 包
sudo apt-get install net-tools   # 对于 Debian/Ubuntu 系统
sudo yum install net-tools       # 对于 CentOS/RHEL 系统

ip addr show
```

### 2 启动 SSH 服务器
```sh
# 安装 ssh 服务器
sudo yum install openssh-server # 同上
sudo apt-get install openssh-server
# 查看系统
ps -p 1
# 启动ssh 服务器 如果是使用 systemd 作为 init 系统
sudo systemctl start sshd
systemctl status systemd    # 检查systemd 服务状态
systemctl start systemd     # 如果没运行启动
systemctl status dbus       # 检查 dbus 服务
systemctl start dbus        # 如果dbus没运行
# 查看系统日志获取信息
`/var/log/messages`
`/var/log/syslog`

#如果是传统的 init 系统
/etc/init.d/httpd start   # 启动 Apache HTTP 服务器
/etc/init.d/httpd stop    # 停止 Apache HTTP 服务器
/etc/init.d/httpd restart # 重启 Apache HTTP 服务器
/etc/init.d/sshd start    # 启动 sshd 服务
sudo /usr/sbin/sshd       # 手动启动 ssh 守护进程

# 生成密钥
sudo ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key # 生成 RSA 密钥
sudo ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key   # DSA
sudo ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key  # ECDSA
sudo ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key   # ED25519

# 为每个密钥配置正确的权限
sudo chmod 600 /etc/ssh/ssh_host_*
sudo /usr/sbin/sshd

# 在wsl中
sudo pkill sshd
sudo /usr/sbin/sshd

```
### 3. 配置 SSHD配置文件
```shell
# 使以下配置生效
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key
# root通过ssh登录
PermitRootLogin yes
PasswordAuthentication yes
```
