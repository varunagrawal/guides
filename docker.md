# Docker

## How To Run Docker Without Sudo

- Add the docker group if it doesn't already exist:

        sudo groupadd docker

- Add the connected user "$USER" to the docker group::

      	sudo usermod -aG docker $USER

 An alternate command is:
 
        sudo gpasswd -a ${USER} docker

- Restart the Docker daemon:

        sudo service docker restart

**Note: this command will stop any Docker containers currently running with this service**

- Either do a newgrp docker or log out/in to activate the changes to groups.

## Docker Full Restart

sudo pkill docker
sudo iptables -t nat -F
sudo ifconfig docker0 down
sudo brctl delbr docker0
sudo service docker restart
