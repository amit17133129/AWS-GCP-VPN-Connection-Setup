# AWS-GCP-VPN-Connection-Setup

<p align="center">
  <img width="1000" height="600" src="https://miro.medium.com/max/1100/1*UYjhPDUhPFaYWphgtPDsrQ.gif">
</p>

Hello guys, hope you all doing good. Back again with another article that will helps you to create a vpn setup with aws and gcp cloud.

## What is VPN connection ?
VPN stands for “Virtual Private Network” and describes the opportunity to establish a protected network connection when using public networks. VPNs encrypt your internet traffic and disguise your online identity. This makes it more difficult for third parties to track your activities online and steal data. The encryption takes place in real time.

## How does a VPN work?
A VPN hides your IP address by letting the network redirect it through a specially configured remote server run by a VPN host. This means that if you surf online with a VPN, the VPN server becomes the source of your data. This means your Internet Service Provider (ISP) and other third parties cannot see which websites you visit or what data you send and receive online. A VPN works like a filter that turns all your data into “gibberish”. Even if someone were to get their hands on your data, it would be useless.

## What are the benefits of a VPN connection?
A VPN connection disguises your data traffic online and protects it from external access. Unencrypted data can be viewed by anyone who has network access and wants to see it. With a VPN, hackers and cyber criminals can’t decipher this data.

### Secure encryption: 
To read the data, you need an encryption key . Without one, it would take millions of years for a computer to decipher the code in the event of a brute force attack . With the help of a VPN, your online activities are hidden even on public networks.

### Disguising your whereabouts : 
VPN servers essentially act as your proxies on the internet. Because the demographic location data comes from a server in another country, your actual location cannot be determined. In addition, most VPN services do not store logs of your activities. Some providers, on the other hand, record your behavior, but do not pass this information on to third parties. This means that any potential record of your user behavior remains permanently hidden.
      
### Access to regional content: 
Regional web content is not always accessible from everywhere. Services and websites often contain content that can only be accessed from certain parts of the world. Standard connections use local servers in the country to determine your location. This means that you cannot access content at home while traveling, and you cannot access international content from home. With VPN location spoofing , you can switch to a server to another country and effectively “change” your location.
      
### Secure data transfer: 
If you work remotely, you may need to access important files on your company’s network. For security reasons, this kind of information requires a secure connection. To gain access to the network, a VPN connection is often required. VPN services connect to private servers and use encryption methods to reduce the risk of data leakage.
      
## What kind of VPNs are there?
There are many different types of VPNs, but you should definitely be familiar with the three main types:

### SSL VPN
Often not all employees of a company have access to a company laptop they can use to work from home. During the corona crisis in Spring 2020, many companies faced the problem of not having enough equipment for their employees. In such cases, use of a private device (PC, laptop, tablet, mobile phone) is often resorted to. In this case, companies fall back on an SSL-VPN solution, which is usually implemented via a corresponding hardware box.

The prerequisite is usually an HTML-5-capable browser, which is used to call up the company’s login page. HTML-5 capable browsers are available for virtually any operating system. Access is guarded with a username and password.

### Site-to-site VPN
A site-to-site VPN is essentially a private network designed to hide private intranets and allow users of these secure networks to access each other’s resources.

A site-to-site VPN is useful if you have multiple locations in your company, each with its own local area network (LAN) connected to the WAN (Wide Area Network). Site-to-site VPNs are also useful if you have two separate intranets between which you want to send files without users from one intranet explicitly accessing the other.

Site-to-site VPNs are mainly used in large companies. They are complex to implement and do not offer the same flexibility as SSL VPNs. However, they are the most effective way to ensure communication within and between large departments.

### Client-to-Server VPN
Connecting via a VPN client can be imagined as if you were connecting your home PC to the company with an extension cable. Employees can dial into the company network from their home office via the secure connection and act as if they were sitting in the office. However, a VPN client must first be installed and configured on the computer.

This involves the user not being connected to the internet via his own ISP, but establishing a direct connection through his/her VPN provider. This essentially shortens the tunnel phase of the VPN journey. Instead of using the VPN to create an encryption tunnel to disguise the existing internet connection, the VPN can automatically encrypt the data before it is made available to the user.

This is an increasingly common form of VPN, which is particularly useful for providers of insecure public WLAN. It prevents third parties from accessing and compromising the network connection and encrypts data all the way to the provider. It also prevents ISPs from accessing data that, for whatever reason, remains unencrypted and bypasses any restrictions on the user’s internet access (for instance, if the government of that country restricts internet access).

The advantage of this type of VPN access is greater efficiency and universal access to company resources. Provided an appropriate telephone system is available, the employee can, for example, connect to the system with a headset and act as if he/she were at their company workplace. For example, customers of the company cannot even tell whether the employee is at work in the company or in their home office.

Here we will be focusing on site-to-site vpn in aws cloud and HA (High Availabilty) vpn in gcp cloud.

### GCP Side Configuration:
So let’s start from the GCP cloud configuration. Create a vpc in gcp as below i have created with the name of aws-gcp-vpc-vpn.

<p align="center">
  <img width="1000" height="100" src="https://miro.medium.com/max/828/1*2NtEAWBpAy7Q3SzQv-mncA.webp">
</p>

Then we need to create subnet inside the above vpc. I have used the subnet cidr as 10.0.0.0/24.

<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*d05K6mBVgHbTKVxbpoR8Vg.webp">
</p>

Finally we will have to create the firewall in this vpc. The firewall will allow two specific rule i.e. for allowing ssh (for ssh) and allowing icmp (for ping).

<p align="center">
  <img width="1000" height="250" src="https://miro.medium.com/max/828/1*XHlc3gnM9ZqUPn-6DnMshQ.webp">
</p>

### AWS Side Configuration:
Now the same setup what we have created in gcp we will have to create in aws cloud as well. I have created the VPC with the name as aws-gcp-vpc as mentioned below. I have given the cidr as 10.1.0.0/16.

### Create VPC:
<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*hbcDXhDIoNCY1wHPi3-LYA.webp">
</p>

Now lets create the subnet inside the aws-gcp-vpc-vpn vpc. I have given the cidr as 10.1.0.0/24.

### Create Subnet:
<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*jrteJYI4OLDv0iEBJT3YcQ.webp">
</p>

For the internet connectivity inside the vpc network we will have to create internet gateway. Finally attach the internet gateway to the vpc.

### Create Internet Gateway:
<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*WwhrmLmRAzSoSwVPIuxnwg.webp">
</p>

Navigate to route table and the vpc aws-gcp-vpc-vpn have one route table we have to name the route table as aws-gcp-rt-vpn. Now we have to edit the routes of that route table.

### Create Route Table:
<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*dXQyctQcW6w6L9Ih4vYOEQ.webp">
</p>

We will add another route in the route table as the highlighted below in the red color. This route indicates that it has the destination as anywhere and it will use the target as internet gateway.
<p align="center">
  <img width="1000" height="100" src="https://miro.medium.com/max/828/1*eCUExMCf5e_yxap2XG5ohg.webp">
</p>

Now we have to associate the subnets with that route. i.e. subnet aws-gcp-subnet-vpc will be associated to aws-gcp-rt-vpn.
<p align="center">
  <img width="1000" height="200" src="https://miro.medium.com/max/828/1*5aHtTDqgsgfouqorIT-FJw.webp">
</p>

### GCP Side Configuration:
Now lets create the HA VPN on gcp side. GCP will provide two types of vpn. HA and classic vpn. Classic vpn is on the edge of deprication. So we will use only HA vpn.

### HA (High Availibilty VPN):

HA VPN gateways use the HA VPN API and provide a 99.99% SLA. This configuration uses a tunnel pair, with one tunnel on each HA VPN gateway interface. To receive a 99.99% SLA, you must configure VPN tunnels on both HA VPN gateway interfaces.

<p align="center">
  <img width="1000" height="900" src="https://miro.medium.com/max/828/1*zvp9-NAwLk8rFw6Voo_sPg.webp">
</p>


<p align="center">
  <img width="1000" height="400" src="https://miro.medium.com/max/828/1*_W8fhU3Y1Sa33OA2NIP5ag.webp">
</p>

After creating HA vpn. I will be giving you 2 interfaces. `i.e interace — 0` and `interface — 1`.

```
Interface - 0 --> 35.242..3.33
Interface - 1 --> 35.220.0.218
```

### Create Customer Gateway:
Now lets move to aws side to create the customer gateway. Note that we will have to create two customer gateway as we have two interfaces given by gcp HA vpn. For creating the customer gateway we will have to give the below details.

```
customer gateway name 1: "aws-gcp-cgw-1-vpn"
customer gateway name 2: "aws-gcp-cgw-2-vpn"
BGP ASN for cgw 1      : "65420"
BGP ASN for cgw 2      : "65420"
IP address for cgw 1   : "35.242.3.33" --> Interface - 0 
IP address for cgw 2   : "35.220.0.218" --> Interface - 1
Certiface ARN          : NA
Device                 : NA
Note: BGP ASN you can give any number between 1 - 2147483647 range. Keep the BGP ASN same for both the customer gateway.
```

<p align="center">
  <img width="1000" height="170" src="https://miro.medium.com/max/828/1*KeTNT6qz6phZ9eKwK5spfw.webp">
</p>

<p align="center">
  <img width="1000" height="170" src="https://miro.medium.com/max/828/1*zlajMUNazyiB5MbOZBpFsQ.webp">
</p>

Now lets create the vpn on aws side. For creating the vpn you have give below details.

```
Name of the vpn: "aws-gcp-vpn"
Select custom ASN and enter: "64512"
```

### Create VPN Connection:
After creating the aws vpn we will have to create the site to site vpn. Below details you have to fill while creating site to site vpn.

<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*ZIwyDjsNFUEP4GNd1NQPgQ.webp">
</p>

<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*4s7kT3oESbI_O8sapTHFHA.webp">
</p>

```

Details while creating vpn follow the below details:
Name of the st to vpn              :  "aws-gcp-vpn-1/aws-gcp-vpn-2"
existing virtual private gateway id: "aws-gcp-vpn"
existing customer gateway id       : "aws-gcp-cgw-vpn-1/aws-gcp-cgw-vpn-2"
Routing options                    : "Dynamic (requires BGP)"
Local IPv4 network CIDR            : NA
Remote IPv4 network CIDR           : NA
Inside IPv4 CIDR for tunnel 1      : NA
Pre-shared key for tunnel 1        : NA
Advanced options for tunnel 1      : "Edit tunnel 1/2 options"

Phase 1 encryption algorithms      : "AES256"
Phase 2 encryption algorithms      : "AES256"
Phase 1 integrity algorithms       : "SHA2-256"
Phase 2 integrity algorithms       : "SHA2-256"
Phase 1 DH group numbers           : "14"
Phase 2 DH group numbers           : "14"
IKE Version                        : "ikev2"
Phase 1 lifetime (seconds)         : NA
Phase 2 lifetime (seconds)         : NA
Rekey margin time (seconds)        : NA
Rekey fuzz (percentage)            : NA
Replay window size (packets)       : NA
DPD timeout (seconds)              : NA
DPD timeout action                 : "clear"
Startup action                     : "Add"
```

After creating the VPN you have to enable the VPN route propagation in the route table configuration.

### Enable the route propagation:

<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*3VrGehoojxs8LPlPOnl_yA.webp">
</p>

Now download the configuration of each site to site vpn. Save the configuration file in your local system.

### Download the VPN configuration file:

<p align="center">
  <img width="1000" height="150" src="https://miro.medium.com/max/828/1*IRlComfP4tHd57_3fvh3XA.webp">
</p>

You have to refer this configuration file on the below ponits for tunnel 1 vpn and tunnel 2 vpn configuration file.

### VPN 1 (tunnel 1 and tunnel 2):

```
Key points to look into configuration file of tunnel 1 vpn 1

Pre-Shared Key           : UAXYOQQlRbY0Sxxxxxxxxxxxxxxxxxx

#3: Tunnel Interface Configuration
Outside IP Addresses:
       Virtual Private Gateway         : 34.206.196.84

Inside IP Addresses:
  - Customer Gateway           : 169.254.96.186/30
  - Virtual Private Gateway             : 169.254.96.185/30
Key points to look into configuration file of tunnel 2 vpn 1

Pre-Shared Key           : uW6SJT5aFEMxxxxxxxxxxxxxxxxxx

#3: Tunnel Interface Configuration
Outside IP Addresses:
       Virtual Private Gateway         : 52.70.2.207

Inside IP Addresses:
  - Customer Gateway           : 169.254.30.166/30
  - Virtual Private Gateway             : 169.254.30.165/30

```

### VPN 2(tunnel 1 and tunnel 2):

```
Key points to look into configuration file of tunnel 1 vpn 2

Pre-Shared Key           : 76sobZuwhxBsrnxxxxxxxxxxxxxxxx

#3: Tunnel Interface Configuration
Outside IP Addresses:
       Virtual Private Gateway         : 3.234.198.192

Inside IP Addresses:
  - Customer Gateway           : 169.254.93.70/30
  - Virtual Private Gateway             : 169.254.93.69/30
Key points to look into configuration file of tunnel 2 vpn 2

Pre-Shared Key           : VNwjrg5PpFbnxxxxxxxxxxxxxxxxx

#3: Tunnel Interface Configuration
Outside IP Addresses:
       Virtual Private Gateway         : 52.6.139.200

Inside IP Addresses:
  - Customer Gateway           : 169.254.34.70/30
  - Virtual Private Gateway             : 169.254.34.69/30

```

## GCP Side Configuration:

### Create Peer VPN Gateway Connection :
Now lets create the peer vpn gateway connection in gcp. Click on create peer vpn gateway and add the below details from the image. Select peer vpn gateway interfaces as four interfaces. Add the virtual gateway outside ip addresses of respective tunnel and vpn from the configuration file which you have downloaded.

<p align="center">
  <img width="1000" height="500" src="https://miro.medium.com/max/828/1*o6VVSnsObXrEomBunDAypQ.webp">
</p>

### Create Cloud Router:
After adding all the details while creating peer vpn gateway click on create. Then we have to create cloud router. For creating cloud router you will have to add then name of the clous router and vpc network i.e. you created earlier select the region in which all the configuration done earlier. Add the amazon ASN number from the aws virtual private gateway in the Google ASN number field and finally click on create.

<p align="center">
  <img width="1000" height="500" src="https://miro.medium.com/max/828/1*1wUGxHF5EFolq7OLdiLTaA.webp">
</p>

Then after creating the cloud router we will have to configure the 4 tunnels. You have to only add the name of the tunnel and the pre-shared key that you will get from the aws vpn configuration file which you have downloaded.

<p align="center">
  <img width="1000" height="600" src="https://miro.medium.com/max/828/1*3CPuu2bey8QyNbXU0tbgDw.webp">
</p>

### Configure BGP sessions:
After configuring the4 tunnels we have to configure the bgp sessions of each bgp sessions. Click on configure BGP sessions to configure the sessions.

<p align="center">
  <img width="1000" height="200" src="https://miro.medium.com/max/828/1*3XMUdWhZ0qPn8FTyTzMj2Q.webp">
</p>

<p align="center">
  <img width="1000" height="600" src="https://miro.medium.com/max/828/1*8upnVYjCu4_age6I9rOXrw.webp">
</p>

Then after that click on save bgp configurations and click on ok. After that we will have to click on tunnel and edit the bgp session. Change the ip address to customer inside gateway ip address and virtual gateway inside ip address. Edit all the bgp sessions of each tunnel and change the ip address to respective ones.

<p align="center">
  <img width="1000" height="600" src="https://miro.medium.com/max/828/1*z3kNdTOqVZcyWpEWI4NmWA.webp">
</p>

You will see that VPN tunnel status will show you Established and BGP session status will shows you BGP established.

<p align="center">
  <img width="1000" height="100" src="https://miro.medium.com/max/1400/1*PfhQbLQxdyoWFKqKZMbkkQ.webp">
</p>

Now if we move to the AWS side in vpn site to site configuration you will see that the status of the all the four tunnel is UP. If it’s showing DOWN so wait for sometime after the configuration of BGP session.

### Tunnel VPN 1 Status:
<p align="center">
  <img width="1000" height="100" src="https://miro.medium.com/max/828/1*FWzVYuENmkpSgbJWsO3Q5Q.webp">
</p>

### Tunnel VPN 2 Status:
<p align="center">
  <img width="1000" height="100" src="https://miro.medium.com/max/828/1*s3UmvINRZ5aPvhlv1ALcwQ.webp">
</p>

Now to check the connectivity of the VPN you have to create an ec2 instance in aws side in the same subnet of the vpc and on the other side create the compute engine on the GCP side.

