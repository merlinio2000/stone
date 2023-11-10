# Protocols
## IPsec

secure communication on the network (3, IP) layer

- requires **Kernel**-level support
- authentication, confidentiality and integrity
- protects data above layer 3
	- ICMP
	- TCP/UDP
	- ...

### Transport mode
Authentication Header (AH)
- IP packets should be authenticated and integrity protected
- virtually never used (not even compatible with NAT)

### Tunnel mode
Encapsulating Security Payload (ESP)
- IP packets should be encrypted and (optionally) authenticated and integrity protected
- **entire** original IP packet is protected with ESP
- result put into new IP packet which gets sented to remote VPN gateway
	- -> hides internal IP addrs

![[esp_packet.png]]

##### Internet Key Exchange (IKE)

key exchange for [[#IPsec]]
IKEv2 as successor

Handshake: similar to [[TLS#Handshake]]
1. select cryptographic algorightms
2. **mutual** authentication (always mutual in IPsec)
3. Exchange key material (e.g. Diffie-Hellman)

### Comparison with TLS

- TLS sits **on top of a TCP connection**
- TLS keys are known to the **applications**
- TLS protects communication between 2 applications
- IPSec secures communication between 2 **HOSTS**
	- data of all applications is encrypted (unknown to them)

## OpenVPN
- runs in userspace (unlike IPSec)
- "slimmer" than IPSec
- **application-layer** tunnel on top of UDP or TCP

Usually uses **UDP** (Port 1194) as the underlying transport protocol:
	- TCP results in poor performance because of conflicting flow control
		 -> tunnel with no guaranteed delivery
	- this isnt a problem because if the application requires reliability, it uses TCP itself which handles data loss
	  -> the tunnel passes the TCP packets

Handshake: uses [[TLS#Handshake]]
- requires **reliability** thus OpenVPN protocol implements ACK-based mechanism that provieds reliablity for TLS Handshake
- every OpenVPN packet with TLS handshake must be **explicitly** acknowleged by the recipient, otherwise retransmitted


![[openvpn_packet.png]]

With the payload (assuming block cipher in CBC mode)

![[openvpn_payload.png]]


### Comparing IPSec and OpenVPN

- security wise no real differences

IPSec advantages:
- more "mature"  and a lot of commercial support

OpenVPN advantages:
- much smaller protocol, usually easier to configure
- runs in user space



## Wireguard

- works on Layer 3 (like [[#IPsec]])
- very little configurability -> smaller attack surface
- modenr crypto (ChaCha20, Curve25519)
- 1-RTT handshake
- perfect forward secrecy (PFS)
- includes DoS-mitigation

![[wireguard_message_flow.png]]
![[wireguard_message_flow_internals.png]]
![[wireguard_message_flow_internals2.png]]


### Handshake & DOS mitigation

![[wireguard_handshake_dos_mitigation.png]]