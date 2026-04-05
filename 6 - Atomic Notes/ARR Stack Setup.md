
2026-03-20 23:15

Tags: [[Proxmox]]

# ARR Stack Setup
To setup the ARR stack we need radarr, lidarr, sonarr, prowlarr, 
https://trash-guides.info/File-and-Folder-Structure/How-to-set-up/Docker/
## Jellyfin setup
We are using a docker-compose.yml file to construct the constainer. The initial file structure can be found on the official jellyfin webpage: 
https://jellyfin.org/docs/general/installation/container/

We will then change user id and group id. See the ids by id -u or id -g.

````
# sudo docker compose down
sudo docker compose up -d
# This will download and setup the container
# -d means detached mode which is the same as running &
`````

### Qbittorrent + Gluetum
Hook up qbittorrent to the vpn handler Gluetum so all traffic gets routerd through the VPN.

Command to print what ip the qbittorrent is using and then check if that is the gluetun vpn address.

````
docker exec -it qbittorrent curl ifconfig.me
`````

### Setting up all the ARRs
To allow writes on the disks by the docker containers you need to change the permissions.
````
sudo chown -R 1000:1000 /mnt/media_vault/media
sudo chmod -R 775 /mnt/media_vault/media
````
# References
