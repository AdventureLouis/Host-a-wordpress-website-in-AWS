### Lunching the Setup Server
![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/f1342a64-519f-4831-b756-336fcaaea203)
In order to install the wordpress we will need an EC2 instance
<br>
We will need to install the wordpress into the EC2 instance and save the code to EFS
The EC2 server that we will create will be deployed to the public subnet so as to enable ease of installation and file transfer to EFS
<br>
![Setup1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/d29f4c01-e5b6-4f3e-b3a4-4bd29bfc37e5)

![setup2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c4756b9a-e893-494c-8385-ca2416cd391c)

Now in order to lunch the instance,on AWS management console,click on services and type EC2,then click on EC2 to open EC2 page and click lunch instance at the bottom as shown above
<br>
![setup3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/2d495444-c481-4e9a-aa2b-5fd37758812f)
![setup4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/4604230e-2c4e-474f-bd9f-d9bc1f491676)
Now we have the page to lunch an instance,under name type the name of your server,under Application and OS Images (Amazon Machine Image) click drop down and select Amazon Linux
<br>

Under Amazon Machine Image (AMI),"Amazon Linux 2 AMI (HVM)", this is the free tier AMI. make sure not to choose "Amazon Linux 2023", even though this one is also free tier, it will not work when we try to install WordPress in it
<br>
Under instance type,select t2.micro
<br>
Under Key pair (login),click drop down and select the key pairs you previously created
<br>
![setup5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/5718b5c6-b31e-4990-8a2c-b218d20b59e0)

Under Network settings,select the default VPC you previously created,Under subnet choose the public subnet in the first Availability zone as shown above
<br>
![Setup6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/fa6a8690-ef45-4585-be77-de7379fb225f)

Under Firewall (security groups),choose Select Existing Security Group
Under Common security groups,SSH SG,Webserver SG and Application load balancer SG as shown above

