---
layout: post
title: "Automating delivery of patent application alerts to Slack"
date: 2019-03-04
tags: legal, programming
---
<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD026 -->
<!-- markdownlint-disable MD002 -->

Recently, I've become obsessed with United States patent applications. Specifically, I'm interested in patent applications from large tech companies. I started reading about patents when I came across some patent applications from Microsoft in an article about facial recognition software. I found the dry and legalistic nature of the patent language fascinating, given the implications of the subject matter. So I googled "how do I find out what patent applications are released" and I found a glorious piece of software: The USPTO's [Patent Application Alert Service](https://www.uspatentappalerts.com/). Now, every week, I sit down with a cup of coffee and read through patent applications.

In this post we'll cover why I do this, what this USPTO service does, what patent databases are available to the public, and what I've done to make the release of patent applications more accessible for my team.

## What are patent applications and why are they important?

### Newsworthiness of patent applications

When patent applications are released to the public, they often result in news stories. Here are just a handful I found while researching this:

1. ["Apple patent hints at AR headset that'll work with your iPhone"](https://www.cnet.com/news/apple-patent-hints-at-ar-headset-thatll-work-with-your-iphone/)
2. ["An Apple patent filing reveals what a foldable iPhone might look like"](https://www.businessinsider.com/apple-patent-filing-reveals-possible-design-for-foldable-iphone-2019-2)
3. ["Amazon Filed A Patent Application For Tech That Could Link You To Your Identity And Job"](https://www.buzzfeednews.com/article/daveyalba/amazon-filed-facial-recognition-patent-application)
4. ["Facebook is eying ridesharing"](https://money.cnn.com/2016/01/28/technology/facebook-ridesharing/index.html)
5. ["Uber wants to patent a way to use AI to identify drunk passengers"](https://money.cnn.com/2018/06/07/technology/uber-patent-identify-drunks/index.html)
6. ["Palantir’s New Patents Shed Rare Light On Its Data Methods"](https://www.cbinsights.com/research/palantir-patents-data-mining/)
7. ["Google, Amazon Patent Filings Reveal Digital Home Assistant Privacy Problems"](https://www.consumerwatchdog.org/sites/default/files/2017-12/Digital%20Assistants%20and%20Privacy.pdf)

As you can see, patent applications contain useful information for the public and reveal what companies consider to be innovation worth protecting.

### Importance of patent application alerts

To persuade you that patent application _alerts_ are important, I need to talk a little bit about how patent applications work. When a company like Facebook or an individual person believes they have invented a novel "process" or "machine," among other things, they can apply for a patent to prevent another entity from making, using, or selling their invention without their consent. In order to obtain a patent, companies are forced to make a tradeoff. While they stand to make money by protecting their idea, they also have to disclose that idea to the public when they apply for a patent.

By law, patent applications must be made public within 18 months of being filed. However, there are few exceptions. First, there is something called a "provisional" patent application. A provisional patent application allows an applicant to establish an early filing date, but the USPTO does not make it public or determine whether to grant a patent unless the applicant files a regular non-provisional patent application within one year. If the applicant doesn't file a non-provisional patent, the provisional application is never made public.

There are two rarer examples of non-published applications and issued patents. First, there are those filed under foreign patent protection. Second, the USPTO may determine that an invention has implications for national security. Those examples aside, in general, after a US patent application is filed, it will be published by USPTO for the public to view (regardless of whether it has been granted yet).

### USPTO databases

So, you may be thinking that means the Patent Application Alert Service (PAAS) spits out an alert for _every_ non-foreign, non-provisional, and non-national-security related patent application before a patent is granted, but this isn't exactly true. Applications that come through the application database will result in alerts to PAAS. However, in some cases, a patent may be approved before the 18 month publication deadline.

There are two major public databases for doing full-text searches for information related to patents: AppFT and PatFT, which contain information for patent _applications_ and patents that were approved.

There are thus _applications_ that are published and indexed in AppFT that will eventually be granted, and those that may never be granted. However, all _patents_ are published and indexed into PatFT (except the ones with national security implications). Thus, those applications published prior to grant and then eventually granted live in both databases.

Now you have enough background to evaluate what alerts coming through the _application_ alert service mean:

1. It doesn't mean that the application is granted (and it may never be granted)
2. You're missing those patents whose applications were not published prior to being granted, and thus only exist in PatFT
3. You're missing provisional patents, some foreign related patents, and those patents that have national security implications

However, dealing directly with AppFT still gives us a lot to work with. With that in mind, let's discuss the alert service.

### The Patent Application Alert Service (PAAS)

PAAS is the system that provides customized email alerts when a patent application is published. It was created to allow the public to monitor the _latest_ patent application releases. You can use the service to add alerts for a variety of search terms.

While these alerts definitely make it easier for reporters to report on companies' patent applications, the central reason for a patent alert system is to spur innovation. USPTO thinks that if people have easy access to patent-related information, they will file higher quality patent applications and pursue novel inventions. This is because patent filings require you to prove your patent is novel using "prior art". "Prior art" is _anything_ that can be used as evidence your invention is already known. USPTO thinks that if it can help you find "prior art" that shows your invention isn't novel, you won't apply for a patent. The more visible patent applications are, the more discoverable the "prior art".

I signed up to start getting these alerts a couple months ago when I found out about PAAS. I included the top 10 tech companies in the US as well as some ones that were recommended to me like Palantir or Clear, just to see what they were like. This is the interface for adding a new company to your alerts:

![Adding an Alert](https://i.imgur.com/Q3qhohA.png)

I get the best luck with just searching for terms and selecting "Applicant". All the other categories will give you too much noise.

I love reading the patent applications. To me, they seem like an unfiltered look into what these companies were working on in the language the engineers would use to describe it. Interestingly, there seems to be a disconnect between the engineering teams building these products and the PR teams who BuzzFeed reporters usually hear from. For example, while Amazon PR downplays the extent to which their facial recognition technology could be used by law enforcement, the language in their patents revels in those possibilities. This is because the incentives of the IP lawyers and the PR departments are misaligned. The lawyers' and engineers' goal is to get the patent approved, not to write the patent in such a way that hides a technology's dystopian features.

If you are thinking of working at a large company, read their patent applications. It'll give you a great look into their work.

## A patent application Slackbot

I almost immediately started annoying my Twitter followers with patent-related tweets once I started getting these alerts.

<div class="center">
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">EYE TRACKING USING TIME MULTIPLEXING: &quot;system implements time-multiplexing by configuring a source assembly comprising a plurality of light sources to project at least a first light pattern towards the user&#39;s eye over a first time period&quot;<br><br>again very cool but very creepy <a href="https://t.co/4a40xToGe6">pic.twitter.com/4a40xToGe6</a></p>&mdash; Logan McDonald (@_loganmcdonald) <a href="https://twitter.com/_loganmcdonald/status/1093504704280252418?ref_src=twsrc%5Etfw">February 7, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

<div class="center">

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Are they building Hunger Games???<br><br>&quot;The module may [...] analyze the metrics data to generate game inputs based on the participants&#39; physical metrics, and provide the game inputs to the game system to affect game play&quot; <a href="https://t.co/BIBQkPWwOL">pic.twitter.com/BIBQkPWwOL</a></p>&mdash; Logan McDonald (@_loganmcdonald) <a href="https://twitter.com/_loganmcdonald/status/1096041820230991873?ref_src=twsrc%5Etfw">February 14, 2019</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

 You may notice that the tweets above and the stories I linked earlier are all on Thursdays. PAAS releases all new patent applications to the public [on Thursdays](http://appft.uspto.gov/netahtml/PTO/help/status.html) around 7am EST. Each Thursday, I get a new round of alerts from the companies to which I subscribe. This is what the looks like:

![Imgur](https://i.imgur.com/ro2cQ9r.png)

I wasn't super happy with the formatting of the email. I'd have to go through and click on every link, and go out to its individual page to read about it. So I had a thought: What if I could turn this email into data that I could display the abstracts and titles only? What would that look like? My  goal was to make PAAS more accessible for people in a hurry to discover the most interesting applications right away.

I looked to see if anyone had built something that accomplished this goal on Github, but could not find anything. Furthermore, while an API exists for searching the actual patent database, none exists for querying recently updated applications. Lastly, I recognize that patents are a big business. Proprietary software to parse new applications probably exists, but I don't have access to it.

So I set out to make a new Slackbot. My general design of the Slackbot relies on incoming webhooks to Slack channels, sending the data to these webhooks when we receive the email from USPTO.

### SES and SNS

The first question is how we get the data from emails to our Slack webhooks/channels.

I already have a DNS entry setup through Route53 so I thought it'd be fun to try out AWS's [Simple Email Service (SES)](https://aws.amazon.com/ses/) to make an email for that entry that I could use to forward USPTO emails to. You have to set up [email receiving](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/receiving-email-setting-up.html) by defining "rulesets" for emails within your account. I set it up to receive UTF8 emails to a `patents@mydomain.com` email.

Then, I hooked up that SES ruleset to a [Simple Notification Service (SNS)](https://aws.amazon.com/sns/) action, which forwarded the emails to an SNS subscription called `patents`.

Then I went and signed up for PAAS using that email, and received the email on the AWS side through SNS and used the link they provided to confirm my email. Great! Now we had `SES -> SNS` and then we just needed to hook SNS up to our Slackbot. So there are a couple ways we could go at this point. We can either use `https` to forward the data to an endpoint as a `POST` _or_ we could setup a lambda function that gets the forwarded data and forwards it to Slack. I decided to setup an endpoint because I didn't want to setup deploying the lambda but either would work.

### Slack applications

Slack has great documentation on [setting up incoming webhooks](https://get.Slack.help/hc/en-us/articles/115005265063-Incoming-WebHooks-for-Slack). I created a Slackbot called "PatentsBot" and gave it permissions to post to channels through certain webhooks.

I decided  to set up a different channel per company I wanted to follow so I have something like:

```txt
#patents-uber
#patents-amazon
#patents-facebook
...
```

and expect my code to parse and understand where it should send any new applications that arrive for those companies and get them to the right channels.

Now we just needed to receive it, parse it, and forward it to our existing webhooks.

### Parsing emails

Before this project, I didn't have experience with receiving and parsing emails with code so I was able to learn a lot about email encoding and the various options available for email parsing in python.

If we look back at the email above, we can see that we are given a list of ids which are hyperlinks. The links don't make a ton of sense (i.e. aren't formatted with consistent routing):

```txt
http://appft.uspto.gov/netacgi/nph-Parser?Sect1=PTO1&Sect2=HITOFF&d=PG01&p=1&u=%2Fnetahtml%2FPTO%2Fsrchnum.html&r=1&f=G&l=50&s1=%2220190065445%22.PGNR.&OS=DN/20190065445&RS=DN/20190065445
```

... great, right? However, if you click through the link you'll find a nicely formatted HTML document that looks like this:

![Patent application](https://i.imgur.com/XSS7SE5.png)

This was enough information, formatted in ~~tolerable~~ parsable XML. I decided to pull all the hyperlinks from the email, load their associated HTML, parse out the abstract, filing date, and company name, and then forward that data as a single Slack message, rather than trying to parse out meaningful information from the email alone.

This is the code, a `build_slack_msgs` method, that does the parsing to build messages we'll send on to Slack. This is receiving json objects from SNS, forwarded by SES, finding all the links that being with the AppFT URL signage, `http://appft.uspto.gov.`, requesting data from each link, parsing that data, and returning some metadata.

```python
message = data['Message']
json_file_parsed = json.loads(message)['content']
parsed_email = email.parser.Parser().parsestr(json_file_parsed)
links = []

# Let's pull out all those nasty links and collect them
for part in parsed_email.get_payload():
    links += re.findall(r'\<(http://appft.uspto.gov.*)\>',quopri.decodestring(str(part)).decode('utf8'))

message_data = []

# Then we parse the information we can obtain from those links
for link in links:
    html = urllib.request.urlopen(link).read().decode()
    html_tree = lxml.html.fromstring(html)
    title = ' '.join(html_tree.xpath('/html/body/font')[0].text_content().strip().split())
    # regarding the following line... I'm sorry, but it works
    applicant = html_tree.xpath('/html/body/table[3]/table/tr/td/table/tr[2]/td')[0].text_content().strip()
    date = ' '.join(html_tree.xpath('/html/body/table[3]/table/tr')[3].text_content().split())
    abstract = ' '.join(html_tree.xpath('/html/body/p[2]')[0].text_content().split())
    slack_webhook = find_slack_webhook(applicant) # method to retrieve our Slack channel from secrets
    if slack_webhook:
        message_data.append(
            {
                'applicant': applicant,
                'title': title,
                'link': link,
                'date': date,
                'slack_webhook': slack_webhook,
                'abstract': abstract
            }
        )
```

There are a couple more special packages I want to point out I'm using to parse the emails from PAAS.

The first is `email`'s [`parser`](https://docs.python.org/3/library/email.parser.html). This package provides a standard parser that understands email document structures, including MIME documents. `parsestr` takes a string object and then reads the data from the object given.

The next package is [`quopri`](https://docs.python.org/2/library/quopri.html). `quopri` performs printable transport encoding and decoding for MIME (Multipurpose Internet Mail Extensions) documents, which is the encoding used in email. It takes the email object and decodes it.

Finally, once we have our links list that we've parsed out from the email, we'll use [`lxml`](https://lxml.de/) to parse the html associated with those links. We give it our decoded string of html we get as a response from `requests` and it returns a nicely formatted tree we can use to grep on html properties.

After we've formed nicely formatted data blobs about our various patent applications in the email, we format the messages to deliver them to slack:

```python
msgs = build_slack_msgs(data)
for msg in msgs:
    if msg['slack_webhook']:
        Slack_data = {
            "attachments": [
                {
                    "fallback": "Patent filing.",
                    "color": "#d32600",
                    "pretext": "New patent from {}".format(msg['applicant']),
                    "title": "{}".format(msg['title']),
                    "title_link": msg['link'],
                    "fields": [
                        {
                            "title": "Date filed",
                            "value": "{}".format(msg['date'])
                        },
                        {
                            "title": "Filing abstract",
                            "value": "{}".format(msg['abstract']),
                            "short": False
                        }
                    ],
                    "footer": "PatentBot"
                }
            ]
        }

        response = requests.post(
            msg['slack_webhook'],
            data=json.dumps(Slack_data),
            headers={'Content-Type': 'application/json'}
        )
```

And that completes our design:

```txt
PAAS service -> SES email -> SNS subscription -> https endpoint POST -> Slack incoming webhook POST
```

When we put this all together we get this:

![Patent scroll](https://i.imgur.com/SFupcJz.gif)

Easily readable, automated patent alerts sent directly to our team Slack channels! Users in Slack can now subscribe to exactly the channels they want. Then, there are three simple steps to extend this code to new companies to follow:

1. You add a company with USPTO alerts by [logging in to USPTO](https://go.uspatentappalerts.com/login/login.php) and selecting "add an alert"
2. Edit our secrets file to add another Slack webhook
3. Add the logic to `find_slack_webhook` to specify which keywords will identify the channel

Currently I have about twenty channels setup in a test slack, while I only subject my coworkers to about six of them 😅.

## Future Improvements

We've been happy to get patent alerts for a variety of companies for the past month, but there are always ways to improve.

We should look into incorporating any of [USPTO's APIs](https://developer.uspto.gov/api-catalog). I would like to query the PatFT database for information we might be missing about patents granted before the 18 month publication deadline. We could possibly use [USPTO's PatentPublicData API](https://github.com/USPTO/PatentPublicData) for that.

Another API, in beta, that I'm interested in is the [USPTO action rejection API](https://developer.uspto.gov/api-catalog/uspto-office-action-rejection-api-beta), which allows for retrieval of rejected applications. It would be great to keep track of those applications accepted or rejection as follow-ups.

As always, I am open to suggestions for new avenues of research for getting updated patent information as fast as possible. Also, if there are any lawyer-devs out there, please let me know if I could expand on anything or got anything wrong. I have no legal background but am eager to learn!

Shoutout to [@frewsxcv](https://github.com/frewsxcv/) for reviewing the code here with me and debugging MINE decoding. Thanks to [@mkaemingk](https://github.com/mkaemingk) for editing and [@chrswng](https://github.com/chrswng) for chatting with me about patents.

Thanks for reading!