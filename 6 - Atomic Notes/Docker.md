
2026-03-21 09:41

Tags: [[Homelab]]

# Docker
Docker contains containers for your applications and you can think of it as an appstore where you keep all your programs running in seperate containers.

### Installation
Download and run the Docker installer
````
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
`````

Add your user to the Docker group (so you don't have to type 'sudo' for every command)
````
sudo usermod -aG docker $USER
````

#### Folder structure
Jellyseerr: - ./jellyseerr:/app/config

    Tailscale: - ./config/tailscale:/var/lib/tailscale

In both cases, everything to the left of the colon : is a folder on your actual Debian hard drive (the Host). Everything to the right is a folder that only exists inside the "virtual world" of the container.

# References
