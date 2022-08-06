### NACL - Network Access Control Lists

<li>Operates in Subnet level</li>
<li>Both "Allow" & "Deny" rules are possible</li>
<li>Rules are evaluated from Lowest to Highest (Lowest number has Highest priority)</li>

### Security groups

<li>Virtual Firewall</li>
<li>EC2 has up to 5 Security Groups</li>
<li>Only has "Allow" rules</li>
<li>Stateful (If Allow inbound traffic it defalut Allow outbound rule from same protocol)</li>

### ENI - Elastic Network Interface

A elastic network interface (ENI) is a virtual virual network interface that is used to connect a virtual machine to a virtual network. <b>Security groups</b> are operated in ENI level.