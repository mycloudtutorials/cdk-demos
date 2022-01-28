# Learn to setup AWS VPC using Management Console

## Tasks 
- Create VPC
- Create One Public and One Private Subnet
- Create Internet Gateway and Associate to VPC
- Create NAT Gateway in Public Subnet
- Create Public Route Table, Add Public Route via Internet Gateway and Associate Public Subnet
- Create Private Route Table, Add Private Route via NAT Gateway and Associate Private Subnet

## Create VPC
- **Name:** mct-demo-vpc
- **IPv4 CIDR Block:** 10.0.0.0/16

### Create Public Subnet
- **VPC ID:** mct-demo-vpc
- **Subnet Name::** mct-demo-vpc-public-subnet-1
- **Availability zone:** us-west-2a
- **IPv4 CIDR Block:** 10.0.0.0/24  (10.0.0.0 - 10.0.0.255  2^8 = 256 IP Addresses)

### Private Subnet
- **VPC ID:** mct-demo-vpc
- **Subnet Name::** mct-demo-vpc-private-subnet-1
- **Availability zone:** us-west-2a
- **IPv4 CIDR Block:** 10.0.16.0/20  ( 10.0.16.0 - 10.0.16.255 2^12 = 4096 IP Addresses)


## Create Internet Gateway and Associate it to VPC
- **Name Tag:** mct-demo-igw
- Click on **Create Internet Gateway**
- Click on Actions -> Attach to VPC -> mct-demo-vpc

## Create NAT Gateway
- **Name:** my-nat-gateway
- **Subnet:** my-public-subnet-1


## Create Public Route Table and Create Routes and Associate Subnets
### Step-06-01: Create Public Route Table
- **Name tag:** my-public-route-table
- **vpc:** mct-demo-vpc
- Click on **Create**
### Step-06-02: Create Public Route in newly created Route Table
- Click on **Add Route**
- **Destination:** 0.0.0.0/0
- **Target:** my-igw
- Click on **Save Route**
### Step-06-03: Associate Public Subnet 1 in Route Table
- Click on **Edit Subnet Associations**
- Select **my-public-subnet-1**
- Click on **Save**


## Step-07: Create Private Route Table and Create Routes and Associate Subnets
### Step-07-01: Create Private Route Table
- **Note:** We will modify the default route table to act as PRIVATE
- **vpc:** mct-demo-vpc

- Click on **Add Route**
- **Destination:** 0.0.0.0/0
- **Target:** my-nat-gateway
- Click on **Save Route**
### Step-07-03: Associate Private Subnet 1 in Route Table
- Click on **Edit Subnet Associations**
- Select **my-private-subnet-1**
- Click on **Save**

## Step-08: Clean-Up
- Delete `my-nat-gateway`
- Wait till NAT Gateway is deleted
- Check the default route table's route, should change to *Blackhole*
- Detach Internet Gateway from VPC
- Delete Internet Gateway
- Delete `mct-demo-vpc`

