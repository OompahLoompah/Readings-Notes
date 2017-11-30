# Networking for Systems Administrators

## Chapter 3: IPv4

### IPv4 Addresses:

- A broadcast domain can be within the same LAN segment or it can be bridged to other LAN segments. Do not confuse subnets with broadcast domains
- Each subnet contains a number of addresses 2^x (e.g. 2, 4, 8, 16, but not 12 addresses)
- If an ISP gives you a # of addresses that don't fit this pattern you're sharing the network with someone else.

### Netmasks and Network Size:

- Netmasks indicate size of subnet
    - Corollary: The subnet dictates the netmask
- Netmasks are defined by their length of "on" bits (11111111111111111111111100000000)
    - 255.255.255.0 is 24 bits long

### Unusable IPv4 Addresses:

- On traditional networks the first and last IP address in a subnet are unusable for protocol design reasons.
    - "Bottom" number is network address, "Top" is broadcast address
- Newer IP stacks allow the top and bottom addresses to be used but older equipment may not handle that well. Be very hesitant to use the top and bottom addresses when you even can