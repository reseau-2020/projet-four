# PLAN D'ADRESSAGE
| Périphérique  |Interfaces  |Infos  | Adresse ipv4  |  Adresse ipv6
|---|-----|-----|----|----|
R1 | Gi0/0 | connected to SW-R1 on port Ethernet0 | 10.32.1.1 | fe80::1:cafe:4 ; 2001:470:c814:4001::/64 ; fd00:fd00:fd00:1::1/64
R1 | Gi0/1 | connected to Provider on port Ethernet0 | 10.32.4.1 | fe80::1:cafe:4
R1 | Gi0/2 | connected to R2 on port Gi0/1 | 10.32.2.1 | fe80::1:cafe:4
R1 | Gi0/3 | connected to R3 on port Gi0/1 | 10.32.3.1 | fe80::1:cafe:4
R1 | Gi0/7 | connected to SW-CTRL on port Ethernet1 | 10.32.5.1 | fe80::1:cafe:4
R2 | Gi0/0 | connected to SW-R2 on port Ethernet0 | 10.32.1.2 | fe80::cafe:4 ; 2001:470:c814:4002::/64 ; fd00:fd00:fd00:2::1/64
R2 | Gi0/1 | connected to R1 on port Gi0/2 | 10.32.2.2 | fe80::2:cafe:4
R2 | Gi0/2 | connected to DS1 on port Gi2/0 | 10.16.1.2 | fe80::2:cafe:4
R2 | Gi0/3 | connected to R3 on port Gi0/2 | 10.32.3.2 | fe80::2:cafe:4
R2 | Gi0/4 | connected to DS1 on port Gi3/0 | 10.16.2.2 | fe80::2:cafe:4
R2 | Gi0/5 | connected to DS2 on port Gi2/1 | 10.16.3.2 | fe80::2:cafe:4
R2 | Gi0/6 | connected to DS2 on port Gi3/1 | 10.16.4.2 | fe80::2:cafe:4
R2 | Gi0/7 | connected to SW-CTRL on port Ethernet2 | 10.32.5.2 | fe80::2:cafe:4
R3 | Gi0/0 | connected to SW-R3 on port Ethernet0 | 10.32.0.3 | fe80::3:cafe:4 ; 2001:470:c814:4003::/64 ; fd00:fd00:fd00:3::1/64
R3 | Gi0/1 | connected to R1 on port Gi0/3 | 10.32.1.3 | fe80::3:cafe:4
R3 | Gi0/2 | connected to R2 on port Gi0/3 | 10.32.2.3 | fe80::3:cafe:4
R3 | Gi0/3 | connected to DS2 on port Gi2/0 | 10.16.1.3 | fe80:3::cafe:4
R3 | Gi0/4 | connected to DS2 on port Gi3/0 | 10.16.2.3 | fe80::3:cafe:4
R3 | Gi0/5 | connected to DS1 on port Gi2/1 | 10.16.3.3 | fe80::3:cafe:4
R3 | Gi0/6 | connected to DS1 on port Gi3/1 | 10.16.4.3 | fe80::3:cafe:4
R3 | Gi0/7 | connected to SW-CTRL on port Ethernet3 | 10.32.5.3 | fe80::3:cafe:4
DS1 | Gi0/0 | connected to AS1 on port Gi0/0 | 10.16.7.11 | 
DS1 | Gi0/1 | connected to AS2 on port Gi0/1 | 10.16.9.11 | 
DS1 | Gi0/2 | connected to DS2 on port Gi0/2 | 10.16.11.11 | 
DS1 | Gi1/0 | connected to AS1 on port Gi1/0 | 10.16.8.11 | 
DS1 | Gi1/1 | connected to AS2 on port Gi1/1 | 10.16.10.11 | 
DS1 | Gi1/2 | connected to DS2 on port Gi1/2 | 10.16.12.11 | 
DS1 | Gi2/0 | connected to R2 on port Gi0/2 | 10.16.2.11 | 
DS1 | Gi2/1 | connected to R3 on port Gi0/5 | 10.16.3.11 | 
DS1 | Gi3/0 | connected to R2 on port Gi0/4 | 10.16.4.11 | 
DS1 | Gi3/1 | connected to R3 on port Gi0/6 | 10.16.6.11 | 
DS1 | Gi3/3 | connected to SW-CTRL on port Ethernet4 |10.16.5.11  | 
DS2 | Gi0/0 | connected to AS2 on port Gi0/0 | 10.16.8.12 | 
DS2 | Gi0/1 | connected to AS1 on port Gi0/1 | 10.16.7.12 | 
DS2 | Gi0/2 | connected to DS1 on port Gi0/2 | 10.16.10.12 | 
DS2 | Gi1/0 | connected to AS2 on port Gi1/0 | 10.16.9.12 | 
DS2 | Gi1/1 | connected to AS1 on port Gi1/1 | 10.16.8.12 | 
DS2 | Gi1/2 | connected to DS1 on port Gi1/2 | 10.16.11.12 | 
DS2 | Gi2/0 | connected to R3 on port Gi0/3 | 10.16.3.12 | 
DS2 | Gi2/1 | connected to R2 on port Gi0/5 | 10.16.2.12 | 
DS2 | Gi3/0 | connected to R3 on port Gi0/4 | 10.16.6.12 | 
DS2 | Gi3/1 | connected to R2 on port Gi0/6 | 10.16.4.12 | 
DS2 | Gi3/3 | connected to SW-CTRL on port Ethernet5 | 10.16.5.12 |  
AS1  |  Gi0/0  |  connected to DS1 on port Gi0/0   | 10.16.1.13 | 
AS1  |  Gi0/1  |  connected to DS2 on port Gi0/1   | 10.16.2.13 | 
AS1  |  Gi1/0  |  connected to DS1 on port Gi1/0   | 10.16.3.13 | 
AS1  |  Gi1/1  |  connected to DS2 on port Gi1/1   | 10.16.4.13 | 
AS1  |  Gi2/0  |  connected to pc-1 on port eth0   | 10.16.6.13 | 
AS1  |  Gi2/1  |  connected to pc-2 on port eth0   | 10.16.7.13 | 
AS1  |  Gi2/2  |  connected to pc-3 on port eth0   | 10.16.8.13 | 
AS1  |  Gi2/3  |  connected to pc-4 on port eth0   | 10.16.9.13 | 
AS1  |  Gi3/3  |  connected to SW-CTRL on port Ethernet6 | 10.16.5.13 | 
AS2 | Gi0/0 | connected to DS2 on port Gi0/0 | 10.16.1.14 | 
AS2 | Gi0/1 | connected to DS1 on port Gi0/1 | 10.16.2.14 | 
AS2 | Gi1/0 | connected to DS2 on port Gi1/0 | 10.16.3.14 | 
AS2 | Gi1/1 | connected to DS1 on port Gi1/1 | 10.16.4.14 | 
AS2 | Gi2/0 | connected to pc-5 on port eth0 | 10.16.6.14 | 
AS2 | Gi2/1 | connected to pc-6 on port eth0 | 10.16.7.14 | 
AS2 | Gi2/2 | connected to pc-7 on port eth0 | 10.16.8.14 | 
AS2 | Gi2/3 | connected to pc-8 on port eth0 | 10.16.9.14 | 
AS2 | Gi3/3 | connected to SW-CTRL on port Ethernet7 | 10.16.5.14 | 


#VLANS
vlan 10 : 10.16.10.0/24, ip default gateway 10.16.10.254
vlan 20 : 10.16.20.0/24, passerelle 10.16.10.254
vlan 30 : 10.16.30.0/24, passerelle 10.16.10.254
vlan 40 : 10.16.40.0/24, passerelle 10.16.10.254
vlan 99 : vlan natif

| Périphérique  |VLAN | Adresse ipv4  |  Adresse ipv6
|---|-----|----|----|
DS1 | VLAN10 | 10.16.10.252/24 | fd00:abc:10::1/24 ; 2001:470:c814:4010::1/64
DS1 | VLAN20 | 10.16.20.252/24 | fd00:abc:20::1/24 ; 2001:470:c814:4020::1/64 
DS1 | VLAN30 | 10.16.30.252/24 | fd00:abc:30::1/24 ; 2001:470:c814:4030::1/64
DS1 | VLAN40 | 10.16.40.252/24 | fd00:abc:40::1/24 ; 2001:470:c814:4040::1/64
DS2 | VLAN10 | 10.16.10.253/24 | fd00:abc:10::2/24 ; 2001:470:c814:4010::2/64
DS2 | VLAN20 | 10.16.20.253/24 | fd00:abc:20::2/24 ; 2001:470:c814:4020::2/64
DS2 | VLAN30 | 10.16.30.253/24 | fd00:abc:30::2/24 ; 2001:470:c814:4030::2/64
DS2 | VLAN40 | 10.16.40.253/24 | fd00:abc:40::2/24 ; 2001:470:c814:4040::2/64
