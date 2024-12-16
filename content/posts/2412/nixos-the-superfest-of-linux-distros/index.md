---
title: "Nixos the Superfest of Linux Distros"
subtitle: ""
date: 2024-12-15T13:27:30-06:00
author: ""
image: ""
imageAlt: ""
category: "update"
tags: ["linux", "nixos", "nix", "rant", "update", "dev-update"]
toc: false
draft: false
---
The configs got me. im a nixos believer.

Wouldn't be nice if you could save all that progress customizing your desktop. Reload everything at a later time when you want to change something about your pc? but not rely on a vm managed virtual desktop to keep your states (because honestly that sounds aweful). no fuckin way im managing that. and god knows if ill be able to get hardware passthrough to work with high success.

I've always dreamed of having some "deploy.sh" that could save a lot of the hassle of setting up a fresh install. It couldn't be large to keep the amount of things that could break to a minimum.

Anyways... I was lamenting about this to a friend over discord and they pointed out that **nixos** exists.
What the fuck is nixos? I asked.

Because at this point im nervous that its some bs i dont really want like deployments targeting servers, or a hacky way to get repeatability in a corporate setting. but no! this is proper.

NixOS is a flavor of gnu/linux built around the nix package manager.

And the nix package manager (which ill be calling just nix from now on) was built on this idea that a package or program shouldn't break because you have the wrong version/type of a dependency.

Now we've all been in dependency hell before and it's never fun figuring out a custom solution to have 4 different versions of the java vm on your system at once and make it make sense to the path variables.

Nix can and will keep a list of multiple versions of software that you are using or have used recently.
Then when you boot the machine you will load a profile that will pull in the list of depencencies for that profile.
Things like, application settings, applications, depencencies for a whole manner of things.
The point is that **EVERYTHING** is a *seperate* module.

So our *'deployments'* look like a config file with a list of applications, application settings, system settings, et al.; *Declared*, telling nix what we need to be happy. and it will figure out the rest. (or rather comunity members have done that work already)

Im still learning but so far im very happy with NixOS. it solved the desktop repeatability problem i had.

Now for the less than savory stuff.
A few gripes that i have is that first: not every package is available in nix packages. ive had to compromise on a few applications that i had on my last machine. Actually, now that i think about it the only thing left that i dont have is private internet access vpn. there's a comunity flake availble but rn private internet access are being bitches not supporting any openvpn certificate methods from the last decade.

And the other gripe is that when updating you can break packages pretty bad. Now this can never brick your system because previous profile states are just as legitimate. It really feels as though you have to babysit all upgrades to make sure they dont break something or have some nasty package interaction. BUUUUUT once you have a stable system its quite literally unbreakable.

Thats why i call NixOS the superfest of linux distros. [Superfest](https://en.wikipedia.org/wiki/Superfest) was this "unbreakable" (break resistant) chemically strengthened glass invented in the 1980s in socialist east germany. No one makes the glass anymore because they had no one else to sell to. Anyways, NixOS is hard to make but once made it's as unbreakable as they come.

And its good enough for me right now

if you want to check on the progess of my personal nixos config click here [nixos-config](https://codeberg.org/signet-marigold/nixos-config)

See you in the next one!!
