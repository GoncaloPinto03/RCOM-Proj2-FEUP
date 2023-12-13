tux12 -> 172.16.11.1
tux13 -> 172.16.10.1
tux14 -> eht0 -> 172.16.10.254, 00:c0:df:25:13:65 
tux14 -> eth1 -> 172.16.11.253, 00:21:5a:5a:7b:3f

ehter21 é o tux13 adicionamos bridge10

ehter23 é tux14 adicionamos bridge10
ether17 é tux14 adicionamos bridge11

ether19 é tux12 adicionamos bridge11

eth1 do tux14 está ligado a bridge11
eth0 do tux14 está ligado a bridge10

no tux13 `route add default gw 172.16.10.254`
no tux12 `route add default gw 172.16.11.253`


No tux13
`ping 172.16.10.254` e funcionou
`ping 172.16.11.253` e funcionou
`ping 172.16.11.1` e funcionou


tux14 `arp -d 172.16.10.1`
tux14 `arp -d 172.16.11.1`

tux13 `arp -d 172.16.10.254`

tux12 `arp -d 172.16.11.253`


do tux13 pingamos tux12 `ping 172.16.11.1`


# What are the commands required to configure this experience?

# What routes are there in the tuxes? What are their meaning?
There are two routes, one in tux12 and other in tux13. They have has gateway tux14 because it is common between the two bridges created.

# What information does an entry of the forwarding table contain?
Each entry has the destination and respective gateway.

# What ARP messages, and associated MAC addresses, are observed and why?
Even though the ping is from Tux13 to Tux12, the exchanged ARP packets contain only the MAC addresses of Tux13 and Tux14, not the final destination. This is due to the route implementation. Tux13 is not aware of the address of Tux12; it only knows the address of the gateway (Tux14) that leads to Tux12.

# What ICMP packets are observed and why?

# What are the IP and MAC addresses associated to ICMP packets and why? 