# PLAN D'ADRESSAGE
Masque par défaut pour les adresses ipv4 : /24
Masque par défaut pour les adresses ipv6 : /64

| Périphérique  |Interfaces  |Infos  | Adresse ipv4  |  Adresse ipv6
|---|-----|-----|----|----|
R1 | Gi0/0 | connected to SW-R1 on port Ethernet0 | 10.32.1.1 | fe80::1 ; 2001:470:c814:4001::2 ; fd00:fd00:fd00:2::1
R1 | Gi0/1 | connected to Internet on port nat0   | 10.32.4.1 | fe80::1:cafe:4 ; 2001:470:c814:4001::1 ; fd00:fd00:fd00:1::1
R1 | Gi0/2 | connected to R2 on port Gi0/1        | 10.32.2.1 | fe80::1
R1 | Gi0/3 | connected to R3 on port Gi0/1        | 10.32.3.1 | fe80::1
R1 | Gi0/7 | connected to SW-CTRL on port Ethernet1 | 10.32.5.1 | fe80::1 ; 2001:470:c814:4001::3 ; fd00:fd00:fd00:2::3
R2 | Gi0/0 | connected to SW-R2 on port Ethernet0   | 10.32.1.2 | fe80::2 ; 2001:470:c814:4002::2:1 ; fd00:fd00:fd00:2::2:1
R2 | Gi0/1 | connected to R1 on port Gi0/2  | 10.32.2.2 | fe80::2
R2 | Gi0/2 | connected to DS1 on port Gi2/0 | 10.16.1.2 | fe80::2
R2 | Gi0/3 | connected to R3 on port Gi0/2  | 10.32.3.2 | fe80::2
R2 | Gi0/4 | connected to DS1 on port Gi3/0 | 10.16.2.2 | fe80::2
R2 | Gi0/5 | connected to DS2 on port Gi2/1 | 10.16.3.2 | fe80::2
R2 | Gi0/6 | connected to DS2 on port Gi3/1 | 10.16.4.2 | fe80::2
R2 | Gi0/7 | connected to SW-CTRL on port Ethernet2 | 10.32.5.2 | fe80::2 ; 2001:470:c814:4002::c:1 ; fd00:fd00:fd00:2::c:1
R3 | Gi0/0 | connected to SW-R3 on port Ethernet0   | 10.32.0.3 | fe80::3 ; 2001:470:c814:4003::3:1 ; fd00:fd00:fd00:3::3:1
R3 | Gi0/1 | connected to R1 on port Gi0/3  | 10.32.1.3 | fe80::3
R3 | Gi0/2 | connected to R2 on port Gi0/3  | 10.32.2.3 | fe80::3
R3 | Gi0/3 | connected to DS2 on port Gi2/0 | 10.16.1.3 | fe80::3
R3 | Gi0/4 | connected to DS2 on port Gi3/0 | 10.16.2.3 | fe80::3
R3 | Gi0/5 | connected to DS1 on port Gi2/1 | 10.16.3.3 | fe80::3
R3 | Gi0/6 | connected to DS1 on port Gi3/1 | 10.16.4.3 | fe80::3
R3 | Gi0/7 | connected to SW-CTRL on port Ethernet3 | 10.32.5.3 | fe80::3 ; 2001:470:c814:4003::c:1 ; fd00:fd00:fd00:3::c:1
DS1 | Gi0/0 | connected to AS1 on port Gi0/0 |  | 
DS1 | Gi0/1 | connected to AS2 on port Gi0/1 |  | 
DS1 | Gi0/2 | connected to DS2 on port Gi0/2 |  | 
DS1 | Gi1/0 | connected to AS1 on port Gi1/0 |  | 
DS1 | Gi1/1 | connected to AS2 on port Gi1/1 |  | 
DS1 | Gi1/2 | connected to DS2 on port Gi1/2 |  | 
DS1 | Gi2/0 | connected to R2 on port Gi0/2  |  | fe80::d:1
DS1 | Gi2/1 | connected to R3 on port Gi0/5  |  | fe80::d:1
DS1 | Gi3/0 | connected to R2 on port Gi0/4  |  | fe80::d:1
DS1 | Gi3/1 | connected to R3 on port Gi0/6  |  | fe80::d:1
DS1 | Gi3/3 | connected to SW-CTRL on port Ethernet4 |  | fe80::d:1
DS2 | Gi0/0 | connected to AS2 on port Gi0/0 |  | 
DS2 | Gi0/1 | connected to AS1 on port Gi0/1 |  | 
DS2 | Gi0/2 | connected to DS1 on port Gi0/2 |  | 
DS2 | Gi1/0 | connected to AS2 on port Gi1/0 |  | 
DS2 | Gi1/1 | connected to AS1 on port Gi1/1 |  | 
DS2 | Gi1/2 | connected to DS1 on port Gi1/2 |  | 
DS2 | Gi2/0 | connected to R3 on port Gi0/3  |  | fe80::d:2 
DS2 | Gi2/1 | connected to R2 on port Gi0/5  |  | fe80::d:2 
DS2 | Gi3/0 | connected to R3 on port Gi0/4  |  | fe80::d:2 
DS2 | Gi3/1 | connected to R2 on port Gi0/6  |  | fe80::d:2 
DS2 | Gi3/3 | connected to SW-CTRL on port Ethernet5 |  |fe80::d:2
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
SW-CTRL | Ethernet0 is in access  mode |  connected to controller-1 on port Ethernet0 |  | fe80::c:1 ; 2001:470:c814:4000::c:1 ; fd00:fd00:fd00::c:1
SW-CTRL | Ethernet1 is in access  mode |  connected to R1 on port Gi0/7 |  | fe80::c:1
SW-CTRL | Ethernet2 is in access  mode |  connected to R2 on port Gi0/7 |  | fe80::c:1
SW-CTRL | Ethernet3 is in access  mode |  connected to R3 on port Gi0/7 |  | fe80::c:1
SW-CTRL | Ethernet4 is in access  mode |  connected to DS1 on port Gi3/3 |  | 
SW-CTRL | Ethernet5 is in access  mode |  connected to DS2 on port Gi3/3 |  | 
SW-CTRL | Ethernet6 is in access  mode |  connected to AS1 on port Gi3/3 |  | 
SW-CTRL | Ethernet7 is in access  mode |  connected to AS2 on port Gi3/3 |  | 


# VLANS
- vlan 10 : 10.16.10.0/24, passerelle 10.16.10.254
- vlan 20 : 10.16.20.0/24, passerelle 10.16.10.254
- vlan 30 : 10.16.30.0/24, passerelle 10.16.10.254
- vlan 40 : 10.16.40.0/24, passerelle 10.16.10.254
- vlan 99 : vlan natif

| Périphérique  |VLAN | Adresse ipv4  |  Adresse ipv6
|---|-----|----|----|
DS1 | VLAN10 | 10.16.10.252/24 | fe80::d1:10 ; fd00:1ab:10::1 ; 2001:470:c814:4010::1
DS1 | VLAN20 | 10.16.20.252/24 | fe80::d1:20 ; fd00:1ab:20::1 ; 2001:470:c814:4020::1 
DS1 | VLAN30 | 10.16.30.252/24 | fe80::d1:30 ; fd00:1ab:30::1 ; 2001:470:c814:4030::1
DS1 | VLAN40 | 10.16.40.252/24 | fe80::d1:40 ; fd00:1ab:40::1 ; 2001:470:c814:4040::1
DS2 | VLAN10 | 10.16.10.253/24 | fe80::d2:10 ; fd00:1ab:10::2 ; 2001:470:c814:4010::2
DS2 | VLAN20 | 10.16.20.253/24 | fe80::d2:20 ; fd00:1ab:20::2 ; 2001:470:c814:4020::2
DS2 | VLAN30 | 10.16.30.253/24 | fe80::d2:30 ; fd00:1ab:30::2 ; 2001:470:c814:4030::2
DS2 | VLAN40 | 10.16.40.253/24 | fe80::d2:40 ; fd00:1ab:40::2 ; 2001:470:c814:4040::2
