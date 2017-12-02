# Networking for Systems Administrators

## Chapter 8: the Domain Name System

### Domains and Zones
- A zone within a zone is a child zone
- subdomains are zones
- test.com is a child zone of .com, home.test.com is a child zone of test.com
- .com is a child zone of the root zone
- root zone is managed by NTIA... for now

### The DNS Heirarchy
- DNS lookup progression
    1. Client contacts its recursive nameserver and requests IP address
    2. recursive nameserver consults its list of root nameservers and contacts one to request the information
    3. root server can provide address of nameservers responsible for the child zone (e.g. .com)
    4. our client's nameserver contacts the new nameserver requesting the information.
    5. New server returns the next child zone (e.g. test.com)
    6. repeat until we get the proper records or the nameserver we query has no further information
    7. ...or the information is cached already on one of these nameservers and it returns the proper records

### DNS Record Types
- PTR record provides a hostname. Reverse DNS _mostly_ uses PTR records. Service Discovery and ZeroConf also use PTR records
- SOA (Start of Authority) record gives timing and responsibility information for zone you're searching and provides information such as how long to cache entries in this zone and who to contact for problems with the domain.
- CNAME (Canonical Name) DNS alias which redirects you from one name to another

### Running DNS Queries

- On unix use `host` not `nslookup`

### DNS Response Codes
- NOERROR
    - Everything worked correctly in the DNS protocol. Does not mean information is correct, just that you were able to retrieve information (e.g. "I don't have that information!!" would be NOERROR)
- NXDOMAIN
    - DNS protocol worked but there are no records of the name you're looking for
- SERVFAIL
    - Something went wrong and you can't get an answer
- There are more but they're rare

### Name Resolution Order
- Order of methods to check for the given record of a zone is set in `/etc/nsswitch.conf` or `/etc/hosts.conf` 