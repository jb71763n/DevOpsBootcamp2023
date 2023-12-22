 # Networking Basics

 - Switching
 - Routing
 - Default Gateway
 - DNS on Linux

## Switching

 - 'ip link' = see the network interface on the linux host
 - 'ip addr add IPADDR/CIDR dev NETWORKINTERFACE' = Add static IP to Linux network interface
```sh
ip addr add 192.168.1.10/24 dev eth0
``` 
Two network interfaces connected to a switch with IP addresses in the same CIDR range can connect to each other and other systems within the same network.

## Router

A router helps connect two or more networks

![Router and Gateway](/Journals/images/BasicRouting.png)

A Gateway is an address on the local network that can route to another network. 

- 'route' = to see the existing routing configuration on a server
- 'ip route add CIDR via GATEWAYIP' = create gateway route to new network
```sh
ip route add 192.168.2.0/24 via 192.168.1.1
```
To setup a route to any unknown network, configure a default gateway
```sh
ip route add default via 192.168.2.1
```

default = 0.0.0.0

If you have separate routers for internal and external networks (Internet), you will need to configure multiple gateways.

By Default in Linux, packages are not forwarded between networks. If both networks are considered "Safe" you can enable port forwarding. 

To persist these changes, you must make them in the /etc/networkinterfaces file

```sh
cat /proc/sys/net/ipv4/ip_forward
0
```

Set the value to 1 enables forwarding. 

In order for this to persist across reboots, the value must also be changed in /etc/sysctl.conf

## DNS

Name Resolution - /etc/hosts file contains pairs of names and IP addresses.

Domain Name System - used to lookup hostname to IP address

Set the DNS name servers in the /etc/resolv.conf file

```sh
cat /etc/resolv.conf
nameserver   192.168.1.100
```

You can still use HOSTS files for name resolution, by default, entries in the hosts file will be used before DNS lookup. This behavior can be changes using the /etc/nsswitch.conf file

DNS servers can be set to forward requests to other DNS servers

### Domain names 
Common top level domain names on the Internet
- .com
- .net
- .edu
- .org
- .io

1. root level is '.'
2. Top level domain ie. '.com'
3. domain name ie. 'google'
4. subdomain ie. 'www', 'maps', 'mail', 'drive', etc.

So www.google.com represents a hiearchy of DNS names, each with its own authoritative name resolution 

When you request an Internet address, the process is as follows:

1. Your organization DNS is the first one used, it forwards your request to the root DNS server for resolution if it doesn't have an entry
2. The Root DNS server will forward to the .com DNS server for resolution
3. The .com DNS server will forward to the google authoritative DNS server for resolution
4. Eventually the name is resolved to an IP which is passed to the requestor. Depending on the configuration of the DNS servers in the request path, the IP address may be cached for some period of time to speed up requests in the near future for the same name. 

Internally you may not want to query on the FQDN and instead only use a server name. You can configure default domain(s) to append to the request

Record types 
- A = IPv4 Primary DNS record
- AAAA = IP V6 primary DNS record
- CNAME = Alias record for a primary to abstract the server from the name used to connect.

### DNS Tools
nslookup - used to query the name server. Note that nslookup does not use hosts files so in a troubleshooting scenario, nslookup does not show issues with hosts entries.

dig - allows you to query DNS servers and perform DNS lookups. You can also find the domain an IP address leads back to (reverse lookup)







