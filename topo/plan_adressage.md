# PLAN D'ADRESSAGE
- Masque par défaut pour les adresses ipv4 : /24
- Masque par défaut pour les adresses ipv6 : /64

## Site principal

| Périphérique  |Interfaces  |Infos  | Adresses ipv4  |  Adresses ipv6
|---|-----|-----|----|----|
R1 | Gi0/0 | connected to SW-R1 on port Ethernet0   | `10.32.201.1` | `fe80::1` ; `2001:470:c814:4001::1:1` ; `fd00:fd00:fd00:1::1:1`
R1 | Gi0/1 | connected to Internet on port nat0     | `DHCP` | `fe80::1:cafe:4`
R1 | Gi0/2 | connected to R2 on port Gi0/1          | `10.32.12.1` | `fe80::1`
R1 | Gi0/3 | connected to R3 on port Gi0/1          | `10.32.13.1` | `fe80::1`
R1 | Gi0/7 | connected to SW-CTRL on port Ethernet1 | `10.32.75.1` | `fe80::1`
R2 | Gi0/0 | connected to SW-R2 on port Ethernet0   | `10.32.202.2` | `fe80::2` ; `2001:470:c814:4002::2:1` ; `fd00:fd00:fd00:2::2:1`
R2 | Gi0/1 | connected to R1 on port Gi0/2  | `10.32.12.2` | `fe80::2`
R2 | Gi0/2 | connected to DS1 on port Gi2/0 | `10.16.214.1` | `fe80::2`
R2 | Gi0/3 | connected to R3 on port Gi0/2  | `10.32.23.1` | `fe80::2`
R2 | Gi0/4 | connected to DS1 on port Gi3/0 | `10.16.224.2` | `fe80::2`
R2 | Gi0/5 | connected to DS2 on port Gi2/1 | `10.16.215.1` | `fe80::2`
R2 | Gi0/6 | connected to DS2 on port Gi3/1 | `10.16.225.2` | `fe80::2`
R2 | Gi0/7 | connected to SW-CTRL on port Ethernet2 | `10.32.75.2` | `fe80::2`
R3 | Gi0/0 | connected to SW-R3 on port Ethernet0   | `10.32.203.1` | `fe80::3` ; `2001:470:c814:4003::3:1` ; `fd00:fd00:fd00:3::3:1`
R3 | Gi0/1 | connected to R1 on port Gi0/3  | `10.32.13.2` | `fe80::3`
R3 | Gi0/2 | connected to R2 on port Gi0/3  | `10.32.23.2` | `fe80::3`
R3 | Gi0/3 | connected to DS2 on port Gi2/0 | `10.16.135.1` | `fe80::3`
R3 | Gi0/4 | connected to DS2 on port Gi3/0 | `10.16.235.2` | `fe80::3`
R3 | Gi0/5 | connected to DS1 on port Gi2/1 | `10.16.134.1` | `fe80::3`
R3 | Gi0/6 | connected to DS1 on port Gi3/1 | `10.16.234.2` | `fe80::3`
R3 | Gi0/7 | connected to SW-CTRL on port Ethernet3 | `10.32.75.3` | `fe80::3`
DS1 | Gi0/0 | connected to AS1 on port Gi0/0 |  | 
DS1 | Gi0/1 | connected to AS2 on port Gi0/1 |  | 
DS1 | Gi0/2 | connected to DS2 on port Gi0/2 |  | 
DS1 | Gi1/0 | connected to AS1 on port Gi1/0 |  | 
DS1 | Gi1/1 | connected to AS2 on port Gi1/1 |  | 
DS1 | Gi1/2 | connected to DS2 on port Gi1/2 |  | 
DS1 | Gi2/0 | connected to R2 on port Gi0/2  | `10.16.214.2` | `fe80::d:1`
DS1 | Gi2/1 | connected to R3 on port Gi0/5  | `10.16.134.2` | `fe80::d:1`
DS1 | Gi3/0 | connected to R2 on port Gi0/4  | `10.16.224.1` | `fe80::d:1`
DS1 | Gi3/1 | connected to R3 on port Gi0/6  | `10.16.234.1` | `fe80::d:1`
DS1 | Gi3/3 | connected to SW-CTRL on port Ethernet4 |  | 
DS2 | Gi0/0 | connected to AS2 on port Gi0/0 |  | 
DS2 | Gi0/1 | connected to AS1 on port Gi0/1 |  | 
DS2 | Gi0/2 | connected to DS1 on port Gi0/2 |  | 
DS2 | Gi1/0 | connected to AS2 on port Gi1/0 |  | 
DS2 | Gi1/1 | connected to AS1 on port Gi1/1 |  | 
DS2 | Gi1/2 | connected to DS1 on port Gi1/2 |  | 
DS2 | Gi2/0 | connected to R3 on port Gi0/3  | `10.16.135.2` | `fe80::d:2` 
DS2 | Gi2/1 | connected to R2 on port Gi0/5  | `10.16.215.2` | `fe80::d:2` 
DS2 | Gi3/0 | connected to R3 on port Gi0/4  | `10.16.235.1` | `fe80::d:2` 
DS2 | Gi3/1 | connected to R2 on port Gi0/6  | `10.16.225.1` | `fe80::d:2` 
DS2 | Gi3/3 | connected to SW-CTRL on port Ethernet5 |  |
AS1 |  Gi0/0 | connected to DS1 on port Gi0/0 |  | 
AS1 |  Gi0/1 | connected to DS2 on port Gi0/1 |  | 
AS1 |  Gi1/0 | connected to DS1 on port Gi1/0 |  | 
AS1 |  Gi1/1 | connected to DS2 on port Gi1/1 |  | 
AS1 |  Gi2/0 | connected to pc-1 on port eth0 |  | 
AS1 |  Gi2/1 | connected to pc-2 on port eth0 |  | 
AS1 |  Gi2/2 | connected to pc-3 on port eth0 |  | 
AS1 |  Gi2/3 | connected to pc-4 on port eth0 |  | 
AS1 |  Gi3/3 | connected to SW-CTRL on port Ethernet6 |  | 
AS2 | Gi0/0 | connected to DS2 on port Gi0/0 |  | 
AS2 | Gi0/1 | connected to DS1 on port Gi0/1 |  | 
AS2 | Gi1/0 | connected to DS2 on port Gi1/0 |  | 
AS2 | Gi1/1 | connected to DS1 on port Gi1/1 |  | 
AS2 | Gi2/0 | connected to pc-5 on port eth0 |  | 
AS2 | Gi2/1 | connected to pc-6 on port eth0 |  | 
AS2 | Gi2/2 | connected to pc-7 on port eth0 |  | 
AS2 | Gi2/3 | connected to pc-8 on port eth0 |  | 
AS2 | Gi3/3 | connected to SW-CTRL on port Ethernet7 |  | 
SW-CTRL | Ethernet0 is in access  mode |  connected to controller-1 on port Ethernet0 |  | 
SW-CTRL | Ethernet1 is in access  mode |  connected to R1 on port Gi0/7 |  | 
SW-CTRL | Ethernet2 is in access  mode |  connected to R2 on port Gi0/7 |  | 
SW-CTRL | Ethernet3 is in access  mode |  connected to R3 on port Gi0/7 |  | 
SW-CTRL | Ethernet4 is in access  mode |  connected to DS1 on port Gi3/3 |  | 
SW-CTRL | Ethernet5 is in access  mode |  connected to DS2 on port Gi3/3 |  | 
SW-CTRL | Ethernet6 is in access  mode |  connected to AS1 on port Gi3/3 |  | 
SW-CTRL | Ethernet7 is in access  mode |  connected to AS2 on port Gi3/3 |  | 
Centos8-1  | eth0  | connected to SW-R1 on port Ethernet1 |   |  `10.32.201.2`
Centos8-2  | eth0  | connected to SW-R1 on port Ethernet2 |   |  `10.32.201.3`

## Site distant

| Périphérique  |Interfaces  |Infos  | Adresses ipv4  |  Adresses ipv6
|---|-----|-----|----|----|
Fortios | Port2 |  connected to Switch1 on port Ethernet0           | `192.168.150.254` | ` `
Fortios | Port3 |  connected to Switch2 on port Ethernet0           | `192.168.122.27` | ` ` ; ` ` ; ` `
Fortios | Port4 |  connected to Server-Ubuntu on port Ethernet0     | `192.1689.10.254` | ` `
Fortios | Port5 |  connected to Switch2 on port Ethernet2           | ` ` | ` ` 
Server-Ubuntu | eth0 | connected to fortios-1 on port Port4         | `192.168.10.1` | ` ` 
Centos-1 |  eth0 |  connected to Switch1 on port Ethernet1          | `192.168.150.1` | ` ` 
Centos-2 |  eth0 |  connected to Switch1 on port Ethernet2          | `192.168.150.2` | ` ` 

# VLANS
- vlan 10 : 10.16.10.0/24, passerelle 10.16.10.254, port acces AS1 & AS2 g2/0
- vlan 20 : 10.16.20.0/24, passerelle 10.16.20.254, port acces AS1 & AS2 g2/1
- vlan 30 : 10.16.30.0/24, passerelle 10.16.30.254, port acces AS1 & AS2 g2/2
- vlan 40 : 10.16.40.0/24, passerelle 10.16.40.254, port acces AS1 & AS2 g2/3
- vlan 99 : vlan natif

| Périphérique  |VLAN | Adresses ipv4  |  Adresses ipv6
|---|-----|----|----|
DS1 | VLAN10 | `10.16.10.252/24` | `fe80::d1:10` ; `fd00:1ab:10::1` ; `2001:470:c814:4011::`
DS1 | VLAN20 | `10.16.20.252/24` | `fe80::d1:20` ; `fd00:1ab:20::1` ; `2001:470:c814:4021::` 
DS1 | VLAN30 | `10.16.30.252/24` | `fe80::d1:30` ; `fd00:1ab:30::1` ; `2001:470:c814:4031::`
DS1 | VLAN40 | `10.16.40.252/24` | `fe80::d1:40` ; `fd00:1ab:40::1` ; `2001:470:c814:4041::`
DS2 | VLAN10 | `10.16.10.253/24` | `fe80::d2:10` ; `fd00:1ab:10::2` ; `2001:470:c814:4012::`
DS2 | VLAN20 | `10.16.20.253/24` | `fe80::d2:20` ; `fd00:1ab:20::2` ; `2001:470:c814:4022::`
DS2 | VLAN30 | `10.16.30.253/24` | `fe80::d2:30` ; `fd00:1ab:30::2` ; `2001:470:c814:4032::`
DS2 | VLAN40 | `10.16.40.253/24` | `fe80::d2:40` ; `fd00:1ab:40::2` ; `2001:470:c814:4042::`

## Ports Etherchannel et Trunk VLANs
Ports channel | Ports physique | Commutateurs
|---|-----|----
po1  | g0/0, g1/0 | AS1-DS1
po2  | g0/1, g1/1 | AS1-DS2
po3  | g0/2, g1/2 | DS1-DS2
po4  | g0/0, g1/0 | AS2-DS2
po5  | g0/1, g1/1 | AS2-DS1

## Spanning-Tree
VLANS | DS1 | DS2
|---|-----|----
VLANs 10,30,99 |	root primary	 |  root secondary
VLANs 20,40    |	root secondary |	root primary

## HSRP
Commutateur  |	Interface |	Adresse IPv4 virtuelle  |	Adresse IPv6 virtuelle  |	Group |	Priorité
|---|-----|----|----|----|----
DS1 | VLAN10 | `10.16.10.254` | `fe80::d10` | 10/16 |	150, prempt
DS1 | VLAN20 | `10.16.20.254` | `fe80::d20` | 20/26 |	default
DS1 | VLAN30 | `10.16.30.254` | `fe80::d30` | 30/36 |	150, prempt
DS1 | VLAN40 | `10.16.40.254` | `fe80::d40` | 40/46 |	default
DS2 | VLAN10 | `10.16.10.254` | `fe80::d10` | 10/16 |	default
DS2 | VLAN20 | `10.16.20.254` | `fe80::d20` | 20/26 |	150, prempt
DS2 | VLAN30 | `10.16.30.254` | `fe80::d30` | 30/36 |	default
DS2 | VLAN40 | `10.16.40.254` | `fe80::d40` | 40/46 |	150, prempt
