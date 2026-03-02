---
title: "Why I stopped contributing to Modmail"
meta_title: "Why I stopped contributing to Modmail"
description: "There are just better alternatives"
date: 2026-03-02T05:00:00Z
image: "/images/project-mei/modmail.png"
categories: ["Updates"]
author: "Raiden"
tags: ["open source", "modmail", "discord bot"]
draft: false
---

## Preface

I know it's a little too late to publish this blog post and tell my story since I left the project many many moons ago, but if you're still interested anyway, here's an insignificant story and my reasons of why I stopped contributing to [modmail-dev/Modmail](https://github.com/modmail-dev/modmail).

As a side note, I was previously a support staff over on the official Discord for a couple of years. I contributed to the main bot repo, its documentation, made my own plugins for Modmail and maintained my own fork of Modmail until recently.

I do not intend to paint a bad light on a FOSS project, after all they work on their own time and willingness so please read this as an article from someone who just wants to tell a story.

## The Reasons

### FOSS in theory, Patreon upsell in disguise

The Modmail project includes a separate web app called [Logviewer](https://github.com/modmail-dev/logviewer) to expose your user's modmail tickets to the web for your staff to access. The transcript for individual ticket can be viewed on your browser through your own web server, and by default it's viewable under https://your_domain.com/logs/`log_id` URL, while your `log_id` is a string of a few randomly generated characters. 

Undoubtedly, by the nature of this app you'd have to expose this to the internet for your staff to access from anywhere, hence lies the problem: **The app does not have any authentication in place.** Anyone on the internet, with a little bit of guessing game or brute-forcing your `log_id` can view your user and staff's private discussions. But of course like any enshittified product these days, they do offer authentication via Discord OAuth in the premium version of the logviewer, requiring you to subscribe to their Patreon (or whatever site they're using now) for them to host it for you, __on their server__ that you have no control over. `logviewer-premium` used to be self-hostable by users, up until a while ago now that they [__actively discourage__](https://docs.modmail.dev/installation/local-hosting-vps/patreon_logviewer) you to do it in their docs, other than the fact that you'd have to request access to that private repository even after subscribing anyway. Security through obscurity should not be a practice on a project with this many users, and while you could argue the web app is purely optional and not important to the bot's functionality, well good luck trying to read back the transcripts from your old tickets when you have to one day.

Sorry, it's just a thing with me as somebody who grew up with open source software and somebody who's obligated to work on closed-source enterprise software for work. There needs to be a clear line between when you're making a product of the users and when you're a making a product out of your users.

![](/images/ew.png)

Yeah, I know that screenshot severely flashbanged you for a bit if you're a dark mode user, it was a thing that I suggested was a limitation of the crappy documentation site generator they're using called Gitbook. It shares quite a similar sad story with this project that it got enshittified and went the closed source, proprietary and freemium route, that you'd have to pay to even let users be able to switch themes freely. Bonus point for when I was writing the docs one time, and their commit hook failed miserably for days that none of my commits got reflected on their deployment server, that __I had to email them about it__ for them to notice and fix it. Surely the world must be running out of good open source documentation site generator. *cough*

Now, getting back on topic, noticing the issue there I decided to offer the OAuth feature on my fork of logviewer [as a plugin](https://github.com/raidensakura/modmail-plugins). It also comes with a bonus feature: A new paginated UI to browse all your logs, it's a product thanks to [a PR that never saw the light of day](https://github.com/modmail-dev/logviewer/pull/68) in the hope of getting merged. Despite the improvements, I remember being met with a discouraging remark from another staff when a community member asked about the plugin, in light that it could cause a performance issue. Oh lord, the fear of my teeny tiny Discord bot exploding from running a webserver. Which speaking of, transitions nicely to the next reason.

### General vibe of negativity and less productivity in the team

I did mention up there I was a support staff for a bit, right? For a while before I decided to quit, I noticed there's been less work getting done, an increase of smack talks and gossips about users in the staff chat, and just overall unwillingness to contribute to the OSS spirit. They have promised a rewrite of the bot for years now, understandably due to code debt and just the nature of old codes in general, but ultimately was never met with a deadline or any hope that it will ever be done. The original project founder, Kyber was found raiding servers and was "booted" from the team, and since then Taku has been the only active project maintainer and somebody with write access, while the others simply never show signs of account activity to even write a single letter on the repo. While I fully understand that nobody should be obligated to do anything in the world of open source software, it's not a reason to be negligent and not look for new maintainers when there's promising candidate in the team. There are thousands of users relying on that software handling data of upmost importance. Negligence is after all the primary reason the internet was only [a few commits away from disaster](https://www.youtube.com/watch?v=aoag03mSuXQ&t=597s&pp=ygUHeHogdnVsbg%3D%3D).

Now, I'm also not generally not the kind to nitpick about not being credited, after all most of the motivation to do all the work I've done is simply to learn and progress in my journey of software development. I have done quite a significant part in writing the documentation for self-hosting the bot over on their official docs, arduously testing all the different operating systems and environment Modmail should run on, on my own rented VPS and virtual machine. You can see my commits [here, in the contribution graph](https://github.com/modmail-dev/modmail-docs/graphs/contributors) or in the commit history of the repo.

Despite all this, seemingly they decided to not include me in the credits section in the organization, while still including all the previous ones before my participation, including the ones I have never even seen during my time there. Maybe it was all in my imagination, that those commits never happened and it was all just a dream that I left my mark on a repository of a public software that thousands of people use.
![](/images/credits.png)

### There are just better ticket bots out there

As it stand these days, Modmail is simply inferior compared to other modern ticket bots available out there. Discord has since included multiple helpful features for channel managements like thread and forum channels that at the time of writing, __Modmail does not yet support__ and will unlikely to ever do so. Modmail creates a regular channel per user ticket and with high volumes of open tickets it's easy for your channel list to be cluttered. Plus the fact that the channel is by default deleted after a ticket is closed further hinders searching and discoverability, along with the fact that you'd have to run a separate web app to conveniently view the closed tickets anyway. Just searching up discord ticket bot on GitHub will surely net you relevant results with modern bots that better support those features. Take a look at [this one](https://github.com/discord-tickets/bot) for example.

I personally run a [Red bot](https://discord.red/) with a ticketing cog created by the community. It has served me well and Red better suits me in terms of documentation, general community friendliness (and sometimes funny remarks), and more extensive customisability. While I've never really done any contribution to the Red codebase itself, I did make a few badly coded cogs for fun and feel more comfortable in being a part of its community. Come for the product, stay for the people, I guess.

## Them's the facts

Ultimately, leaving Modmail was not about abandoning the open-source spirit—it was about realizing that my time and energy could be better spent contributing to projects that align more with my values, and ones that offer a better user and developer experience. Open-source should empower both users and contributors, but it needs to be handled responsibly and with respect for the community’s needs.

If you're still using Modmail, or are considering it for your Discord server, I'd recommend looking into alternatives. The landscape of ticket bots has evolved, and there are now better solutions out there that offer the features and flexibility that Modmail struggles to keep up with. It's been an interesting journey, but like any project, it's a matter of time before other tools take the spotlight.

But of course, I did not regret contributing to or being a part of Modmail. After all, my core value from doing all this is still the same, and I learned a lot from it. Mostly how you should consider the project's values and culture before deciding to dip your toes into it or even digging deep down the rabbit hole down the road. Don't be afraid to speak up, share your thoughts, and above all, never stop learning. I always believe likeminded people will eventually end up with likeminded people so don't be afraid to speak up about something you disagree with or be afraid to leave a project behind if it stops aligning with what you value. The community you choose to be a part of should challenge you, support you, and help you grow.

Thank you for coming to my Ted Talk (nah, not really). If you read this far, I'm really jealous of you for having this much attention span, reading this bumbling nonsense from a goofball who does nerdy stuff on the internet and nothing else.

Raiden out. 🎤⬇️