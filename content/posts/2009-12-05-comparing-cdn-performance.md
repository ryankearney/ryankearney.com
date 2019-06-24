---
author: Ryan Kearney
categories:
- Reviews
date: 2009-12-05T21:14:54Z
dsq_thread_id:
- ""
guid: http://blog.ryankearney.com/?p=45
id: 45
title: Comparing CDN Performance
url: /2009/12/comparing-cdn-performance/
---

[View Part 2 Here](http://blog.ryankearney.com/2009/12/comparing-cdn-performance-part-2/)

More and more CDN providers are appearing with competing prices and features. Here I&#8217;m going to compare Amazon CloudFront, Rackspace CloudFiles, and Amazon S3.

First off, Amazon S3 isn&#8217;t really a CDN per se, but I&#8217;ve ran across quite a few sites comparing Rackspace Cloud to S3, which isn&#8217;t a fair comparison. Amazon S3 does, however, have its own strong points which we will get into later.

<!--more-->

## Response Time

We will start by taking a look at the response time for the three services over a period of 1 month

<div id='gallery-1' class='gallery galleryid-45 gallery-columns-3 gallery-size-thumbnail'>
  <dl class='gallery-item'>
    <dt class='gallery-icon portrait'>
      <a href='https://blog.ryankearney.com/2009/12/comparing-cdn-performance/rackspace1m/'><img width="75" height="80" src="https://blog.ryankearney.com/wp-content/uploads/2009/12/rackspace1m.png" class="attachment-thumbnail size-thumbnail" alt="Response time over 1 month for Rackspace CloudFiles" aria-describedby="gallery-1-60" /></a>
    </dt>
    
    <dd class='wp-caption-text gallery-caption' id='gallery-1-60'>
      Response time over 1 month for Rackspace CloudFiles
    </dd>
  </dl>
  
  <dl class='gallery-item'>
    <dt class='gallery-icon portrait'>
      <a href='https://blog.ryankearney.com/2009/12/comparing-cdn-performance/cf1m/'><img width="75" height="80" src="https://blog.ryankearney.com/wp-content/uploads/2009/12/cf1m.png" class="attachment-thumbnail size-thumbnail" alt="Response time over 1 month for AWS CloudFront" aria-describedby="gallery-1-61" /></a>
    </dt>
    
    <dd class='wp-caption-text gallery-caption' id='gallery-1-61'>
      Response time over 1 month for AWS CloudFront
    </dd>
  </dl>
  
  <dl class='gallery-item'>
    <dt class='gallery-icon portrait'>
      <a href='https://blog.ryankearney.com/2009/12/comparing-cdn-performance/s31m/'><img width="75" height="80" src="https://blog.ryankearney.com/wp-content/uploads/2009/12/s31m.png" class="attachment-thumbnail size-thumbnail" alt="Response time over 1 month for AWS S3" aria-describedby="gallery-1-62" /></a>
    </dt>
    
    <dd class='wp-caption-text gallery-caption' id='gallery-1-62'>
      Response time over 1 month for AWS S3
    </dd>
  </dl>
  
  <br style="clear: both" />
</div>

The average response time for Amazon S3 was **819ms** which is pretty bad. However, S3 was never really meant to be a CDN, this is what their Cloud Front service is for. After looking at the Cloud Front average response time we can see it to be **310ms**, a much better response time. And then there&#8217;s Rackspace Cloud Files, coming in at **210ms**, which is even better. Rackspace Cloud Files uses Limelight for their CDN solution which is one of the industry leaders in content delivery, up there with Akamai. I would have done a comparison to Akamai, however I lack the funds to even get close to that. Rackspace Cloud makes it easy to be able to use the &#8220;big guys&#8221; infrastructure without having to pay the big price.<!--more-->

## Pricing

Here&#8217;s a quick breakdown of pricing for Amazon and Rackspace CDN services.

<table border="0">
  <tr>
    <th>
    </th>
    
    <th>
      Amazon
    </th>
    
    <th>
      Rackspace
    </th>
  </tr>
  
  <tr>
    <td>
      Storage Costs
    </td>
    
    <td>
      $0.15 / GB†
    </td>
    
    <td>
      $0.15 / GB
    </td>
  </tr>
  
  <tr>
    <td>
      Bandwidth Out
    </td>
    
    <td>
      $0.17 / GB† (US Traffic‡)
    </td>
    
    <td>
      $0.22 / GB
    </td>
  </tr>
  
  <tr>
    <td>
      Bandwidth In
    </td>
    
    <td>
      Free until June 30th 2010*
    </td>
    
    <td>
      $0.08 / GB
    </td>
  </tr>
  
  <tr>
    <td>
      PUT/POST/LIST Requests
    </td>
    
    <td>
      $0.01 per 1,000
    </td>
    
    <td>
      $0.01 per 500<br /> Free for files over 250k
    </td>
  </tr>
  
  <tr>
    <td>
      GET Requests
    </td>
    
    <td>
      $0.01 per 10,000 (US Traffic‡)
    </td>
    
    <td>
      Free
    </td>
  </tr>
  
  <tr>
    <td>
      DELETE Requests
    </td>
    
    <td>
      Free
    </td>
    
    <td>
      Free
    </td>
  </tr>
</table>

*After June 30th inbound data transfer is $0.10 / GB
  
†Variable Cost; Decreases as more space or bandwidth is used.
  
‡Higher charges apply for other regions such as Japan. <a href="http://aws.amazon.com/cloudfront/#pricing" target="_blank">Click here to view the full pricing model.</a>

Keep in mind with Amazon, you&#8217;re paying the transfer cost to transfer your file from their S3 storage to various end points around the globe. Rackspace has no such charge. Due to amazons tiered pricing, if you needed to store and deliver hundreds to thousands of terabytes of data a month, then Amazon would be cheaper for you. But then again, if you had that much volume, chances are you don&#8217;t care what I think is best for you and you defiantly don&#8217;t need help picking the right CDN. You can view the cost calculator for both services here. [Rackspace Cloud Files](http://www.rackspacecloud.com/cloud_hosting_products/files/pricing) | [Amazon Web Services](http://calculator.s3.amazonaws.com/calc5.html) Keep in mind when you setup the Amazon Web Services monthly calculator you will need to add S3 and Cloud Front. The S3 account will hold all of your data, and the outbound bandwidth will vary depending on how many files you have, their sizes, and how often the Cloud Front endpoints refresh their cache of your data. Cloud Front will then be where you allocate your total projected outbound bandwidth and average object size (which is to calculate GET requests I&#8217;m guessing) as well as allocate percentages to different regions, since Amazon charges differently per GB depending on the region the server responding to the request is located.

## Speed

Next up is a speed test. I&#8217;ve uploaded a 100MB file to Amazon S3 and Rackspace Cloud Files to download from various locations. Listed below is the time taken (in seconds) to download the 100MB file.

<table border="0">
  <tr>
    <th>
      Network
    </th>
    
    <th>
      Amazon
    </th>
    
    <th>
      Rackspace
    </th>
  </tr>
  
  <tr>
    <td>
      Roadrunner (Central Florida (Residential))
    </td>
    
    <td>
      52 Seconds (1.92 MB/s)
    </td>
    
    <td>
      59 Seconds (1.71 MB/s)
    </td>
  </tr>
  
  <tr>
    <td>
      Rackspace (Texas)
    </td>
    
    <td>
      2.1 Seconds (47.2 MB/s)
    </td>
    
    <td>
      1.9 Seconds (45.7 MB/s)
    </td>
  </tr>
  
  <tr>
    <td>
      Amazon (N. Virginia)
    </td>
    
    <td>
      7.4 Seconds (13.3 MB/s)
    </td>
    
    <td>
      15 Seconds (6.13 MB/s)
    </td>
  </tr>
  
  <tr>
    <td>
      The Planet (Texas)
    </td>
    
    <td>
      8.9 Seconds (11.2 MB/s)
    </td>
    
    <td>
      9.3 Seconds (10.8 MB/s)
    </td>
  </tr>
</table>

It&#8217;s clear the Roadrunner residential connection was the bottle neck in both downloads. However, when tested from Rackspace Cloud Servers, both Amazon Cloud Front and Rackspace Cloud Files performed quite well. In the test using Amazon EC2, it&#8217;s clear that Amazon was the winner. However, the speeds were MUCH worse than when accessed from Rackspace&#8217;s network. This leads me to believe that the only reason Amazon won that test was because of their extremely close proximity to their CDN servers. Both providers were faster when pulling from their own network, this was no surprise. However, when pulled from a separate network, in this case Roadrunner and The Planet, Amazon scored slightly faster.

## Features

What&#8217;s a CDN without features? Well, it&#8217;s just a CDN. But hey, that&#8217;s what a CDN does, deliver content. Anything above and beyond that is an added bonus. Lets go over the various features Amazon and Rackspace have to offer.

<table border="0">
  <tr>
    <th>
      Feature
    </th>
    
    <th>
      Amazon
    </th>
    
    <th>
      Rackspace
    </th>
  </tr>
  
  <tr>
    <td>
      Maximum File Size
    </td>
    
    <td>
      5GB
    </td>
    
    <td>
      5GB
    </td>
  </tr>
  
  <tr>
    <td>
      Free Storage->Endpoint transfer
    </td>
    
    <td>
      No
    </td>
    
    <td>
      Yes
    </td>
  </tr>
  
  <tr>
    <td>
      HTTPS
    </td>
    
    <td>
      S3 Only, Wildcard Certificate
    </td>
    
    <td>
      No
    </td>
  </tr>
  
  <tr>
    <td>
      Detailed Logs
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
  </tr>
  
  <tr>
    <td>
      Custom CNAME
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      In the works
    </td>
  </tr>
  
  <tr>
    <td>
      Custom Response Headers
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      No
    </td>
  </tr>
  
  <tr>
    <td>
      Torrent Support
    </td>
    
    <td>
      S3 Only
    </td>
    
    <td>
      No
    </td>
  </tr>
</table>

Two really nice features of Amazon S3 are HTTPS and Torrents. Now keep in mind these are S3 features only, meaning they don&#8217;t apply to Amazon&#8217;s CDN service Cloud Front. They use a wildcard certificate on the domain *.s3.amazonaws.com so you can use HTTPS to deliver content over S3, although most browsers will give you an invalid certificate warning (ssl\_error\_bad\_cert\_domain on firefox). Their other nice feature is torrent support. If you add &#8220;?torrent&#8221; to the end of any S3 URL, the server will return a .torrent file instead of the file requested. This is especially great for large files since you will have other users helping you out with distribution, lowering your bandwidth cost. The torrent uses Amazons&#8217; tracker and their S3 machines are seeding the file. This way your torrent will never die, so long as the file remains on the S3 servers. Once again, while this isn&#8217;t a feature of their CDN service, it&#8217;s still a feature of S3, which is required to use their CDN service.

## Conclusion

There are many content delivery services out there. Limelight, Akamai, Amazon, Level 3, and many others. Not all of us can afford the nice ones such as Akamai or Level 3, but that&#8217;s why there&#8217;s amazing pay-as-you-go solutions such as the two mentioned in this article, Amazon and Rackspace. There are others, I just haven&#8217;t had the time to try them all. It&#8217;s still a very close call between these two CDN&#8217;s. They both have their strong points and weaknesses. However, knowing that Rackspace Cloud Files uses Limelight Networks to deliver content really caught my attention. It really depends on how you&#8217;re using the service to determine which one is the most affordable. Amazon&#8217;s prices are a tad bit cheaper, starting at $0.17 per GB of outbound transfer inside the United States but you&#8217;ll be paying for S3 to Cloud Front transfers, as well as GET requests. Amazon also offers the ability to set custom response headers, allowing you to set custom cache settings for various content. When it comes down to it, most of the extra features that Amazon has over Rackspace don&#8217;t really apply to Cloud Front, their CDN service. These include torrents, HTTPS, and URL&#8217;s that expire after a certain time. Comparing apples to apples, Amazon has the leg up with custom CNAME support and custom response headers at the cost of having to pay for S3 to Cloud Front transfer. If you need a robust solution and plan on transferring extremely massive amounts of data, then Amazon might be your best bet. But if it&#8217;s ease of use and bandwidth provided by Limelight, one of the industry leaders in CDN, then Rackspace Cloud Files may be best for you.