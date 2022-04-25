# Synproxy Research

What is a syn proxy? 

SYN Proxies are very good at doing their jobs syn proxys intercept the 3 way handshake and instead of using contrack connection it uses SYN Cookies thus preventing most SYN Floods this prevents resource usage from connection tracked.  The SYNPROXY receives the SYN-ACK and responds to the server with an ACK. Now, the connection is marked as an Established connection. 
FIlter-Firewall marks the packet as UNTRACKED which is given to SYNPROXY. In conclusion proxies TCP handshakes before handing them to the server.

![Syn_Proxy](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.heise.de%2Fsecurity%2Fimgs%2F07%2F6%2F9%2F2%2F5%2F0%2F0%2Fscreenshot-26Jul11-474661983-b1d2024e5f075d55.png&f=1&nofb=1)


# Syn Proxy Paramaters 
MSS 1460 (MAX)
WS (Unassigned) 
timestamp (pass client time)
sack (pass client ACK to backend) 
Total bits: 26 (Per pass)

![Syn_Proxy_BIT_LENGTH](https://i.imgur.com/tDoG50s.png)


# How we mitigate 200 gb/s TCP DDos attacks.
Intelligence Hosting - Here at Intelligence Hosting we mitigate up to tb/s worth of DDos attacks and help against many other exploits like RCE injection you can contact us @ Ohiocloud.net 

![Providers](https://cdn.discordapp.com/attachments/957362982248153179/968006391111487538/unknown.png)


# Setup
```
// (If want different ports / interface change them)
iptables -t raw -I PREROUTING -i eth0 -p tcp -m tcp --syn --dport 22 -j CT --notrack



sysctl -w net.netfilter.nf_conntrack_tcp_loose=0
sysctl -w net.ipv4.tcp_timestamps=1

// (If want different ports / interface change them)
iptables -A INPUT -i eth0 -p tcp -m tcp --dport 22 -m state --state INVALID,UNTRACKED -j SYNPROXY --sack-perm --timestamp --wscale 7 --mss 1460
iptables -A INPUT -m state --state INVALID -j DROP


```

## Performance
| Attack | Max PPS |
|--|--|
| SYN flood | 2,869,824 PPS |
| SYN-ACK flood | 5,653,120 PPS |
| ACK flood | 4,948,480 PPS |

