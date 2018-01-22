+++
title = "WiFi Down (Or how 802.1x stopped working)"
date = 2013-01-06T23:48:22Z
categories = ["Cisco"]
tags = [ "802.1x", "AAA", "ACS", "Certificate", "PEAP", "RADIUS", "WLC" ]
+++
Around this time last a year 802.1x was configured on our wireless network. Everything worked fine for the most part until this morning. All wireless devices on the SSID configured for 802.1x were failing to connect. Non 802.1x SSID's were fine, so it wasn't an issue with the wireless access point being down. Additionally the network was being broadcast across multiple physical locations in different states and they all seemed to be down. Since no changes were made to the Cisco Wireless LAN Controller it must be an issue outside of the individual access points.

Taking a look at the RADIUS logs on the Cisco ACS yields this Christmas colored mess:

{{< figure src="/images/2013/01/RADIUS-Auth-Failures.png" caption="The first authentication failure occurs at 10:05:40AM" alt="RADIUS log on a Cisco ACS showing an increasing number of authentication fails" title="RADIUS Auth Failures" >}}

To put that in comparison, here's one page before and one page after the incident.

{{< figure src="/images/2013/01/RADIUS-Auth-Success.png" caption="Just before" alt="RADIUS log on a Cisco ACS showing successful authentications" title="RADIUS Auth Success" >}}

{{< figure src="/images/2013/01/RADIUS-Auth-Errors.png" caption="Just after" alt="RADIUS log on a Cisco ACS showing mostly authentication failures" title="RADIUS Auth Errors" >}}

The Failure Reason reads: "<span style="color: #F00;">11514 Unexpectedly received empty TLS message; treating as a rejection by the client</span>"

Clicking on the message gives us some very useful information:

| Description |
|:-------------|
| While trying to negotiate a TLS handshake with the client, ACS expected to receive a non-empty TLS message or TLS alert message, but instead received an empty TLS message. This could be due to an inconformity in the implementation of the protocol between ACS and the supplicant. For example, it is a known issue that the XP supplicant sends an empty TLS message instead of a non-empty TLS alert message. <b>It might also involve the supplicant not trusting the ACS server certificate for some reason</b>. ACS treated the unexpected message as a sign that the client rejected the tunnel establishment.

| Resolution Steps |
|:-------------|
| Ensure that the supplicant of the client does not have any known compatibility issues and that it is properly configured.<b>Also ensure that the ACS server certificate is trusted by the client</b>, by configuring the supplicant with the CA certificate that signed the ACS server certificate. It is strongly recommended to not disable the server certificate validation on the client!

I've put in bold the relevant parts of the message. Remember when I mentioned we set this up about a year ago? After putting two and two together I realize the certificate we're using more than likely expired.

I head on over to System Administration > Configuration > Local Server Certificates > Local Certificates and I take a look at the certificate being used for EAP and that's when I notice the following:

| Key                    | Value            |
|:-----------------------|:-----------------|
| Valid From:            | 20:23 16.01.2012 |
| Valid To (Expiration): | 15:06 07.12.2012 |

Adjust the time zone offset and what do you get? Authentication errors starting at exactly the same time the certificate expired. Go figure.

A simple re-issuing of the certificate corrected the issues and clients were once again able to connect to networks using 802.1x.