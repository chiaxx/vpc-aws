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


