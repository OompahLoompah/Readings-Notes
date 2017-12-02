# Networking for Systems Administrators

## Chapter 5: TCP/IP

### ICMP
- Blocking ICMP is very bad, m'kay?

### UDP
- Almost all VPNs use UDP
    - Some use VPN-specific protocols e.g. IPSec

### TCP
- stateful, connection-oriented, returns an ack for each packet received
- OS verifies integrity of datastream
- Three-way handshake
    - client send request to server
    - destination accepts request, sends back information on how to connect
    - client transmits actual data
- Four-way handshake
    - used to tear down connections

### Logical Ports
- Range from 0, 65535
- TCP ports are separate things from UDP ports

### The Services File
- lists services commonly used on machine
- Some programs use this file to determine port to connect to on server it's trying to reach

### Sockets
- Communication endpoint for processes
- IPC is an in-memory socket protocol
- In TCP/IP sockets listen for network connections
- network socket == open TCP/IP port
- network sockets can accept any number of connections (not strictly true. e.g. the linux kernel limits the number of queued requests with `net.core.somaxconn` but this is a kernel limit not a protocol limit. Other kernel limits exist as well: net.ipv4.tcp_max_syn_backlog, net.core.netdev_max_backlog, etc)

### Network Daemons and the Root User
- Privileged ports are all TCP/UDP ports below 1024
- Only root normally can open privileged ports
- Programs should NEVER listen to a port while running as root user (duh)
- programs listening to ports should only have read access to their own config files

### TCP Connection State
- Three-way handshake:
    - SYN request (SYN_SENT, Synchronization Request) sent to request connection to host
    - SYN-ACK, the server's response to the SYN request and requests synchronization with client
    - ACK the client ACKs the synchronization request
    - We need one SYN and one ACK in each direction
    - at the end connection state is ESTABLISHED
- TCP teardown:
    - both sides request and acknowledge teardown
    - states: CLOSE_WAIT, TIME_WAIT, FIN_WAIT_2, LAST_ACK
    - States may linger until timeout depending on OS

### TCP Failures
- Client or server can send `TCP reset` messages in which case the connection is immediately dropped and higher-level protocols are cut off. Client can then decide to try reconnecting if it wants

### More protocols
- supported protocols are listed usually in `/etc/protocols`
    - protocols are assigned integers