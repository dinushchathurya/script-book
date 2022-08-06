### Internet Gateway

Allow talk to internet via Internet Gateway

### Route Table (Public Subnet)

| Destination   | Target             |
| ------------- |:------------------:|
| 10.0.0.0/16   | local              |
| 0.0.0.0/0     | internet-gateway-id|

### NAT Gateway

NAT Gateway is located in Public subnet.

<li>Need to attach Elastic IP</li>
<li>Need to update Route Table</li>

#### Route Table (Private Subnet)


| Destination   | Target             |
| ------------- |:------------------:|
| 10.0.0.0/16   | local              |
| 0.0.0.0/0     | nat-gateway-id     |


### Security Group (Public Subnet)

Web-Server-SG

| Destination   | Target  |   Source  |
| ------------- |:--------|:----------|
| HTTP          | 80      | 0.0.0.0/0 |
| HTTPS         | 443     | 0.0.0.0/0 |

### Security Group (Public Subnet)

Backend-Server-SG

| Destination   | Target  |   Source      |
| ------------- |:--------|:----------    |
| ALL TCP       | 4000    | Web-Server-SG |
