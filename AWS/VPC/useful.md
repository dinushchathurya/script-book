## Route Table (Public Subnet)

Allow talk to internet via Internet Gateway

| Destination   | Target             |
| ------------- |:------------------:|
| 10.0.0.0/16   | local              |
| 0.0.0.0/0     | internet-gateway-id|

### NAT Gateway

NAT Gateway is located in Public subnet.

#### Route Table (Private Subnet)


| Destination   | Target             |
| ------------- |:------------------:|
| 10.0.0.0/16   | local              |
| 0.0.0.0/0     | nat-gateway-id     |
