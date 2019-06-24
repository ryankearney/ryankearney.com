+++
title = "Never Give Your Information To 10 Minute Old Startups"
date = 2012-10-05T21:24:17Z
categories = ["Security", "Technology"]
tags = [ "Dropbox", "AWS", "Glacier", "Hack" ]
toc = true
+++
Handing over sensitive information to startups that are only a few minutes old can lead to bad, bad things.

## The Startup

The startup under fire today is a web service by the name of _Ice Box Pro_ posted on [Hacker News](http://news.ycombinator.com/item?id=4619132) today proved that point. The service was designed as a way to back up filed to Amazon Glacier that you put in a special Dropbox folder. I was curious to see how well it performed, so I decided to sign up and give it a test run. What follows is a perfect example on how not to handle security.

Clicking on the Account tab brings you to your account page, visible below.

{{< figure src="/images/2012/10/Screen-Shot-2012-10-05-at-9.05.03-PM.png" title="Ice Box Pro Account Page" caption="The Your Account page of an Ice Box Pro account" alt="The Your Account page of an Ice Box Pro account" >}}

Visible are your name, email, AWS ID and Key, and the AWS Glacier vault created by Ice Box Pro. Upon setting your AWS ID and Key, only the last few characters are actually visible. What's even more interesting, however, is the **/users/87** part of the URL. As it turns out, your User ID is baked into the URL. In this example, I was the 87th user to sign up for Ice Box Pro. My original account was somewhere between 5 and 15, although I entered in random text for the email address so I couldn't log back in.

So what's the problem? I'll give you one guess as to what happens when you change that 87 to another number.

## Viewing other users information

That's right, you could change that 87 to any number you could think of and it would spit back the information for that user. You would see exactly the same information you could see for yourself. This quickly reminded me of the [Stripe CTF](https://stripe-ctf.com/) a few months ago. Since you can only see the Name, Email, and the last few characters of the users ID and Key, the information isn't too dangerous with the exception of it being a spammers gold mine. But wait, it gets worse...

## Compromising accounts

See that Edit link at the bottom of the account page? Click it and you'll see the account edit view!

{{< figure src="/images/2012/10/Screen-Shot-2012-10-05-at-9.12.53-PM.png" title="Ice Box Pro Edit Account Page" caption="In the Edit your profile view, you can change your name, email, password, and AWS info" alt="Edit your account page for IceBox" >}}

The important part here is to note that if I had filled out an AWS access key ID and AWS secret access key previously, the entire key would be visible on this screen. So while only the last few characters are visible from the account view, the entire key is visible from the edit view. It's worth noting that the edit option is available for **any user account** and can be accessed by **anyone**.

This means that by going to /users/1/edit and /users/2/edit, you could edit the details of the two founders of Ice Box Pro. From here you can reset their password, login as them, and get access to any file they backed up. Even worse it gives you access to their AWS keys.

If you setup your access correctly, then only your AWS glacier service can be accessed. Some users, however, I found used their master AWS keys which give access to every area of Amazon Web Services (EC2, S3, etc).

## Conclusion

Never give any kind of information to a startup that came into existence just 10 minutes ago. At least give it a few days for them to work out the security vulnerabilities such as this. The one I saw today was one of the worst imaginable. Full control over any users account, password, and AWS keys. Users that used their master AWS keys opened themselves up to a major headache if the keys were accessed by the wrong people and not revoked in time.