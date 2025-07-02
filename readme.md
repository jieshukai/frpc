## frpc for install 

```shell
go install github.com/jieshukai/frpc@latest
```

### Examples
```shell
# nat hole discover
frpc nathole discover --nat_hole_stun_server stun.easyvoip.com:3478

```
```shell
#配置 frpc 服务
mkdir /etc/frp
cat > /etc/frp/frpc.toml <<EOF
serverAddr = "x.x.x.x"
serverPort = 7000
auth.token = "x-x-x-x"
EOF


cat > /etc/systemd/system/frpc.service << EOF
[Unit]
# 服务名称，可自定义
Description = frp server
After = network.target syslog.target
Wants = network.target

[Service]
Type = simple
# 启动frps的命令，需修改为您的frps的安装路径
ExecStart =/root/go/bin/frpc -c /etc/frp/frpc.toml

[Install]
WantedBy = multi-user.target
EOF
```