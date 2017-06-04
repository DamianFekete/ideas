# Personal notes
* Can be used without JFFS, don't specify addn-hosts
   addn-hosts=/jffs/etc/hosts.home
Reboot host machine too, not only guest machines (in case of VirtualBox machines)


[Source](https://unfinishedbitness.info/2013/03/26/using-dd-wrt-for-local-dns-and-dhcp/ "Permalink to Using DD-WRT for Local DNS and DHCP")

# Using DD-WRT for Local DNS and DHCP

![English: Screenshot of DD-WRT v24 SP2 mini bui...][1]

English: Screenshot of DD-WRT v24 SP2 mini build running on a Linksys WRT160N. MAC address and WAN IP blanked out. (Photo credit: Wikipedia)

I've been slowly feeding you information on how to get the most out of the open-source [DD-WRT][2] router firmware.

In this article I'll show you how to setup DD-WRT to act as a local name server on your home network and as a forwarder for external requests.  This will let you lookup names on your internal network (like xbox360, bluray, printer, etc) and continue to lookup names for external sites (like , , , etc).

Before you begin you should have already enabled JFFS.  I showed you how here: [Enable JFFS on DD-WRT][3]

## Enable DNS and DHCP

First you need to enable Local [DNS][4] and [DHCP][5].  This turns on [DNSMasq][6] (built into DD-WRT) to do local network name resolution and distribute IP addresses via DHCP.  Pooled addresses get used and released via timed leases (devices using a pooled address may not always get the same IP address).  Static Addresses entered in the DHCP options are respected by DNSMasq and issued to the devices when they connect and request an IP address (devices using static addresses always get the same IP address).  Use a static address for devices that will never need to change, like your printer or a desktop computer.

* Open a browser and point it to your router running DD-WRT.  Authenticate with the admin ID and password when needed.
* Go to the "Setup > Basic Setup" tab.
* In the "Network Setup > Router IP" section, enter the following details:
    
```    
    Local DNS = 0.0.0.0
```
* In the "Setup > Basic" tab, in the "Network Address Server Settings (DHCP)" section, set the following options:
```
    DHCP Type = DHCP Server
    DHCP Server = Enable
    Start IP Address = Whatever you want
    Maximum DHCP Users = However big a pool you want. Do not overrun subnet!
    Client Lease Time = 1440
    Static DNS Addresses: 192.168.64.1, 208.67.220.220, 208.67.222.123
    WINS = 0.0.0.0
    Use DNSMasq for DHCP = Enable
    Use DNSMasq for DNS = Enable
    DHCP Authoritative = Enable
```
Note:  The Static DNS Addresses will be different for your network.  In this case I have set the address of the router itself (192.168.64.1) – fill in your routers address here (not the WAN one), and two [OpenDNS][7] name servers (208.67.220.220 and 208.67.222.123).  I'll talk about OpenDNS in another post, but what these do is filter websites based on my custom criteria (*.220.220).  In the event that server does not respond in a timely manner, the request then goes to a more restrictive pre-configured filter supplied by [OpenDNS FamilyShield][8] (*.222.123).  The filtering effectively blocks access to sites deemed inappropriate.

* In the "Services Management > DHCP Server" section, set the following options.  In this example I use "home.net" as the home network identifier.   You can replace "home" with whatever your like.  You can replace ".net" with a few different choices.  Home networks are most closely categorized into ".net" or ".info".  If you are not registering a domain name to point to your WAN IP address, you can use whatever you want including ".com" or ".mil".  You can, but don't – home networks are not commercial or military.  Further, don't use ".example", ".test", ".invalid", or ".localhost" – these are reserved.  See the following link for a list you can choose from: [top level domains][9].
    
 ```   
    Used Domain: LAN & WLAN
    LAN Domain: home
    Add any static leases you want or need.
```
* In the "Services Management > DNSMasq" section, set the following options:
    
 ```   
    DNSMasq = Enable
    Local DNS = Enable
```
* There is a field for "Addition DNSMasq Options" in the DNSMasq section.  Set it as follows:
    
 ```   
    local=/home/
    expand-hosts
    domain-needed
    bogus-priv
    addn-hosts=/jffs/etc/hosts.home
    strict-order
```
You may find these options useful as well:  
no-poll : (may be useful to reduce system load on non embedded as well)  
no-hosts : (we're not going to read from any system generated hosts file on a ram disk) (for this configuration DO NOT set this!)

* Click "Apply Settings", then "Save".

## Create Static Hosts File

Now you need to create a hosts file that will be persistent across reboots for those devices which are you want using static IP addresses (like printers, routers, etc).

* ssh into the router and login as root.
* Change directory to jffs/etc: "cd /jffs/etc"
* Create and edit the file "hosts.home" using vi (vi hosts.home).
* Add the entries and save the file (with "ESC Z Z" or ":w!:q!".  Entry formats are "xxx.xxx.xxx.xxx name" where xxx.xxx.xxx.xxx is the IP address you want to reserve and name is the device name you want referenced as.  Multiple names can be given, just enter them all on the same line separated by a space (xxx.xxx.xxx.xxx name1 name2 etc).

## Reboot

Reboot the router by going to the "Administration > Management" tab in the browser interface.  Scroll to the bottom and click the "Reboot Router" button.

If all goes well, you should be able to lookup names on your network like "xbox360" or "xbox360.home" and get a result, as well as normal internet name resolution for external sites like "www.apple.com".

If you can not resolve local names, you may need to release and re-acquire the IP and DNS information on the host your trying to resolve from.  The easiest way is to just reboot it as well.

Note: Netflix on iOS devices causes DNSMasq to think a DNS rebind attack is occurring and by default an option in DNSMasq is forcibly set that you can not override in the GUI. A special workaround is needed to remove that option when DNSMasq starts.  I showed you how to fix rebind here: [Fixing DNS Rebind on DD-WRT][10]


[1]: https://i2.wp.com/upload.wikimedia.org/wikipedia/commons/thumb/f/fa/Ddwrtv24rc7.png/300px-Ddwrtv24rc7.png "English: Screenshot of DD-WRT v24 SP2 mini bui..."
[2]: http://www.dd-wrt.com/site/index "DD-WRT"
[3]: https://unfinishedbitness.wordpress.com/2013/02/24/enabling-jffs-on-dd-wrt/ "Enable JFFS on DD-WRT"
[4]: http://en.wikipedia.org/wiki/Domain_Name_System "DNS"
[5]: http://en.wikipedia.org/wiki/DHCP "DHCP"
[6]: http://www.thekelleys.org.uk/dnsmasq/doc.html "DNSMasq"
[7]: http://www.opendns.com "OpenDNS"
[8]: http://www.opendns.com/home-solutions/parental-controls/ "OpenDNS Family Shield"
[9]: http://en.wikipedia.org/wiki/List_of_Internet_top-level_domains "Top Level Domains (TLD)"
[10]: https://unfinishedbitness.wordpress.com/2013/03/04/fixing-dns-rebind-on-dd-wrt/ "Fixing DNS Rebind on DD-WRT"
