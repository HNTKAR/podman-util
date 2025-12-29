# podman_util

## selinux


### my_proxy
```bash
# ポリシーをインストール
make -f /usr/share/selinux/devel/Makefile my_proxy.pp
sudo semodule -i my_proxy.pp
```

#### _debug_
```bash
sudo tail -F /var/log/audit/audit.log | grep avc
grep-r $MACRO /usr/share/selinux/devel/include/

# corenet library
# /usr/share/selinux/devel/include/kernel/corenetwork.if

# init library
# /usr/share/selinux/devel/include/system/init.if
```

## sock2port

sock2port is a systemd service that forwards traffic from a TCP port to a Unix socket.

### Usage

```bash

# サービスを登録
sudo cp sock2port/sock2port* /usr/local/lib/systemd/system/
sudo systemctl daemon-reload

# SELinux設定
sudo setsebool -P systemd_socket_proxyd_bind_any 1

# 80/tcpをプロキシしたい場合
systemctl start sock2port@80.socket
systemctl enable sock2port@80.socket

# 443/tcpをプロキシしたい場合
systemctl start sock2port@443.socket
systemctl enable sock2port@443.socket
```