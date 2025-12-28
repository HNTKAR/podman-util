# podman_util

## sock2port

sock2port is a systemd service that forwards traffic from a TCP port to a Unix socket.

### Usage

```bash
# SELinux設定
sudo setsebool -P systemd_socket_proxyd_bind_any 1

# 80/tcpをプロキシしたい場合
systemctl start sock2port@80.socket
systemctl enable sock2port@80.socket

# 443/tcpをプロキシしたい場合
systemctl start sock2port@443.socket
systemctl enable sock2port@443.socket
```