---
author: Ryan Kearney
categories:
- Technology
date: 2012-08-20T15:55:17Z
dsq_thread_id:
- "1299665174"
guid: http://blog.ryankearney.com/?p=15
id: 287
title: It costs $35 Million to send an HD video over SMS while roaming on AT&#038;T
url: /2012/08/it-costs-35-million-to-send-an-hd-video-over-sms-while-roaming-on-att/
---

AT&T [has the following chart on their webpage](https://www.wireless.att.com/learn/international/roaming/international-roaming.jsp) which outlines roaming rates while outside the U.S. We&#8217;re going to concentrate on the Text Messages row, also known as SMS messages.

<table border="0" summary="" cellspacing="0" cellpadding="0">
  <tr>
    <th colspan="2">
      SENDING TEXT, PICTURE, AND VIDEO MESSAGES WHEN OUTSIDE THE U.S.
    </th>
  </tr>
  
  <tr>
    <td>
      Text Messages
    </td>
    
    <td>
      $0.50 per message sent
    </td>
  </tr>
  
  <tr>
    <td>
      Picture and Video Messages
    </td>
    
    <td>
      $1.30 per message sent
    </td>
  </tr>
</table>

I did the math and Tweeted my findings.

<!--more-->

   
<https://twitter.com/RyanAKearney/statuses/237585880276144128>

A few hours later, an AT&T employee Tweets back (at least according to their Twitter bio they appear to be), but then almost immediately deletes their Tweet. No matter, their reply was already sent via text message, email, and cached on my desktop Twitter client Tweetbot. Below is a screenshot.

<div id="attachment_16" style="max-width: 490px" class="wp-caption alignnone">
  <img class="size-full wp-image-16 " title="Reply from someone affiliated with AT&T" src="https://blog.ryankearney.com/wp-content/uploads/2012/11/screen-shot-2012-08-20-at-3-49-56-pm1.png" alt="Twitter response from AT&T employee." width="480" height="646" />
  
  <p class="wp-caption-text">
    Someone affiliated with AT&T replies back, only to quickly delete their post.
  </p>
</div>

> @RyanAKearney actually 1 character in a msg equals abt 1 kb.1024KB=1MB..same conversion to GB-AT&T charges 19.97/mb or 120mb for $30 #fact

Actually, the body of a text message is 140 bytes which is 160 7-bit characters. I incorrectly assumed they were 160 bytes when I made my initial calculation #fact. So one character in a text message is 7 bits, far off from the 1,000 bits you claim it is. Then she goes off to say AT&T charges $19.97 per megabit and somehow that amounts to 120 megabits for $30? I can see why they deleted the tweet.

Now lets do the math here one step at a time.

  1. 1024 bytes = 1 KiB
  2. 1024 KiB = 1 MiB
  3. 1024 MiB = 1 Gib
  4. 1024 \* 1024 \* 1024 = 1,073,741,824 bytes per GiB   
    Now that we know how many bytes are in 1GiB, we can divide that number by 140, the number of bytes of data you can send in a text message.
  5. 1,073,741,824 / 140 = 7,669,585 (rounded up)

This means we have to send 7,669,585 SMS messages to send 1GB of data (and this is assuming you can represent any set of data in an SMS message which I don&#8217;t believe you can, but that&#8217;s besides the point since it would just made this already large number even larger).

Finally, since AT&T charges $0.50 per SMS message, we just multiply our number of messages by $0.50 to get&#8230;

$3,834,792.50

If you were sending that 1GiB of data to another AT&T customer, that amount would be

$7,669,585

What&#8217;s this mean? If you wanted to send a typical HD video from one AT&T cell phone to another via SMS messages, assuming the video is 4.6GiB in size, it would cost:

$35,280,091

So there you have it. $35 Million to send a 4.6GiB HD movie from one phone to another using SMS while roaming.