---
title: "Lemmy Selfhost Install"
subtitle: "My experience and problems ran into starting up my own instance"
date: 2023-11-29T23:42:46Z
lastMod: 2023-11-29T23:42:46Z
author: ""
image: ""
category: "dev"
tags: ["how-to","tutorial","lemmy","docker","web"]
draft: true
---
ansible with docker / arm64 raspi mods to make it work
- had to manually install a few things on first time setup
- docker cant connect without /etc/resolv.conf having external name servers (8.8.8.8, 8.8.4.4) before local adresses
- /etc/resolv.conf keeps being reset
- /etc/nginx/sites-enabled/DEFAULT removed
- on ansible lemmy.yml docker images for lemmy need to be set to arm images (masquernya/lemmy, masquernya/lemmy-ui)
- on ansible templates/docker-compose.yml needs "platform: linux/arm64" in almost every service. "platform: linux/arm64/v8" for lemmy/lemmy-ui




{WEBSITENAME}_proxy_1  
{WEBSITENAME}_lemmy-ui_1  
{WEBSITENAME}_lemmy_1  
{WEBSITENAME}_postgres_1  
{WEBSITENAME}_pictrs_1  
{WEBSITENAME}_postfix_1  


`docker save {WEBSITENAME}_proxy_1 | gzip | ssh lemmy@192.168.1.17 'gunzip | docker load'`  


issues installing:  
python docker "This environment is externally managed"
- `sudo rm /usr/lib/python3.x/EXTERNALLY-MANAGED`

letsencrypt "Some challenges have failed"
- port forward `80 (http) & 443 (https)`



pnr = probably not required  

## migration

docker volume transfer  
[<https://github.com/ricardobranco777/docker-volumes.sh/>]

- stop containers on doner server

pnr - commit containers to repos  
pnr - `docker commit $CONTAINER $CONTAINER` for each  
pnr - save repos and send to host server to load  
pnr - `docker save $CONTAINER | ssh $USER@$HOST docker load`  

- save volumes for each docker service  
`docker-volumes.sh $CONTAINER save $CONTAINER-volumes.tar`  

- copy volumes to host  
`scp $CONTAINER-volumes.tar $USER@$HOST:` (that leading colon is important)  

on host:  
run ansible install compleatly  
stop all docker services  
load volumes, but only volumes that are not empty
- {WEBSITENAME}_pictrs_1-volumes.tar  
- {WEBSITENAME}_postfix_1-volumes.tar  
- {WEBSITENAME}_postgres_1-volumes.tar  

`docker-volumes.sh $CONTAINER load $CONTAINER-volumes.tar`  
start all docker services  

## email dns records

dmarc record:  
`v=DMARC1; p=quarantine; pct=25; rua=mailto:dmarcreports@{WEBSITENAME}; ruf=mailto:dmarcfailurereports@{WEBSITENAME}; aspf=s;`  

spf record:  
`v=spf1 ip4:192.168.0.1 a:{WEBSITENAME}`  