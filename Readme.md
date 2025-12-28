# podman_util

## sock2port

sock2port is a systemd service that forwards traffic from a TCP port to a Unix socket.

### Usage

```bash
systemctl enable --now sock2port@%i.socket
systemctl enable --now sock2port@%i.service
```