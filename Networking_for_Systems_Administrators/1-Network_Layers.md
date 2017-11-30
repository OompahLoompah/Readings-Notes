# Networking for Systems Administrators

## Chapter 1: Network Layers
- Physical
    - The actual physical thing which transports signals
- Datalink
    - Transforms the upper layers into signals.
    - Usually uses the ethernet protocol but can use other transmission protocols
    - Includes MAC (IPv4) and Neighbor Discovery (IPv6)
    - Single lump of data is called a frame
- Network
    - Maps connectivity between hosts (IP addresses live in this layer)
    - Lowest, but not only, layer NAT works at.
- Transport
    - ICMP
    - TCP
    - UDP
- Everything else
    - Session
    - Presentation
    - Application