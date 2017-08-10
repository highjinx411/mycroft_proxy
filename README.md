# Mycroft SSL Proxy
This is a nginx reverse proxy to allow to securely talk to mycroft instances over wss.

# Installation
1. Setup a docker instance and then clone the repo:
`git clone https://github.com/Geeked-Out-Solutions/mycroft_proxy.git`

2. Run the following commands to generate the self signed certs for your instances, example: mycroft1.domain.com, mycroft2.domain.com, etc
CD into the SSL dir first from the clone so that we can insert them into the container:
`cd /mycroft_proxy/proxy/ssl`
Then run the commands to generate the self signed certs:
`openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mycroft1.key -out mycroft1.crt`
`openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout mycroft2.key -out mycroft2.crt`

3. Now we are going to follow the information from the Let's Encrypt Certbot guide [https://certbot.eff.org/#ubuntuxenial-nginx] to setup our reverse proxy container with Let's Encrypt cert's:
So if done right up until now you should be able to cd into the mycroft_proxy/proxy folder and build and run the image:
`cd mycroft_proxy/proxy`
`docker-compose build` - wait for the build to finish
`docker-compose up -d` - now if you run docker ps you should see the proxy up.
`docker exec -it proxy_proxy_1 /bin/bash` - this will take us to a bash prompt on the container

Now we are going to install a few items needed on the container to get the let's encrypt part setup:

`apt-get update`

`apt-get install gpg software-properties-common -y`

`add-apt-repository ppa:certbot/certbot`

`apt-get update`

`apt-get install python-certbot-nginx -y`

`certbot --nginx`

Now we will get some menus on which domains we want to create certs for and your email address, etc.  Fill out these answers and when done you will have a secured SSL setup.
