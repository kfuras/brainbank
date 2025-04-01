In my homelab setup, I'm running **Jackett in a Docker container**. The web UI doesn’t offer an obvious way to refresh the API key, so here’s how to regenerate it manually:

### Steps

1. **SSH into your Docker server**:

```bash
ssh docker-01
```

2. **Locate Jackett’s configuration folder**  
For me, it's located at:
  
```bash
docker/media-stack/appdata/jackett/
```

3. **Open the config file**:

```bash
vi ServerConfig.json
```

4. **Delete the line containing the API key**  
Find and remove the line that starts with:

```bash
"APIKey":
```

5. **Save and exit** `vi`

6. **Restart the Jackett container**:

```bash
docker restart jackett
# or
docker compose restart jackett
```

**Done!**  

Next time Jackett starts, it will automatically generate a new API key and write it back to `ServerConfig.json`.

### Tip

After regenerating the key, update it in any connected services like:

- Sonarr, Radarr, etc.