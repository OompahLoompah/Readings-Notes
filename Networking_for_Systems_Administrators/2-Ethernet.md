# Networking for Systems Administrators

## Chapter 2: Ethernet

Frames:
- minimum frame sizes to allow checksumming of frames without new frames coming in too quickly overloading the system
- minimum frame size also prevents collisions... somehow
    - RESEARCH ME
- Maximum frame size (MTU - Maximum Transmission Unit) prevents any one interface from hogging the connection transmitting an endless frame
- Default MTU is 1500 bytes

Address Resolution Protocol:
- ARP maps ethernet addresses to IPv4 addresses
- MAC - IP address pairs are cached in arp cache
    - If a host's MAC address changes connections can fail until after ARP cache expires and the MAC address responsible for a given IP can be re-requested
    - ARP failover allows multiple hosts to share a MAC/IP address pair. When the primary host fails a secondary can take over the MAC address and IP address in a "live-failover"

Neighbor Discovery:
- Responsible for mapping MAC to IPv6 addresses
- Similar to ARP but entries in the cache table can be more than just present or missing. 
    - Reachable: currently live on network
    - Stale: Were live but have expired from cache
    - Permanent: Either local addresses or special, always-present addresses
    - Failed: Addresses which were looked for but not found

VLANs:
- Ethernet frames have an extra tag added designating which LAN they belong on
    - Without this tag frames are assumed to belong to default LAN when they reach network card
- VLANs are identified by an assigned integer 1 - 4096
- Hosts can use virtual interfaces to manage VLANs, each of which has its own IP configuration
- VLANs often described as 802.1Q

- Most common datalink errors are:
    - Drops
    - Overruns
    - Frame Errors
    - Collisions
    - These errors reduce performance but won't necessarily bring the link down.
        - Unix: use `netstat -i` to view total count of these errors since boot and other stats
 