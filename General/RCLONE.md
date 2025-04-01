Copy and Sync folder to Remote destination on Jottacloud

```Shell
rclone copy -P /mnt/user/data/media/movies/ jottacloud:/movies
rclone sync -P /mnt/user/data/media/movies/ jottacloud:/movies
```