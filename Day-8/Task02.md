## AWS

### Day 8: Enable Stop Protection for EC2 Instance

During the migration process, the Nautilus DevOps team created several EC2 instances in different regions. They are currently in the process of identifying the correct resources and utilization and are making continuous changes to ensure optimal resource utilization. Recently, they discovered that one of the EC2 instances was underutilized, prompting them to decide to change the instance type. Please make sure the Status check is completed (if its still in Initializing state) before making any changes to the instance.

1) Change the instance type from t2.micro to t2.nano for datacenter-ec2 instance.

2) Make sure the ec2 instance datacenter-ec2 is in running state after the change.



Use below given AWS Credentials: (You can run the showcreds command on aws-client host to retrieve these credentials)

Console URL	https://295533237186.signin.aws.amazon.com/console?region=us-east-1
Username	kk_labs_user_871687
Password	dVWg^8We@JhA
Start Time	Thu Jan 01 12:39:32 UTC 2026
End Time	Thu Jan 01 13:39:32 UTC 2026

![alt text](image-2.png)