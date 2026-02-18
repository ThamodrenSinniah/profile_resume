---
date: '2026-02-18T16:50:16+08:00'
title: 'Hosting this Site'
tags: ["tech", "homelab", "dns", "duckdns"]
---
# Where am I hosting this?
<!--more-->

As you could already tell, I'm hosting this app on [Vercel](https://vercel.com). Was not the initial plan since I would like to host it under my own domain.

What I had in mind is using my free DuckDNS domain.

## Why Duck DNS
Main reason why I have DuckDNS in the first place is because my ISP does not provide a static public IP. For fixed static IP, it would require you to upgrade to a business tier and also cost you RM200+ for 1 fixed IP. Nah I am not doing that.
Thats where duck DNS comes in. 

Here is why DuckDNS solves my problem. 

>most connections to the internet are through a dynamic external IP address which changes quite often (weekly or even daily).
this can make it very difficult to connect to home services from an external computer. 

>to get around this, Duck DNS is a provider of what is known as a DDNS (Dynamic DNS) service
we provide a public DNS server that anyone can get a subdomain and use one of our provided scripts to update their record(s).
so instead of trying to remember an IP address, you can use a domain name that is kept up-to-date by a computer at home

>once this is done, periodically (usually every 5 minutes), the computer running the client, tells our central system (via a HTTPS post), to update the record with its latest external IP

>it's up to you what you do with it, usually the IP address is for your router, most people login to their router and configure certain ports to be forwarded to other computers running that are connected to the router

>if you had setup your domain to be exampledomain, then told your router to forward the port 80 traffic to a server plugged into it running a webserver, then from anywhere around the world you could hit exampledomain.duckdns.org in a web browser

In short, a DuckDNS client runs on your machine, and it periodically updates the mapping between the DNS and its IP address. Perfect for my case.


## What is the Problem?
Problem is, I need to run my homeserver 24/7 in order for the DuckDNS client to send my public IP to this central system. Due to reasons I wish not to disclose, I cannot have my homeserver run 24/7. So this would mean there would be downtime on this site.

Would look pretty bad if a possible Google headhunter comes across my site and see that its down.

Why not spool up a VM like an EC2 instance? Too many things to consider in my opinion. EC2, configure DNS zone, setup security groups. Maybe I'm a noob and its is actually easier than I'm thinking. 

## Solution
Settled with Vercel for now. Gets the job done and its fairly straight forward. It has analytics too so thats great.

## Future Plans
Maybe I follow through with one of these options
- Host it on AWS
- Buy a fixed IP


## A quick guide on DuckDNS

1. Go to [DuckDNS.org](https://www.duckdns.org/)
1. Sign in with GitHub
1. You are then provided a token you can find at the top.
1. Create a subdomain of your choosing. This subdomain is piggy backing of of duckdns.org so your site would a link like the following - `http://my-site.duckdns.org`
1. Head over your server and run a DuckDNS client on a container. Here is the [link](https://hub.docker.com/r/linuxserver/duckdns) to DockerHub. Remember to use the token you saw earlier as the value for the `TOKEN` environment variable.

If everything went correctly, you should have a DuckDNS client container running on your machine which will map your correct public IP to the DNS, even if the IP changes.

Do hit me up of my steps were unclear or if it is outdated. Have fun!

