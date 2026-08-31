# AWS Hybrid Cloud Network & Security

Hybrid cloud networking and security project connecting a segmented GNS3 environment to AWS through an encrypted Site-to-Site VPN.

The project demonstrates VLAN segmentation, DHCP, firewall policies, AWS VPC design, NAT, security groups, hybrid routing, and defense-in-depth security.

## Architecture

![Hybrid Network Architecture](diagrams/full-network-diagram.png)

## Network Design

### On-Premises

| VLAN | Purpose | Network |
|---|---|---|
| 10 | Administration | 192.168.10.0/24 |
| 20 | Design | 192.168.20.0/24 |
| 30 | Servers | 192.168.30.0/24 |
| 99 | Management | 192.168.99.0/24 |

### AWS

| Tier | Network |
|---|---|
| VPC | 10.20.0.0/16 |
| Public | 10.20.1.0/24 |
| Application | 10.20.10.0/24 |
| Database | 10.20.20.0/24 |

## Technologies

AWS VPC, EC2, NAT Gateway, Internet Gateway, Security Groups, Site-to-Site VPN, VyOS, GNS3, strongSwan, VLANs, DHCP, routing, IPsec, and firewall policies.

## Validation

### Test Case 1 — VLAN Segmentation
Configured VLANs and 802.1Q trunking. Verified same-VLAN communication and controlled inter-VLAN routing.

[Configuration](configs/test-case-1-vlan-config.txt)

### Test Case 2 — DHCP
Configured DHCP for Administration, Design, and Server VLANs. Verified correct IP, gateway, and DNS assignments.

[Configuration](configs/test-case-2-dhcp-config.txt)

### Test Case 3 — Firewall Security
Configured VyOS firewall rules to enforce least-privilege communication between VLANs. Packet counters confirmed permit and deny rules.

[Configuration](configs/test-case-3-firewall-config.txt)

### Test Case 4 — AWS Network Segmentation
Created public, application, and database subnets. Verified application internet access through NAT while the database subnet remained isolated.

[Configuration](configs/test-case-4-aws-networking.txt)

### Test Case 5 — AWS Addressing
Validated stable private addressing for DB1 and Elastic IP addressing for the bastion host after instance restarts.

[Configuration](configs/test-case-5-addressing.txt)

### Test Case 6 — AWS Security Groups
Restricted DB1 TCP/3306 access to the application security group. APP1 succeeded while BAST1 was denied.

[Configuration](configs/test-case-6-security-groups.txt)

### Test Case 7 — Site-to-Site VPN
Connected GNS3 to AWS using an encrypted IPsec VPN. Tunnel status and packet counters confirmed active hybrid traffic.

[Configuration](configs/test-case-7-vpn-config.txt)

### Test Case 8 — Hybrid Security
Applied least-privilege rules across the hybrid network using VyOS firewall policies and AWS security groups.

[Configuration](configs/test-case-8-hybrid-security.txt)

## Security Design

The environment uses multiple security layers:

- VLAN segmentation
- VyOS firewall policies
- Encrypted IPsec VPN
- AWS subnet isolation
- AWS security groups
- Private application and database tiers

## Troubleshooting

Issues resolved during implementation included VLAN assignment errors, TAP interface permissions, VPN traffic not matching IPsec policies, and VyOS configuration persistence.

## Repository Structure

- `configs/` — network and AWS configuration files
- `screenshots/` — validation evidence
- `diagrams/` — full network architecture
- `docs/` — detailed project documentation

## Skills Demonstrated

AWS networking, hybrid cloud architecture, VPNs, IPsec, VLANs, routing, DHCP, firewall policy design, security groups, least privilege, defense in depth, and network troubleshooting.
