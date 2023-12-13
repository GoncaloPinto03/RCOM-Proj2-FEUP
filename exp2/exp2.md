tux12 -> 172.16.11.1
tux13 -> 172.16.10.1
tux14 -> 172.16.10.254

sysctl net.ipv4.icmp_echo_ignore_broadcasts=0

# How to configure bridgeY0?
Firstly we created the bridge10 and bridge11 using the commands <br>
`interface add bridge name=bridge10`
`interface add bridge name=bridge10`

Secondly we removed the default connections and configurations from the switch using the commands <br> `interface brigde port remove [find interface=etherXX]`

We then added the new ports, that we previously connected via the switch, to the correct bridges using the command <br> 
`bridge port add bridge=bridge10 interface=ether21`
`bridge port add bridge=bridge10 interface=ether23`
`bridge port add bridge=bridge11 interface=ether19`

# How many broadcast domains are there? How can you conclude it from the logs?
There are two domain broadcats because of the two bridges we created. Since tux13 and tux14 are connected to the bridge10 they can communicate but since tux12 is connected to bridge11 it can't communicate with tux13 and tux14. Knowing that the ping from tux13 reached tux14 but didn't reach tux12 because they are not in the same bridge/domain.