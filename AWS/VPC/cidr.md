### VPC CIDR 

<li>Maximum / 16 (65536 IPS)</li>
<li>Minimum /28  (16 IPS)</li>
<li>VPC private CIDR IP range (IRC 1918)</li>
<br>
    <ol>1.  10.0.0.0 - 10.255.255.255 (10/8 prefix)</ol>
    <ol>2.  0172.16.0.0 - 172.31.255.255 (172.16/12 prefix)</ol>
    <ol>3.  192.168.0.0 - 192.168.255.255 (192.168/16 prefix)</ol>

<li>CIDR Calculation</li>
<br>

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

### Example

```
VPC CIDR:

10.0.0.0/16

Subnet CIDR:

Avaliabilty Zone One
10.0.0.0/24
10.0.1.0/24

Avaliability Zone Two
10.0.10.0/24
10.0.20.0/24