---
title: "Lemmy Selfhost Install"
subtitle: "My experience and problems ran into starting up my own instance"
date: 2023-11-29T23:42:46Z
lastMod: 2023-11-29T23:42:46Z
author: ""
image: ""
category: "dev"
tags: ["how-to","tutorial","lemmy","docker","web"]
toc: true
draft: false
---
## Notice ~~!
this page is very far from where i want it rn  
these are the notes i made when i first learned to install lemmy on docker using ansible  
i plan to redo this page when i have time. but for now i hope this helps if you ran into some of the same problems i did

at the time of writing lemmy does not compile and host their own image for arm. so you will need to use someone elses.
i found masquernya on docker was compiling and hosting an arm version of lemmy and lemmy-ui so i used that.

ansible with docker / arm64 raspi mods to make it work
- had to manually install a few things on first time setup
- docker cant connect without `/etc/resolv.conf` having external name servers (`8.8.8.8`, `8.8.4.4`) before local adresses
- `/etc/resolv.conf` keeps being reset
- `/etc/nginx/sites-enabled/DEFAULT` removed
- on ansible lemmy.yml docker images for lemmy need to be set to arm images (`masquernya/lemmy`, `masquernya/lemmy-ui`)
- on ansible `templates/docker-compose.yml` needs `"platform: linux/arm64"` in almost every service. `"platform: linux/arm64/v8"` for lemmy/lemmy-ui

trying to pull images from the repo to docker kept saying it could not resolve.
this is because on my version of debian the dns resolver by default was only looking on my intranet.
adding cloudflare's or googles dns to my /etc/resolv.conf before my local address fixed that issue.
but a more permanent solution is to set that external dns resolver to the list of used dns inside of, in this case, NetworkManager.
no im not going to tell you how to do that... look it up

### Docker containers

```text
{WEBSITENAME}_proxy_1  
{WEBSITENAME}_lemmy-ui_1  
{WEBSITENAME}_lemmy_1  
{WEBSITENAME}_postgres_1  
{WEBSITENAME}_pictrs_1  
{WEBSITENAME}_postfix_1  
```

transfer images to target and load
`docker save {WEBSITENAME}_proxy_1 | gzip | ssh lemmy@{SERVERIP} 'gunzip | docker load'`  


issues installing:  
- python docker "This environment is externally managed"  
FIX: remove Externally Managed folder `sudo rm /usr/lib/python3.x/EXTERNALLY-MANAGED`

- letsencrypt "Some challenges have failed"  
FIX: port forward `80 (http) & 443 (https)`


## Migration

ok so you are transfering both the container images plus their respective volumes

docker volume transfer script  
[<https://github.com/ricardobranco777/docker-volumes.sh/>]

not every volume needs to be migrated  
i cant remember which ones. i hope to fill this tutorial out later when i have time to test install again

- stop containers on donor server

`pnr` = probably not required  
- commit containers to repos `pnr`  
- `docker commit $CONTAINER $CONTAINER` for each `pnr`  
- save repos and send to host server to load `pnr`  
- `docker save $CONTAINER | ssh $USER@$HOST docker load` `pnr`  

- save volumes for each docker service  
`docker-volumes.sh $CONTAINER save $CONTAINER-volumes.tar`  

- copy volumes to host  
`scp $CONTAINER-volumes.tar $USER@$HOST:` (that leading colon is important)  

on host:  
run ansible install compleatly  
stop all docker services  
load volumes, but only volumes that are not empty
```text
{WEBSITENAME}_pictrs_1-volumes.tar  
{WEBSITENAME}_postfix_1-volumes.tar  
{WEBSITENAME}_postgres_1-volumes.tar  
```

`docker-volumes.sh $CONTAINER load $CONTAINER-volumes.tar`  
start all docker services  

## Email DNS records

this is not a complete list of email records required for full auth  
but this is what started allowed email to start working for me

dmarc record:  
`v=DMARC1; p=quarantine; pct=25; rua=mailto:dmarcreports@{WEBSITENAME}; ruf=mailto:dmarcfailurereports@{WEBSITENAME}; aspf=s;`  

spf record:  
`v=spf1 ip4:192.168.0.1 a:{WEBSITENAME}`  