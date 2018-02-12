---
layout: post
title: "Day in the Life of an Ops Engineer"
date: 2018-01-20T17:45:00-04:00
tags: industry
---
# Day in the Life of an Ops Engineer

I'm always excited to introduce people to the operations engineering field so I decided to write this blog post envisioning what a day in my professional life is like. You'll often hear operations engineers referred to as Site Reliability Engineers (SRE) or Ops or DevOps. In this post, I will give an overview of some of the concepts I work with every day. In order to cover these topics, I'll center this post around a story. This story is constructed as a timeline of a day working as an ops engineer. This is based off my experience at Kickstarter. Though not all these things happened in exactly this order on one day, all of these events did happen. Throughout the story I'll be discussing real events that an operations engineer might be tasked to handle.. I will use each of these events to introduce us to different concepts in the very broad field of ops engineering.

As ops engineers, we solve tough problems and set the path forward for our engineering organization. I hope that someone could use this post as a way to test if they are interested in going into site reliability.

## 9:15AM - Is the site down? (Concept: Metrics and Monitoring)

Our day begins with a message from my coworker Nick. He got in a little earlier this morning and saw that there was some code sitting on our master branch in Github and decided to deploy it. After his deploy he gets an automated message from one of our Slack chatbots to go check our metrics system to make sure his deploy went ok. This is a normal message after every deploy and Nick, being the great developer he is, goes to check Grafana, where our metrics dashboards live. On our dashboards indicating responses from the site he notices something's off. We're spiking a bit in 404 responses and it started a short while after his deploy. When I get into the office I have a message from Nick explaining the situation and asking if I can look into why this might be happening.

I'll talk about what monitoring a site means and about the system we set up to track the health of site. I'll talk about how I used these tools I built (the metrics pipeline) to solve Nick's problem.

## 10:00AM - Working on a Project (Concept: Build and Release Engineering)

Things have settled down with Nick's problem, so I turn my attention to my main project for this sprint. Lately, we've noticed that our CI (continuous integration) system is getting super slow. From the time a developer merges their changes, it takes 20 minutes for them to deploy! It only took 10 minutes a month ago.

I'll talk about what continuous integration, delivery, and deployment are, the differences between them, and why they are important to the health of an engineering team. We'll take a look at a particular system, Circle CI, and talk a little about it's features and how I went about solving this puzzle.

## 12:30PM - Developer Happiness

It's lunch time! And I notice that a couple of frontend and fullstack engineers are getting lunch in the kitchen so I join them. I start talking about my project to improve the build times and they're really excited. However, one speaks up. She says that what bothers her is not as much about the build times being so slow, but that they've noticed a lot of spurious failures lately, meaning even when the 20 minutes of tests stop running, sometimes the build is red for no reason and you have to go back and build again. This means that builds take 40 minutes! And sometimes more!

"Developer Happiness" is a key part of an ops engineers job. Your customers are the other engineers on your team. It's key that you take user input and listen to them. We thought the main problem with our CI was how slow it was, but it seems that getting of these spurious failures may be more important. I'll talk about the importance of user experience from the SRE perspective and why communication in ops engineering is so important. Making sure that people trust me is an incredibly important part of my job. I want people to feel like they can tell me things about our processes and tools that bother them, alert me when issues arise, and trust me enough to let me help them fix it.

## 1:30PM - Security Engineering Meeting (Management skills)

After lunch, I have a meeting we call the "Security Roundup". We meet every other week. Because we have such a small team, we don't have a full time security engineer. In order to make sure we don't miss out on security issues with Kickstarter, we have this meeting of interested parties discussing any security issues that may come up. This week our CTO is in the meeting. We've been informed that a controversial project is launching in the near future and are being asked what we would recommend to do to prepare as operations engineers and fraud specialists.

The meeting is a dialogue that results in a list of action items. It's important in this meeting that these action items get completed, but they require many different teams coming together and some of the people who will need to work on the list are not in the room. I'm tasked with seeing the list is completed. Even though I'm not a manager, often because of my position in the organization and admin access, as an ops engineer I am tasked with management. I'll talk about the manager skills it takes to be an ops engineer.

## 2:46PM - Chaos (Incident Response)

After the security meeting, I work on my CI project. Suddenly, my coworker Corey runs up to my desk a little panicked and says "payments RDS replica is about to crash, production is next". I'll explain what RDS is and why this is making Corey so worried. I hop in our "incidents" Slack room and alert the channel about what's going on and take the role of "Incident Commander". Then I ping my coworker Natacha and ask her to be the second in command for the incident. Together we hop on a call to remediate.

I'll take us through looking at the AWS console, discovering the problem, and modifying some instances to fix it. We discover that the original problem was a large migration that the payments team is running on the database that is causing it to run out of storage and for the memory to spike into swap (we'll explain what these things mean). We add more storage to the database and watch the systems cool down.

This story is to explain the role of incident response and the ops engineers job in promoting resilient systems. I will explain how after every outage like this we conduct "blameless postmortems" to ensure accountability and make our processes better in the future.

## 4:45PM - Unable to Work (Local and Deployed Dev Environments)

After taking a break after the outage to clear my head, I return to a message from my coworker Julie. She needs to finish a project today but can't get her deployed developer environment to load. She's seeing an error that Short read or OOM loading DB. Unrecoverable error, aborting now. in her Redis logs. She needs to be able to see how her code is working in this environment so she can open a Pull Request by the end of the day. Can we help?

We'll talk about how ops engineers manage and build developer environments to support other engineers and how as an ops engineer you'll spend a lot of your time troubleshooting what you built.
It's the end of the day! We made it. But wait...

## 3:21AM - On Call Selfies

We're not done yet! This week we're on call, which means if something happens with the site we are responsible for fixing it, no matter the time. At 3:21AM we get a "page" from PagerDuty about a problem with Elasticsearch refilling its indexes. Luckily for us, the team is forward thinking and we've seen this problem before. We look at our Runbookand find the exact line of code we need to run to solve the problem.

We make sure everything is ok, snap a quick "on call selfie" and head back to bed. I'll explain how "on call" systems work, what it takes to make on equitable, and how we maintain global software that operates on different time zones.

## Concluding Thoughts

Finally, I want to conclude with some thoughts about what it means to be an ops engineer and why it's so great.
* It may be scary from the outside, because it seems like ops engineers know so much about computers. But really, the most important skills are communication and keeping calm under pressure.
* It's fun! You get to cover a wide range of topics and interact with lots of other types of engineers on the team.
* Although it seems like the computer science issues that come up are "expert level" learning about ops is actually a really good introduction to a lot of these topics because there are tangible examples of realistic issues like "running out of memory" or "efficient algorithm design" that you see everyday.
* Even if you don't want to be an ops engineer, understanding some of these topics and the constraints on your code when it gets put on servers at scale is important because things will break and you can learn how to fix them!

## Resources

### General

* [Effective DevOps by Katherine Daniels and Jennifer Davis](http://shop.oreilly.com/product/0636920039846.do)
* ["Web Developer Road Map 2017: DevOps Map"](https://github.com/kamranahmedse/developer-roadmap/blob/master/project-files/devops-map.json)
* ["WTF is Operations? #Serverless"](https://charity.wtf/2016/05/31/wtf-is-operations-serverless/)

### Metrics and Monitoring

* ["Practical Applications of the Dickerson Pyramid" by Nat Welch](https://www.youtube.com/watch?v=xWAfTAu0Mww)
* ["Google SRE Book Chapter 3 "Practices"](https://landing.google.com/sre/book/chapters/part3.html)
* ["Too Big To Fail: Lessons Learnt from Google and HealthCare.gov" by Daniel Bryant](https://www.infoq.com/news/2015/06/too-big-to-fail)

### Continuous Integration

* [Continuous integration vs. continuous delivery vs. continuous deployment](https://www.atlassian.com/continuous-delivery/ci-vs-ci-vs-cd)
* [Orchestrating Circle CI Workflows](https://circleci.com/docs/2.0/workflows/)
* [Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation by Jez Humble and David Farley](https://books.google.com/books/about/Continuous_Delivery.html?id=6ADDuzere-YC)
* [The Practice and Future of Release Engineering](https://drive.google.com/file/d/0B_Jl94nModqdSFVseUotQVB1Rnc/view)

### Incident Response

* [Resillience Engineering in Practice](https://www.crcpress.com/Resilience-Engineering-in-Practice-A-Guidebook/Paries-Wreathall-Hollnagel/p/book/9781472420749)
* [A talk by J. Paul Reed on Incident Response](https://vimeo.com/221060764)

### Postmortem processes

* ["Blameless Postmortems and a Just Culture" by John Allspaw](https://codeascraft.com/2012/05/22/blameless-postmortems/)

### Developer Environments

* ["The value of reliable developer tooling" by Aaron Suggs](https://kickstarter.engineering/the-value-of-reliable-developer-tooling-e94791d1482e)

### On Call

* [On Call Selfie](https://www.pagerduty.com/blog/oncallselfie/)
* [A talk about On Call by Alice Goldfruss](https://vimeo.com/221050366)