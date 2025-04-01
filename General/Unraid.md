Notify when container is down

```Shell
#!/bin/bashBlacklist=(vm_custom_icons
)Containers=$(docker ps -a --format "{{.Names}}")Checkin=true
for val in $Containers; doSkip=false
for check in ${Blacklist[@]}; doif [ $val == $check ]thenSkip=true
fidoneif [ $(docker container inspect -f '{{.State.Running}}' $val) == "false" ] && [ $Skip == "false" ]thendocker container start $valsleep 5
if [ $(docker container inspect -f '{{.State.Running}}' $val) == "false" ] && [ $Skip == "false" ]thenCheckin=false
/usr/local/emhttp/plugins/dynamix/scripts/notify -s Docker -d "$val service is down, restart failed"else/usr/local/emhttp/plugins/dynamix/scripts/notify -s Docker -d "$val service is down, restart succeeded"fifidoneif [ $Checkin == "true" ]thencurl https://hc-ping.com/9b2e3194-61cc-4df8-89bf-ba97ced8a5d8
fi
```