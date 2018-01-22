---
author: Ryan Kearney
categories:
- Security
- Technology
date: 2012-10-05T21:24:17Z
dsq_thread_id:
- ""
guid: http://blog.ryankearney.com/?p=5
id: 5
title: Never Give Your Information To 10 Minute Old Startups
url: /2012/10/never-give-your-information-to-10-minute-old-startups/
---

Handing over sensitive information to startups that are only a few minutes old can lead to bad, bad things.

## The Startup

The startup under fire today is a web service by the name of _Ice Box Pro_ posted on <a href="http://news.ycombinator.com/item?id=4619132" target="_blank">Hacker News</a> today proved that point. The service was designed as a way to back up filed to Amazon Glacier that you put in a special Dropbox folder. I was curious to see how well it performed, so I decided to sign up and give it a test run. What follows is a perfect example on how not to handle security.<!--more-->

Clicking on the Account tab brings you to your account page, visible below.

<div id="attachment_8" style="max-width: 587px" class="wp-caption alignnone">
  <img class="size-full wp-image-8 " title="Screen-Shot-2012-10-05-at-9.05.03-PM" src="https://blog.ryankearney.com/wp-content/uploads/2012/10/Screen-Shot-2012-10-05-at-9.05.03-PM.png" alt="The Your Account page of an Ice Box Pro account" width="577" height="400" />
  
  <p class="wp-caption-text">
    The Your Account page of an Ice Box Pro account
  </p>
</div>

Visible are your name, email, AWS ID and Key, and the AWS Glacier vault created by Ice Box Pro. Upon setting your AWS ID and Key, only the last few characters are actually visible. What&#8217;s even more interesting, however, is the **/users/87** part of the URL. As it turns out, your User ID is baked into the URL. In this example, I was the 87th user to sign up for Ice Box Pro. My original account was somewhere between 5 and 15, although I entered in random text for the email address so I couldn&#8217;t log back in.

So what&#8217;s the problem? I&#8217;ll give you one guess as to what happens when you change that 87 to another number.

## Viewing other users information

That&#8217;s right, you could change that 87 to any number you could think of and it would spit back the information for that user. You would see exactly the same information you could see for yourself. This quickly reminded me of the <a href="https://stripe-ctf.com/" target="_blank">Stripe CTF</a> a few months ago. Since you can only see the Name, Email, and the last few characters of the users ID and Key, the information isn&#8217;t too dangerous with the exception of it being a spammers gold mine. But wait, it gets worse&#8230;

## Compromising accounts

See that Edit link at the bottom of the account page? Click it and you&#8217;ll see the account edit view!

<div id="attachment_10" style="max-width: 587px" class="wp-caption alignnone">
  <img class="size-full wp-image-10 " title="Screen-Shot-2012-10-05-at-9.12.53-PM" src="https://blog.ryankearney.com/wp-content/uploads/2012/10/Screen-Shot-2012-10-05-at-9.12.53-PM.png" alt="Edit your account page for IceBox" width="577" height="733" />
  
  <p class="wp-caption-text">
    In the Edit your profile view, you can change your name, email, password, and AWS info
  </p>
</div>

The important part here is to note that if I had filled out an AWS access key ID and AWS secret access key previously, the entire key would be visible on this screen. So while only the last few characters are visible from the account view, the entire key is visible from the edit view. It&#8217;s worth noting that the edit option is available for **any user account** and can be accessed by **anyone**.

This means that by going to /users/1/edit and /users/2/edit, you could edit the details of the two founders of Ice Box Pro. From here you can reset their password, login as them, and get access to any file they backed up. Even worse it gives you access to their AWS keys.

If you setup your access correctly, then only your AWS glacier service can be accessed. Some users, however, I found used their master AWS keys which give access to every area of Amazon Web Services (EC2, S3, etc).

## Conclusion

Never give any kind of information to a startup that came into existence just 10 minutes ago. At least give it a few days for them to work out the security vulnerabilities such as this. The one I saw today was one of the worst imaginable. Full control over any users account, password, and AWS keys. Users that used their master AWS keys opened themselves up to a major headache if the keys were accessed by the wrong people and not revoked in time.