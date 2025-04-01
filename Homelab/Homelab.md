## Examples of Branch Naming Patterns

| Branch Name                    | When to use it                              |
| ------------------------------ | ------------------------------------------- |
| `blog_image_generator`         | Working on that tool                        |
| `feature/blog_image_generator` | If you want to follow Git Flow-style naming |
| `fix/image-wrap-bug`           | Bug fix in an existing project              |
| `refactor/shared-utils`        | Refactor or cleanup work                    |
| `experiment/openai-image`      | Quick test or lab idea                      |

## Your SSH Key Management Workflow

We'll organize your keys and SSH config like this:

## Directory Structure

```Shell
~/.ssh/
├── id_ed25519_homelab         # Private key for Homelab server
├── id_ed25519_homelab.pub     # Public key for Homelab
├── id_ed25519_hetzner         # For Hetzner VPS
├── id_ed25519_hetzner.pub
├── id_ed25519_github          # For GitHub or CI/CD
├── id_ed25519_github.pub
├── config                     # SSH config file
```

## Step-by-Step Setup

### 1. Generate One Key per Server

```Shell
ssh-keygen -t ed25519 -C "docker-01" -f ~/.ssh/id_ed25519_docker_01
ssh-keygen -t ed25519 -C "pve-1" -f ~/.ssh/id_ed25519_pve_1
ssh-keygen -t ed25519 -C "hetzner" -f ~/.ssh/id_ed25519_hetzner_example
ssh-keygen -t ed25519 -C "github"  -f ~/.ssh/id_ed25519_github_example
```

Press Enter to skip a passphrase if you're okay with no prompt (or set one for extra security).

### 2. Copy Public Keys to Your Servers

```Shell
ssh-copy-id -i ~/.ssh/id_ed25519_docker_01.pub kaf@10.160.0.22
ssh-copy-id -i ~/.ssh/id_ed25519_pve_1.pub root@10.160.0.20
ssh-copy-id -i ~/.ssh/id_ed25519_hetzner.pub root@your-vps-ip
```

### 3. Create or Edit Your `~/.ssh/config`

```Shell
vim ~/.ssh/config
```

Add entries like this:

```Shell
# Docker server (Docker-01)
Host docker-01
  HostName 10.160.0.22
  User kaf
  IdentityFile ~/.ssh/id_ed25519_docker_01

# Proxmox (pve-1)
Host pve-1
  HostName 10.160.0.20
  User root
  IdentityFile ~/.ssh/id_ed25519_pve_1

# Hetzner VPS
Host hetzner
  HostName 65.21.xx.xx
  User root
  IdentityFile ~/.ssh/id_ed25519_hetzner

# GitHub (if you push with SSH)
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_github
  IdentitiesOnly yes
```

IdentitiesOnly yes ensures only the specified key is used, avoiding SSH confusion.

### 3.1. Copy the entire key to clipboard (GitHub)

- On **macOS**:
    
    ```Shell
    pbcopy < ~/.ssh/id_ed25519_github.pub
    ```
    
- On **Linux** (if using `xclip` or `wl-copy`):
    
    ```Shell
    xclip -sel clip < ~/.ssh/id_ed25519_github.pub
    # or
    wl-copy < ~/.ssh/id_ed25519_github.pub
    ```
    
- Or manually copy it from the terminal.

### 3. 2. Add the key on GitHub

1. Go to [https://github.com/settings/keys](https://github.com/settings/keys)
2. Click **“New SSH key”**
3. **Title**: Name it something like `Mac`
4. **Paste the key** into the big text box
5. Click **“Add SSH key”**

### 3.3. Test it (GitHub)

After it’s added, run:

```Shell
ssh -T git@github.com
```

Success:

```Plain
Hi kfuras! You've successfully authenticated, but GitHub does not provide shell access.
```

### 4. Test It

Now you can just:

```Shell
ssh docker_01
ssh pve-1
ssh hetzner
```

Or use `git@github.com` for GitHub actions.

## Optional Tips

- **Back up your keys** securely (encrypted USB or password manager with file support)
- Add keys to `ssh-agent` if you want automatic login:

```Shell
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_docker_01
```

### Check Which Key Was Used

Add `-v` to SSH to debug:

```Shell
ssh -v docker_01
```

You'll see:

```Shell
Offering public key: ~/.ssh/id_ed25519_docker_01
```

### Disable Password Prompt when Running `sudo` Commands

```Shell
sudo visudo

#
# This file MUST be edited with the 'visudo' command as root.
#
# Please consider adding local content in /etc/sudoers.d/ instead of
# directly modifying this file.
#
# See the man page for details on how to write a sudoers file.
#
Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

# This fixes CVE-2005-4890 and possibly breaks some versions of kdesu
# (#1011624, https://bugs.kde.org/show_bug.cgi?id=452532)
Defaults	use_pty

# This preserves proxy settings from user environments of root
# equivalent users (group sudo)
\#Defaults:%sudo env_keep += "http_proxy https_proxy ftp_proxy all_proxy no_proxy"

# This allows running arbitrary commands, but so does ALL, and it means
# different sudoers have their choice of editor respected.
\#Defaults:%sudo env_keep += "EDITOR"

# Completely harmless preservation of a user preference.
\#Defaults:%sudo env_keep += "GREP_COLOR"

# While you shouldn't normally run git as root, you need to with etckeeper
\#Defaults:%sudo env_keep += "GIT_AUTHOR_* GIT_COMMITTER_*"

# Per-user preferences; root won't have sensible values for them.
\#Defaults:%sudo env_keep += "EMAIL DEBEMAIL DEBFULLNAME"

# "sudo scp" or "sudo rsync" should be able to use your SSH agent.
\#Defaults:%sudo env_keep += "SSH_AGENT_PID SSH_AUTH_SOCK"

# Ditto for GPG agent
\#Defaults:%sudo env_keep += "GPG_AGENT_INFO"

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root	ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
# -> Add "NOPASSWD:" to the line below, before the last "ALL" entry <-
%sudo	ALL=(ALL:ALL) NOPASSWD: ALL

# See sudoers(5) for more information on "@include" directives:

@includedir /etc/sudoers.d
```

## Setup Docker & Docker Compose

## 1. Install using the `apt` repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker `apt` repository. Afterward, you can install and update Docker from the repository.

1. Set up Docker's `apt` repository.
    
    ```Shell
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    
    # Add the repository to Apt sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    ```
    
2. Install the Docker packages.
    
    Latest Specific version
    
    ---
    
    To install the latest version, run:
    
    ```Shell
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```
    
3. Verify that the installation is successful by running the `hello-world` image:
    
    ```Shell
    sudo docker run hello-world
    ```
    
    This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.
    

You have now successfully installed and started Docker Engine.

> Tip
> 
> Receiving errors when trying to run without root?
> 
> The `docker` user group exists but contains no users, which is why you’re required to use `sudo` to run Docker commands. Continue to [Linux postinstall](https://docs.docker.com/engine/install/linux-postinstall) to allow non-privileged users to run Docker commands and for other optional configuration steps.

## 2. Manage Docker as a non-root user

The Docker daemon binds to a Unix socket, not a TCP port. By default it's the `root` user that owns the Unix socket, and other users can only access it using `sudo`. The Docker daemon always runs as the `root` user.

If you don't want to preface the `docker` command with `sudo`, create a Unix group called `docker` and add users to it. When the Docker daemon starts, it creates a Unix socket accessible by members of the `docker` group. On some Linux distributions, the system automatically creates this group when installing Docker Engine using a package manager. In that case, there is no need for you to manually create the group.

> Warning
> 
> The `docker` group grants root-level privileges to the user. For details on how this impacts security in your system, see [Docker Daemon Attack Surface](https://docs.docker.com/engine/security/#docker-daemon-attack-surface).

> Note
> 
> To run Docker without root privileges, see [Run the Docker daemon as a non-root user (Rootless mode)](https://docs.docker.com/engine/security/rootless/).

To create the `docker` group and add your user:

1. Create the `docker` group.
    
    ```Shell
    sudo groupadd docker
    ```
    
2. Add your user to the `docker` group.
    
    ```Shell
    sudo usermod -aG docker $USER
    ```
    
3. Log out and log back in so that your group membership is re-evaluated.
    
    > If you're running Linux in a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.
    
    You can also run the following command to activate the changes to groups:
    
    ```Shell
    newgrp docker
    ```
    
4. Verify that you can run `docker` commands without `sudo`.
    
    ```Shell
    docker run hello-world
    ```
    
    This command downloads a test image and runs it in a container. When the container runs, it prints a message and exits.
    
    If you initially ran Docker CLI commands using `sudo` before adding your user to the `docker` group, you may see the following error:
    
    ```Shell
    WARNING: Error loading config file: /home/user/.docker/config.json -
    stat /home/user/.docker/config.json: permission denied
    ```
    
    This error indicates that the permission settings for the `~/.docker/` directory are incorrect, due to having used the `sudo` command earlier.
    
    To fix this problem, either remove the `~/.docker/` directory (it's recreated automatically, but any custom settings are lost), or change its ownership and permissions using the following commands:
    
    ```Shell
    sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
    sudo chmod g+rwx "$HOME/.docker" -R
    ```
    

## 2.1 (Optional) [Configure Docker to start on boot with systemd](https://docs.docker.com/engine/install/linux-postinstall/#configure-docker-to-start-on-boot-with-systemd)

Many modern Linux distributions use [systemd](https://systemd.io/) to manage which services start when the system boots. On Debian and Ubuntu, the Docker service starts on boot by default. To automatically start Docker and containerd on boot for other Linux distributions using systemd, run the following commands:

```Shell
$ sudo systemctl enable docker.service
$ sudo systemctl enable containerd.service
```

To stop this behavior, use `disable` instead.

```Shell
$ sudo systemctl disable docker.service
$ sudo systemctl disable containerd.service
```

You can use systemd unit files to configure the Docker service on startup, for example to add an HTTP proxy, set a different directory or partition for the Docker runtime files, or other customizations. For an example, see [Configure the daemon to use a proxy](https://docs.docker.com/engine/daemon/proxy/#systemd-unit-file).

## 3. (Optional) Install Docker Compose Plugin

Docker Compose is now included as a Docker plugin. To ensure it's installed:

1. **Update the package index:**
    
    ```Shell
    sudo apt-get update
    ```
    
2. **Install the Docker Compose plugin:**
    
    ```Shell
    sudo apt-get install -y docker-compose-plugin
    ```
    
3. **Verify the installation:**
    
    ```Shell
    docker compose version
    ```
    

_For more information, refer to the Docker Compose installation guide._

## 4. Mount NFS Share via `**fstab**`

To automatically mount an NFS share on your Ubuntu system:

1. **Install NFS client utilities:**
    
    ```Shell
    sudo apt-get install -y nfs-common
    ```
    
2. **Create a mount point:**
    
    ```Shell
    sudo mkdir -p /mnt/data
    ```
    
3. **Edit the** `**fstab**` **file to add the NFS share:**
    
    ```Shell
    sudo vim /etc/fstab
    ```
    
4. **Add the following line to the end of the file:**
    
    ```Plain
    nfs_server_ip:/exported/path /mnt/share_name nfs defaults,_netdev 0 0
    ```
    

Replace `nfs_server_ip` with the IP address of your NFS server and `/exported/path` with the path exported on the NFS server.

1. **Apply the changes by mounting all filesystems:**
    
    ```Shell
    sudo mount -a
    ```
    
2. **Verify the mount:**
    
    ```Shell
    df -h
    ```
    

You should see your NFS share listed.

By following these steps, you've installed Docker and Docker Compose on your Ubuntu system and configured an NFS share to mount automatically.

## Problem: Unraid Maps All NFS Users to `nobody` by Default

(If you’re unable to read or right data of the share, check out this section).

That’s why you see `nobody:users` on everything from your Ubuntu side — Unraid is **squashing remote UIDs**.

## Solution: Stop Squashing All Users

To allow your Ubuntu user `kaf` (UID 1000) to access the NFS share **as UID 1000**, you need to **remove** `**all_squash**` **and** `**anonuid**` **options**.

### Update the export line to:

```Plain
"/mnt/user/data" -fsid=106,async,no_subtree_check *(rw,sec=sys,insecure)
```

### What this does:

- Keeps NFS export readable and writable
- **Preserves real UID/GID from the client**
- Your Ubuntu user `kaf` (UID 1000) will access files as themselves

## Step-by-Step Fix

### On Unraid:

1. Edit the file:

```Shell
vi /etc/exports
```

1. Replace the line with:

```Plain
"/mnt/user/data" -fsid=106,async,no_subtree_check *(rw,sec=sys,insecure)
```

1. Apply the new rules:

```Shell
exportfs -ra
```

### On Ubuntu (Client):

No need to change `/etc/fstab` if it looks like this:

```Plain
10.160.0.21:/mnt/user/data /mnt/data nfs defaults,_netdev 0 0
```

Now remount it:

```Shell
sudo umount /mnt/data
sudo mount -a
```

### Verify It Works

Check ownership:

```Shell
ls -l /mnt/data
```

Files should now appear as owned by your actual user (`kaf`) instead of `nobody`.

Try creating a file:

```Shell
touch /mnt/data/testfile
ls -l /mnt/data/testfile
```

## Make It Persistent on Reboot

Since Unraid regenerates `/etc/exports`, use the **User Scripts plugin** to reapply the change on boot:

### Example script:

```Shell
#!/bin/bash
sleep 10

# Clean up NFS export options properly
sed -i -E 's/(,|\s)?all_squash(,|\s)?//g' /etc/exports
sed -i -E 's/(,|\s)?anonuid=99(,|\s)?//g' /etc/exports
sed -i -E 's/(,|\s)?anongid=100(,|\s)?//g' /etc/exports

# Remove trailing commas if any
sed -i -E 's/,+/,/g' /etc/exports       # collapse multiple commas into one
sed -i -E 's/\(,/\(/g' /etc/exports     # remove comma after opening parenthesis
sed -i -E 's/,\)/\)/g' /etc/exports     # remove comma before closing parenthesis

# Apply changes
exportfs -ra
```

Set it to run **"At Startup of Array"**

## Docker-compose

### `media-stack/.env.example`

```Plain
# -------- Shared Settings --------
TZ=Europe/Oslo
PUID=1000
PGID=1000
MEDIA=/mnt/data/media
TORRENTS=/mnt/data/torrents

# -------- Plex --------
PLEX_NAME=plex
PLEX_IMAGE=hotio/plex
PLEX_CLAIM=your_plex_claim_code_here
PLEX_PASS=yes
PLEX_PORT=32400
PLEX_CONFIG=/home/kaf/docker/media-stack/appdata/plex

# -------- Radarr --------
RADARR_NAME=radarr
RADARR_IMAGE=lscr.io/linuxserver/radarr
RADARR_PORT=7878
RADARR_CONFIG=/home/kaf/docker/media-stack/appdata/radarr

# -------- Sonarr --------
SONARR_NAME=sonarr
SONARR_IMAGE=lscr.io/linuxserver/sonarr
SONARR_PORT=8989
SONARR_CONFIG=/home/kaf/docker/media-stack/appdata/sonarr

# -------- Jackett --------
JACKETT_NAME=jackett
JACKETT_IMAGE=hotio/jackett
JACKETT_PORT=9117
JACKETT_CONFIG=/home/kaf/docker/media-stack/appdata/jackett

# -------- qBittorrent --------
QBITTORRENT_NAME=qbittorrent
QBITTORRENT_IMAGE=ghcr.io/hotio/qbittorrent:latest
QBITTORRENT_PORT=8081
QBITTORRENT_UMASK=002
QBITTORRENT_WEBUI_PORT=8081
QBITTORRENT_CONFIG=/home/kaf/docker/media-stack/appdata/qbittorrent

# -------- Unpackerr --------
UNPACKERR_NAME=unpackerr
UNPACKERR_IMAGE=golift/unpackerr
UN_DEBUG=false
UN_LOG_FILE=/downloads/unpackerr.log
UN_SONARR_0_URL=http://sonarr:8989/
UN_SONARR_0_API_KEY=your_sonarr_api_key_here
UN_SONARR_0_PATH=/downloads/tv/
UN_RADARR_0_URL=http://radarr:7878/
UN_RADARR_0_API_KEY=your_radarr_api_key_here
UN_RADARR_0_PATH=/downloads/movies/
UN_SONARR_0_DELETE_DELAY=-1m
UN_RADARR_0_DELETE_DELAY=-1m
UN_TIMEOUT=15s
UN_PARALLEL=1
UN_INTERVAL=2m
UN_DELETE_DELAY=1h
UN_START_DELAY=1m
UN_RETRY_DELAY=5m
UNPACKERR_CONFIG=/home/kaf/docker/media-stack/appdata/unpackerr

```

### `unifi-stack/.env.example`

```Plain
# -------- Unifi Controller --------
UNIFI_NAME=unifi-network-application
UNIFI_IMAGE=lscr.io/linuxserver/unifi-network-application
UNIFI_MEM_LIMIT=1024
UNIFI_MEM_STARTUP=1024
UNIFI_CONFIG=/home/kaf/docker/unifi-stack/appdata/unifi-network-application

# -------- MongoDB --------
MONGO_NAME=mongodb
MONGO_IMAGE=mongo
MONGO_PORT=27017
MONGO_CONFIG=/home/kaf/docker/unifi-stack/appdata/mongodb

# -------- MongoDB Connection --------
MONGO_USER=unifi
MONGO_PASS=your_mongo_password_here
MONGO_HOST=10.160.0.20
MONGO_DBNAME=unifi
MONGO_AUTHSOURCE=unifi

# -------- Shared Settings --------
TZ=Europe/Oslo
PUID=1000
PGID=1000

```

### Media-stack

media-stack.yaml

```YAML
version: "3.8"

services:
  plex:
    container_name: ${PLEX_NAME}
    image: ${PLEX_IMAGE}
    restart: unless-stopped
    network_mode: bridge
    environment:
      - TZ=${TZ}
      - PLEX_CLAIM=${PLEX_CLAIM}
      - PLEX_PASS=${PLEX_PASS}
      - PUID=${PUID}
      - PGID=${PGID}
    ports:
      - "${PLEX_PORT}:32400"
    volumes:
      - ${PLEX_CONFIG}:/config
      - /dev/shm:/transcode
      - ${MEDIA}:/data
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:32400/web"]
      interval: 30s
      timeout: 10s
      retries: 3

  radarr:
    container_name: ${RADARR_NAME}
    image: ${RADARR_IMAGE}
    restart: unless-stopped
    network_mode: bridge
    environment:
      - TZ=${TZ}
      - PUID=${PUID}
      - PGID=${PGID}
    ports:
      - "${RADARR_PORT}:7878"
    volumes:
      - ${RADARR_CONFIG}:/config
      - ${MEDIA}:/movies
      - ${TORRENTS}:/downloads
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:7878/ping"]
      interval: 30s
      timeout: 5s
      retries: 3

  sonarr:
    container_name: ${SONARR_NAME}
    image: ${SONARR_IMAGE}
    restart: unless-stopped
    network_mode: bridge
    environment:
      - TZ=${TZ}
      - PUID=${PUID}
      - PGID=${PGID}
    ports:
      - "${SONARR_PORT}:8989"
    volumes:
      - ${SONARR_CONFIG}:/config
      - ${MEDIA}:/tv
      - ${TORRENTS}:/downloads
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8989/ping"]
      interval: 30s
      timeout: 5s
      retries: 3

  jackett:
    container_name: ${JACKETT_NAME}
    image: ${JACKETT_IMAGE}
    restart: unless-stopped
    network_mode: bridge
    environment:
      - TZ=${TZ}
      - PUID=${PUID}
      - PGID=${PGID}
    ports:
      - "${JACKETT_PORT}:9117"
    volumes:
      - ${JACKETT_CONFIG}:/config
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9117"]
      interval: 30s
      timeout: 5s
      retries: 3

  qbittorrent:
    container_name: ${QBITTORRENT_NAME}
    image: ${QBITTORRENT_IMAGE}
    restart: unless-stopped
    network_mode: bridge
    environment:
      - TZ=${TZ}
      - PUID=${PUID}
      - PGID=${PGID}
      - UMASK=${QBITTORRENT_UMASK}
      - WebUI_Port=${QBITTORRENT_WEBUI_PORT}
    ports:
      - "${QBITTORRENT_PORT}:8080"
    volumes:
      - ${QBITTORRENT_CONFIG}:/config
      - ${TORRENTS}:/data/torrents
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080"]
      interval: 30s
      timeout: 5s
      retries: 3

  unpackerr:
    container_name: ${UNPACKERR_NAME}
    image: ${UNPACKERR_IMAGE}
    restart: unless-stopped
    network_mode: bridge
    environment:
      - TZ=${TZ}
      - UN_DEBUG=${UN_DEBUG}
      - UN_LOG_FILE=${UN_LOG_FILE}
      - UN_SONARR_0_URL=${UN_SONARR_0_URL}
      - UN_SONARR_0_API_KEY=${SONARR_API_KEY}
      - UN_SONARR_0_PATH=${UN_SONARR_0_PATH}
      - UN_RADARR_0_URL=${UN_RADARR_0_URL}
      - UN_RADARR_0_API_KEY=${RADARR_API_KEY}
      - UN_RADARR_0_PATH=${UN_RADARR_0_PATH}
      - UN_SONARR_0_DELETE_DELAY=${UN_SONARR_0_DELETE_DELAY}
      - UN_RADARR_0_DELETE_DELAY=${UN_RADARR_0_DELETE_DELAY}
      - UN_TIMEOUT=${UN_TIMEOUT}
      - UN_PARALLEL=${UN_PARALLEL}
      - UN_INTERVAL=${UN_INTERVAL}
      - UN_DELETE_DELAY=${UN_DELETE_DELAY}
      - UN_START_DELAY=${UN_START_DELAY}
      - UN_RETRY_DELAY=${UN_RETRY_DELAY}
    volumes:
      - ${TORRENTS}:/downloads
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:5656"]
      interval: 30s
      timeout: 5s
      retries: 3
```

### Unifi-stack

docker-compose.yml

```YAML
version: "3.8"

services:
  mongodb:
    container_name: ${MONGO_NAME}
    image: ${MONGO_IMAGE}
    restart: unless-stopped
    network_mode: bridge
    environment:
      - TZ=${TZ}
    ports:
      - "${MONGO_PORT}:27017"
    volumes:
      - ${MONGO_CONFIG}:/data/db
    healthcheck:
      test: ["CMD", "mongo", "--eval", "db.adminCommand('ping')"]
      interval: 30s
      timeout: 10s
      retries: 3

  unifi:
    container_name: ${UNIFI_NAME}
    image: ${UNIFI_IMAGE}
    restart: unless-stopped
    network_mode: host
    environment:
      - TZ=${TZ}
      - PUID=${PUID}
      - PGID=${PGID}
      - MONGO_USER=${MONGO_USER}
      - MONGO_PASS=${MONGO_PASS}
      - MONGO_HOST=${MONGO_HOST}
      - MONGO_PORT=${MONGO_PORT}
      - MONGO_DBNAME=${MONGO_DBNAME}
      - MONGO_AUTHSOURCE=${MONGO_AUTHSOURCE}
      - MEM_LIMIT=${UNIFI_MEM_LIMIT}
      - MEM_STARTUP=${UNIFI_MEM_STARTUP}
    volumes:
      - ${UNIFI_CONFIG}:/config
    healthcheck:
      test: ["CMD", "curl", "-f", "https://localhost:8443"]
      interval: 30s
      timeout: 10s
      retries: 3
```

## How to Check if Plex is Using RAM (tmpfs) for Transcoding

### 1. Confirm `tmpfs` is configured in `docker-compose.yml`

```YAML
tmpfs:
  - /transcode:rw,size=3g
environment:
  - PLEX_TRANSCODE_DIR=/transcode
```

> PLEX_TRANSCODE_DIR is required — without it, Plex won’t use /transcode.

### 2. Restart Plex and play a video that forces transcoding

- Use a mobile app or unsupported format (e.g., subtitles, 4K -> 1080p)
- Check **Now Playing** in Plex UI:
    - `Transcode (H.264)` → good
    - `Direct Play` → no transcoding = no RAM usage

---

### 3. Check usage from inside the container

Run:

```Shell
docker exec -it plex df -h /transcode
```

You should see:

```Plain
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           3.0G  100M  2.9G   4% /transcode
```

Or use:

```Shell
docker exec -it plex watch -n 1 du -sh /transcode
```

### 4. Check the mount type (should say `tmpfs`)

```Shell
docker exec -it plex mount | grep /transcode
```

Expected output:

```Plain
tmpfs on /transcode type tmpfs (rw,size=3145728k)
```

### Nothing showing up?

- Check if the stream is actually transcoding
- Double-check that `PLEX_TRANSCODE_DIR=/transcode` is set
- Restart the container after editing `docker-compose.yml`

## `.gitignore` (place in each stack folder)

Here's how you should set up your `.gitignore` for both `media-stack` and `unifi-stack` folders to keep your sensitive and runtime data out of version control.

**Example:** `**/docker/media-stack/.gitignore**`

```Plain
# Ignore the env file with sensitive keys
.env

# Ignore all app config folders if present locally
plex/
radarr/
sonarr/
prowlarr/
jackett/
qbittorrent/
unpackerr/
mongodb/

# Ignore any logs, secrets, or runtime files
*.log
*.env.*
.env.local
.env.secret
```

**Example:** `**/docker/unifi-stack/.gitignore**`

```Plain
.env
unifi/
mongodb/
*.log
```

## Best Practices

- Keep `.env` out of Git to protect secrets/API keys.
- Commit `.env.example` if you want to share a safe template.
- Use `README.md` to document which variables the `.env` file should include.

## Copy All Appdata Folders via SSH with `rsync`

Run this **on your Docker server** (`docker-01`):

```Shell
rsync -avz --progress -e ssh \
  root@10.160.0.21:/mnt/user/appdata/{jackett,mongodb,plex,qbittorrent,radarr,sonarr,unifi-network-application,unpackerr}/ \
  ~/docker/

```

> This will copy each folder directly into ~/docker/ on your server.
> 
> If you want to copy into a subfolder like `media-stack/` or `unifi-stack/`, you can adjust the target path like this:

### Example: split between media and unifi stacks

```Shell
# Media stack apps
rsync -avz --progress -e ssh \
  root@10.160.0.21:/mnt/user/appdata/{plex,qbittorrent,radarr,sonarr,prowlarr,unpackerr,jackett} \
  ~/docker/media-stack/

# Unifi stack apps
rsync -avz --progress -e ssh \
  root@10.160.0.21:/mnt/user/appdata/{unifi-network-application,mongodb} \
  ~/docker/unifi-stack/appdata/
```

## After the copy, fix ownership:

```Shell
sudo chown -R kaf:kaf ~/docker/
```