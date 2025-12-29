# podman_util

## selinux


### my_proxy
```bash
# ポリシーをインストール
make -f /usr/share/selinux/devel/Makefile my_{tcp,udp}_proxy.pp
sudo semodule -i my_{tcp,udp}_proxy.pp
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

## sockMgr

sockMgr is a systemd service that forwards traffic from a TCP/UDP port to a Unix socket.

### Usage

```bash

# サービスを登録
sudo cp sockMgr/* /usr/local/lib/systemd/system/
sudo systemctl daemon-reload

# SELinux設定(独自policyを使用しているので不要)
# sudo setsebool -P systemd_socket_proxyd_bind_any 1

# 80/tcpをプロキシしたい場合
systemctl start tcp2sock@80.socket
systemctl enable tcp2sock@80.socket

# 554/udpをプロキシしたい場合
systemctl start udp2sock@554.socket
systemctl enable udp2sock@554.socket
```