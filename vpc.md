# STEPS TO CREATE A VPC IN AWS CONSOLE + NAMING CONVENTION

[VPC -> IGW -> SUBNETS -> RT -> ROUTE -> SUBNET ASSOOCIATION]

1. select the region [ie: us-east-1]
2. create vpc [dev-vpc]
3. enable dns hostname in the vpc [VPC -> Actions: edit dns hostname ]
4. Create internet gateway [dev-igw]
5. Attach igw to the VPC [Actions -> Attach to VPC]
6. Create the public subnets [dev-public-subnet AZ1][Filter by VPC]
7. Enable Auto Assign IP settings [Select -> Actions -> edit subnet -> enable ]
8. Create Public Route Table [dev-public-RT -> select VPC]
9. Add public Route to the Public Route Table
   [Route -> edit route -> add route -> anywhere (0.0.0.0/0)-> target(igw) ]
10. Associate the public subnets with the public route table
   [subnet associations -> edit -> select public subnet and save association]
11. Create the private Subnets [dev-private-subnet AZ1]


============================================================================================

https://bandandevopsjourney.hashnode.dev/devopsday-80-project-1
VPC
create two ec2 instance
we have a client and they want 150 ip adress 
so we are working with 10.0.0.0/24

jumpServer
- amazon linux
- to have both a public and a private ip address
- create a new SG (jumpSG)
   -open port 22 and myIP cidr myipaddress
- enable public ip address
- add the create VPC

dbServer
- amazon linux
- just a private ip adress
- create a new SG (dbSG)
  -open ssh 22 and vpc cidr block 10.0.0.0/24
- need NAT allocated on the private route table where the db server is located
  -db AZ [ex: us-west-2b]
  -go to route table and look for [private us-west-2b ]
  - edit route --> 0.0.0.0/0 and then teslaNAT
  - to connect to internet
 ping google.com
and it connects

create a webserver
create an ec2 instance
- named webserver
- amazon linux --> tesla vpc --> public subnet --> enable auto assign 
- create a webSG --> ssh from myIP/custom 10.0.0.0/24 local access
                     all icmp ipv4 custom 10.0.0.0/24
                     and 80, 443 anywhere
- use user data to install an apache server
#!/bin/bash
 sudo yum install httpd -y 
 sudo systemctl start httpd
 sudo systemctl enable httpd 
 sudo echo "<h1> Hello World</h1>" >> /var/www/html/index.html
 sudo echo "<h1>This is a simple web server </h1> " >> /var/www/html/index.html
 
- ping the webserver == ping [public and private ipaddress of webserver]
 - dont work packages lost
 - add the icmp SG
- curl  [private/pub ip add on jumpserver]:80
     - we see the webserver



