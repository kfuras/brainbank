Recently while setting up a Docker Compose-based media stack, I ran into a tricky and silent issue. It looked like everything was working — the containers were up, the mounts were in place, and the files were visible — yet I couldn't write to my NFS share from inside the containers.

Here’s what happened, and how I fixed it.

## The Setup

I had a shared NFS mount point at `/mnt/data` on my Ubuntu Docker host, and I wanted to use environment variables to keep things clean:

```Plain
# NFS Share Mount
DATA=/mnt/data
```

And in my `docker-compose.yml`:

```YAML
services:
  radarr:
    image: linuxserver/radarr
    volumes:
      - ${DATA}:/data
```

This approach seemed solid — clean, reusable, and friendly for future automation.

## What Worked

- The container started successfully
- The NFS share mounted properly on the host
- Inside the container, I could `ls /data` and see all my files and folders
- Permissions looked fine on the host: the NFS export mapped to UID/GID 1000, which matched the container user

## The Problem

Despite being able to browse files, I couldn’t **write** to the mounted folder inside the container. Commands like:

```Shell
touch /data/testfile
```

would fail with:

```Plain
Permission denied
```

## What I Discovered

After hours of chasing NFS export settings, UID mapping, and file ownership, I tried one small change that fixed it instantly:

```YAML
volumes:
  - /mnt/data:/data
```

Just like that, everything worked — I could read, write, and delete files inside `/data` from within the container.

## The Real Issue

While using environment variables like `${DATA}` in volume paths is supported by Docker Compose, they don’t always behave reliably with bind mounts, especially when the host path involves mounted filesystems like NFS.

Even though `${DATA}` correctly pointed to `/mnt/data`

- Docker Compose resolved the variable
- Mounted the NFS share correctly
- But bind permissions didn’t behave as expected when the path came via an environment variable

It's unclear whether this is a quirk of Docker Compose, the NFS client, or how the filesystem is resolved — but the outcome is clear: using an env variable in the volume path led to silent permission issues, even though everything else appeared fine.

## The Fixes

### 1. Use a hardcoded absolute path for bind mounts

```YAML
volumes:
  - /mnt/data:/data
```

It’s simple, reliable, and eliminates variable resolution from the bind mount path.

### 2. Use a wrapper script if you really want to keep everything in `.env`

```Shell
#!/bin/bash
set -a
source .env
set +a
docker compose up -d
```

This ensures the variables are exported into the environment before Compose parses the `docker-compose.yml`.

## Final Thoughts

If your container can read but not write to an NFS-mounted volume using an environment variable, try hardcoding the path. It might just save you hours of debugging.