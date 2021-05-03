---
layout: post
title: "Slack dorking for the win!"
date: 2021-05-03
tags: observability
---
<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD026 -->
<!-- markdownlint-disable MD002 -->

A while back I was on the [Dev Discuss podcast](https://devpods.herokuapp.com/podcasts/devdiscuss/episodes/28) to talk about being an SRE. At some point I made a comment about a pet peeve of mine: When folks post screenshots of some error they are seeing to Slack. I wanted to take some time to expand on that and talk a little bit about how I use Slack to explain why.

Slack is one of the most powerful logging systems I use. When investigating an error or incident, I'm probably using [Slack search](https://slack.com/help/articles/202528808-Search-in-Slack) as a first move. Often I'll find the error we're seeing in the backlog of our chats and it often leads to valuable clues — "oh something similar happens every thrid Monday of the month???" When I find past mentions of the bug or error we're currently seeing, I have a load of context to give me even more clues. Who worked on this last time? What was the content of the conversation? Even if I can't figure out what's happening from the previous chat, maybe I can contact the people involved previously.

Slack search is hugely helpful even if there isn't something I'm actively trying to debug. There are search modifiers Slack provides that can help us find information more easily. For example, say I'm looking for any documentation our team has on our Fastly SSO because I need to add a new user, and I know that historically my teammate Steven has owned our integration with Fastly. Before pinging him, I can search `from:@steven fastly login` in Slack. I've now saved myself and Steven some time!

Other modifiers, aka "dorks", I've found useful:

* Searching DMs for a message someone sent me but I don't remember who: `to:logan that thing`
* Narrow your search to a channel or DM using `in:` — probably my most common dork.
* Use `before:`, `after:`, `on:`, or `during:` to do time based searches. For example, if you remember an incident from March but don't recall what: `during:March in:opsalerts feature flags outage`
* Use `has:` to retrieve messages that have a specific emoji reaction. This is especially helpful if you also have any automation that adds emoji reactions to particular messages. For example we tag deploy messages with `:rocket:` so I could search: `has:rocket in:infra on:5/1/2021 rig_controller_api` to find anything that deployed mentioning that service on May 1st.

Like many organizations, my work has embraced a lot of ChatOps for organizing teams, incidents, and work in general. We send all of our alerts to Slack, work on RFCs, and keep a ton of our context there. With all that in mind, do you understand why screenshotting (i.e. destroying) context frustrates me 😬 ? I've actually gotten in the habit of describing what is in the screenshot in a threaded comment response when I see them, so at least now it is tagged with searchable content.

I hope this post inspires you to help an operations engineer out and copy and paste your errors, or at least add as much context as possible when posting screenshots. You are doing your team and your future self a huge favor.
