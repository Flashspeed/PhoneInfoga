This page is a summary of the [OSINT tutorial originally posted on my blog](https://medium.com/@SundownDEV/phone-number-scanning-osint-recon-tool-6ad8f0cac27b)

----

Everyone has a phone, using at least one phone number. Phone numbers are a very common resource for Social Engineering. It’s something we use almost every day to communicate and sometimes we may have to deal with unsolicited phone calls or messages. We may have to gather information about a phone number we found about a company or an individual. Basic information such as line type and carrier can be very useful for a Social Engineer.

Supposing I know your name and your phone number, I could send you a phishing threat using your carrier’s mail template. Or I may call your carrier’s support service to gather as much information as I can on you. Another example, if the number is a land line, some of the digits will tell me the area where it comes from. These information are very simple to get without using a tool, but what about going further ?

The goal of this project is to gather as much information as possible on the given phone number, including the ITSP or the owner.

>An Internet telephony service provider (ITSP) offers digital telecommunications services based on Voice over Internet Protocol (VoIP) that are provisioned via the Internet. [Wikipedia](https://en.wikipedia.org/wiki/Internet_telephony_service_provider)

## What is Open Source Intelligence ?

On my way learning about security, I discovered months ago Open Source Intelligence (OSINT). OSINT is the collection of information from publicly available and open data sources to be used in an intelligence context.

>In the intelligence community, the term “open” refers to overt, publicly available sources (as opposed to covert or clandestine sources). It is not related to open-source software or public intelligence. [Wikipedia](https://en.wikipedia.org/wiki/Open-source_intelligence)

Open Source Intelligence (OSINT) takes three forms: Passive, Semi-passive, and Active. There are several way to deal with information in an intelligence context. Especially when it comes to footprinting. I’m gonna practice Passive Information Gathering (or Passive Reconnaissance), it means I will not store data gathered and mostly use third party sources. But I’ll gather information from many sources and filter the results to find the owner or the ITSP.

Learn more about OSINT reconnaissance techniques and footprinting [here](http://www.pentest-standard.org/index.php/Intelligence_Gathering).

First of all, I want my OSINT tool to check for :

- Phone number reputation (phone fraud reports)
- Footprints on VoIP and temporary number providers websites
- Social media pages (facebook, twitter, linkedin, instagram) and phone books results

To find documents and web pages related to the phone number, I use Google Dork requests. I make a list of every disposable number providers I found. Some of them exposes their numbers and all of this is indexed by search engines. For example if I ask Google for a web page on one of these sites with the number included in content and found a result, this usually means the number is part of their number range. As my OSINT reconnaissance is pretty basic, I’ll never consider a result as a success.

## Footprinting proccess

![](https://i.imgur.com/bWx79dy.png)

## The problems

At this point we are able to gather a lot of information about almost every phone number in the world and that’s amazing! But I’m facing two major problems while building my tool.

First, Google blacklist the client IP and ask you to complete a captcha after a few amount of requests. When you practice complex custom requests, Google ask you to complete the captcha.

When you search on Google using custom requests (Google Dorks), you get very easily blacklisted. So Google shows up a page where you have to complete a captcha to continue. As soon as the captcha is completed, Google create a cookie named “GOOGLE_ABUSE_EXEMPTION” which is used to whitelist your browser and IP address for some minutes. This temporary whitelist is enough to let you gather a lot of information from many sources. So I decided to add a simple user manipulation to bypass this bot detection.

I make a user-agent list to make the request as random as possible. I’ll not use proxies since Google blacklists free proxies instantly. I’ll use the exact same headers as a normal user that uses a browser and, of course, that “GOOGLE_ABUSE_EXEMPTION” cookie. Of course, I can’t generate a new token as Google generate it by time and IP address. So I’ll just try make requests and wait until I get a 503 error, which means I got blacklisted. Then I ask the user to follow an URL to manually complete the captcha and copy the whitelist token to paste it in the CLI. The tool is now able to continue to scan! At this point this is not really a bypass, but rather a workaround.

Second, ITSPs doesn’t share their phone number ranges. At the moment this is way too difficult to gather phone number of every single providers in the world, or maybe this is just another level of OSINT. Also telephone numbers change too often. It’s very hard to find the ITSPs using only footprinting. But I noticed that some lookup websites (such as 411.com) were able to recover the ITSP that owns the number.