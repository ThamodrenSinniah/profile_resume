---
date: '2026-02-18T16:50:16+08:00'
title: 'Hosting this Site'
tags: ["tech", "homelab", "dns", "duckdns"]
---
# Where am I hosting this?
<!--more-->

As you can already tell, I'm hosting this site on [Vercel](https://vercel.com). That wasn't the initial plan since I would've liked to host it under my own domain.

What I had in mind was using my free DuckDNS domain.

## Why Duck DNS
The main reason I use DuckDNS in the first place is because my ISP doesn't provide a static public IP. A fixed static IP would require upgrading to a business tier and cost RM200+ per IP. Yeah, I'm not doing that.
That's where Duck DNS comes in. 

Here is why DuckDNS solves my problem. 

>most connections to the internet are through a dynamic external IP address which changes quite often (weekly or even daily).
this can make it very difficult to connect to home services from an external computer. 

>to get around this, Duck DNS is a provider of what is known as a DDNS (Dynamic DNS) service
we provide a public DNS server that anyone can get a subdomain and use one of our provided scripts to update their record(s).
so instead of trying to remember an IP address, you can use a domain name that is kept up-to-date by a computer at home

>once this is done, periodically (usually every 5 minutes), the computer running the client tells our central system (via HTTPS POST) to update the record with its latest external IP

>it's up to you what you do with it. Usually the IP address points to your router—most people log in to their router and configure certain ports to be forwarded to other computers connected to the router

>if you had set up your domain to be exampledomain, then told your router to forward port 80 traffic to a server running a web server, then from anywhere around the world you could visit exampledomain.duckdns.org in a web browser

In short, a DuckDNS client runs on your machine, and it periodically updates the mapping between the DNS and its IP address. Perfect for my case.


## What's the Problem?
The issue is that I need to run my homeserver 24/7 for the DuckDNS client to send my public IP to their central system. Due to reasons I wish not to disclose, I can't run my homeserver 24/7, which would mean downtime on this site.

It would look pretty bad if a potential Google recruiter came across my site and found it down.

Why not spin up a VM like an EC2 instance? There are too many things to consider, in my opinion—configuring EC2, DNS zones, and security groups. Maybe I'm overthinking it and it's actually simpler than I think. 

## Solution
I settled with Vercel for now. It gets the job done and it's fairly straightforward. Plus, it has analytics, which is great.

## Future Plans
Maybe I follow through with one of these options
- Host it on AWS
- Buy a fixed IP


## A quick guide on DuckDNS

1. Go to [DuckDNS.org](https://www.duckdns.org/)
1. Sign in with GitHub
1. You are then provided a token you can find at the top.
1. Create a subdomain of your choosing. This subdomain is piggybacking off duckdns.org, so your site would have a link like the following: `http://my-site.duckdns.org`
1. Head over to your server and run a DuckDNS client on a container. Here is the [link](https://hub.docker.com/r/linuxserver/duckdns) to DockerHub. Remember to use the token you saw earlier as the value for the `TOKEN` environment variable.

If everything went correctly, you should have a DuckDNS client container running on your machine which will map your correct public IP to the DNS, even if the IP changes.

Do hit me up if my steps are unclear or outdated. Have fun!

