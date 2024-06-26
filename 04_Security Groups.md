### Security Groups
![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/55d1d736-910d-4019-8fb6-06b8d06d6911)

The security group is a virtual firewall that controls inbound and outbound traffic on EC2 instances
Try to look at the architectural diagram above,we notice that VPC is our private section in the cloud and all AWS services that will be used for this project is embeded inside the VPC,
Now the security which is also one of the resources in the architecture will help to control how traffic flow through every other resources.
we will be creating resource groups for  Webservers,Databases,Application load Balancers,EFS etc.
Now in other illustrate how the security groups will combine to control traffic,by observing the architecture above,when traffic comes from the internet the traffic must first go through the Application load balancer before it can access the webservers and as such the webservers can only accept traffic from the application load balancer and the Database servers are only going to accept traffic from the webservers and the EFS can only accept traffic from the webservers.

#### Creating Security Groups

![SG1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/f7e3cb58-f672-4459-b5eb-a40f322d122f)

Now lets begin the process of creating security groups in the AWS management console,while in management console,ensure that your region is selected my own region is Singapore
on the left part select security group click create security group at the top left corner AS shown above
The list of security groups that will be created are
### Application Load Balancer Security Group(ALB)
<br>
### Webservers Security Group
<br>
### Database Security Group
<br>
### Elastic File System Security Group(EFS)
<br>
### SSH Security Group
<br>
### Application Load Balancer Security Group(ALB)
The first security group we will be creating today is ALB security group
![ALB1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/ded9654d-46ee-421f-826b-beca4e124a8a)

![ALB2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/1f34ed5b-8e57-41e0-8b77-1420a13cd1e7)

![ALB3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/1cb3a60e-9757-4faf-90cd-6d7b4749fb6e)

On the create security group page,give a name to the security group,under Description can use same name as  name of the security group,under VPC select the VPC we created earlier,under Inbound rules,click add rules,under type
select HTTP,under source select Anywhere,click add rules again this time under Type select HTTPS and under source select Anywhere and scroll down at the bottom right corner and select Create security Group,all these can be seen in 3 diagrams above


### Webservers Security Group
![WB_SG1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/70ce0fea-852e-4e6e-9283-6164fc2f396f)

![WB_SG2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/737ffd04-b77c-4408-95fb-acf00e5d88f4)

![WB_SG3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/d47c6b9e-b887-4e03-b1c0-c53cf65bb535)

The second security group we will be creating is webservers security group,so click create security group again,give a name to the security group,under Description can use same name as name of the security group,under VPC select the VPC we created earlier,under Inbound rules,click add rules,under type select HTTP,under  Source  select the Application Load Balancer Security Group we created previously,
again click add rules again this time under Type select HTTPS and under source select  Application Load Balancer Security Group we created previously,and scroll down at the bottom right corner and select Create security Group,all these can be seen in 3 diagrams above

### Database Security Group
![DB_SG1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/3eccfc9c-5882-4933-baec-35fc33ebeca0)

![DB_SG2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/55a6c009-1bf1-4c04-beec-06270aa3762a)

![DB_SG3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e8470328-0561-438c-a203-ead66c920c73)

The next security group that we will create now is Database Security Group,so click create security group again,give a name to the security group,under Description can use same name as
name of the security group,under VPC select the VPC we created earlier,under Inbound rules,click add rules,under type select MySQL/Aurora,under Source Select Webservers Security Group that we created previously

### Elastic File System Security Group(EFS)
![EFS_SG1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/017bd777-4aba-4e73-aece-2a90fa2aafe4)
![EFS_SG2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/edf32ab3-ea79-45a3-a7ea-6bca230d52e9)

The next Security Group we wil create is the EFS security group,so click create security group again,give a name to the security group,under Description can use same name as name of the security group,under VPC select the VPC we created earlier,under Inbound rules,click add rules,under Type select NFS and uner source select Webservers Security Group that we created previously.This can be seen in above diagrams

![EFS_SG3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/6a977c29-5372-4f6f-ab2a-d6bdbd84fdc9)

One last step to do is to route traffic to the EFS itself,and to do this,check the box next to the EFS security group and click edit inbound rules,under Type select NFS again and under source this time select NFS security group we created previously.This can be seen in above diagrams

### SSH Security Group
![SSH_SG1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/b223b775-2163-463a-91d5-a1c7ba7af4b4)

![SSH_SG2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a083fce4-65e5-4b91-b877-71ab1be8b0ba)

The last security group we will be creating is SSH security group,to begin click create security group again,give a name to the security group,under Description can use same name as name of the security group,under VPC select the VPC we created earlier,under Inbound rules,click add rules,under Type select SSH,under source select MY IP and this will authomatically display IP of your local machine and click create security group at the bottom right corner.
