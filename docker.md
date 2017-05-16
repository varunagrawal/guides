# Docker

## Deleting Images and Containers

### All Untagged Images

```shell
docker rmi -f $(docker images -a | grep "^<none>" | awk '{print $3}')
```

### All Stopped Containers

```shell
docker rm $(docker ps -a -q)
```

## How To Run Docker Without Sudo

1. Add the docker group if it doesn't already exist:

        sudo groupadd docker

2. Add the connected user "$USER" to the docker group:

        sudo usermod -aG docker $USER

3. If the above doesn't work, an alternate command is:
 
        sudo gpasswd -a ${USER} docker

4. Restart the Docker daemon:

        sudo service docker restart

**Note: the above command will stop any Docker containers currently running with this service**


5. Log out and log in again to activate the changes to groups.

6. You should be be able to access `docker` without `sudo`.

        docker system info


## Docker Full Restart

```
sudo pkill docker
sudo iptables -t nat -F
sudo ifconfig docker0 down
sudo brctl delbr docker0
sudo service docker restart
```