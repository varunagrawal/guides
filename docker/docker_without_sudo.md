## How To Run Docker Without Sudo

- Add the docker group if it doesn't already exist:

        sudo groupadd docker

- Add the connected user "${USER}" to the docker group. Change the user name to match your preferred user:
  
        sudo gpasswd -a ${USER} docker

- Restart the Docker daemon:

        sudo service docker restart

**Note: this command will stop any Docker containers currently running with this service**

- Either do a newgrp docker or log out/in to activate the changes to groups.