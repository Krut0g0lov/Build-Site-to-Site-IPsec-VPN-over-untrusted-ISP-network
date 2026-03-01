# Build-Site-to-Site-IPsec-VPN-over-untrusted-ISP-network

🔐 Cisco IPsec Site-to-Site VPN Lab (CML)

📌 Overview
This lab demonstrates a full Site-to-Site IPsec VPN deployment between two enterprise routers over an untrusted ISP network using Cisco Modeling Labs (CML).
The tunnel protects multiple internal subnets and uses strong cryptographic parameters (AES-256, SHA256, PFS group14).

🏗 Topology
        HQ (R1) -------- ISP -------- Branch (R3)

        LAN HQ:      10.10.0.0/22
        LAN Branch:  10.10.4.0/22
        Extra LAN:   10.10.16.0/21

        
Dynamic routing: OSPF area 0 inside sites
WAN links: 64.100.0.0/30 and 64.100.1.0/30
Public transport network via ISP router

🎯 Objectives
Build Site-to-Site IPsec VPN over untrusted network
Protect multiple subnets
Use strong encryption standards
Enable Perfect Forward Secrecy (PFS)
Verify tunnel establishment and traffic encryption
Troubleshoot common VPN issues

🔐 Security Configuration
IKE Phase 1 (ISAKMP Policy)
Encryption: AES-256
Hash: SHA256
Authentication: Pre-Shared Key
Diffie-Hellman Group: 14
Lifetime: 900 seconds
IKE Phase 2 (IPsec Transform Set)
ESP AES-256
ESP SHA256-HMAC
PFS enabled (group14)

📂 Repository Structure
/configs
   R1.txt
   R3.txt
   ISP.txt

/topology
   diagram.png
   
🔄 Traffic Encryption ACL
HQ (R1)
access-list S2S permit ip 10.10.0.0 0.0.3.255 10.10.4.0 0.0.3.255
access-list S2S permit ip 10.10.0.0 0.0.3.255 10.10.16.0 0.0.7.255
Branch (R3)
access-list s2s permit ip 10.10.4.0 0.0.3.255 10.10.0.0 0.0.3.255
access-list s2s permit ip 10.10.16.0 0.0.7.255 10.10.0.0 0.0.3.255
ACLs are mirrored as required for IPsec policy matching.

✅ Verification
Phase 1
show crypto isakmp sa
Expected state:
QM_IDLE
Phase 2
show crypto ipsec sa

