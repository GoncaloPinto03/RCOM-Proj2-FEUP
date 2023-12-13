tux 13:
ip address : 172.16.10.1
mac address : ether -> 00:21:5a:5a:7d:16

tux 14:
ip address : 172.16.10.254
mac address : ether -> 00:c0:df:25:13:65

# What are the commands required to configure this experience?
`ifconfig` and `route`.

# What are the ARP packets and what are they used for?
ARP (Address Resolution Protocol) is used to map an IP address to a physical MAC address on a local network.
Device A sends a request packet to find the MAC address associated to an IP address in the local network.
Device B recognizes it's IP address and sends back an ARP reply packet containing it's MAC address.
Device A receives the reply, updates its ARP cache with the MAC address of Device B, and can now send data packets to Device B using the MAC address.

# What are the MAC and IP addresses of ARP packets and why?
The destination machine's IP (172.16.10.254, tux14) and the source machine's IP (172.16.10.1, tux13) in the same ARP packet. In response, tux14 sends an ARP packet to tux13 containing its MAC address, 00:c0:df:25:13:65.

# What packets does the ping command generate?
The ping command initially uses ARP packets to obtain the MAC address of the target machine based on its IP address. Once the mapping is complete, ping generates ICMP(Internet Control Message Protocol) packets for communication between devices. ICMP Echo Request packets are sent to check for connectivity, and the target responds with ICMP Echo Reply packets, confirming successful communication.


# What are the MAC and IP addresses of the ping packets?
The MAC and IP addresses of the ping packets are the tux13 and tux14 IP and MAC address.

# How to determine if a receiving Ethernet frame is ARP, IP, ICMP?
On the Wireshark program, the "Protocol" collumn indicates the type of the receiving frame. 

# How to determine the length of a receiving frame?
On the Wireshark program, the "Length" collumn indicates the size in bytes of the receiving frame. 

# What is the loopback interface and why is it important?
The loopback interface is a special network interface on a computer. It enables a device to communicate with its own network stack, allowing for local testing, diagnostics, and development. The loopback interface is commonly used to simulate network interactions without external connections and serves as a valuable tool for verifying the functionality of the network stack on a device, with this it is possible to periodically check if network connections are configured correctly.