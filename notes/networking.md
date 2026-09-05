


### Network:

```192.168.0.0/16```

//
### Subnet: 

```
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

//


## ICMP

**Internet Control Message Protocol**

It is used to communicate error information or updates between network devices. 
For example `ping` and `traceroute` use ICMP messages to collect latency information or locate the source of a network delay.

ICMP can be exploited to perform DOS (Denial Of Service) attacks. 
Here are some example uses:
- **ping sweep**


- **ping flood**

- **smurf attack** (Attacker spoofs victims IP, sends a huge amount of ICMP echo request messages to a network's broadcast address¹. Many hosts on that network will reply with ICMP echo replies to the target. This huge amount of information will overwhelm the victim with traffic causing a DOS.)

¹*broadcast address: a broadcast address is an IP address used to send a packet to every host on a local subnet at once* 

