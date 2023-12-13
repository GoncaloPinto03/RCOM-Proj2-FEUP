Same configuration as exp4 (same PC)

Run `nano /etc/resolv.conf` on all tux, and added a `nameserve: 8.8.8.8`.

# How to configure the DNS service in a host?
DNS can be configured by adding the line "nameserver <IP>" to the /etc/resolv.conf file on all present Tux.

# What packets are exchanged by DNS and what information is transported
The packets exchanged over the network are initially of the DNS type, allowing the router to identify and translate the destination IP address.
