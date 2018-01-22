---
author: Ryan Kearney
categories:
- Security
date: 2013-01-09T17:19:55Z
dsq_thread_id:
- ""
footer:
- ""
guid: http://blog.ryankearney.com/?p=93
header_title_bar:
- ""
header_transparency:
- ""
id: 93
image: /wp-content/uploads/2012/11/Screen-Shot-2012-11-26-at-12.38.21-AM.png
sidebar:
- ""
title: Comcast caught hijacking web traffic
url: /2013/01/comcast-caught-intercepting-and-altering-your-web-traffic/
---

On November 20th, 2012 Comcast hijacked my HTTP traffic and re-routed it through their own servers, injecting a &#8220;notice&#8221; on the page before completing the request. What this means is instead of my web request being routed to the website I wanted to visit, Comcast took it upon themselves to hijack my web traffic, forcing it to go through their servers instead. This poses a massive security risk for users since there&#8217;s no telling what type of logging Comcast uses on their end. Why did they do all this? To force a &#8220;courtesy notice&#8221; on every webpage I visit until I logged into my Comcast account because I was within 90% of my new 300GB limit?

<!--more-->In my testing I discovered that this only affects HTTP traffic and not HTTPS traffic. What this means is while your online banking may be safe, any other website you visit over HTTP may cause your privacy to be at risk. This is a prime example of why SSL encryption on websites is so important. However, it may only be a matter of time before Comcast starts executing man in the middle attacks on SSL traffic.

## Web Log

Here&#8217;s an excerpt from the servers web log

    2601:5:300:83:6997:f2b7:4d2d:c7fd - - [20/Nov/2012:21:38:44 -0800] "GET / HTTP/1.1" 200
    68.87.68.230 - - [20/Nov/2012:21:38:31 -0800] "GET / HTTP/1.1" 200
    68.87.68.230 - - [20/Nov/2012:21:35:58 -0800] "GET / HTTP/1.1" 200
    2601:5:300:83:6997:f2b7:4d2d:c7fd - - [20/Nov/2012:21:35:56 -0800] "GET / HTTP/1.1" 200<
    

All four requests were made by my computer. The first was made straight to the server using my IPv6 address of **2601:5:300:83:6997:f2b7:4d2d:c7fd**. The second two requests were hijacked by Comcast so the request ended up coming from **68.87.68.230** (one of Comcast&#8217;s used to hijack customer&#8217;s web traffic).

After a request is hijacked, HTML code is injected into the web page to display this message

![Comcast Courtesy Notice](https://blog.ryankearney.com/wp-content/uploads/2012/11/Screen-Shot-2012-11-26-at-12.38.21-AM.png)

Below is the code that Comcast is injecting into the page. If your browser doesn&#8217;t load the code below, you can [view it here on GitHub](https://gist.github.com/4146814).

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/4146814">Gist</a>.
  </noscript>
</div>