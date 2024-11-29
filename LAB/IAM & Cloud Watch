Tasks Performed:
1. Create 4 IAM users named “Dev1”, “Dev2”, “Test1”, and “Test2”.
2. Create 2 groups named “Dev Team” and “Ops Team”.
3. Add Dev1 and Dev2 to the Dev Team.
4. Add Dev1, Test1 and Test2 to the Ops Team.

Tasks Performed:
1. Create policy number 1 which lets the users to:
a. Access S3 completely
b. Only create EC2 instances
c. Full access to RDS
2. Create a policy number 2 which allows the users to:
a. Access CloudWatch and billing completely
b. Can only list EC2 and S3 resources
3. Attach policy number 1 to the Dev Team from task 1
4. Attach policy number 2 to Ops Team from task 1

Tasks Performed:
1. Create a role which only lets user1 and user2 from task 1 to have complete access to VPCs and DynamoDB.
2. Login into user1 and shift to the role to test out the feature.

Tasks Performed: 
1. Create a dashboard which lets you check the CPU utilization and networking for a particular EC2 instance.

Tasks Performed: 
1. Create a CloudWatch billing alarm which goes off when the estimated charges go above $500. 
2. Create a CloudWatch alarm which goes off to an Alarm state when the CPU utilization of an EC2 instance goes above 65%. Also add an SNS topic so that it notifies the person when the threshold is crossed.



Here I Mentioned the Steps which I performed for this LAB

Step 1: Create IAM Users
1.	Go to the IAM Console:
o	Open the AWS Management Console and navigate to IAM.
2.	Create Users:
o	Click on Users > Add users.
o	Add the user names: Dev1, Dev2, Test1, Test2.
o	For each user:
	Enable AWS Management Console access.
	Set a custom password or let AWS generate one.
	Uncheck the box for Require password reset (optional).
o	Click Next.
3.	Permissions:
o	Skip permissions for now (they will be added later through groups).
o	Click Next and then Create users.

Step 2: Create Groups
1.	Create Dev Team Group:
o	In the IAM console, click User groups > Create group.
o	Name the group Dev Team.
o	Skip attaching permissions for now (permissions can be added later).
o	Click Create group.
2.	Create Ops Team Group:
o	Repeat the steps above and name the group Ops Team.

Step 3: Add Users to Groups
1.	Add Users to Dev Team:
o	Go to User groups in the IAM console.
o	Click on the Dev Team group.
o	Under the Users tab, click Add users.
o	Select Dev1 and Dev2 and click Add users.
2.	Add Users to Ops Team:
o	Go to User groups in the IAM console.
o	Click on the Ops Team group.
o	Under the Users tab, click Add users.
o	Select Dev1, Test1, and Test2, then click Add users.


Step 4: Create Policy Number 1
Policy Number 1 Permissions:
•	Full access to S3.
•	Create EC2 instances only.
•	Full access to RDS.
1.	Go to the IAM Console:
o	Open the AWS Management Console and navigate to IAM > Policies > Create policy.
2.	Define the Policy JSON:
o	Choose the JSON tab and paste the following policy:
json
Copy code
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "ec2:RunInstances",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "rds:*",
            "Resource": "*"
        }
    ]
}
3.	Review and Name the Policy:
o	Click Next.
o	Provide a name like Policy1
o	Click Create policy.

Step 5: Create Policy Number 2
Policy Number 2 Permissions:
•	Full access to CloudWatch and Billing.
•	List EC2 and S3 resources only.
1.	Create Another Policy:
o	Go to IAM > Policies > Create policy.
2.	Define the Policy JSON:
o	Use the following JSON for Policy Number 2:
json
Copy code
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "cloudwatch:*",
                "aws-portal:*"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:Describe*",
                "s3:List*"
            ],
            "Resource": "*"
        }
    ]
}
3.	Review and Name the Policy:
o	Click Next.
o	Provide a name like Policy2
o	Click Create policy.

Step 6: Attach Policy Number 1 to Dev Team
1.	Navigate to Groups:
o	Go to IAM > User groups and select the Dev Team group.
2.	Attach the Policy:
o	Under the Permissions tab, click Add permissions > Attach policies.
o	Search for Policy1 and select it.
o	Click Add permissions.

Step 7: Attach Policy Number 2 to Ops Team
1.	Navigate to Groups:
o	Go to IAM > User groups and select the Ops Team group.
2.	Attach the Policy:
o	Under the Permissions tab, click Add permissions > Attach policies.
o	Search for Policy2 and select it.
o	Click Add permissions.




Task 8: Create a Role for User1 and User2 with Access to VPCs and DynamoDB
1.	Go to the IAM Console:
o	Open the AWS Management Console and navigate to IAM > Roles.
2.	Click on “Create Role”:
o	Under Select trusted entity, choose Custom trust policy.
3.	Define the Trust Policy:
o	Use the following JSON as the trust policy:
json
Copy code
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::YOUR_ACCOUNT_ID:user/Dev1",
                    "arn:aws:iam::YOUR_ACCOUNT_ID:user/Dev2"
                ]
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
o	Replace YOUR_ACCOUNT_ID with your AWS account ID.
o	Replace Dev1 and Dev2 with the exact names of User1 and User2 created in Task 1.
4.	Attach Permissions for VPC and DynamoDB:
o	In the next step, attach an existing policy or create a custom policy.
Example Custom Policy for VPC and DynamoDB:
o	Choose Create Policy and use the following JSON:
json
Copy code
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "vpc:*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "dynamodb:*",
            "Resource": "*"
        }
    ]
}
o	Save this policy as VPC-DynamoDB-FullAccess and attach it to the role.
5.	Review and Name the Role:
o	Name the role (e.g., VPC-DynamoDB-Role).
o	Review the settings and click Create Role.

Task 9: Grant Users Permission to Assume the Role
1.	Go to IAM Users:
o	Navigate to IAM > Users.
o	Select Dev1 (User1).
2.	Add an Inline Policy for Role Assumption:
o	Under Permissions, click Add inline policy.
o	Use the following JSON to allow User1 to assume the role:
json
Copy code
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "sts:AssumeRole",
            "Resource": "arn:aws:iam::YOUR_ACCOUNT_ID:role/VPC-DynamoDB-Role"
        }
    ]
}
o	Click Review Policy, name it Assume-VPC-DynamoDB-Role, and save.
3.	Repeat for User2 (Dev2):
o	Attach the same inline policy to User2.

Task 10: Test the Role by Logging in as User1
1.	Log in as IAM User1:
o	Use the credentials for User1 (Dev1) to log in to the AWS Management Console.
2.	Switch to the Role:
o	In the top-right corner, click the Account/Username dropdown > Switch Role.
o	Enter the Account ID and Role Name (e.g., VPC-DynamoDB-Role).
o	Click Switch Role.
3.	Test Access to VPC and DynamoDB:
o	Navigate to VPC:
	Try creating or modifying subnets, route tables, or other VPC resources.
o	Navigate to DynamoDB:
	Try creating, querying, or modifying tables.
4.	Log in as User2 (Dev2):
o	Repeat the same steps to ensure User2 can assume the role and access the required services.




Step 11: Access the CloudWatch Console
1.	Open the AWS Management Console.
2.	Search for and select CloudWatch.

Step 2: Create a New Dashboard
1.	In the CloudWatch console, click Dashboards in the left navigation pane.
2.	Click Create dashboard.
3.	Enter a name for your dashboard (e.g., EC2-Monitoring).
4.	Click Create dashboard.

Step 12: Add a Widget for CPU Utilization
1.	In the Add widget dialog box, select Line (or any other graph type you prefer).
2.	Click Configure.
Configure the Widget:
1.	Under Metric name, search for and select CPUUtilization.
o	Path: EC2 > Per-Instance Metrics > CPUUtilization.
2.	Select the instance you want to monitor from the list.
3.	Configure additional options:
o	Set the Period (e.g., 1 minute, 5 minutes).
o	Set the Statistic to Average or as required.
4.	Click Add to dashboard.

Step 13: Add a Widget for Network Traffic
1.	Click Add widget again.
2.	Select Line (or another graph type).
3.	Click Configure.
Configure the Widget:
1.	Search for metrics related to network traffic:
o	NetworkIn: Amount of incoming network traffic to the instance.
o	NetworkOut: Amount of outgoing network traffic from the instance.
o	Path: EC2 > Per-Instance Metrics > NetworkIn / NetworkOut.
2.	Select the instance you want to monitor from the list.
3.	Configure additional options:
o	Set the Period (e.g., 1 minute, 5 minutes).
o	Set the Statistic to Sum or as required.
4.	Click Add to dashboard.



Step 14: Save the Dashboard
1.	After adding all desired widgets, click Save dashboard.
2.	Review the dashboard to ensure the widgets display the data correctly.

Step 15: Test and Verify
1.	Navigate to the dashboard from the CloudWatch console.
2.	Observe the real-time metrics for CPU utilization and network traffic.
3.	Optionally, simulate load on the EC2 instance to test how metrics respond.


Task 16: Create a CloudWatch Billing Alarm for Charges Above $500
1.	Access CloudWatch Console:
o	Open the AWS Management Console and navigate to CloudWatch.
2.	Enable Billing Alerts (if not already enabled):
o	Go to Billing Preferences in the Billing Dashboard.
o	Check Receive Billing Alerts and save your preferences.
3.	Create a Billing Alarm:
o	In the CloudWatch console, go to Alarms > Create alarm.
o	Under Select metric, click Billing (or search for it).
o	Choose Total Estimated Charge.
o	Click Select metric.
4.	Define Alarm Conditions:
o	Set the threshold type to Static.
o	Choose Greater than and set the value to 500.
o	Adjust the period (e.g., 6 hours for periodic evaluation).
5.	Configure Actions:
o	Create or select an existing SNS topic to notify a recipient (e.g., your email or phone number).
o	If creating a new topic:
	Provide a topic name (e.g., BillingAlarmTopic).
	Add recipient email(s) under Subscriptions.
	Confirm the subscription in your email.
6.	Name and Save Alarm:
o	Name the alarm (e.g., Billing-Over-500).
o	Click Create alarm.

Task 17: Create a CloudWatch Alarm for CPU Utilization Above 65%
1.	Access CloudWatch Console:
o	Go to CloudWatch > Alarms > Create alarm.
2.	Select the EC2 CPU Utilization Metric:
o	Click Select metric.
o	Navigate to EC2 > Per-Instance Metrics > CPUUtilization.
o	Choose the specific EC2 instance you want to monitor.
o	Click Select metric.
3.	Define Alarm Conditions:
o	Set the threshold type to Static.
o	Choose Greater than and set the value to 65.
o	Adjust the Period (e.g., 5 minutes) for more granular evaluation.
4.	Configure Actions:
o	Create or select an existing SNS topic to notify when the alarm enters the ALARM state.
o	If creating a new topic:
	Provide a topic name (e.g., CPUAlarmTopic).
	Add recipient email(s) under Subscriptions.
	Confirm the subscription in your email.
5.	Name and Save Alarm:
o	Name the alarm (e.g., High-CPU-Alarm).
o	Click Create alarm.

Testing and Verification
1.	Billing Alarm:
o	Confirm you received the subscription email and approved it.
o	Simulate increased billing (e.g., launch additional resources) to test the threshold alert.
2.	CPU Utilization Alarm:
o	Stress test the EC2 instance to push CPU usage above 65% (e.g., by running compute-intensive tasks).
o	Check if the alarm triggers and sends the SNS notification.
