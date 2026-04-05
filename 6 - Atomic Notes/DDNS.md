
2026-02-01 19:47

Status:

Tags: #Networking #Proxmox

# References
dynamic data network system

En DNS mappar domän namn till ip addresser och vanligtvis så har man en dynamisk IP address hemma. 

Ifall man är utanför hemmet och vill ta sig in ens nätverk måste man memorera IP-addressen samt lösenordet men IPn ändras ibland så det blir krångligt. Därav vill man ha en DDNS.

T.ex myhomepc.ddns.org så finns det en databas som kopplar om till DDNS.

### Setup
To setup a DDNS I used dynu ddns. Create an account and register a free domain then link that in the router settings found under WAN>DDNS.

### Ad-Blockers
Using for example Adguard your can filter out DNS requests to your server and using these different filters you can drop any requests asscoiated with ads or spyware that has been setup in the rules (the filters).

A helper script to create a Proxmox LXC with adguard running on it. Lightweight and quick.
````
bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/ct/adguard.sh)"
````
now neovim is working yayyy.