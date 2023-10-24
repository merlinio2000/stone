
## Application Level Firewalls

### Web Application Firewall (WAF)

Solves shortcomings of packet level firewalls by looking into the packet content
	(understands higher level protocols like HTTP)

Requires unencrypted traffic -> **TLS Termination**

#### WAF Architecture
- Firewall must block direct traffic to the server
- DNS-Record must point to TLS-termination, not server

![[waf_architecture.png]]


### Secure Web Gateway (SWG)
"How can I avoid that my employees visit naughty websites"
- also known as **(Forward-)Proxy**
- capabilities:
	- URL filtering
	- Data Leakage Prevention (DLP)
	- TLS Inspection
	- ...

![[swg.png]]


### Cloud Access Security Broker (CASB)
- capabilites
	- cloud usage control
	- DLP
	- anomaly detection
	- ...
- implementation
	- API Scanning, direct API to cloud provider
	- Forward Proxy, similar to [[#Secure Web Gateway (SWG)]]
	- Reverse Proxy, cloud provider redirects request to CASB

![[casb.png]]





# Netfilter / Linux Kernel

netfilter allows access to packets in the network stack to analyze, modify, extract and delete them.


## nftables
packet classifcation and mangling framework. Runs on rule sets defined on for packets
`nft` is the CLI-tool for nftables

![[netfilter.png]]

### Rules

"classification part" 1-m  "action parts"

Classification:
- what packets does this rule apply to?

Action:
- `accept`, continue as normal
- `drop`
- `reject`, `drop` and tell the sender
- `jump`, continue processing elsewhere

#### Examples

##### Count then drop packets going to IPv4 8.8.8.8
`ip daddr 8.8.8.8 counter drop`

- ip = address family, rule applies to IP(v4)
- daddr = destination  address (CIDR possible), rule applies to packets with certain destination address
- counter drop = actions


### Chains

- Rules can be organized into chains
- classification applied **top down until first match**
- if match -> execute & stop chain
- if no match -> **policy** of the chain decides what happens
- have type & priority


