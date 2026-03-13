# Model Comparison

OSI Model

| layer | name         | examples                                         | PDU      |
| ----: | ------------ | ------------------------------------------------ | -------- |
|     7 | application  | http, ssh, ftp, smtp                             |          |
|     6 | presentation | ssl, tls, encryption, serialization, compression |          |
|     5 | session      | client-server state                              |          |
|     4 | transport    | tcp, udp, ports                                  | segments |
|     3 | network      | ip, icmp, data packets                           | packets  |
|     2 | data-link    | mac, llc                                         | frames   |
|     1 | physical     | ethernet, nic                                    | bits     |

TCP/IP Model

| layer | name        | OSI layer |
| ----- | ----------- | --------- |
| 4     | Application | 5, 6, 7   |
| 3     | Transport   | 4         |
| 2     | Internet    | 3         |
| 1     | Network     | 1, 2      |

# OSI Breakdown

## Layer 1

Radio waves
Optic cables
Electricity

Cross over cables
```
connects two devices
```

Hubs
```
connects multiple devices
```

## Layer 2

Switches
```
connect devices within LAN
```

Access Points
```
a sub router that connects a WLAN to LAN
```

Mesh
```
a node in a unified network (usually WIFI), to help with dead zones by providing wider coverage
```

Backplane
```
connection between ports in a switch
```

## Layer 3

ARP
```
maps IP addresses with MAC addresses
```

Gateway/Router
```
connect devices within different networks (LAN <-> LAN or LAN <-> WAN)
```

LAN/WAN/Internet
```
LAN -> devices within the same private network
WAN -> LANs within the same private/public network
Internet -> the public network
```

Data Packets

IP forwarding
```
used for passing packets from one network to another
```

Routing table
```
mapping of a network(IP address ranges) to a gateway that is used by a router
```

Anycast/Global Anycast

| Feature        | Anycast                                                 | Global Anycast                                            |
| -------------- | ------------------------------------------------------- | --------------------------------------------------------- |
| Network Scope  | Generally local or regional                             | Global                                                    |
| Infrastructure | May use a variety of networks                           | Typically utilizes a CDN or global network infrastructure |
| Latency        | Can vary depending on network conditions                | Generally very low due to global distribution             |
| Availability   | May have limitations based on provider's infrastructure | High global availability                                  |
| Complexity     | Can be more complex to implement                        | Typically requires less configuration from the user       |

## Layer 4

Subnet mask
>[!hint]
using octets give more granular control over host bits over CIDR
```
0.0.0.0 -> /0
255.0.0.0 -> /8
255.255.0.0 -> /16
255.255.255.0 -> /24
255.255.255.255 -> /32

Ranges with CIDR:
192.168.0.1/24 -> 192.168.0.1 .. 192.168.0.255
192.168.0.1/16 -> 192.168.0.1 .. 192.168.255.255
192.168.0.1/8 -> 192.0.0.1 .. 192.255.255.255
192.168.0.1/0 -> 0.0.0.0 .. 255.255.255.255
```

Commonly used ports
>[!info]
>these ports are mapped to layer 7 of the OSI model. Meaning, the ports are used at layer 4, but the protocols are defined at layer 7
```yaml
HTTP: 80
HTTPS: 443
SSH: 22
FTP: 20
SMTP: 25
DNS: 53
RDP: 3389
RTMP: 1935
```

DHCP
BGP
OSPF
Port forwarding

NAT
```
outbound routing to another network(LAN/WAN/internet)
```

# Forwarding Rules

DMZ
Port Trigger
Port Mapping