# nginx

Install Nginx for your system. This step varies depending on your Linux distro (Windows users be damned).

For Ubuntu this is super easy: `sudo apt-get install nginx`

For more information:

https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04

For AWS EC2, this is a great resource:

https://www.nginx.com/blog/setting-up-nginx/

TIL: You need to add rules to the instance's security group to allow HTTP and HTTPS.

## SSL with Let's Encrypt


#### AWS

Unfortunately, AWS is blacklisted by Let's Encrypt. Head over to `dot.tk` to get a free domain name for you to use as a proxy.