On fait un ping du pc1, et sur DS1 on fait un shut sur l'interface Po1. 
````
PING fd00:1ab:10::2(fd00:1ab:10::2) 56 data bytes
64 bytes from fd00:1ab:10::2: icmp_seq=1 ttl=64 time=13.6 ms
64 bytes from fd00:1ab:10::2: icmp_seq=2 ttl=64 time=5.94 ms
64 bytes from fd00:1ab:10::2: icmp_seq=3 ttl=64 time=7.91 ms
64 bytes from fd00:1ab:10::2: icmp_seq=4 ttl=64 time=6.06 ms
64 bytes from fd00:1ab:10::2: icmp_seq=5 ttl=64 time=5.36 ms
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=36 Destination unreachable: Address unreachable  !On fait tomber le po1 sur Ds1
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=37 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=38 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=39 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=40 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=41 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=42 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=43 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=44 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=45 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=46 Destination unreachable: Address unreachable
From fd00:1ab:10:0:e8c:12ff:fe3a:c400 icmp_seq=47 Destination unreachable: Address unreachable
64 bytes from fd00:1ab:10::2: icmp_seq=48 ttl=64 time=14.3 ms                                    ! on fait monté po1 sur DS1
64 bytes from fd00:1ab:10::2: icmp_seq=49 ttl=64 time=5.57 ms
64 bytes from fd00:1ab:10::2: icmp_seq=50 ttl=64 time=4.97 ms
64 bytes from fd00:1ab:10::2: icmp_seq=51 ttl=64 time=6.51 ms
64 bytes from fd00:1ab:10::2: icmp_seq=52 ttl=64 time=4.61 ms
64 bytes from fd00:1ab:10::2: icmp_seq=53 ttl=64 time=5.94 ms
64 bytes from fd00:1ab:10::2: icmp_seq=54 ttl=64 time=5.12 ms
64 bytes from fd00:1ab:10::2: icmp_seq=55 ttl=64 time=10.5 ms
64 bytes from fd00:1ab:10::2: icmp_seq=56 ttl=64 time=7.16 ms
64 bytes from fd00:1ab:10::2: icmp_seq=57 ttl=64 time=4.87 ms
64 bytes from fd00:1ab:10::2: icmp_seq=58 ttl=64 time=6.22 ms
64 bytes from fd00:1ab:10::2: icmp_seq=59 ttl=64 time=6.27 ms
64 bytes from fd00:1ab:10::2: icmp_seq=60 ttl=64 time=6.17 ms

--- fd00:1ab:10::2 ping statistics ---
60 packets transmitted, 18 received, +12 errors, 70% packet loss, time 59030ms
rtt min/avg/max/mdev = 4.618/7.069/14.313/2.775 ms

````
