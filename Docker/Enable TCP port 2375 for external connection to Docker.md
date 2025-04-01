See this [issue](https://github.com/moby/moby/issues/25471).

1. Create `daemon.json` file in `/etc/docker`:

```Plain
{"hosts": ["tcp://0.0.0.0:2375", "unix:///var/run/docker.sock"]}
```

1. Create `/etc/systemd/system/docker.service.d` folder
2. Add `/etc/systemd/system/docker.service.d/override.conf`

```Plain
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd
```

3. Reload the systemd daemon:

```Plain
sudo systemctl daemon-reload
```

4. Restart docker:

```Plain
sudo ystemctl restart docker.service
```

# Setup Tailscale container

