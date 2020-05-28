Pour tester le syslog on fait un shut sur l'une des interfaces d'un élément cisco. On remarque l'envoie des log qu'on collecte par la suite sur le serveur syslog. 

### Sur le routeur (R1 et R2)
````
R1(config)#int G0/2
R1(config-if)#shut
*May 28 07:53:19: %DUAL-5-NBRCHANGE: EIGRP-IPv6 1: Neighbor FE80::2 (GigabitEthernet0/2) is down: interface down
*May 28 07:53:19: %DUAL-5-NBRCHANGE: EIGRP-IPv4 1: Neighbor 10.32.12.2 (GigabitEthernet0/2) is down: interface down
*May 28 07:53:19: %DUAL-5-NBRCHANGE: EIGRP-IPv6 1: Neighbor FE80::2 (GigabitEthernet0/2) is down: interface down
*May 28 07:53:19: %DUAL-5-NBRCHANGE: EIGRP-IPv4 1: Neighbor 10.32.12.2 (GigabitEthernet0/2) is down: interface down
R1(config-if)#no
*May 28 07:53:21: %LINK-5-CHANGED: Interface GigabitEthernet0/2, changed state to administratively down
*May 28 07:53:22: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/2, changed state to down
*May 28 08:00:41: %FW-6-DROP_PKT: Dropping tcp session 192.168.122.223:37148 192.168.122.18:3005 on zone-pair internet-self class class-default due to  DROP action found in policy-map with ip ident 52882
R1#
*May 28 08:01:11: %FW-6-DROP_PKT: Dropping tcp session 192.168.122.223:37149 192.168.122.18:32781 on zone-pair internet-self class class-default due to  DROP action found in policy-map with ip ident 11917


R2(config)#int g0/1
R2(config-if)#shut
R2(config-if)#
*May 28 08:04:00: %DUAL-5-NBRCHANGE: EIGRP-IPv6 1: Neighbor FE80::1 (GigabitEthernet0/1) is down: interface down
*May 28 08:04:00: %DUAL-5-NBRCHANGE: EIGRP-IPv4 1: Neighbor 10.32.12.1 (GigabitEthernet0/1) is down: interface down
R2(config-if)#no s
*May 28 08:04:02: %LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to administratively down
*May 28 08:04:03: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to downh
R2(config-if)#no shut
R2(config-if)#exit
````
### Sur le serveur Syslog
````
2020-05-28T10:00:45.001938+02:00 10.32.12.1 91: R1: *May 28 08:00:41: %FW-6-DROP_PKT: Dropping tcp session 192.168.122.223:37148 192.168.122.18:3005 on zone-pair internet-self class class-default due to  DROP action found in policy-map with ip ident 52882
2020-05-28T10:01:15.123737+02:00 10.32.12.1 92: R1: *May 28 08:01:11: %FW-6-DROP_PKT: Dropping tcp session 192.168.122.223:37149 192.168.122.18:32781 on zone-pair internet-self class class-default due to  DROP action found in policy-map with ip ident 11917

2020-05-28T10:04:03.567211+02:00 _gateway 57: R2: *May 28 08:04:00: %DUAL-5-NBRCHANGE: EIGRP-IPv6 1: Neighbor FE80::1 (GigabitEthernet0/1) is down: interface down
2020-05-28T10:04:03.568226+02:00 _gateway 58: R2: *May 28 08:04:00: %DUAL-5-NBRCHANGE: EIGRP-IPv4 1: Neighbor 10.32.12.1 (GigabitEthernet0/1) is down: interface down
2020-05-28T10:04:05.548297+02:00 _gateway 59: R2: *May 28 08:04:02: %LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to administratively down
2020-05-28T10:04:05.548945+02:00 _gateway 60: R2: *May 28 08:04:03: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to down
2020-05-28T10:04:09.751601+02:00 _gateway 61: R2: *May 28 08:04:07: %LINK-3-UPDOWN: Interface GigabitEthernet0/1, changed state to up
2020-05-28T10:04:09.755683+02:00 _gateway 62: R2: *May 28 08:04:08: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
2020-05-28T10:04:13.454673+02:00 _gateway 63: R2: *May 28 08:04:10: %DUAL-5-NBRCHANGE: EIGRP-IPv6 1: Neighbor FE80::1 (GigabitEthernet0/1) is up: new adjacency
2020-05-28T10:04:13.458910+02:00 _gateway 64: R2: *May 28 08:04:11: %DUAL-5-NBRCHANGE: EIGRP-IPv4 1: Neighbor 10.32.12.1 (GigabitEthernet0/1) is up: new adjacency

````

