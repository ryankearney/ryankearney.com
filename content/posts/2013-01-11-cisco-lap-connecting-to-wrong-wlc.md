+++
title = "Cisco LAP Connecting to Wrong WLC"
date = 2013-01-11T23:54:04Z
description = "Dealing with a difficult access point that isn't connecting to the primary Wireless LAN Controller"
toc = false
categories = ["Cisco"]
tags = ["LAP", "SSC", "WLC"]
+++

After setting up a new Cisco Wireless LAN Controller (WLC), I decided to go ahead and setup a spare Cisco Lightweight Access Point (LAP) to connect to it. I did so by changing DHCP option 43 to point to the new WLC instead of the old one for that DHCP reservation. I plugged in the AP and... Damn, it still connected to the production WLC. I rebooted it again, and then a third time. After multiple restarts it was still connecting to the production WLC time and time again. I even went so far as to setting the LAP's primary controller to point to the new WLC. Still, it failed to register with the new WLC and instead kept hitting the production one.

That's when I remember, LAPs can use a DNS record to find the WLC they're supposed to use if it can't find one via DHCP option 43. I fire up DNS and sure enough, there are the two entries:

```plain
CISCO-CAPWAP-CONTROLLER
CISCO-LWAPP-CONTROLLER
```

Both were A records pointing to the production WLC. Since every subnet our LAPs are a part of use DHCP option 43, it wasn't completely necessary for these records to be around. Thinking that was the cause of my problems, I went ahead and removed the records. After waiting a few minutes for DNS to propagate to the other DNS servers, I rebooted the LAP one more time. This time it didn't connect to the production WLC. Success! Or was it?

The status LED began cycling through red, green, and amber. A simple Google search indicated that this indicates the LAP is searching for a controller. This went on for quite some time before I just gave up and unplugged the LAP. At this point I decide to plug a console cable into the LAP to see any log messages, something I should have probably done a while ago. After the LAP booted, this was being output to the console over and over:

```plain
    *Mar 1 00:21:57.082: %CAPWAP-3-DHCP_RENEW: Could not discover WLC using DHCP IP. Renewing DHCP IP.
    *Mar 1 00:22:00.105: %CAPWAP-3-ERRORLOG: Invalid event 38 &amp; state 2 combination.
    *Mar 1 00:22:00.208: %DHCP-6-ADDRESS_ASSIGN: Interface BVI1 assigned DHCP address 192.168.1.250, mask 255.255.255.0, hostname AP7081.0500.0000

    Translating "CISCO-CAPWAP-CONTROLLER.example.com"...domain server (172.16.50.100)

    *Mar 1 00:22:08.083: %CAPWAP-5-DHCP_OPTION_43: Controller address 172.16.50.25 obtained through DHCP
    *Mar 1 00:22:08.083: %CAPWAP-3-ERRORLOG: Did not get log server settings from DHCP.
    *Mar 1 00:22:08.173: %CAPWAP-3-ERRORLOG: Could Not resolve CISCO-CAPWAP-CONTROLLER.example.com
    Not in Bound state.
```

So it was finding the new WLC at 172.16.50.25, but for whatever reason it could not associate with it. After tinkering with the WLC and investigating even more log files, I was able to discover the WLC was rejecting the LAP because the LAP was using a Self Signed Certificate (SSC). Logging into the WLC and navigating to _Security > AAA > AP Policies_ shows an option for _Accept Self Signed Certificate (SSC)_ under _Policy Configuration_. Sure enough, checking box and allowing self signed certificates resulted in the LAP successfully connecting to the WLC.

It's worth noting I also rebooted the WLC after checking the check box to allow SSC. I'm not sure if this had any affect or if it was even necessary, but if you're encountering this problem as well and checking the box doesn't fix it, try rebooting the WLC.