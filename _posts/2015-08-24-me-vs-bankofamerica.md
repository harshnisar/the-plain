---
title: How Bank of America sniped my domain
layout: post
category: posts
published: true
---


Disclaimer: Well not mine technically.

We had been finalizing the website and the content for a month before publicly announcing machine learning india (ml-india). We weren't sure of the name; Should we go for ds-india and try to encompass a wider audience? Or should we remain ml-india. But rolling out the website and content was more important so we stuck to ml-india.

After finally creasing out all the issues in the Tableau story which I had been working on (shoutout, tableau is amazing), creating the invite list etc- 
We were finally ready. 
We had (obviously) checked earlier and the fact remained true that the domain ml-india.com was available.

###Day 1.
I was supposed to buy the domain from Varun's (Boss) godaddy account and his credit card. We filled the form and the rest of the details but failed in the payment procedure because Varun's CC had some issues. We tried multiple times in the day but alas it didn't work. Shashank's CC was blocked. I suggested to use mine, but it was discussed that reimbursement would be an issue. We pretty much shrugged it off given it didn't really matter if we released the website that day or the next. We weren't really chasing a deadline as it was a side project. I took the opportunity to add more finishing touches to ml-india. I changed the description of the GH repo and added the url to the to be website. I even added the the url to the twitter profile of ml-india and pretty much did all those touches one would do with excess time on their hands. 

###Day 2. 
I got busy with my work at office and the day went on normally. 
We tried Varun's CC again and it didn't work. 
Fine, we'll try tomorrow. 

###Day 3.
There had been some issue with the card but now they had been cleared. So in the evening after finishing my day's work, I decided to spend time on ml-india. I initiated my daily ritual. 

###But wait, ml-india.com was no longer available!

What? Maybe it’s locked on in my other GoDaddy account. Do they even have locking? Maybe there is some issue with the cache. I started hyperventilating. I was/am really attached to the project. It can't be just bought like that. What are the odds? Wait, did Varun buy it? Are they playing a prank on me? Did one my colleagues in the R&D department buy it? What other name we would use now? No other name made sense. I told Varun, but he thought I was the one joking. 

I took the next logical step, checked the whois information. 

```
Registrar: CSC CORPORATE DOMAINS, INC.
```

What? Who are they? Was my repeated trying to buy a domain on GoDaddy, my intent, leaked out or sold? Are they a domain reseller? Is this some kind of extortion  Wait, the fact that I put out domains on the twitter and GH which didn't point to anything and were unsold acted as triggers and representations of intent?
I started googling about CSC. A lot of acquisitions yes. Major clients yes. But what do they do?

> With our NameProtect® trademark monitoring application, CSC Digital
> Brand Services has created the first unified monitoring platform for
> domain names, Internet content and trademark jurisdictions. We also
> provide robust enforcement services to help you protect and enforce
> your brand rights.
> 
> The NameProtect platform enables you to detect potential
> infringements, prioritize results, and take appropriate action against
> abuses. It also helps you track changes via automated alerts and
> archive them for evidence building.

https://www.cscglobal.com/global/web/csc/trademark-monitoring.html

They buy clashing domains pre-emptively and actively scan the internet. So it must be my GH repo and twitter profile?

But who was their customer? My previous whois search didn't give me the entire detail, so I tried a different website.

```
Registry Registrant ID: 
Registrant Name: Domain Admin
Registrant Organization: Bank of America
Registrant Street: 5000 US HWY 17
Registrant City: Fleming Island
Registrant State/Province: FL
Registrant Postal Code: 32003
Registrant Country: US
Registrant Phone: +1.9049870917
Registrant Phone Ext: 
Registrant Fax: +1.4692018592
```

[https://who.is/whois/ml-india.com](whois infomation)

But why?
Why would Bank of America buy my domain. Do I need to now buy it from them? It’s a business? 

I googled *Bank of America buying domains* etc. (I wasn’t really thinking clearly, frantic mostly)
I stumbled upon [https://en.wikipedia.org/wiki/Bank_of_America#WikiLeaks](this). They’ve been notorious for buying domains. But this is different.

So I googled Bank of America ML and it all started to make sense.
Bank of America owned Merrill Lynch. Merrill Lynch's website? ml.com

Now the picture connected. CSC Global was working on the behalf of Bank of America and safegaurding its trademark. 

Ofcourse, I can’t direct hate towards CSC Global ( however many Orwellian and anti corporate  rants I had on that day ), I can only rather commend them for delivering on what they promise their clients (even if a day late, and successful only because of my CC issue). But we meant no harm to Merrill Lynch's identity nor were we trying to spoof. Also, if it's true that they figured it out from my twitter or GH repo, its my fault entirely. IRL, no one gives out newspaper ads about a real estate property they've not even bought. But who could imagine. Ah, I feel so small. Well. My manager, ofcourse not as much affected by this entire episode couldn't understand my confused feelings. I remained sour through the day. 

I was so amused and crushed at the same time. A part of me felt really really small and weak against these forces. Another part of me was excited by the idea how connected the world was, how in a weird way, Bank of America and I were now connected. 

PS. We settled for ml-india.org and I like the sound of it more.

> If you are an Indian doing or even mildly interested in machine
> learning or any data science checkout ml-india. Its an initiative to
> foster and increase collaboration in the Indian ml/data eco-system.
> Join the discussion.

[ml-india.org](http://ml-india.org)

Tableau Story:  [India's contribution to machine learning in the last 15 years](http://ml-india.org/insights)


