# IPv6

## Connectivité avec l'internet
```
[root@pc8 ~]# ping6 google.com
PING google.com(par21s05-in-x0e.1e100.net (2a00:1450:4007:812::200e)) 56 data bytes
64 bytes from par21s05-in-x0e.1e100.net (2a00:1450:4007:812::200e): icmp_seq=1 ttl=54 time=9.88 ms
64 bytes from par21s05-in-x0e.1e100.net (2a00:1450:4007:812::200e): icmp_seq=2 ttl=54 time=10.1 ms
64 bytes from par21s05-in-x0e.1e100.net (2a00:1450:4007:812::200e): icmp_seq=3 ttl=54 time=13.4 ms
64 bytes from par21s05-in-x0e.1e100.net (2a00:1450:4007:812::200e): icmp_seq=4 ttl=54 time=10.4 ms
64 bytes from par21s05-in-x0e.1e100.net (2a00:1450:4007:812::200e): icmp_seq=5 ttl=54 time=11.1 ms
```
## Connectivité dans vlan10
```
[root@pc1 ~]# ping6 2001:470:c814:4011:e8c:12ff:fef1:b900
PING 2001:470:c814:4011:e8c:12ff:fef1:b900(2001:470:c814:4011:e8c:12ff:fef1:b900) 56 data bytes
64 bytes from 2001:470:c814:4011:e8c:12ff:fef1:b900: icmp_seq=1 ttl=64 time=12.7 ms
64 bytes from 2001:470:c814:4011:e8c:12ff:fef1:b900: icmp_seq=2 ttl=64 time=6.57 ms
64 bytes from 2001:470:c814:4011:e8c:12ff:fef1:b900: icmp_seq=3 ttl=64 time=8.17 ms
64 bytes from 2001:470:c814:4011:e8c:12ff:fef1:b900: icmp_seq=4 ttl=64 time=7.11 ms
64 bytes from 2001:470:c814:4011:e8c:12ff:fef1:b900: icmp_seq=5 ttl=64 time=7.66 ms
```

## Connectivité entre le vlan10 & le vlan20
```
[root@pc1 ~]# ping6 2001:470:c814:4022:e8c:12ff:fe11:7a00
PING 2001:470:c814:4022:e8c:12ff:fe11:7a00(2001:470:c814:4022:e8c:12ff:fe11:7a00) 56 data bytes
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=1 ttl=63 time=7.94 ms
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=2 ttl=63 time=8.26 ms
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=3 ttl=63 time=8.69 ms
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=4 ttl=63 time=8.98 ms
```

## Connectivité entre le vlan10 & le vlan30
```
[root@pc1 ~]# ping6 2001:470:c814:4031:e8c:12ff:fe32:b400
PING 2001:470:c814:4031:e8c:12ff:fe32:b400(2001:470:c814:4031:e8c:12ff:fe32:b400) 56 data bytes
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=1 ttl=61 time=12.5 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=2 ttl=61 time=10.8 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=3 ttl=61 time=12.2 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=4 ttl=61 time=10.8 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=5 ttl=61 time=10.7 ms
```

## Connectivité entre le vlan10 & le vlan40
```
[root@pc1 ~]# ping6 2001:470:c814:4042:e8c:12ff:febf:bf00
PING 2001:470:c814:4042:e8c:12ff:febf:bf00(2001:470:c814:4042:e8c:12ff:febf:bf00) 56 data bytes
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=1 ttl=63 time=10.6 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=2 ttl=63 time=9.24 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=3 ttl=63 time=9.78 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=4 ttl=63 time=7.73 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=5 ttl=63 time=9.28 ms
```

## Connectivité dans vlan20
```
[root@pc2 ~]# ping6 2001:470:c814:4022:e8c:12ff:fe11:7a00
PING 2001:470:c814:4022:e8c:12ff:fe11:7a00(2001:470:c814:4022:e8c:12ff:fe11:7a00) 56 data bytes
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=1 ttl=64 time=12.0 ms
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=2 ttl=64 time=6.47 ms
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=3 ttl=64 time=6.05 ms
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=4 ttl=64 time=6.72 ms
64 bytes from 2001:470:c814:4022:e8c:12ff:fe11:7a00: icmp_seq=5 ttl=64 time=6.25 ms
```

## Connectivité entre le vlan20 & le vlan30
```
[root@pc2 ~]# ping6  2001:470:c814:4031:e8c:12ff:fe32:b400
PING 2001:470:c814:4031:e8c:12ff:fe32:b400(2001:470:c814:4031:e8c:12ff:fe32:b400) 56 data bytes
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=1 ttl=63 time=8.29 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=2 ttl=63 time=9.49 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=3 ttl=63 time=6.74 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=4 ttl=63 time=8.20 ms
```

## Connectivité entre le vlan20 & le vlan40
```
[root@pc2 ~]# ping6 2001:470:c814:4042:e8c:12ff:febf:bf00
PING 2001:470:c814:4042:e8c:12ff:febf:bf00(2001:470:c814:4042:e8c:12ff:febf:bf00) 56 data bytes
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=1 ttl=61 time=8.66 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=2 ttl=61 time=11.1 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=3 ttl=61 time=11.7 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=4 ttl=61 time=9.77 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=5 ttl=61 time=10.6 ms
```

## Connectivité dans vlan30
```
[root@pc3 ~]# ping6 2001:470:c814:4031:e8c:12ff:fe32:b400
PING 2001:470:c814:4031:e8c:12ff:fe32:b400(2001:470:c814:4031:e8c:12ff:fe32:b400) 56 data bytes
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=1 ttl=64 time=13.3 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=2 ttl=64 time=6.76 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=3 ttl=64 time=6.06 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=4 ttl=64 time=14.8 ms
64 bytes from 2001:470:c814:4031:e8c:12ff:fe32:b400: icmp_seq=5 ttl=64 time=5.93 ms
```

## Connectivité entre le vlan30 & le vlan40
```
[root@pc3 ~]# ping6 2001:470:c814:4042:e8c:12ff:febf:bf00
PING 2001:470:c814:4042:e8c:12ff:febf:bf00(2001:470:c814:4042:e8c:12ff:febf:bf00) 56 data bytes
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=1 ttl=63 time=15.1 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=2 ttl=63 time=7.50 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=3 ttl=63 time=9.05 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=4 ttl=63 time=8.54 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=5 ttl=63 time=8.90 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=6 ttl=63 time=9.35 ms
```

## Connectivité dans vlan40
```
[root@pc4 ~]# ping6 2001:470:c814:4042:e8c:12ff:febf:bf00
PING 2001:470:c814:4042:e8c:12ff:febf:bf00(2001:470:c814:4042:e8c:12ff:febf:bf00) 56 data bytes
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=1 ttl=64 time=10.7 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=2 ttl=64 time=7.04 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=3 ttl=64 time=9.76 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=4 ttl=64 time=6.84 ms
64 bytes from 2001:470:c814:4042:e8c:12ff:febf:bf00: icmp_seq=5 ttl=64 time=7.34 ms
```
