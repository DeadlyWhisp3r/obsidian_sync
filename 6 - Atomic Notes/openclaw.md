
2026-04-02 02:03

Tags:

# openclaw
This is an introduction to openclaw aswell as the setup.

### Initial setup

Setting up a firewall so that only ssh and clawbot can do stuff on the internet
````
sudo ufw allow ssh
sudo ufw allow 18789/tcp
sudo ufw enable
````

This adds the OpenClaw folder to your profile so the command `openclaw` works forever:
```
echo 'export PATH="/home/deadlywhisp3r/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Install claude cli so that you do not have to use the pay as you go api
```
curl -fsSL https://claude.ai/install.sh | bash
```
then export the cli to the bashrc
```
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

After setting up and logging in to claude code on the VM then it is time to get back into clawbot
if the installation of clawbot was already started:
```
openclaw onboard
```
Otherwise run the easy download command:
```
curl -fsSL https://openclaw.ai/install.sh | bash
```

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
# References
