Login docker

```Plain
docker exec -it homeassistant /bin/bash
```

Home Assistand Components location

```Plain
/usr/local/lib/python3.10/site-packages/
```

Verisure Component faster sync timer Set Scan Interval, SCAN_INTERVAL  
can be set in config  
`verisure/__init__.py` Source: [Verisure  
lock status - Configuration - Home Assistant Community  
(home-assistant.io)  
](https://community.home-assistant.io/t/verisure-lock-status/22431/36)

```Plain
MIN_SCAN_INTERVAL
```