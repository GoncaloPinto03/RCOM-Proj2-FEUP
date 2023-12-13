!!! MUDAMOS DE BANCADA PARA A 4!!!

tux42 -> 172.16.41.1, 00:1f:29:d7:45:c4
tux43 -> 172.16.40.1, 00:21:5a:61:2f:d4
tux44 -> eht0 -> 172.16.40.254, 00:21:5a:5a:7b:ea
tux44 -> eth1 -> 172.16.41.253, 00:c0:df:25:1a:f4

ehter21 é o tux43 adicionamos bridge40

ehter23 é tux44 adicionamos bridge40
ether17 é tux44 adicionamos bridge41

ether19 é tux42 adicionamos bridge41

eth1 do tux44 está ligado a bridge41
eth0 do tux44 está ligado a bridge40


no tux43 `route add default gw 172.16.40.254`
no tux42 `route add default gw 172.16.41.253`


No tux43
`ping 172.16.40.254` e funcionou
`ping 172.16.41.253` e funcionou
`ping 172.16.41.1` e funcionou

Ligamos eth1 do Router à porta 4.1 da régua

Ligamos eth2 do Router ao Switch

Eliminamos as portas default do ether9 do switch e ligar o ether9 à bridge41

`/interface bridge port remove [find interface=ether9]`

`/interface bridge port add bridge=bridge41 interface=ether9`

Depois disto demos reset às configurações do router.

`/system reset-configuration`

Configuração dos endereços IPs do Router

`/ip address add address=172.16.1.29/24 interface=ether1`

`/ip address add address=172.16.41.254/24 interface=ether2`

Adicionamos as rotas para o Router:

`route add default gw 172.16.40.254 # Tux43`
`route add default gw 172.16.41.254 # Tux42`
`route add default gw 172.16.41.254 # Tux44`

`/ip route add dst-address=172.16.40.0/24 gateway=172.16.41.253  # Router console`

`/ip route add dst-address=0.0.0.0/0 gateway=172.16.1.254        # Router console`

Desativamos o accept_redirects:

`echo 0 > /proc/sys/net/ipv4/conf/eth0/accept_redirects`

`echo 0 > /proc/sys/net/ipv4/conf/all/accept_redirects`

Removemos a rota que liga o tux42 ao tux 44

`route del -net 172.16.40.0 gw 172.16.41.253 netmask 255.255.255.0`

No tux42 fizemos traceroute ao tux43:

`traceroute -n 172.16.40.1`

Voltamos a adicionar a rota que liga o tux42 ao tux44 e voltamos a fazer traceroute

`route add -net 172.16.40.0 gw 172.16.41.253 netmask 255.255.255.0`

`traceroute -n 172.16.40.1`

Voltamos a reativar o accept_redirects:

`echo 0 > /proc/sys/net/ipv4/conf/eth0/accept_redirects`

`echo 0 > /proc/sys/net/ipv4/conf/all/accept_redirects`

Ping do router da sala I321

`ping 172.16.1.254`

Desativar NAT do Router

`/ip firewall nat disable 0`

Ping do router da sala I321

`ping 172.16.1.254`

Reativar NAT do Router

`/ip firewall nat enable 0`

# How to configure a static route in a commercial router?
Reset its settings, add it to the internal network (to the corresponding bridge), and assign an internal IP and an external IP.

# What are the paths followed by the packets in the experiments carried out and why?
In the first experiment, without the connection from Tux52 to Tux54, the data packets were redirected (ICMP redirect) through the implemented router to the destination IP address.
In the second experiment, there was no redirection because the shortest connection in the network was available.

# How to configure NAT in a commercial router?
With the command /ip firewall nat enable 0 in the router's terminal.

# What does NAT do?
NAT (Network Address Translation) translates addresses from the local network to a single public address, and vice versa. Thus, when a packet is sent to an external network, it is sent with the public address as the source. When the destination computer responds, it sends the response to that public address, which is then translated back to the local address of the destination that originally sent the packet. This way, it is possible to reduce the number of public addresses used.
