+++
title = 'Nextcloud'
date = 2026-04-04T08:04:49-05:00
authors = ["Aaron"]
banner = "img/Nextcloud.png"
draft = false
+++

# Self-hosted Nextcloud

## Why?

I simply wanted a private data storage solution where I could store a lot of data. At the time, I distro-hopped a lot and thus wanted a place I could easily sync all my data to. In fact, even though I don't distro hop nearly as much as I used to, all the files I consider “unreplaceable” are stored in my Nextcloud instance.

Though I still sync my data to my laptop, so if something happens to my server, I still have the files at the very least.

## Setup

### Hardware

It runs on a Raspberry Pi 5 (previously it used to run on an old laptop) that is connected to a USB hard drive. The host OS as well as Nextcloud data all live inside the USB hard drive. It isn't optimal, and I did consider upgrading it to an SSD recently, but at this point I am waiting for SSD prices to go down.

### Operating System

Unfortunately, I got the device when it was still new, and Raspbian, the Debian-based OS that is “recommended” for these devices, had the best support when I was installing the OS. Normally I wouldn't mind a Debian-based OS, but it seems this OS comes with the unfortunate issue that Raspberry Pi as a team does not recommend upgrading between major Debian versions. This means, for now, the server is locked behind Debian 11. It is still supported for quite a while, but I was eagerly waiting for some of the new improvements to the podman quadlet setup that comes with Debian 12. Not to mention, in general, I like newer software and the improvements they bring.

### Nextcloud Deployment

As a fan of containers, I opted to go for a containerized deployment for this. In hindsight, this was quite smart of me since I do expect to move this deployment to a new SSD and a new OS at some point. Had I installed everything on the host OS or used a snap installation for simplicity, that would have made the process much more annoying.

The deployment uses Podman with systemd services to manage these containers; all I had to do was create a podman run command and run the initial container using that. Afterward, I used a podman tool to export the container configuration as a systemd service file that I can use to manage this container. In a way, this systemd service acts as a Docker Compose, but with much better system integration. Since I can just use systemd to manage the deployment instead of having an extra Docker daemon to do it for me.  This is especially convenient since I can see the logs of the container as a systemd service logs in the cockpit web portal I use in conjunction with good old SSH to manage the system.

I was eagerly waiting for the new improvements to this setup that Podman and systemd would bring in Debian 12. Here I wouldn't even need a systemd service, and I could instead manage everything through a declarative config file that is simpler to read and understand than a systemd service. Here is a [Red Hat article](https://www.redhat.com/en/blog/quadlet-podman) briefly explaining how podman quadlets work (I use the older version of doing this where I manage the .service file instead of the .container file, which generates ephemeral services).

### Networking

The Raspberry Pi moves somewhat often and has to be able to move between my home and my college dorm room.  As such, it required a networking solution that would allow me to keep my instance running and be accessible to the public internet regardless of its networking conditions. I briefly considered Cloudflare Funnel to do this, but I wasn’t a fan of the fact that Cloudflare could read potential data. It is not a company I trust personally. Instead I chose to use Tailscale. It is a mesh VPN, which allows WireGuard connections between devices and does DNS magic that allows devices to talk to each other through human-readable DNS names instead of IP addresses. We can also connect these same DNS names to the public internet through something called Tailscale funnel, which exposes a single port on a device to the public internet with SSL. In fact, the SSL certificate allows for actual end-to-end encryption even when devices connect from the internet. Additionally, the fact that only a single port is exposed to the internet vastly increases the security of this system while still letting me access other ports from within the mesh VPN network. Of course, there are severe network performance issues since Tailscale allows all of this for free, but I can accept that since this performance penalty only applies when connecting to it from the public internet. The connection speed is much better between devices actually connected in the mesh VPN system (which all my devices are). 