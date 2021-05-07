---
layout: post
title: "What happens when: bureaucracy edition"
date: 2019-05-06
tags: infrastructure, governance
---
<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD026 -->
<!-- markdownlint-disable MD002 -->

The familiar "what happens when" we go to a URL in the address bar of a browser walkthrough, but in terms of who controls all the things that make that process possible.

> "Collectively, these are the primary virtual identifiers that keep the Internet operational. The requirement that each identifier be globally unique has necessitated centralized administration. The global struggle over who controls and possesses these resources has been along-standing issue of Internet governance." - Laura DeNardis, The Global War for Internet Governance

This post is inspired by a series of recent decisions by private companies to take action to terminate the accounts of sites known to spread hate speech. Following mass shootings in Dayton, Ohio and El Paso, Texas, [Cloudflare][cloudflare] decided to terminate an account held by the website 8chan. There has been widespread pressure for years on the company to end their relationship with 8chan, but they've been reluctant to do so. Per their blog post:

> Cloudflare is not a government. While we've been successful as a company, that does not give us the political legitimacy to make determinations on what content is good and bad. Nor should it. Questions around content are real societal issues that need politically legitimate solutions. We will continue to engage with lawmakers around the world as they set the boundaries of what is acceptable in their countries through due process of law. And we will comply with those boundaries when and where they are set.

Cloudflare's insistence is that the regulatory power surrounding these hate sites sits with the government and not a private company, but the truth is private companies have controlled large swaths of internet governance since the beginning of the internet.

Similarly, after realizing they were hosting an investment page for the social media network Gab, a site frequented by white supremacists, Amazon's cloud service shutdown the server connected with the subdomain invest.gab.com.

So why is this such a big deal? The internet is a large, decentralized, and distributed system with many different points of control. Most people don't understand everything that goes into a single request to one website. Furthermore, even if they have prepared for technical interviews and they do understand that, they probably don't know about each of the individual protocols and organizations that govern the process.

In light of these events and subsequent cries of "free speech!" regarding these account shutdowns, I wanted to resurrect a blog post idea I've been thinking about for a while.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Would love a /what-happens-when ~*~bureaucracy edition~*~ 😂<br><br>&quot;here are all the organizations that exist to govern the infrastructure you are using to search for something on the internet&quot;</p>&mdash; Logan McDonald (@_loganmcdonald) <a href="https://twitter.com/_loganmcdonald/status/1156663790546640896?ref_src=twsrc%5Etfw">July 31, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Finally, before we get started, I want to note that this post was largely inspired by a book I'm reading: [The Global War for Internet Governance by Laura DeNardis][denardis]. The book covers a lot of what's in the post in greater detail and I highly encourage you to check it out.

We're going to walk through how most people access websites today and examine at each turn what organizations might control those processes. I'm going to purposefully ignore certain parts of the process in favor of brevity, and if you think of others that are important, let me know in the comments!

## The Browser

Let's start with a user coming to the browser.

When you type a url into the browser, the browser first needs to read the url. It will take the protocol (`https` in the case of `https://buzzfeednews.com`) and the domain (`buzzfeednews.com`) and convert any non-ASCII characters into punycode. If you're interested in learning more about punycode, checkout this post I wrote on [homograph attacks][homograph].

The Browsers have control over several things in this process, mainly the user interface for interacting with a given website. You may have seen the `Insecure` label on sites not using `https` for example. They also have the power to show all urls in their pure-ASCII form by forcing addresses to translate to punycode in the url bar (Chrome does this, Firefox does not). At this point, Mozilla, Apple, Google, and any other company running a browser has moderate control over your experience in accessing a website, by "nudging" you to do things that they deem "secure".

## DNS

Then your Browser performs a DNS lookup. It'll make a call in your operating system to get the hostname locally. If it cannot find it on your operating system, it will try resolving the hostname through DNS. DNS is the domain name system. Its primary function is to translate the human-readable addresses we see in our browsers to binary addresses that routers use to locate servers belonging to those addresses.

## HTTP

## CDN

Let's take a look at what happens when you curl for BuzzFeedNews:

```bash

```

## The Host

## All the random shit you need to run a website in 2019

In this day and age, most sites are run using "cloud computing", which means that you need a way to get your code to the cloud. This presents the opportunity for many other points of possible disruption for a site.

In Gab's case, they were using Heroku to deploy their application, but the servers that Heroku uses are actually owned by Amazon. So at that point either Heroku could have terminated their account

Part of what's so hard to understand when examining how the technical design of the internet impacts socio-politics is that there are so many areas of study involved. It's hard to find scholars who are engineers, legal experts, and sociologists. It requires a technical and social understanding. That said, there's an entire field dedicated to understanding these issues called STS or science and technology studies. There are also many lawyers and programmers who cross over both fields. I'll list some research that I've found reading about this below.

What's important to understand is that every technical point of control creates a political choice. ICANN, registrars, CDNs, hosting sites, all choose to enforce certain conduct by either action or inaction. And while there are laws that govern some of these control points and commit to _legal_ choices, because of the decentralized nature of control, the private intermediary's choice is a moral one.

## Resources

* [Alex Gaynor's /what-happens-when](whw)

[cloudflare]: https://blog.cloudflare.com/terminating-service-for-8chan/
[ipo]: https://news.crunchbase.com/news/cloudflare-said-to-pursue-september-ipo-we-say-heck-yes/
[denardis]: https://yalebooks.yale.edu/book/9780300181357/global-war-internet-governance
[whw]: https://github.com/alex/what-happens-when
[homograph]: https://dev.to/logan/homographs-attack--5a1p
[denardisbook]: https://yalebooks.yale.edu/book/9780300181357/global-war-internet-governance
[denardisdns]: https://onlinelibrary.wiley.com/doi/full/10.1002/poi3.195
