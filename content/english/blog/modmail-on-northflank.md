---
title: "Hosting Modmail on Northflank"
meta_title: "Hosting Modmail on Northflank"
description: "Hosting modmail-dev/Modmail on Northflank free tier PaaS"
date: 2025-05-07T04:17:00Z
image: "/images/2023-08-02/nf.png"
categories: ["Guides"]
author: "Raiden"
tags: ["modmail", "northflank", "discord bot"]
draft: false
---

Another alternative on a shrinking list of free-tier PaaS.

<!-- more -->

## What is Northflank?

[Northflank](https://northflank.com/) is a Platform as a Service (PaaS) like Railway or Heroku that offers abilities to run micro-services like bots, schedule jobs that run periodically and databases with a powerful UI, API and CLI. Their panel is a bit more advanced as compared to Railway but comes with the perk of more customization and features.

I decided to write this guide due to the ever-dying lists of Platform as a Service (PaaS) that <u>*actually* has a free tier</u>. Railway [ended theirs](https://blog.railway.app/p/introducing-trial-hobby-pro-plans) with a _sneakily written_ blog post that downplays the switch, joining the grave with Heroku.

### Is this *actually* free?

Yes, but for who knows how long. But if it isn't obvious already, you will need a valid payment method to verify your account, but will unlock a free tier project that's separated from paid resources. They will not charge your card if you go over resource usage as you have limited allocation per service.

![Image Example](/images/2023-08-02/nf-overview.png)
<sub>An overview of how Northflank panel looks like.</sub>

## Signing-up on Northflank

If you're a new Northflank user, you will need an account on Northflank (obviously). SSO is supported so you can also register with your GitHub or Google account if you prefer.

{{< button label="Sign up here" link="https://app.northflank.com/signup" style="solid" >}}<br>
<sub>No referral system sadge.</sub>

When it prompts you to create a new service, click on the **Free one**.

![Image Example](/images/2023-08-02/nf-acc-setup.png)

## Creating your Modmail service

After you've arrived at the main dashboard page, go ahead and create a new Service using the button top right of your screen.

![Image Example](/images/2023-08-02/nf-create-new.png)

Select "Deploy a Docker Image" as the service type. The "Service Name" can be whatever you want, but I usually just use "modmail" to keep things simple.

![Image Example](/images/2023-08-02/nf-service-type.png)

Select "External image" as the deployment source and use this as your "Image path":

```
ghcr.io/modmail-dev/modmail:master
```

![Image Example](/images/2023-08-02/nf-image-type.png)

Fill the environmental variables for your bot. They are covered in the [main docs](https://docs.modmail.dev/installation#preparing-your-environmental-variables) so read about them there if you don't know how to obtain them.

![Image Example](/images/2023-08-02/nf-env.png)

Make sure to bump up the resource allocation to 512MB of RAM so you won't strangle your bot if your server has a lot of members.

![Image Example](/images/2023-08-02/nf-resource.png)

Now you can create the service. If you don't have a payment method linked to your account, this is where they will prompt you because, duh... abuse reasons.

![Swipe dat card.](https://media.tenor.com/Zq7s-7MC9f0AAAAd/genshin-impact-genshin-meme.gif)

## That's it, really.

Now you can go ahead and flex to your friends about your very own Modmail bot for your server. 

![Image Example](/images/2023-08-02/bot-info.png)

If you wanna check the console logs, you can view them by the auto-generated container name in the tab shown below:

![Image Example](/images/2023-08-02/nf-logs.png)

## But what about logviewer?

I recommend using my logviewer plugin since it's significantly easier to set up. Find out how to install it [here](https://github.com/raidensakura/modmail-plugins).

After you have it installed, simply copy these settings in the network tab and restart your Modmail service for the changes to apply. You can also link a custom domain if you own one and know how to link it.

![Image Example](/images/2023-08-02/networking.png)