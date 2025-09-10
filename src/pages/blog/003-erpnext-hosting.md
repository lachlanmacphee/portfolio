---
layout: ../../layouts/BlogPostLayout.astro
date: "2025-09-10"
title: "ERP for Everyone 01: Hosting"
description: "Deploy your ERP on infrastructure that's under your control."
status: "published"
---

## Glossary

| Term    | Definition                                                                                                       | Example                                                                                                              |
| ------- | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Hosting | The process of deploying and maintaining software applications on servers that are accessible over the internet. | The apps you open on your phone often talk to servers running software. Those servers are **hosting** that software. |

## Options

When it comes to hosting software, you generally have three options:

1. **Self-Hosting**: You can host software on your own server or a virtual private server (VPS). This gives you full control over the environment and data, but requires some level of technical knowledge to set up and maintain.
2. **Cloud Hosting**: You can use cloud providers like AWS, Google Cloud, or DigitalOcean. This option offers scalability and reliability, but often incurs a much higher ongoing costs, and can leave you with a hefty bill if not setup correctly.
3. **Managed Hosting**: Providers like Frappe offer managed hosting services for their software, where they take care of the setup, maintenance, and updates for you. This is a good option if you want to avoid the technical aspects of hosting, but it can be expensive and may limit your control over the software.

## Recommended Approach

Given this blog series is all about empowering small businesses to take control of their ERP systems, I recommend going with the **Self-Hosting** option. I will provide you with everything you need to know to get your ERP up and running, with a great suite of shortcuts to help you along the way. Given most small businesses don't have the hardware or internet connection to deploy software on their own servers, I recommend a VPS. They are usually billed at a flat monthly rate (no suprises!), and you can choose a server that fits your budget and performance needs.

## VPS - Provider

To keep things simple, I will be setting up the VPS for this blog series on DigitalOcean. They offer a user-friendly experince and server locations all around the world. Feel free to choose another provider, just note that your setup steps might look quite different to what I show below. I've included some handy tips at the end of this post to help you choose a provider if you wish to shop around.

If you're happy to go ahead with DigitalOcean, the first step is creating an account. You can support my mission to help businesses transition to an ERP they can control by signing up with the referral button below. It will give me a small kickback at no extra cost to you, and I would greatly appreciate it!

<a href="https://www.digitalocean.com/?refcode=bb216368dae5&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge" target="_blank" rel="noopener noreferrer">
  <img src="https://web-platforms.sfo2.cdn.digitaloceanspaces.com/WWW/Badge%203.svg" alt="DigitalOcean Referral Badge">
</a>

Once you've created your account and logged in, <a href="https://cloud.digitalocean.com/droplets/new" target="_blank" rel="noopener noreferrer">click here</a> to go directly to the required page for the next step.

## VPS - Creation

Assuming you're on the page I linked in the last section, we can now create our VPS (or "Droplet" as DigitalOcean calls it). Please use the following selections (or better):

- **Region**: Choose one close to your business location (e.g. if you live in Australia you would choose "Sydney")
- **Datacenter**: Any (usually the first option is fine).
- **Image**: The default option should be fine. For me, this was Ubuntu 25.04 (LTS) x64. Any LTS Ubuntu would be a good choice.
- **Size - Droplet Type**: Basic is sufficient for the droplet type.
- **Size - CPU Option**: Regular with SSD is fine. Choose one with at least 2 vCPUs, 4GB RAM, and 50GB SSD.
- **Backups**: Optional, but recommended if you want to be able to restore your ERP to a previous state in case of issues.
- **Authentication**: Password is fine. It should be at least 50 characters long (the higher the better), and include a mix of uppercase, lowercase, numbers, and symbols. You can use a password manager like [Bitwarden](https://bitwarden.com/) to generate and store this password for you. If you are familiar with SSH keys, that is a more secure option.
- **Improved Metrics**: Optional, but can be useful for monitoring your server's performance. If it's free, I recommend enabling it.
- **Hostname**: Choose something relevant to your business, e.g. `mybusiness-erp`.

Once you've made these selections, click the "Create Droplet" button at the bottom of the page. It will take a few minutes for your droplet to be created. Once it's ready, you will see it listed on your DigitalOcean dashboard. Click on the icon that looks like a terminal. This will open a web-based terminal that you can use to interact with your VPS. You should see a prompt asking for your username. The default username for Ubuntu is `root`. Enter that and press Enter. Next, it will ask for your password. Enter the password you set during the droplet creation process (note that you won't see any characters appear as you type). Press Enter again.

## VPS - ERPNext

Now that you have access to your VPS, we can start setting up ERPNext. This is as simple as copy pasting all of the commands at once from the code block below into the terminal and then hitting enter.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

git clone https://github.com/frappe/frappe_docker
cd frappe_docker
docker compose -f pwd.yml up -d
```

This will take a while to run, as it needs to download and set up a lot of software. Once it's done, you should see a message saying "Creating site...". This means the ERP has been successfully installed on your VPS. You can now [move to the next step](https://lachlanmacphee.com/blog/003-erpnext-setup).

## Appendix (optional reading)

### VPS Provider Choices

If you want to compare VPS offerings, here are a few popular providers I've heard good things about as of September 2025:

- [DigitalOcean](https://www.digitalocean.com/)
- [Linode](https://www.linode.com/)
- [Vultr](https://www.vultr.com/)
- [Hetzner](https://www.hetzner.com/)
- [OVHcloud](https://www.ovhcloud.com/en-au/)
- [Binary Lane](https://www.binarylane.com.au/)

I recommend choosing a provider based on two factors:

1. Price: Look for a provider that offers a plan that fits your budget. Most providers have plans starting from as low as $5 USD per month that would be sufficient for a small business ERP.
2. Location: Choose a provider that has data centres close to your business location, as this will help with latency and performance.
