---
author: Ryan Kearney
categories:
- Technology
date: 2009-12-15T23:25:09Z
dsq_thread_id:
- ""
guid: http://blog.ryankearney.com/?p=54
id: 54
title: Comparing CDN Performance (Part 2)
url: /2009/12/comparing-cdn-performance-part-2/
---

<p style="text-align: justify;">
  Last week I wrote an article comparing Amazon S3 and Cloud Front to Rackspace Cloud Files. Since then I have gotten additional requests to compare more content delivery networks. The following is a comparison of Amazon Cloud Front, Rackspace Cloud Files, SimpleCDN, and GoGrid CDN. I tried to cover as many bases as I could. Please let me know if I missed anything.
</p>

## Response Time

We will start by taking a look at the response time for the three services over a period of 1 week

<div id='gallery-2' class='gallery galleryid-54 gallery-columns-4 gallery-size-thumbnail'>
  <dl class='gallery-item'>
    <dt class='gallery-icon portrait'>
      <a href='https://blog.ryankearney.com/2009/12/comparing-cdn-performance-part-2/cf1/'><img width="74" height="80" src="https://blog.ryankearney.com/wp-content/uploads/2009/12/cf1.png" class="attachment-thumbnail size-thumbnail" alt="Amazon CloudFront Pingdom Graph" aria-describedby="gallery-2-64" /></a>
    </dt>
    
    <dd class='wp-caption-text gallery-caption' id='gallery-2-64'>
      Amazon CloudFront
    </dd>
  </dl>
  
  <dl class='gallery-item'>
    <dt class='gallery-icon portrait'>
      <a href='https://blog.ryankearney.com/2009/12/comparing-cdn-performance-part-2/gogrid1/'><img width="75" height="80" src="https://blog.ryankearney.com/wp-content/uploads/2009/12/gogrid1.png" class="attachment-thumbnail size-thumbnail" alt="GoGrid Pingdom Graph" aria-describedby="gallery-2-65" /></a>
    </dt>
    
    <dd class='wp-caption-text gallery-caption' id='gallery-2-65'>
      GoGrid CDN
    </dd>
  </dl>
  
  <dl class='gallery-item'>
    <dt class='gallery-icon portrait'>
      <a href='https://blog.ryankearney.com/2009/12/comparing-cdn-performance-part-2/rackspace1/'><img width="75" height="80" src="https://blog.ryankearney.com/wp-content/uploads/2009/12/rackspace1.png" class="attachment-thumbnail size-thumbnail" alt="Rackspace CloudFiles Pingdom Graph" aria-describedby="gallery-2-66" /></a>
    </dt>
    
    <dd class='wp-caption-text gallery-caption' id='gallery-2-66'>
      Rackspace CloudFiles
    </dd>
  </dl>
  
  <dl class='gallery-item'>
    <dt class='gallery-icon portrait'>
      <a href='https://blog.ryankearney.com/2009/12/comparing-cdn-performance-part-2/simplecdn1/'><img width="75" height="80" src="https://blog.ryankearney.com/wp-content/uploads/2009/12/simplecdn1.png" class="attachment-thumbnail size-thumbnail" alt="SimpleCDN Pingdom Graph" aria-describedby="gallery-2-67" /></a>
    </dt>
    
    <dd class='wp-caption-text gallery-caption' id='gallery-2-67'>
      SimpleCDN
    </dd>
  </dl>
  
  <br style="clear: both" />
</div>

<p style="text-align: justify;">
  Rackspace Cloud Files came in first place with an average response time of just <strong>69ms</strong>, however, GoGrid CDN was very close behind with <strong>70ms</strong>. In third place was Amazon Cloud Front with an average response time of <strong>225ms</strong> and in last place was SimpleCDN with an average response time of <strong>402ms</strong>. Here&#8217;s a chart with the four Content Delivery Network&#8217;s average, fastest, and slowest response times over a period of one week.<!--more-->
</p>

<table border="0">
  <tr>
    <th colspan="4">
      Response times in milliseconds
    </th>
  </tr>
  
  <tr style="text-align: center;">
    <th>
    </th>
    
    <th>
      Average
    </th>
    
    <th>
      Fastest
    </th>
    
    <th>
      Slowest
    </th>
  </tr>
  
  <tr>
    <th>
      Rackspace Cloud Files
    </th>
    
    <td>
      69
    </td>
    
    <td>
      24
    </td>
    
    <td>
      651
    </td>
  </tr>
  
  <tr>
    <th>
      Amazon Cloud Front
    </th>
    
    <td>
      225
    </td>
    
    <td>
      53
    </td>
    
    <td>
      522
    </td>
  </tr>
  
  <tr>
    <th>
      SimpleCDN
    </th>
    
    <td>
      402
    </td>
    
    <td>
      188
    </td>
    
    <td>
      2,235
    </td>
  </tr>
  
  <tr>
    <th>
      GoGrid CDN
    </th>
    
    <td>
      70
    </td>
    
    <td>
      26
    </td>
    
    <td>
      814
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Not only did Rackspace Cloud Files the lowest average response time, it also had the fastest response time overall in the one week time frame. GoGrid CDN also proved to be a good contestant with an average response time of a mere one millisecond over that of Rackspace Cloud Files. While Amazon Cloud Front had quite a bit higher average response time, it did have the lowest, slowest response time with <strong>522ms</strong> as the longest response time. SimpleCDN has slowest response time of over two seconds, which is just awful for a content delivery network.
</p>

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
    
    <th>
      GoGrid
    </th>
    
    <th>
      SimpleCDN
    </th>
  </tr>
  
  <tr>
    <th>
      Storage Costs
    </th>
    
    <td>
      $0.15 / GB†
    </td>
    
    <td>
      $0.15 / GB
    </td>
    
    <td>
      $0.60 / GB††
    </td>
    
    <td>
      $0.75 / GB††
    </td>
  </tr>
  
  <tr>
    <th>
      Bandwidth Out
    </th>
    
    <td>
      $0.17 / GB† (US Traffic‡)
    </td>
    
    <td>
      $0.22 / GB
    </td>
    
    <td>
      $0.25 / GB
    </td>
    
    <td>
      $0.039 / GB†
    </td>
  </tr>
  
  <tr>
    <th>
      Bandwidth In
    </th>
    
    <td>
      Free until June 30th 2010*
    </td>
    
    <td>
      $0.08 / GB
    </td>
    
    <td>
      Free
    </td>
    
    <td>
      Free
    </td>
  </tr>
  
  <tr>
    <th>
      PUT/POST/LIST Requests
    </th>
    
    <td>
      $0.01 per 1,000
    </td>
    
    <td>
      $0.01 per 500<br /> Free for files over 250k
    </td>
    
    <td>
      Free
    </td>
    
    <td>
      Free
    </td>
  </tr>
  
  <tr>
    <th>
      GET Requests
    </th>
    
    <td>
      $0.01 per 10,000 (US Traffic‡)
    </td>
    
    <td>
      Free
    </td>
    
    <td>
      Free
    </td>
    
    <td>
      Free
    </td>
  </tr>
  
  <tr>
    <th>
      DELETE Requests
    </th>
    
    <td>
      Free
    </td>
    
    <td>
      Free
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
  
††Storage not necessary, more information in the features section.
  
‡Higher charges apply for other regions such as Japan. <a href="http://aws.amazon.com/cloudfront/#pricing" target="_blank">Click here to view the full pricing model.</a>

<p style="text-align: justify;">
  I wouldn&#8217;t consider SimpleCDN to be a true pay-as-you-go service, they require you to add funds to your account, with the smallest amount being $50. You can view the cost calculator for the services here. <a href="http://www.rackspacecloud.com/cloud_hosting_products/files/pricing">Rackspace Cloud Files</a>, <a href="http://calculator.s3.amazonaws.com/calc5.html">Amazon Web Services</a>, <a href="http://simplecdn.com/calculator">SimpleCDN</a>, (GoGrid CDN currently has no cost estimation calculator). Keep in mind when you setup the Amazon Web Services monthly calculator you will need to add S3 and Cloud Front. The S3 account will hold all of your data, and the outbound bandwidth will vary depending on how many files you have, their sizes, and how often the Cloud Front endpoints refresh their cache of your data. Cloud Front will then be where you allocate your total projected outbound bandwidth and average object size (which is to calculate GET requests I&#8217;m guessing) as well as allocate percentages to different regions, since Amazon charges differently per GB depending on the region the server responding to the request is located.
</p>

## Speed

Next up is a speed test. I&#8217;ve uploaded a 100MB file to Amazon S, Rackspace Cloud Files, SimpleCDN, and GoGrid CDN to download from various locations. Listed below is the time taken (in seconds) to download the 100MB file. Each test was done three times with the fastest of the three tests listed below.

<table border="0">
  <tr>
    <th>
      Network Tested From
    </th>
    
    <th>
      Amazon
    </th>
    
    <th>
      Rackspace
    </th>
    
    <th>
      GoGrid CDN
    </th>
    
    <th>
      Simple CDN
    </th>
  </tr>
  
  <tr>
    <th>
      Residential ISP (Central Florida)
    </th>
    
    <td>
      53s (1.89MB/s)
    </td>
    
    <td>
      63s (1.58MB/s)
    </td>
    
    <td>
      75s (1.34MB/s)
    </td>
    
    <td>
      59s (1.71MB/s)
    </td>
  </tr>
  
  <tr>
    <th>
      Rackspace (Texas)
    </th>
    
    <td>
      2.1s (46.7MB/s)
    </td>
    
    <td>
      1.7s (58.8MB/s)
    </td>
    
    <td>
      1.3s (74.6MB/s)
    </td>
    
    <td>
      3.3s (30.4MB/s)
    </td>
  </tr>
  
  <tr>
    <th>
      Amazon (N. Virginia)
    </th>
    
    <td>
      2.5s (40.0MB/s)
    </td>
    
    <td>
      13s (7.42MB/s)
    </td>
    
    <td>
      10s (9.8MB/s)
    </td>
    
    <td>
      3.3s (30.5MS/s)
    </td>
  </tr>
  
  <tr>
    <th>
      Amazon (N. California)
    </th>
    
    <td>
      2.4s (41.7MB/s)
    </td>
    
    <td>
      2.9s (35.1MB/s)
    </td>
    
    <td>
      3.6s (27.6MB/s)
    </td>
    
    <td>
      1.6s (54.0MB/s)
    </td>
  </tr>
  
  <tr>
    <th>
      Amazon (Ireland)
    </th>
    
    <td>
      2.1s (46.7MB/s)
    </td>
    
    <td>
      7.4s (13.6MB/s)
    </td>
    
    <td>
      2.0s (51.3MB/s)
    </td>
    
    <td>
      7.2s (13.8MB/s)
    </td>
  </tr>
  
  <tr>
    <th>
      GoGrid (California)
    </th>
    
    <td>
      2.0s (49.8MB/s)
    </td>
    
    <td>
      2.7s (37.1MB/s)
    </td>
    
    <td>
      2.1s (47.1MB/s)
    </td>
    
    <td>
      2.6s (38.1MB/s)
    </td>
  </tr>
  
  <tr>
    <th>
      The Planet (Texas)
    </th>
    
    <td>
      9.0s (11.1MB/s)
    </td>
    
    <td>
      9.2s (10.9MB/s)
    </td>
    
    <td>
      8.9s (11.2MB/s)
    </td>
    
    <td>
      32s (3.09MB/s)
    </td>
  </tr>
  
  <tr>
    <th>
      Average (Residential ISP Excluded)
    </th>
    
    <td>
      3.35s (39.3MB/s)
    </td>
    
    <td>
      6.15s (34.3MB/s)
    </td>
    
    <td>
      4.65s (36.9MB/s)
    </td>
    
    <td>
      8.3s (28.3MB/s)
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Not counting the slow residential ISP download rate we can see that Amazon Cloud Front came out ahead on the speed tests with an average download speed of <strong>39.3MB/s</strong>. Coming in second was GoGrid CDN with <strong>36.9MB/s</strong> followed by Rackspace Cloud Files at <strong>34.3MB/s</strong> and finally SimpleCDN with just <strong>28.3MB/s</strong>. SimpleCDN had some good tests, however, with a fastest speed of <strong>54MB/s</strong> clocked from Amazon&#8217;s networks in Northern California. The <strong>3.09MB/s</strong> speed was what really brought it down, which came from ThePlanet&#8217;s network in Texas. All these tests were done between 7PM and 9PM EST and are subject to change throughout the day due to network congestion.
</p>

## Features

<p style="text-align: justify;">
  What&#8217;s a CDN without features? Well, it&#8217;s just a CDN. But hey, that&#8217;s what a CDN does, deliver content. Anything above and beyond that is an added bonus. Lets go over the various features Amazon and Rackspace have to offer.
</p>

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
    
    <th>
      GoGrid CDN
    </th>
    
    <th>
      Simple CDN
    </th>
  </tr>
  
  <tr>
    <th>
      Maximum File Size
    </th>
    
    <td>
      5GB
    </td>
    
    <td>
      5GB
    </td>
    
    <td>
      Unknown
    </td>
    
    <td>
      Unknown
    </td>
  </tr>
  
  <tr>
    <th>
      File Storage Required
    </th>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
  </tr>
  
  <tr>
    <th>
      FTP Access
    </th>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
  </tr>
  
  <tr>
    <th>
      Free Endpoint Transfer
    </th>
    
    <td>
      No
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
  </tr>
  
  <tr>
    <th>
      HTTPS
    </th>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
    
    <td>
      Yes ($299 Setup $299/Month)
    </td>
    
    <td>
      Yes (Free)
    </td>
  </tr>
  
  <tr>
    <th>
      Raw Logs
    </th>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      No
    </td>
  </tr>
  
  <tr>
    <th>
      Real Time Logging
    </th>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
    
    <td>
      Yes ($199.98 Setup $199.98/Month)
    </td>
    
    <td>
      No
    </td>
  </tr>
  
  <tr>
    <th>
      Custom CNAME
    </th>
    
    <td>
      Yes (Free)
    </td>
    
    <td>
      No
    </td>
    
    <td>
      Yes (Free)
    </td>
    
    <td>
      Yes ($5 each)
    </td>
  </tr>
  
  <tr>
    <th>
      Custom Response Headers
    </th>
    
    <td>
      Yes
    </td>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
  </tr>
  
  <tr>
    <th>
      Flash Streaming (rtmp)
    </th>
    
    <td>
      Yes
    </td>
    
    <td>
      No
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
  </tr>
  
  <tr>
    <th>
      Windows Media (mms)
    </th>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
    
    <td>
      Yes
    </td>
    
    <td>
      Yes
    </td>
  </tr>
  
  <tr>
    <th>
      Torrent Support
    </th>
    
    <td>
      S3 Only
    </td>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
    
    <td>
      No
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  GoGrid also offers live streaming, allowing you to push your live content to a rtmp server and having others tune in. GoGrid charges you their standard rate for how much bandwidth you use, however, SimpleCDN charges you a flat monthly fee for Live services starting at $59 a month for 250 concurrent views and going up from there. On the plus side, there is no bandwidth charges for their Live services, and no limit to the video bitrate. You would have to do the math to determine if GoGrid or SimpleCDN would be more cost-effective for you. Chances are if you plan to do a lot of streaming, or stream high-definition content, SimpleCDN might be the better  bet for you.
</p>

<p style="text-align: justify;">
  GoGrid and SimpleCDN offer something else that Rackspace and Amazon don&#8217;t, the ability to map a CDN URL to your server. What I mean is, instead of uploading files to GoGrid and SimpleCDN and having to pay monthly storage costs, you could just host the files on your server and use what they call Customer Origin/Mirror Buckets. After you map one of these to a URL where you keep all of your files, requests to the file through the CDN url will cause that end point to fetch the data from your own server and cache it for future requests. You&#8217;ll be able to get the same CDN delivery speed with none of the CDN storage costs.
</p>

<p style="text-align: justify;">
  Using Amazon Cloud Front requires an Amazon S3 account. Having an S3 account means you can use its torrent feature. If you add &#8220;?torrent&#8221; to the end of any S3 URL, the server will return a .torrent file instead of the file requested. This is especially great for large files since you will have other users helping you out with distribution, lowering your bandwidth cost. The torrent uses Amazons&#8217; tracker and their S3 machines are seeding the file. This way your torrent will never die, so long as the file remains on the S3 servers. Once again, while this isn&#8217;t a feature of their CDN service, it&#8217;s still a feature of S3, which is required to use their CDN service. If it&#8217;s streaming video you want, then GoGrid CDN or SimpleCDN is the choice for you. Both offer Windows Media and Flash Streaming services for your content. Using these will allow users to fast forward through your video without having to wait for it to load to that point. GoGrid also offers a way to throttle bandwidth usage. This is especially useful and can save you a ton on bandwidth costs. Limiting the users bandwidth will allow the video to buffer and offer a constant viewing experience, however, it will prevent the entire video from buffering too quickly. This way, if the user decides they do not wish the watch the entire video, you won&#8217;t have to pay for the bandwidth of the entire video, only that which has been buffered.
</p>

## Conclusion

<p style="text-align: justify;">
  GoGrid CDN is still in beta and is relatively new. However, it&#8217;s proven so far to have very low response times like Rackspace Cloud Files. While GoGrid wasn&#8217;t as fast as Amazon Cloud Front, it was still in second place and achieved very high speeds. SimpleCDN used to be a great CDN service, giving users streaming capabilities with their media. However, now with GoGrid CDN stepping up to the plate with the same streaming services as SimpleCDN, it looks like it&#8217;s taken the lead. The great thing about pay-as-you-go CDN networks is that you can use them all, and not have to pay  large monthly fees. For example, I&#8217;m using GoGrid CDN to deliver streaming video content, while using Amazon Cloud Front to deliver my static content. It all comes down to what you need. And if you need to stream live high-definition content to thousands of people at the same time, well then SimpleCDN just might be the best thing for you. Each CDN has their own features, and it&#8217;s up to you to decide exactly what you need. With pay-as-you-go services, you really have nothing to lose but your time.
</p>

### <span style="color: #ff0000;">Update (December 17, 2009)</span>

I&#8217;m in the process of adding 2 more CDN networks to the charts along with different tests (i.e. rtmp streaming, downloading many small images, and anything else I can think of). A new article will be posted with the new test results along with pretty charts and graphs!