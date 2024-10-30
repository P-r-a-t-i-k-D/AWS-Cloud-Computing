Lab Scenario

1.	Create an EFS and Connect it to 3 different EC2 Instances. Make sure that all instances have different operating systems. For instance, Amazon Linux 2, Redhat Linux, Ubuntu.

Note: In AWS, security groups are stateful. This means if you let traffic come into your instance, the responses can leave without needing specific outbound rules. So, once you allow an incoming request, the replies are automatically allowed out.


Need to allow below mentioned Inbound rules (Also you can allow as per your requirement)


EFS: Elastic File System


Instances Amazon Linux2, Redhat Linux, Ubuntu


All the Systems are attached with EFS (EFS ID - fs-0287872a4a0dee2e0)


All the instances are connected to EFS, which means you can access the same files across all instances. This allows for consistent file sharing and collaboration, as any changes made to a file will be reflected on every instance.


Here are the steps I took to create the lab below I mentioned the steps briefly:
1.	Set Up Environment: Selected AWS region and configured IAM roles.
2.	Configure Security Groups: Set up inbound and outbound rules.
3.	Launch EC2 Instances: Created [number] instances with required specifications.
4.	Install Software: Installed necessary tools on each instance.
5.	Attach EFS: Created and mounted EFS file system to all instances.
6.	Test Connectivity: Verified access to EFS and shared files.
7.	Final Verification: Checked file access across instances.
Steps to Launch Amazon_Linux_2 and Attach the EFS in it
	
1.	Launch EC2 Instance (Amazon_Linux_2) with Public IP
Go to Ec2 – Go to Instances under Instances – Launch Instance – Give Name (Amazon_Linux_2) – Select OS Image (Amazon Linux 2) – Select Instance type (type t3.micro free tire eligible) – Create Key Pair – Give Key Pair Name – Select .ppk key for access Instance through Putty – Edit Network Settings – Select VPC (Default) – Select Subnet (Default) – Enable Auto Assign Public IP – Select existing Security Group – Select (Default) – Configure Storage as per your need (8GB, Standard) – Launch Instance

2.	Access your Instance (Amazon_Linux_2) through Putty
•	Go to google – 
•	Search putty,org – 
•	Select the Putty Version as per your OS (Operating System) – 
•	Download and Install Putty in your system – 
•	Launch Putty – 
•	Give your Instance’s Public IP (Amazon_Linux_2) in Host Name or IP Address – 
•	Go to Connection in left pane – 
•	Go to SSH – 
•	Go to Auth – 
•	Go to – Credential – Browse the .ppk file in Private Key File for Authentication and open – 
•	Go to Session – Open – Accept – 
•	Login  with ec2-user(Default user name of Amazon Linux)

1.	Attach EFS to Your Instance (Amazon_Linux_2)
•	mkdir /efs-mnt (For create a directory where you mount the NFS) 
•	sudo su (For change the user now I’m a root user)
•	sudo yum update –y (For update the YUM repository)
•	sudo yum install amazon-efs-utils (For Install NFS Package)
•	sudo mkdir efs-mnt (For create the mount point)
Go to File System under NFS Click on – File system ID – Click on attach – Copy the mount helper command and run it – Copy the NFS client command and run it
1.	sudo mount -t efs -o tls fs-0287872a4a0dee2e0:/ ~/efs-mnt (Mount Point)
2.	sudo mount -t nfs4 –o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0287872a4a0dee2e0.efs.eu-north-1.amazonaws.com:/  ~/efs-mnt (Mount Point)
•	Go to /efs-mnt and Create a directory and create one text file in the directory and add some comments in it to check the EFS is properly working or not.
•	cd /efs-mnt (For go to the directory)
•	sudo mkdir File Name (For create directory)
•	cd File Name (For go to the directory)
•	sudo nano file1.txt (File Name) – Add some comments in the File – Press (Ctrl+X) (For create and save the File)
•	sudo cat file1.txt (For see the Comment in the file)



Steps to Launch Redhat_Linux and Attach the EFS in it

	
3.	Launch EC2 Instance (Redhat_Linux) with Public IP
Go to Ec2 – Go to Instances under Instances – Launch Instance – Give Name (Redhat_Linux) – Select OS Image (Redhat Linux) – Select Instance type (type t3.micro free tire eligible) – Create Key Pair – Give Key Pair Name – Select .ppk key for access Instance through Putty – Edit Network Settings – Select VPC (Default) – Select Subnet (Default) – Enable Auto Assign Public IP – Select existing Security Group – Select (Default) – Configure Storage as per your need (8GB, Standard) – Launch Instance

4.	Access your Instance (Redhat_Linux) through Putty
•	Go to google – 
•	Search putty,org – 
•	Select the Putty Version as per your OS (Operating System) – 
•	Download and Install Putty in your system – 
•	Launch Putty – 
•	Give your Instance’s Public IP (Redhat_Linux) in Host Name or IP Address – 
•	Go to Connection in left pane – 
•	Go to SSH – Go to Auth – 
•	Go to Credential – Browse the .ppk file in Private Key File for Authentication and open – 
•	Go to Session – Open – Accept – 
•	Login  with ec2-user(Default user name of Redhat Linux in AWS)

2.	Attach EFS to Your Instance (Redhat_Linux)
•	mkdir /efs-mnt (For create a directory where you mount the NFS) 
•	sudo yum update –y (For update the YUM repository)
•	sudo yum install nfs-utils (For Install NFS Package)
•	sudo mkdir efs-mnt (For create the mount point)
Go to File System under NFS Click on – File system ID – Click on attach – Copy the NFS client command and run it
1.	sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0287872a4a0dee2e0.efs.eu-north-1.amazonaws.com:/  ~/efs-mnt (Mount Point)
•	Go to /efs-mnt and Create a directory and create one text file in the directory and add some comments in it to check the EFS is properly working or not.
•	cd /efs-mnt (For go to the directory)
•	sudo mkdir EFS (For create directory)
•	cd File EFS (For go to the directory)
•	sudo vi file1.txt (File Name) – i (For edit the file) Add some comments in the File – Press Esc then type :wq! - Enter  (For create and save the File)
•	sudo cat file1.txt (For see the Comment in the file)








Steps to Launch Ubuntu and Attach the EFS in it

	
5.	Launch EC2 Instance (Ubuntu) with Public IP
Go to Ec2 – Go to Instances under Instances – Launch Instance – Give Name (Ubuntu) – Select OS Image (Ubuntu) – Select Instance type (type t3.micro free tire eligible) – Create Key Pair – Give Key Pair Name – Select .ppk key for access Instance through Putty – Edit Network Settings – Select VPC (Default) – Select Subnet (Default) – Enable Auto Assign Public IP – Select existing Security Group – Select (Default) – Configure Storage as per your need (8GB, Standard) – Launch Instance

6.	Access your Instance (Redhat_Linux) through Putty
•	Go to google – 
•	Search putty,org – 
•	Select the Putty Version as per your OS (Operating System) – 
•	Download and Install Putty in your system – 
•	Launch Putty – 
•	Give your Instance’s Public IP (Redhat_Linux) in Host Name or IP Address – 
•	Go to Connection in left pane – 
•	Go to SSH – Go to Auth – 
•	Go to Credential – Browse the .ppk file in Private Key File for Authentication and open – 
•	Go to Session – Open – Accept – 
•	Login  with Ubuntu (Default user name of Ubuntu in AWS)

3.	Attach EFS to Your Instance (Ubuntu)
•	mkdir /efs-mnt (For create a directory where you mount the NFS) 
•	sudo apt-get (For update the repository)
•	sudo apt-get install nfs-common -y (For Install NFS Package)
•	sudo mkdir efs-mnt (For create the mount point)
Go to File System under NFS Click on – File system ID – Copy the DNS Name
1.	sudo mount -t nfs4 fs-0287872a4a0dee2e0.efs.eu-north-1.amazonaws.com:/ ~/efs-mnt (Mount Point)
•	Go to /efs-mnt and Create a directory and create one text file in the directory and add some comments in it to check the EFS is properly working or not.
•	cd /efs-mnt (For go to the directory)
•	sudo mkdir EFS (For create directory)
•	cd File EFS (For go to the directory)
•	sudo vi file1.txt (File Name) – i (For edit the file) Add some comments in the File – Press Esc then type :wq! - Enter  (For create and save the File)
•	sudo cat file1.txt (For see the Comment in the file)
