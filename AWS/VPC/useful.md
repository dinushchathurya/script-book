## Route Table (Public Subnet)

Allow talk to internet via Internet Gateway

| Destination   | Target             |
| ------------- |:------------------:|
| 10.0.0.0/16   | local              |
| 0.0.0.0/0     | internet-gateway-id|