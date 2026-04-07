
2026-04-06 17:51

Tags: [[Homelab]]

# Reverse proxy
Setting up a reverse proxy is like having a receptionist which routes the guests to the correct ip using nice names instead of long IPs.

The Tool: Nginx Proxy Manager (NPM)

I highly recommend Nginx Proxy Manager. It has a clean web interface and makes this incredibly easy.
1. Add NPM to your Docker VM

Create a new folder and a compose file:
``` bash
mkdir -p ~/docker/npm
cd ~/docker/npm
nano docker-compose.yml
```
Paste this in:
``` bash
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    container_name: npm
    restart: unless-stopped
    ports:
      - '80:80'   # Public HTTP Port
      - '443:443' # Public HTTPS Port
      - '81:81'   # Admin Web Interface
    volumes:
      - /mnt/serviceVM_storage/npm/data:/data
      - /mnt/serviceVM_storage/npm/letsencrypt:/etc/letsencrypt
```
Run it with 
```
docker compose up -d.
```


# References
