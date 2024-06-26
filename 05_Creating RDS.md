### Relational Database System(RDS) Creation
![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/b01fe126-d04f-4d21-87a7-06e44dc2d1d7)

Now we will be creating an RDS in AWS,while in the management console,ensure you are in the right region,click on services,click Databases at the buttom and select RDS
Now the Amazon RDS page is on display as seen above.
<br>

![RDS1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/68a0a578-13d3-49c1-853b-aeea459f7d0b)

![RDS2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/004548f9-264c-4913-bf53-2bc3ad975407)

Before creating the RDS,we first need to create subnet groups,so on the left select subnet groups,now select create DB Subnet Group at the top left,give a name to the subnet group,
under description give same name as subnet group,under VPC select the demo VPC that was earlier created,under Availability zone,select the two availability zones,in my case its ap-southeast-1a and ap-southeast-1b,under subnet,in the first availability zone select 10.0.4.0/24 and in second availabilty zone select select 10.0.5.0/24 and the reason we specifically selected these two 1pv4 CIDR is because they are the private subnets created for the  Database Tier during creating of the VPC.
<br>
The diagrams for creating subnet groups is shown above
<br>
Now that we have successfully created subnet group we can now go ahaed to create the RDS
<br>



![RDS9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/09ed5083-daf2-4e90-bcca-46c421423afd)

![RDS6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c8c94d93-ad10-4b38-824f-b8cc9daa46f6)

![RDS4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c6672b3c-8a50-4c98-95a9-94d64be30db4)

Click create Database,under Choose a database creation method leave at Standard create,under Engine options choose Mysql,Engine Version choose MySQL 5.7.44,under Template choose free tier,DB instance identifier choose a name,under Credential settings choose a master username, as shown above
<br>
Under credentials management choose self management and specify your password.
<br>
![RDS7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c60b3390-106b-4fef-aea9-96d82dad3484)

under Instance configuration,leave it as default to db.t3.micro and also leave the storage as default as shown above
<br>
under Connectivity,leave the Compute resource as default,under Virtual private cloud (VPC) select our VPC we created earlier
<br>
under DB subnet group,ensure to select the subnet group we just created,under Public access choose NO
<br>
![RDS8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/213a6e90-8111-4532-abc7-0211550d463b)
under VPC security group (firewall)Info choose existing,under Existing VPC security groups choose the Database security group we created
<br>
Under Availability zone select any of your choice in my case I will choose the first Availability zone 
<br>
Additional configuration leave default at port 3306,under Database authentication leave default to password usage
<br>
under Additional configuration,give a name to your Database and click create Database and wait for a while for the database to create

The Database is successfully  created as seen above
<br>
Now that we have created the Database,it is important to save the Database credentials,so at the top right click on view credentials
Now you can see your Database credentials as shown above
<br>

Now once the Database is available,under Connectivity and Security tab you will see your Database endpoint
<br>
Under Configuration tab you will see every information of your Database as shown above



