---
title: "How to Set Up Ollama"
subtitle: "Run a chatbot on your own hardware"
date: 2024-02-25T23:53:49-06:00
lastMod: 2024-02-25T23:53:49-06:00
author: ""
image: ""
imageAlt: ""
category: "dev"
tags: ["how-to","tutorial","llm"]
toc: false
draft: false
---

Project homepage: <https://ollama.ai/>  
Project github: <https://github.com/jmorganca/ollama>  

## Man this projects moving fast!

The technology is **not** ready *but it's here!* (・ω<)
Ironically, thanks to the efforts of meta and their llamma2 model being opened; *you too can have the **power of gods**.*
No but seriously having the models and loader open-sourced allows for projects like ollama to exist.
And ollama is quite a project. At the time of writing on github we've seen 49 updates in a few months.
More than 140+ contributors working on it right now. With updates coming two a week on average.

### Features (as of writing)
- 68 compatible models
- full api
- plugins
	- cli
	- web
	- db
	- editors
	- desktop and mobile
- library support (like langchain)
- built in gpu accel

## Alright let's get into it

### Install
There are two install options
- Binary
- Docker image

#### Docker image

There is an official docker image on docker hub as `ollama/ollama`

#### Binary

The README has links to the binary and instructions for setting up a service but it's literally just running `ollama serve`  

---

Either way you are going to be starting in the cli with `ollama run <model>`  

Running a model for the first time will also run the pull command before anything else `ollama pull <model>`
which will download the model for use later.
These models are *Very* large so you may be forced to delete some as you shop around for something that fits your needs.
`ollama rm <model>`

After that, models can be initialized with a prompt. Which can help tune the output to fit your needs.

Personally the only setup I have constantly running is a mistral model hosted on a computer at home to that I can use it from my phone anytime I want.

I plan to make another post when I am using ollama as a part of a project.