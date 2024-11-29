AWS LAB Scenario:
1.	Create two Instances in one VPC with different subnet and Route Table in one AZ (Availability Zone). One is with Public and Private IP both and one is only with Private IP.
2.	Create custom IGW (Internet Gateway) for Public EC2 and Create NAT (Network Address Translation) for private EC2 and connect the Private EC2 from Public EC2 and update the package of Private EC2.
3.	Create custom SG (Security Group) and Nacl (Network Access Control List) for your VPC.
4.	Create one another Instance in different region with custom VPC, Subnet and Route Table with Private IP and configure VPC Peering and connect from the 1st Public EC2 Instance.


Steps:
1.	Create VPC
Go to VPC – Your VPC – Create VPC – Give Name (My_VPC) – Give Private IPv4 IP range with CIDR (192.168.0.0/16) – Tenancy Default – Create VPC
2.	Create IGW and attached to VPC
Go to Internet Gateway under VPC – Create IGW – Give Name – Create IGW – Go to action – Select your VPC (My_VPC) – Attach IGW
3.	Create Subnet for Public Instance
Go to Subnets under VPC – Create Subnet – Select VPC (My_VPC) – Give Subnet Name (My_Public_Subnet) – Choose AZ {AP-South-1a (Mumbai)} – Give IPv4 Subnet CIDR block (192.168.0.0/24) – Create Subnet
4.	Create Route Table for Public Instance and add Route towards IGW
Go to Route Table under VPC – Give Name (My_Public_RT) – Select VPC (My_VPC) – Create Route Table – Action – Edit Route – Add Route – Select Destination 0.0.0.0/0 – Select Target Internet Gateway – Select My_IGW – Save Changes
5.	Edit Route Table Association in Your Custom Subnet (My_Public Subnet)
Go to Subnets under VPC – Select Subnet (My_Public Subnet) – Action – Edit Route Table Association – Select Route Table ID (My_Public_RT) - Save
6.	Create SG
Go to Security Group under Security – Create SG – Give Name (My_SG) – Give Description (My_SG) - Select VPC (My_VPC) – Add rule in Inbound rule select All Traffic in type then select 0.0.0.0/0 CIRD block – Create Security Group
Note: Outbound rule (All Traffic) was already created you can also modify it.


7.	Create NACL
Go to Network ALC under Security – Create Network ALC – Give Name (My_NACL) – Select VPC (My_VPC) – Create Network ALC – Action – Edit Inbound and Outbound Rule – Rule Number 1 Type All Traffic Source 0.0.0.0/0 Allow – Save Changes (Do the same for Inbound and Outbound rule)
Note: NACL’s evaluate rules in order, starting with the lowest number rules means lower the number higher the president.
8.	Launch EC2 Instance (Amazon Linux) with Public IP
Go to Ec2 – Go to Instances under Instances – Launch Instance – Give Name (My_Public_Instance) – Select OS Image (Amazon Linux) – Select Instance type (type t3.micro free tire eligible) – Create Key Pair – Give Key Pair Name – Select .ppk key for access Instance through Putty – Edit Network Settings – Select VPC (My_VPC) – Select Subnet (My_Public_Subnet) – Enable Auto Assign Public IP – Select existing Security Group – Select (My_SG) – Configure Storage as per your need (8GB, Standard) – Launch Instance
9.	Access your Instance (My_Public_Instance) through Putty
Go to google – Search putty,org – Select the Putty Version as per your OS (Operating System) – Download and Install Putty in your system – Launch Putty – Give your Instance’s Public IP (My_Public Instance) in Host Name or IP Address – Go to Connection in left pane – Go to SSH – Go to Auth – Go to – Credential – Browse the .ppk file in Private Key File for Authentication and open – Go to Session – Open – Accept – Login  with ec2-user(Default user name in Amazon Linux)
10.	Create another Subnet for Private Instance
Go to Subnet under VPC – Create Subnet – Select VPC (My_VPC) – Give Name (My_Private_Subnet) – Give IPv4 CIDR subnet block (192.168.1.0/24) – Create VPC
11.	Create another Route Table Association for Private Instance and attached Subnet (My_Private_Subnet)
Go to Route Table under VPC – Create Route Table – Give Name (My_Private_RT) – Select VPC (My_VPC) – Action – Edit Subnet Association – Select Subnet (My_Private_Subnet) – Save Association
12.	Create NAT and attach to Subnet and Add Route towards NAT
Go to NAT Gateway under VPC – Create NAT Gateway – Give Name (My_Private_NAT) – Select Subnet (My_Public_Subnet) – Connectivity Type Public – Select EIP (Elastic Private IP) – Create NAT Gateway – Go to Route Table under VPC – Select Route Table – Action – Edit Route – Select Destination 0.0.0.0/0 – Select Target NAT Gateway – Select My_Private_NAT – Save Changes
13.	Launch another Instance (Amazon Linux) only with Private IP
Go to EC2 – Go to Instances under Instances – Launch Instance – Give Name (My_Private_Instance) – Select OS Image (Amazon Linux) - Select Instance type (type t2.micro free tire eligible) - Create Key Pair – Give Key Pair Name (My_PEM_Key) – Select .pem key for access Instance through SSH terminal – Edit Network Settings – Select VPC (My_VPC) – Select Subnet (My_Private_Subnet) – Disable Auto Assign Public IP – Select existing Security Group – Select (My_SG) – Configure Storage as per your need (8GB, Standard) – Launch Instance

14.	Connect Private Instance from Public Instance
Connect Your Public Instance through Putty – Login with User Name (ec2-user) – Create a .pem key file in root directory of Public Instance - Now some commands need to perform Below I Mentioned
	sudo su (For change the user now I’m a root user)
	sudo yum update –y (For update the YUM repository)
	vi My_PEM_Key.pem (For create a file with file name and extention) – will open a file here paste the  .pem key’s file content which was downloaded in the time of .pem key creation
	:wq! (for save the file)
	Chmod 400 My_PEM_Key (For change the permission of the file)
	ssh –i My_PEM_Key.pem ec2-user@Private IP of Private Instance (For Connect Private Instance from Public Instance) – Now you are in Private Instance – Type yes – Login with user name (ec2-user)
	sudo su (For change the user now I’m a root user)
	sudo yum update –y (For update the YUM repository)


15.	Create VPC in Another Region {ap-southeast-1b(Singapore)}
Go to VPC – Your VPC – Create VPC – Give Name (My_Singapore_VPC) – Give Private IPv4 IP range with CIDR (10.0.0.0/16) – Tenancy Default – Create VPC
16.	Create Subnet in {ap-southeast-1b(Singapore)} Region
Go to Subnets under VPC – Create Subnet – Select VPC (My_Singapore_VPC) – Give Subnet Name (My_Singapore_Subnet) – Choose AZ – Give IPv4 Subnet CIDR block (10.0.0.0/24) – Create Subnet
17.	Create Route Table in {ap-southeast-1b(Singapore)} Region
Go to Route Table under VPC – Give Name (My_Singapore_RT) – Select VPC (My_Singapore_VPC) – Create Route Table
Note: Here we didn’t create custom Security Group here we are using Default Security Group.
18.	Edit Route Table Association in {ap-southeast-1b(Singapore)} Region (My_Singapore_ Subnet)
Go to Subnets under VPC – Select Subnet (My_Public Subnet) – Action – Edit Route Table Association – Select Route Table ID (My_Singapore_RT) – Save
19.	Edit Default Security Group’s Inbound Rule in {ap-southeast-1b(Singapore)} Region
Go to Security Group under Security – Select Default SG –Action – Edit inbound Rule – Add rule select All Traffic in type then select 0.0.0.0/0 CIRD block – Save Rules
Note: Outbound rule (All Traffic) was already created you can also modify it.



20.	Launch another Instance in {ap-southeast-1b(Singapore)} Region (Amazon Linux) only with Private IP
Go to EC2 – Go to Instances under Instances – Launch Instance – Give Name (My_Singapore_Instance) – Select OS Image (Amazon Linux) - Select Instance type (type t2.micro free tire eligible) - Create Key Pair – Give Key Pair Name (Singapore_Key) – Select .pem key for access Instance through SSH terminal – Edit Network Settings – Select VPC (My_Singapore_VPC) – Select Subnet (My_Singapore_Subnet) – Disable Auto Assign Public IP – Select existing Security Group – Select (Dafault) – Configure Storage as per your need (8GB, Standard) – Launch Instance

21.	Configure VPC Peering 
Go to Peering Connection under VPC of {AP-South-1a (Mumbai)} – Create Peering Connection – Give Name (India_to_Singapore) – Select Requester VPC (My_VPC) – Select Another VPC Peer with My Account (Because both the VPC’s are created in same account but in Different Region) – Select Region Another Region – Select Region (ap-southeast-1) – Select Accepter VPC ID (My_Singapore_VPC) – Go to Peering Connection under VPC of Singapore Region – Select Peering Connection – Action – Accept Request – Go to Route Table under VPC of Singapore Region – Select Route Table (My_Singapore_RT) – Edit Route – Add Route – Destination 192.168.0.0/16 (IPv4 CIDR range of My_VPC which is in {AP-South-1a (Mumbai)} – Target Peering Connection – Select Peering Connection – Save Changes - Go to Route Table under VPC of Mumbai  Region – Select Route Table (My_Public_RT) – Edit Route – Add Route – Destination 10.0.0.0/16 (IPv4 CIDR range of My_Singapore_VPC which is in {ap-southeast-1b(Singapore)} – Target Peering Connection – Select Peering Connection – Save Changes
22.	Connect Singapore Region Private Instance from Mumbai Region Public Instance
Connect Your Public Instance through Putty – Login with User Name (ec2-user) – Create a .pem key file in root directory of Public Instance - Now some commands need to perform Below I Mentioned
	sudo su (For change the user now I’m a root user)
	sudo yum update –y (For update the YUM repository)
	vi Singapore_Key.pem (For create a file with file name and extention) – will open a file here paste the  .pem key’s file content which was downloaded in the time of .pem key creation
	:wq! (for save the file)
	Chmod 400 My_PEM_Key (For change the permission of the file)
	ssh –i Singapore_Key.pem ec2-user@Private IP of Singapore Region Private Instance (For Connect Singapore Region Private Instance from Mumbai Region Public Instance) – Now you are in Singapore Region Private Instance – Type yes – Login with user name (ec2-user)
