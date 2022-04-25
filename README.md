# Forta-Run-Node-Guide
- Prepare VPS (I use Ubuntu  and run as root)
- Install docker >= v20.10: https://docs.docker.com/engine/install/centos/ and https://docs.docker.com/engine/install/linux-postinstall/
- Add file /etc/docker/daemon.json: check content at https://docs.forta.network/en/latest/scanner-quickstart
- Restart docker: systemctl restart docker
- Install Forta via YUM:
    sudo curl https://dist.forta.network/repositories/yum/Forta.repo -o /etc/yum.repos.d/Forta.repo -s
    sudo yum install forta
- Initialize Forta using the forta init command:  forta init --passphrase INPUT_YOUR_PASSWORD then backup the "Scanner address" to somewhere
- Configure systemd if need:
   vi /etc/systemd/system/forta.service.d/env.conf with below content:
        [Service]
        Environment="FORTA_DIR=/root/.forta"
        Environment="FORTA_PASSPHRASE=INPUT_YOUR_PASSWORD"
- Go to alchemy, register and create app: https://alchemy.com/?s=DY3OTc5MTE4OTY4N, select Polygon network when create app and get jsonRpc to input in config/yaml file.
- Configure config.yml: (I run with polygon network)
vi /root/.forta/config.yml with below content
        chainId: 137
        scan:
          jsonRpc:
            url: https://polygon-mainnet.g.alchemy.com/v2/XXXXXXXXYYYYYYYYZZZZ
        trace:
          enabled: false
- Send 1 $Matic to your scan node address: Run $forta account address to get scan node address, send some $Matic to this address.
- Register Scan Node: 
forta register --owner-address <your_address_that_you_own_the_key>
your_address_that_you_own_the_key is different with the Scan Node Address, maybe metamask address.

- Go to email from Forta, submit the form and wait for team. 

- You can go to https://explorer.forta.network/network to check your node status
