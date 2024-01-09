---
title: "Share Tracking and Analytic Profile Generation"
subtitle: "How companies like google track you outside of their platforms"
date: 2024-01-01T00:55:25Z
lastMod: 2024-01-01T00:55:25Z
author: ""
image: "NSEm9wj7Kyz.png"
imageAlt: ""
category: ""
tags: ["news","tech","privacy"]
draft: true
---

You may have noticed that some of your youtube links are a bit longer than you've seen before.

`https://youtu.be/dQw4w9WgXcQ?si=4xDc5_c39H5gZEqM`  

For example: here are some source ids i've collected from my friends discord server over the last month

## Youtube

{{< grid markdown="true" >}}
`?si=wJ0BawHIBjyA_2Oe`
`?si=3SbRGhjV336mhBcG`
`?si=tmKvmvaUOG2nh0D-`
`?si=Hc37xOJKkaHFKc2h`
`?si=H07IPxKs3ZS2vfPX`
`?si=ObkO56m7UbK75y98`
`?si=e0aYIKVJiLnYtNlA`
`?si=idwT1a5EiRJgK6ma`
`?si=nLJZO29DojLjgn0n`
`?si=O0DVwzNVkulrQULx`
`?si=blxECajnrvrERpnO`
`?si=rcgwx7jXnjuzHkPW`
`?si=jT0ifUb4tGOS_vyH`
`?si=fdfuTHhtauL_RBnJ`
`?si=jA5AH66plTBVvZdX`
`?si=gQ2NdY5F2TRF9Nbo`
`?si=z2ruBKeFCs9th7gw`
`?si=UNpKQgnmnu9AKAgv`
`?si=3UovfPJKVzh3UFzs`
`?si=eFKSrdFZbaAhUXCd`
`?si=rg_W6yyzsGJGxyyL`
`?si=49Kt2QyMcBuW7ftj`
`?si=aXozv3XzODmM-ZyS`
`?si=LzpH7Jeu1om7CDy-`
`?si=hYGjXduqP7quWyJE`
`?si=DiAO3F3914wlIQ38`
`?si=i8aIiTnmhAPVQXT8`
`?si=ZYq_N5nbldbdZmkd`
`?si=DS3xL4hDigN65oYe`
`?si=cl0FZ4AUb6ZWFivT`
`?si=QsqG8n-1WuPbpuHK`
`?si=1OZR2N8c--MLQxBY`
`?si=9KlyUcoGBtUH5C2a`
`?si=BI-UQhH57hRMg6DA`
`?si=igMAZaiILoTr7zG9`
`?si=7U9Cwuqne6pf8wVz`
`?si=S4jP0qGOsasSHsuT`
`?si=r7RHKF3meHd-V5Vo`
`?si=pBtXQWWKf1YjfEdk`
`?si=4RVxcLwGvBotlXUa`
`?si=n2HJrbJORZJ33KUp`
`?si=70UYsF4SVMCJcCBE`
`?si=C24nEVDUYhVBOMH0`
`?si=dZ0TZQZC3y2KIdtJ`
`?si=l4kbxfHkgz2UJ4yH`
`?si=ihIx6TkrIKJgT8E2`
`?si=Djt95c4IBOh6PMG_`
`?si=m55PRygwQEJzyNoD`
`?si=86iTHzp0EdFNWVv0`
`?si=nLJZO29DojLjgn0n`
`?si=Hgu9YRksul5tVLYE`
`?si=e1Cfv2w2axGgTXbK`
`?si=4uI5vX3mijDW2lO0`
`?si=7FJFRfH_LyklrKML`
`?si=O0DVwzNVkulrQULx`
{{< /grid >}}

## Spotify
{{< grid markdown="true" >}}
`?si=d84e4e601b184040`
{{< /grid >}}

Youtube's codes appear to be base64 encoding without padding. Just like their video ids.
But unlike their video ids of 11 characters long, these are 16 characters long.

64 to the power of 16 is `7,92282 × 10^28` or `79 octillion` possible codes!
That's a bit overkill unless you mean to track every video share for the forseeable future.

Spotify seems to have gone a less drastic route with hexadecimal. Still 16 characters long, _interestingly enough_.

16 ^ 16 is `1,84467 × 10^19` or `18 quintillion`. Plenty enough for all your tracking needs. (particularly if you recycle 'em)



not necessary  
only on share links  
?? only on shortened links (not)  
started in august  
