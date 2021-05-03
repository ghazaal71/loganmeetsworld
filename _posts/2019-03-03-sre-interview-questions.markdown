---
layout: post
title: "Questions I ask in SRE interviews"
date: 2019-03-03
tags: careers, interviewing
---
<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD026 -->
<!-- markdownlint-disable MD002 -->

![](https://thepracticaldev.s3.amazonaws.com/i/rvidqn8y735n9ebtxye3.jpg)

I was recently asked by a friend who has been interviewing for SRE jobs for good questions to ask at the end of the interview. In writing the email back to them I realize I had lots of ideas and it might be worth it to share a short post for them, my future self and anyone else who is interested.

These are the questions I make sure to ask when interviewing for positions on infrastructure or site reliability teams. Depending on the structure of your interviews, these may be appropriate for the recruiter, but are most likely questions for the hiring manager or other members of the team. Most of this centers around where the team is at with their tooling and how happy developers are. I'm also trying to get at the relationship between the operations engineering team and the rest of the team and org.

## SRE related questions

* What is the tech stack?
  * I'm looking at the question from an operations perspective. Are they using a hodgepodge of languages or is the development flow opinionated? How many different technologies does the team have to support?
* What is the infrastructure stack?
  * Depending on what they say, we'll be talking about this for a while and will probably create a lot of other questions.
* What does your metrics & monitoring setup look like? How do you debug issues with the system?
* This may be a controversial one, but if the title is "SRE" I ask why the title is "SRE" and not something else (same for "DevOps"). I'm looking to see if they're being thoughtful about what the term means and how they are defining "resilience" for their systems.
* Walk me through the experience a developer has on-boarding to your development environment. How long do you think it takes?
* Walk me through the experience a developer has deploying with your pipeline. What would you say are the biggest pain points?
  * How would you rate test coverage and do you continue to measure that? What about test coverage is important to the team?
  * Do you have blue-green deployments? Do you have canaries?
  * How do engineers share their work with product teammates in the QA phase? How many environments do you have?
  * These questions are incredibly important to me. It could both surface fun red flags for you to discuss with your interviewer and see how receptive they are to your opinions and give you an idea of things you might be working on for them.
* How would you describe the relationship between the operations team, IT, and the rest of the engineering team?
* How do you handle app security? How do you encourage developers to think about the security of their services?
* Do you have to be GDPR compliant? Did that process go smoothly for you?
* What's your on-call set up look like?
  * How many times a month are you on-call?
  * When you are on-call, how many times during that period are you getting paged?
  * Would you say when you get paged, alerts are actionable?
  * Are developers on-call for their services?
  * How do you on-board people to on-call?
  * How much time is spent on the team in "reactive" rather than "proactive" mode?
* Are most things in the infrastructure stack self-service? Like, what's the process of setting up a new service with data stores?
* Which level of [Dickerson's hierarchy of site reliability](https://landing.google.com/sre/sre-book/chapters/part3/) do you think needs the most work in your stack?
* Overall, how would you rate developer productivity?
* Do you have any open source projects? If not, are you interested in open sourcing anything?

### Standard interview questions

* Does your engineering team have a values statement? What's in it?
* What do you do to foster an environment of learning?
* What does success in this role look like? What sorts of projects or accomplishments could you see being completed 3 months, 6 months, and 1 year out?
* Is the working environment collaborative during work or do people mostly keep to themselves? How so? Is the office open? (I would also ask during on-sites that they show you where you'd be sitting. If you're sensitive to lots of noise while working this could be very important.)
* How much of the team is distributed? What is your "work from home" or "work from X" policy? Is it flexible or set?
* What is the thing you are most excited about working on or launching in the next year?
* What do you like best about working here?

I want to point out there are some things I didn't ask here and that doesn't mean that I don't value them. For example, I never ask directly about diversity on the team. I hope that's something that I see around the office and in my interviews. When I go to lunch with one of the developers, I'll ask questions that indirectly get to those issues. I don't really need the PR line about diversity.

What are your questions you always make sure to ask in either general tech or SRE interviews? Let me know!

Image used from [unsplash](https://unsplash.com/photos/u3o7il8s1Fc)