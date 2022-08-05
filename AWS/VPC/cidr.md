### VPC CIDR 

<li>Maximum / 16 (65536 IPS)</li>
<li>Minimum /28  (16 IPS)</li>
<li>VPC private CIDR IP range</li>
    <ol>1.  10.0.0.0 - 10.255.255.255 (10/8 prefix)</ol>
    <ol>2.  0172.16.0.0 - 172.31.255.255 (172.16/12 prefix)</ol>
    <ol>3.  192.168.0.0 - 192.168.255.255 (192.168/16 prefix)</ol>

<li>CIDR Calculation</li>

```
Network->[x.x] x.x/16<-prefix(calculate network>)
32-16 =16
2 ^{16}
65536
```
```
Network->[x.x.x].x/24<-prefix(calculate network>)
32-24 =8
2 ^{8}
256
```