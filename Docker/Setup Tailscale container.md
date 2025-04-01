1. Login to [Tailscale](https://login.tailscale.com/admin/settings/keys) and create a Auth key  

2. Configure the Docker VM to forward and masquerade traffic faccording to the tailscale setup guide: [Subnet routers and traffic relay nodes · Tailscale](https://tailscale.com/kb/1019/subnets/?tab=linux\#enable-ip-forwarding)

```bash
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

3. Create tailscale.yaml file

```yml
services:

  tailscaled:
    container_name: tailscale
    user: "0:0"
    privileged: true
    cap_add:
        - NET_ADMIN
    volumes:
        - '/nfs/docker/tailscale/settings:/var/lib'
        - '/dev/net/tun:/dev/net/tun'
    network_mode: "bridge"
    image: tailscale/tailscale
    command:
        - tailscaled
    restart: unless-stopped
    environment:
      - PUID=1000
      - PGID=1000
      - TS_USERSPACE=true
      - TS_AUTH_KEY="<TS_AUTH_KEY>"
      - TS_ROUTES=10.170.0.0/24,10.160.0.0/24
```

1. From the Docker VM run:

```bash
sudo docker exec tailscale tailscale up --authkey="<TS_AUTH_KEY>"
```

From the Tailscale portal, If you don’t see your subnets listed under Machines, run: 

```bash
sudo docker exec tailscale tailscale up --accept-routes --advertise-routes=10.160.0.0/24,10.170.0.0/24
```

1. You may need to Approve routes from the portal under docker-host    ![GeneralLinuxattachmentsPasted_image_20230714123120](attachments/GeneralLinuxattachmentsPasted_image_20230714123120.png)