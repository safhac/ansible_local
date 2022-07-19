1. get nginx
---
    a. docker pull nginx:stable-alpine
    b. docker pull nginx

2. create a network
---
docker network create --subnet=172.20.0.0/16 customnetwork

3. add to local server /etc/hosts
---
172.20.0.10     yourmom.com

4. create and run the container
---
    a. docker run -d --rm -ti --net customnetwork --ip 172.20.0.10 --name nginx1 -p 80:80 -p 22:22 --add-host yourmom.com:172.20.0.10 nginx:stable-alpine

    b. docker run -d --rm -ti --net customnetwork --ip 172.20.0.10 --name nginx2 -p 80:80 -p 22:22 --add-host yourmom.com:172.20.0.10 nginx:latest

5. go into the nginx and add ssh
---
    a. docker exec -ti nginx1 sh
    b. docker exec -ti nginx2 bash

    a. apk add openssh bash curl openvpn ip6tables iptables openrc && rm -rf /var/cache/apk/* && rc-update add sshd && echo "tun" >> /etc/modules

    b. apt-get update && apt-get upgrade -y && apt-get install ssh nano 
    nano /etc/ssh/sshd_config
    set PermitRootLogin yes
    /etc/init.d/ssh restart
    service ssh status


6. commit the changes for future reference
---
    a. docker commit --author pronged_epoch -m "apk add & rc-update" nginx1 nginx/rc-update:ssh

    b. docker commit --author pronged_epoch -m "installed and root ssh login" nginx2 nginx:latest/ssh

    docker create --add-host yourmom.com:172.20.0.10 --ip 172.20.0.10 --name nginx2 --network customnetwork -p 80:80 -p 22:22 nginx:with_ssh_started 

    docker start nginx2


7. inspect the IP address 
---
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name

8. ping the IP
---
    ping -c 3 172.20.0.10

9. connect using ssh
---
    ssh root@172.20.0.10

    if the connection refused
    ssh: connect to host 172.20.0.10 port 22: Connection refused
    a. apk add -u awall