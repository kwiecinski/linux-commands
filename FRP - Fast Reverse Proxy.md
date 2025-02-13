# FRP - Fast Reverse Proxy

[GitHub - fatedier/frp: A fast reverse proxy to help you expose a local server behind a NAT or firewall to the internet.](https://github.com/fatedier/frp)

You need to download the latest version of FRP:

[Releases · fatedier/frp · GitHub](https://github.com/fatedier/frp/releases/)

Example:

```
wget https://github.com/fatedier/frp/releases/download/v0.61.1/frp_0.61.1_linux_amd64.tar.gz
```

Unpack using:

```
tar -xvzf archive.tar.gz
```

Copy `frpc` (client) to your local machine and `frps` to your VPS.

Move the file to a more convenient location, such as `/home/user/frpc`.

---

### Running FRP at System Startup

To automatically start FRP at system boot, you can create a <u>systemd</u> service.

1. Create a systemd unit file:

```bash
sudo nano /etc/systemd/system/frp.service
```

2. Paste the following code into the `frp.service` file:

```ini
[Unit]
Description=FRP - Fast Reverse Proxy
After=network.target

[Service]
ExecStart=/home/user/frpc -c /home/user/frpc.toml
Type=simple
Restart=always
DynamicUser=yes
LimitNOFILE=1048576

[Install]
WantedBy=multi-user.target
```

In this file:

- `LimitNOFILE=1048576` increases the number of open file descriptors, which can be useful for handling high network traffic.
- `DynamicUser=yes` ensures that a temporary user is created for this service, enhancing security by preventing the service from running as root.
- `Restart=always` makes sure the service restarts even after a normal process termination.
- `Type=simple` means systemd considers the service as a basic process, assuming that the process started by `ExecStart` runs in the background and that its termination indicates the service has stopped.

With `Type=simple`, systemd does not wait for any signals from the process or check whether it has completed initialization. This type is commonly used for services that:

- Run as background daemons, such as HTTP servers or proxy servers.
- Operate as a single process without requiring extra systemd interactions.

Replace `/path/to/frp/` with the actual directory where FRP is located.

3. Save the file and close the editor.

4. Now, reload and start the service:

```bash
# Reload systemd configuration
sudo systemctl daemon-reload

# Start the service
sudo systemctl start frp

# Enable the service to start on boot
sudo systemctl enable frp
```

5. To check the service status:

```bash
sudo systemctl status frp
```

#### FRP Logs

You can also check FRP logs to ensure it's running correctly:

```bash
journalctl -u frp
```

View the latest logs in real time (live monitoring):

```bash
journalctl -u frp -f
```

Display the last 20 log entries:

```bash
journalctl -u frp -n 20
```

Display logs in reverse order (newest first):

```bash
journalctl -u frp -r
```

Following these steps, FRP will start automatically at system boot.

---
