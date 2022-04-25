
#Openvpn Reset Floods


The affects of Openvpn reset flooding

```
The attacker only needs to send little sized packets of OPENVPN for it to register a RESET Client packet this is 
what openvpn does when theUSERS keydata is not accepted from the openvpn server. The openvpn is basically doing 
RST (Reset Client Protcol) which validate only for connections using the TCP Keep Alive option. The keep alive 
packets were not responded to in the designated ttl. In conclusion this causes many problems like blocking 
legitmate openvpn traffic / lagging it. 
```

![Affects of Openvpn_Reset_floods](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fwww.identity-theft-scout.com%2Fimages%2FUDP-Flood.png&f=1&nofb=1)

What are ways to patch this method?

```
hostings not affected this
Ohiocloud.net (Truely Magic Mitigation, EBPF, XDP, Transit-Line based Mitigation without blocking legitmate traffic.)
path.net (Ebpf XDP filtering that doesn't block legitmate traffic)

DDos protection companys vulnerable:
OVH (without applied fw rules)
NFO (without applied fw rules)
Hydra (without applied fw rules)

```
![Providers](https://cdn.discordapp.com/attachments/958886784245313567/968003640356929536/unknown.png)

We stop large volumetric udp based floods @ Ohiocloud.net

```
Netfilter
XDP /EbpF
```
![Ebpf / XDP_FILTER](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fblog.cb.dev%2Fcontent%2Fimages%2F2019%2F09%2Fimage.png&f=1&nofb=1)


Apply This Netfilter rule to help mitigate from OPENVPN resets 
```
Drop high udp lengths: 

iptables -A PREROUTING -t raw -p udp -m length --length 800:10000 -m connlimit --connlimit-above 10 -j REJECT

Limiting the amount of connections per(IP):
iptables -A PREROUTING -t raw -p udp --dport 1194 -m connlimit --connlimit-above 4 -j REJECT

```
![Summary of OPENVPN_RESET_FLOODS](https://i.ibb.co/fMCgb6V/3.jpg)
