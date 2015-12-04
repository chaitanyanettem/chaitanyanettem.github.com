---
layout: post
title: Scraping CBSE Class XII results for fun and profit
date: 2015-12-04 01:23
permalink: scraping-cbse
summary: A post on how I go about scraping the Class XII results from CBSE's results website using Python and asyncio.
categories: python scraping
---

So a couple of days ago [Avinash](avi.im) mentioned that he had scraped the 12th standard board results from the CBSE website and it seemed like something I would be interested in doing as well. I remembered Debarghya Das's excellent [post](https://deedy.quora.com/Hacking-into-the-Indian-Education-System) from a couple of years ago about ICSE results and how they seemed very peculiar. Not having seen anyone do something similar for CBSE my curiosity was piqued.

###Initial impressions of the website
The results page [here](http://cbseresults.nic.in/class12/cbse122015_all.htm) hadn't changed at all since 2009 when ***I*** checked my class 12 results. There's of course absolutely no authentication. Having been told about the roll number ranges by Avinash, I tried a couple of inputs to check what the parameters of the post request are. There is also a roll number validator in the Javascript of that page so its not very difficult to decipher what all the valid roll numbers are.

There are 2 parameters of the post request:

* regno (which is the roll number you give as input)

* B1 (which I presume specifies the button name and is always equal to "Submit")

Trying a simple post request with curl without setting any of the headers failed with the site reporting ***"Access denied, pl. click here to visit the site"***. To avoid that I tried doing the same by copying the entire post request using Chrome DevTools. And of course it worked that way. These were the headers used:

```
Origin: http://cbseresults.nic.in
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.8
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/46.0.2490.80 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Cache-Control: max-age=0
Referer: http://cbseresults.nic.in/class12/cbse122015_all.htm
Connection: keep-alive
DNT: 1
```

Presumably, they were checking for the presence of the Referer header but I didn't spend time trying to find that out.

###Tools for the job
Python was of course the language to be used. I decided against using Scrapy. Instead I decided to go with asyncio, BeautifulSoup4 and roll my own scraper. I've been wanting to take a look at asyncio for some time now and haven't had the opportunity to use it on anything. I glanced through the post [here](http://aosabook.org/en/500L/a-web-crawler-with-asyncio-coroutines.html) by Guido Van Rossum before proceeding (great post if any one wants to get into web scraping with Python).
