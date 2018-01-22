---
author: Ryan Kearney
categories:
- Cisco
date: 2013-01-06T23:48:22Z
dsq_thread_id:
- "1012103629"
guid: http://blog.ryankearney.com/?p=144
id: 144
title: WiFi Down (Or how 802.1x stopped working)
url: /2013/01/wifi-down-or-how-802-1x-stopped-working/
---

Around this time last a year 802.1x was configured on our wireless network. Everything worked fine for the most part until this morning. All wireless devices on the SSID configured for 802.1x were failing to connect. Non 802.1x SSID&#8217;s were fine, so it wasn&#8217;t an issue with the wireless access point being down. Additionally the network was being broadcast across multiple physical locations in different states and they all seemed to be down. Since no changes were made to the Cisco Wireless LAN Controller it must be an issue outside of the individual access points.

Taking a look at the RADIUS logs on the Cisco ACS yields this Christmas colored mess:<!--more-->

<div id="attachment_145" style="max-width: 626px" class="wp-caption alignnone">
  <a href="https://blog.ryankearney.com/wp-content/uploads/2013/01/RADIUS-Auth-Failures.png"><img class="size-large wp-image-145  " title="RADIUS Auth Failures" alt="RADIUS log on a Cisco ACS showing an increasing number of authentication fails" src="https://blog.ryankearney.com/wp-content/uploads/2013/01/RADIUS-Auth-Failures.png" width="616" height="338" /></a>
  
  <p class="wp-caption-text">
    The first authentication failure occurs at 10:05:40AM
  </p>
</div>

To put that in comparison, here&#8217;s one page before and one page after the incident.

<div id="attachment_146" style="max-width: 626px" class="wp-caption alignnone">
  <a href="https://blog.ryankearney.com/wp-content/uploads/2013/01/RADIUS-Auth-Success.png"><img class="size-large wp-image-146 " title="RADIUS Auth Success" alt="RADIUS log on a Cisco ACS showing successful authentications" src="https://blog.ryankearney.com/wp-content/uploads/2013/01/RADIUS-Auth-Success.png" width="616" height="423" /></a>
  
  <p class="wp-caption-text">
    Just before
  </p>
</div>

<div id="attachment_147" style="max-width: 626px" class="wp-caption alignnone">
  <a href="https://blog.ryankearney.com/wp-content/uploads/2013/01/RADIUS-Auth-Errors.png"><img class="size-large wp-image-147" title="RADIUS Auth Errors" alt="RADIUS log on a Cisco ACS showing mostly authentication failures" src="https://blog.ryankearney.com/wp-content/uploads/2013/01/RADIUS-Auth-Errors.png" width="616" height="333" /></a>
  
  <p class="wp-caption-text">
    Just After
  </p>
</div>

The Failure Reason reads: &#8220;<span style="color: #ff0000;">11514 Unexpectedly received empty TLS message; treating as a rejection by the client</span>&#8220;

Clicking on the message gives us some very useful information:

<table>
  <tr align="left" valign="middle">
    <th align="center" valign="middle">
      <div>
        Description
      </div>
    </th>
  </tr>
  
  <tr align="left" valign="middle">
    <td valign="middle">
      <div>
        While trying to negotiate a TLS handshake with the client, ACS expected to receive a non-empty TLS message or TLS alert message, but instead received an empty TLS message. This could be due to an inconformity in the implementation of the protocol between ACS and the supplicant. For example, it is a known issue that the XP supplicant sends an empty TLS message instead of a non-empty TLS alert message. <b>It might also involve the supplicant not trusting the ACS server certificate for some reason</b>. ACS treated the unexpected message as a sign that the client rejected the tunnel establishment.
      </div>
    </td>
  </tr>
</table>

<table>
  <tr align="left" valign="middle">
    <th align="center" valign="middle">
      <div>
        Resolution Steps
      </div>
    </th>
  </tr>
  
  <tr align="left" valign="middle">
    <td valign="middle">
      <div>
        Ensure that the supplicant of the client does not have any known compatibility issues and that it is properly configured.<b>Also ensure that the ACS server certificate is trusted by the client</b>, by configuring the supplicant with the CA certificate that signed the ACS server certificate. It is strongly recommended to not disable the server certificate validation on the client!
      </div>
    </td>
  </tr>
</table>

I&#8217;ve put in bold the relevant parts of the message. Remember when I mentioned we set this up about a year ago? After putting two and two together I realize the certificate we&#8217;re using more than likely expired.

I head on over to System Administration > Configuration > Local Server Certificates > Local Certificates and I take a look at the certificate being used for EAP and that&#8217;s when I notice the following:

<table>
  <tr>
    <td>
      Valid From:
    </td>
    
    <td align="left">
      20:23 16.01.2012
    </td>
  </tr>
  
  <tr>
    <td>
      Valid To (Expiration):
    </td>
    
    <td align="left">
      15:06 07.12.2012
    </td>
  </tr>
</table>

Adjust the time zone offset and what do you get? Authentication errors starting at exactly the same time the certificate expired. Go figure.

A simple re-issuing of the certificate corrected the issues and clients were once again able to connect to networks using 802.1x.