# TLS 1.3

## Message format


![[TLS_record.png]]


## Handshake

#sep **IMPORTANT FOR SEP**

Client:
#### Part A
- I support TLSv 1.2/1.3
- For encryption I support the following in order, choose first you support
	- AES_128_GCM_SHA256
	- ...
- For Diffie-Hellman I support these groups, choose first
	- X25519
	- P-256
	- ...
- In case you support X25519 or P-256 here are my public keys:
	- $g^c$

#### Part B

Handshake-Key $P = (g^s)^c$ generated with HKDF

- Check signature with publc key from server cert
- Verify hash over all handshake messages matches
- (I will encrypt messages from know on) (`ChangeCiperSpec` which is no-op in 1.3)

Server:
#### Part A
- I support TLSv1.3
- Encrpytion chosen: 128bit AES, GCM, SHA-256 for HKDF
- Here is my X25519 public key
	- $g^s$
- (I will encrypt messages from know on) (`ChangeCiperSpec` which is no-op in 1.3)
- Here is a hash over all handshake messages I (client) have sent and received

Generate **separate** traffic keys

#### Part B

Handshake-Key $P = (g^c)^s$ generated with HKDF
- `Certificate`: Here is my cert chain (excluding root cert)
- `CertificateVerify`: Here is a signature over previous handshake messages, made with  private key corresponding to public key in the certificate
- Here is a hash over all handshake messages I (server) have sent and received
- Finished


Generate **separate** traffic keys




## Session resumeing