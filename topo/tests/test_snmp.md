### Test sur les éléments Cisco

!Verification de la configuration SNMP sur les routeurs/ switchs
````
R1#sh snmp
0 SNMP packets input
    0 Bad SNMP version errors
    0 Unknown community name
    0 Illegal operation for community name supplied
    0 Encoding errors
    0 Number of requested variables
    0 Number of altered variables
    0 Get-request PDUs
    0 Get-next PDUs
    0 Set-request PDUs
    0 Input queue packet drops (Maximum queue size 1000)
22 SNMP packets output
    0 Too big errors (Maximum packet size 1500)
    0 No such name errors
    0 Bad values errors
    0 General errors
    0 Response PDUs
    22 Trap PDUs
SNMP Dispatcher:
   queue 0/75 (current/max), 0 dropped
SNMP Engine:
   queue 0/1000 (current/max), 0 dropped

SNMP logging: enabled
    Logging to 10.32.202.3.162, 0/10, 22 sent, 0 dropped.

R2#sh snmp
0 SNMP packets input
    0 Bad SNMP version errors
    0 Unknown community name
    0 Illegal operation for community name supplied
    0 Encoding errors
    0 Number of requested variables
    0 Number of altered variables
    0 Get-request PDUs
    0 Get-next PDUs
    0 Set-request PDUs
    0 Input queue packet drops (Maximum queue size 1000)
12 SNMP packets output
    0 Too big errors (Maximum packet size 1500)
    0 No such name errors
    0 Bad values errors
    0 General errors
    0 Response PDUs
    12 Trap PDUs
SNMP Dispatcher:
   queue 0/75 (current/max), 0 dropped
SNMP Engine:
   queue 0/1000 (current/max), 0 dropped

SNMP logging: enabled
    Logging to 10.32.202.3.162, 0/10, 12 sent, 0 dropped.


R3#sh snmp
0 SNMP packets input
    0 Bad SNMP version errors
    0 Unknown community name
    0 Illegal operation for community name supplied
    0 Encoding errors
    0 Number of requested variables
    0 Number of altered variables
    0 Get-request PDUs
    0 Get-next PDUs
    0 Set-request PDUs
    0 Input queue packet drops (Maximum queue size 1000)
13 SNMP packets output
    0 Too big errors (Maximum packet size 1500)
    0 No such name errors
    0 Bad values errors
    0 General errors
    0 Response PDUs
    13 Trap PDUs
SNMP Dispatcher:
   queue 0/75 (current/max), 0 dropped
SNMP Engine:
   queue 0/1000 (current/max), 0 dropped

SNMP logging: enabled
    Logging to 10.32.202.3.162, 0/10, 13 sent, 0 dropped.

DS1#show snmp
Chassis: 9PD79P3RWNP
0 SNMP packets input
    0 Bad SNMP version errors
    0 Unknown community name
    0 Illegal operation for community name supplied
    0 Encoding errors
    0 Number of requested variables
    0 Number of altered variables
    0 Get-request PDUs
    0 Get-next PDUs
    0 Set-request PDUs
    0 Input queue packet drops (Maximum queue size 1000)
79 SNMP packets output
    0 Too big errors (Maximum packet size 1500)
    0 No such name errors
    0 Bad values errors
    0 General errors
    0 Response PDUs
    79 Trap PDUs
SNMP global trap: enabled

SNMP logging: enabled
    Logging to 10.32.202.3.162, 0/10, 28 sent, 51 dropped.

DS2#sh snmp
Chassis: 93S4VT4SUP4
0 SNMP packets input
    0 Bad SNMP version errors
    0 Unknown community name
    0 Illegal operation for community name supplied
    0 Encoding errors
    0 Number of requested variables
    0 Number of altered variables
    0 Get-request PDUs
    0 Get-next PDUs
    0 Set-request PDUs
    0 Input queue packet drops (Maximum queue size 1000)
96 SNMP packets output
    0 Too big errors (Maximum packet size 1500)
    0 No such name errors
    0 Bad values errors
    0 General errors
    0 Response PDUs
    96 Trap PDUs
SNMP global trap: enabled

SNMP logging: enabled
    Logging to 10.32.202.3.162, 0/10, 24 sent, 72 dropped.

````
### Test sur le serveur Snmp - syslog

! Collecte des traps snmp du serveur Centos 7
````
[root@pc2-r2 ~]# snmpwalk -v2c -cprivate 10.16.134.2
SNMPv2-MIB::sysDescr.0 = STRING: Cisco IOS Software, vios_l2 Software (vios_l2-ADVENTERPRISEK9-M), Experimental Version 15.2(20170321:233949) [mmen 101]
Copyright (c) 1986-2017 by Cisco Systems, Inc.
Compiled Wed 22-Mar-17 08:38 by mmen
SNMPv2-MIB::sysObjectID.0 = OID: SNMPv2-SMI::enterprises.9.1.1227
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (101714) 0:16:57.14
SNMPv2-MIB::sysContact.0 = STRING:
SNMPv2-MIB::sysName.0 = STRING: DS1.lan.project4
SNMPv2-MIB::sysLocation.0 = STRING:
SNMPv2-MIB::sysServices.0 = INTEGER: 78
SNMPv2-MIB::sysORLastChange.0 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORID.1 = OID: SNMPv2-SMI::enterprises.9.7.129
SNMPv2-MIB::sysORID.2 = OID: SNMPv2-SMI::enterprises.9.7.115
SNMPv2-MIB::sysORID.3 = OID: SNMPv2-SMI::enterprises.9.7.265
SNMPv2-MIB::sysORID.4 = OID: SNMPv2-SMI::enterprises.9.7.112
SNMPv2-MIB::sysORID.5 = OID: SNMPv2-SMI::enterprises.9.7.106
SNMPv2-MIB::sysORID.6 = OID: SNMPv2-SMI::enterprises.9.7.47
SNMPv2-MIB::sysORID.7 = OID: SNMPv2-SMI::enterprises.9.7.135
SNMPv2-MIB::sysORID.8 = OID: SNMPv2-SMI::enterprises.9.7.122
SNMPv2-MIB::sysORID.9 = OID: SNMPv2-SMI::enterprises.9.7.37
SNMPv2-MIB::sysORID.10 = OID: SNMPv2-SMI::enterprises.9.7.92
SNMPv2-MIB::sysORID.11 = OID: SNMPv2-SMI::enterprises.9.7.53
SNMPv2-MIB::sysORID.12 = OID: SNMPv2-SMI::enterprises.9.7.54
SNMPv2-MIB::sysORID.13 = OID: SNMPv2-SMI::enterprises.9.7.52
SNMPv2-MIB::sysORID.14 = OID: SNMPv2-SMI::enterprises.9.7.93
SNMPv2-MIB::sysORID.15 = OID: SNMPv2-SMI::enterprises.9.7.186
SNMPv2-MIB::sysORID.16 = OID: SNMPv2-SMI::enterprises.9.7.128
SNMPv2-MIB::sysORID.17 = OID: SNMPv2-SMI::enterprises.9.7.121
SNMPv2-MIB::sysORID.18 = OID: SNMPv2-SMI::enterprises.9.7.44
SNMPv2-MIB::sysORID.19 = OID: SNMPv2-SMI::enterprises.9.7.350
SNMPv2-MIB::sysORID.20 = OID: SNMPv2-SMI::enterprises.9.7.33
SNMPv2-MIB::sysORID.21 = OID: SNMPv2-SMI::enterprises.9.7.130
SNMPv2-MIB::sysORID.22 = OID: SNMPv2-SMI::enterprises.9.7.568
SNMPv2-MIB::sysORID.23 = OID: SNMPv2-SMI::enterprises.9.7.116
SNMPv2-MIB::sysORID.24 = OID: SNMPv2-SMI::enterprises.9.7.91
SNMPv2-MIB::sysORID.25 = OID: SNMPv2-SMI::enterprises.9.7.999
SNMPv2-MIB::sysORID.26 = OID: SNMPv2-SMI::enterprises.9.7.9999
SNMPv2-MIB::sysORID.27 = OID: SNMPv2-SMI::enterprises.9.7.126
SNMPv2-MIB::sysORID.28 = OID: SNMPv2-SMI::enterprises.9.7.127
SNMPv2-MIB::sysORID.29 = OID: SNMPv2-SMI::enterprises.9.7.64
SNMPv2-MIB::sysORID.30 = OID: SNMPv2-SMI::enterprises.9.7.439
SNMPv2-MIB::sysORID.31 = OID: SNMPv2-SMI::enterprises.9.7.438
SNMPv2-MIB::sysORID.32 = OID: SNMPv2-SMI::enterprises.9.7.123
SNMPv2-MIB::sysORID.33 = OID: SNMPv2-SMI::enterprises.9.7.120

[root@pc2-r2 ~]# snmpwalk -v2c -cprivate 10.32.13.2
SNMPv2-MIB::sysDescr.0 = STRING: Cisco IOS Software, IOSv Software (VIOS-ADVENTERPRISEK9-M), Version 15.6(2)T, RELEASE SOFTWARE (fc2)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2016 by Cisco Systems, Inc.
Compiled Tue 22-Mar-16 16:19 by prod_rel_team
SNMPv2-MIB::sysObjectID.0 = OID: SNMPv2-SMI::enterprises.9.1.1041
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (109426) 0:18:14.26
SNMPv2-MIB::sysContact.0 = STRING:
SNMPv2-MIB::sysName.0 = STRING: R3.LAN.PROJECT4
SNMPv2-MIB::sysLocation.0 = STRING:
SNMPv2-MIB::sysServices.0 = INTEGER: 78
SNMPv2-MIB::sysORLastChange.0 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORID.1 = OID: SNMPv2-SMI::enterprises.9.7.129
SNMPv2-MIB::sysORID.2 = OID: SNMPv2-SMI::enterprises.9.7.115
SNMPv2-MIB::sysORID.3 = OID: SNMPv2-SMI::enterprises.9.7.265
SNMPv2-MIB::sysORID.4 = OID: SNMPv2-SMI::enterprises.9.7.112
SNMPv2-MIB::sysORID.5 = OID: SNMPv2-SMI::enterprises.9.7.106
SNMPv2-MIB::sysORID.6 = OID: SNMPv2-SMI::enterprises.9.7.47
SNMPv2-MIB::sysORID.7 = OID: SNMPv2-SMI::enterprises.9.7.122
SNMPv2-MIB::sysORID.8 = OID: SNMPv2-SMI::enterprises.9.7.37
SNMPv2-MIB::sysORID.9 = OID: SNMPv2-SMI::enterprises.9.7.92
SNMPv2-MIB::sysORID.10 = OID: SNMPv2-SMI::enterprises.9.7.53
SNMPv2-MIB::sysORID.11 = OID: SNMPv2-SMI::enterprises.9.7.54
SNMPv2-MIB::sysORID.12 = OID: SNMPv2-SMI::enterprises.9.7.52
SNMPv2-MIB::sysORID.13 = OID: SNMPv2-SMI::enterprises.9.7.93
SNMPv2-MIB::sysORID.14 = OID: SNMPv2-SMI::enterprises.9.7.186
SNMPv2-MIB::sysORID.15 = OID: SNMPv2-SMI::enterprises.9.7.128
SNMPv2-MIB::sysORID.16 = OID: SNMPv2-SMI::enterprises.9.7.425
SNMPv2-MIB::sysORID.17 = OID: SNMPv2-SMI::enterprises.9.7.517
SNMPv2-MIB::sysORID.18 = OID: SNMPv2-SMI::enterprises.9.7.516
SNMPv2-MIB::sysORID.19 = OID: SNMPv2-SMI::enterprises.9.7.518
SNMPv2-MIB::sysORID.20 = OID: SNMPv2-SMI::enterprises.9.7.267
SNMPv2-MIB::sysORID.21 = OID: SNMPv2-SMI::enterprises.9.7.273
SNMPv2-MIB::sysORID.22 = OID: SNMPv2-SMI::enterprises.9.7.265
SNMPv2-MIB::sysORID.23 = OID: SNMPv2-SMI::enterprises.9.7.121
SNMPv2-MIB::sysORID.24 = OID: SNMPv2-SMI::enterprises.9.7.44
SNMPv2-MIB::sysORID.25 = OID: SNMPv2-SMI::enterprises.9.7.99999
SNMPv2-MIB::sysORID.26 = OID: SNMPv2-SMI::enterprises.9.7.202
SNMPv2-MIB::sysORID.27 = OID: SNMPv2-SMI::enterprises.9.7.264
SNMPv2-MIB::sysORID.28 = OID: SNMPv2-SMI::enterprises.9.7.33
SNMPv2-MIB::sysORID.29 = OID: SNMPv2-SMI::enterprises.9.7.492
SNMPv2-MIB::sysORID.30 = OID: SNMPv2-SMI::enterprises.9.7.130
SNMPv2-MIB::sysORID.31 = OID: SNMPv2-SMI::enterprises.9.7.116
SNMPv2-MIB::sysORID.32 = OID: SNMPv2-SMI::enterprises.9.7.91
SNMPv2-MIB::sysORID.33 = OID: SNMPv2-SMI::enterprises.9.7.999
SNMPv2-MIB::sysORID.34 = OID: SNMPv2-SMI::enterprises.9.7.212
SNMPv2-MIB::sysORID.35 = OID: SNMPv2-SMI::enterprises.9.7.547
SNMPv2-MIB::sysORID.36 = OID: SNMPv2-SMI::enterprises.9.7.126
SNMPv2-MIB::sysORID.37 = OID: SNMPv2-SMI::enterprises.9.7.127
SNMPv2-MIB::sysORID.38 = OID: SNMPv2-SMI::enterprises.9.7.64
SNMPv2-MIB::sysORID.39 = OID: SNMPv2-SMI::enterprises.9.7.123
SNMPv2-MIB::sysORID.40 = OID: SNMPv2-SMI::enterprises.9.7.120
SNMPv2-MIB::sysORID.41 = OID: SNMPv2-SMI::enterprises.9.7.124
SNMPv2-MIB::sysORID.42 = OID: SNMPv2-SMI::enterprises.9.7.218
SNMPv2-MIB::sysORID.43 = OID: SNMPv2-SMI::enterprises.9.7.119
SNMPv2-MIB::sysORID.44 = OID: SNMPv2-SMI::enterprises.9.7.125
SNMPv2-MIB::sysORID.45 = OID: SNMPv2-SMI::enterprises.9.7.524
SNMPv2-MIB::sysORID.46 = OID: SNMPv2-SMI::enterprises.9.7.45
SNMPv2-MIB::sysORID.47 = OID: SNMPv2-SMI::enterprises.9.7.605
SNMPv2-MIB::sysORID.48 = OID: SNMPv2-SMI::enterprises.9.7.46
SNMPv2-MIB::sysORID.49 = OID: SNMPv2-SMI::enterprises.9.7.557
SNMPv2-MIB::sysORID.50 = OID: SNMPv2-SMI::enterprises.9.7.604
SNMPv2-MIB::sysORID.51 = OID: SNMPv2-SMI::enterprises.9.7.203
SNMPv2-MIB::sysORID.52 = OID: SNMPv2-SMI::enterprises.9.7.201
SNMPv2-MIB::sysORID.53 = OID: SNMPv2-SMI::enterprises.9.7.1
SNMPv2-MIB::sysORID.54 = OID: SNMPv2-SMI::enterprises.9.7.202
SNMPv2-MIB::sysORID.55 = OID: SNMPv2-SMI::enterprises.9.7.440
SNMPv2-MIB::sysORID.56 = OID: SNMPv2-SMI::enterprises.9.7.463
SNMPv2-MIB::sysORID.57 = OID: SNMPv2-SMI::enterprises.9.7.16
SNMPv2-MIB::sysORID.58 = OID: SNMPv2-SMI::enterprises.9.7.17
SNMPv2-MIB::sysORID.59 = OID: SNMPv2-SMI::enterprises.9.7.36
SNMPv2-MIB::sysORID.60 = OID: SNMPv2-SMI::enterprises.9.7.447
SNMPv2-MIB::sysORID.61 = OID: SNMPv2-SMI::enterprises.9.7.548
SNMPv2-MIB::sysORID.62 = OID: SNMPv2-SMI::enterprises.9.7.256
SNMPv2-MIB::sysORID.63 = OID: SNMPv2-SMI::enterprises.9.7.101
SNMPv2-MIB::sysORID.64 = OID: SNMPv2-SMI::enterprises.9.7.105
SNMPv2-MIB::sysORID.65 = OID: SNMPv2-SMI::enterprises.9.7.108
SNMPv2-MIB::sysORID.66 = OID: SNMPv2-SMI::enterprises.9.7.117
SNMPv2-MIB::sysORID.67 = OID: SNMPv2-SMI::enterprises.9.7.103
SNMPv2-MIB::sysORID.68 = OID: SNMPv2-SMI::enterprises.9.7.107
SNMPv2-MIB::sysORID.69 = OID: SNMPv2-SMI::enterprises.9.7.109
SNMPv2-MIB::sysORID.70 = OID: SNMPv2-SMI::enterprises.9.7.110
SNMPv2-MIB::sysORID.71 = OID: SNMPv2-SMI::enterprises.9.7.111
SNMPv2-MIB::sysORID.72 = OID: SNMPv2-SMI::enterprises.9.7.102
SNMPv2-MIB::sysORID.73 = OID: SNMPv2-SMI::enterprises.9.7.102
SNMPv2-MIB::sysORID.74 = OID: SNMPv2-SMI::enterprises.9.7.120
SNMPv2-MIB::sysORID.75 = OID: SNMPv2-SMI::enterprises.9.7.115
SNMPv2-MIB::sysORID.76 = OID: SNMPv2-SMI::enterprises.9.7.172
````
