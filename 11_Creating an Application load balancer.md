### Create Application load balancer and private instances

![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/d563dcd9-9a26-48ec-9e2c-47ebd36f4a24)
<br>
Before I explain the importance and use of Application balancer first I will like to refresh your mind on how our architecture is designed as seen in above diagram. 

Our architecture is designed in such a way that a user from outside or a user from the internet cannot directly access or interact with instances in our private subnet such ec2 and RDS 
and this is security best practice.Now in order to achieve this goal we will utilize an Application load balancer in AWS.
<br>
An Application balancer(ALB) is a load balancing service that is managed by AWS,It is designed to distribute traffic  accross multiple targets such as Amazon ec2 instances,containers,IP addresses,
or lambda functions
<br>
Before creating an Application load balancer,we first need to create two ec2 instances in the private app subnets that we earliear created.Recall that previously,we created the setup server instance and had the wordpress
files saved in EFS,now we create instances in the private subnet,attach them to EFS and delete the setup instance in the public subnet.
<br>

### Creating Private Instances

![Private_instance1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/7349c32b-a869-4962-ac2f-62f36093ed9a)

![private_instance2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/509c40c0-aaf3-482a-823f-fc7619420a33)


While in AWS management console,on the search bar type ec2 and start creating your new instance  Give it a name and choose the "Amazon Linux 2 AMI (HVM)" instance, this is important for compatibility with WordPress. as seen above
<br>
![Private_instance3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/d3117345-f709-4400-8e04-f472ab47b1c2)

Make sure that your "Instance type" is in the free tier mode, like the "t2.micro" that is chosen by default. Then, select the "newEC2key" key pair that we created.
<br>

![Private_instance4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/628d824b-2148-4e2b-b329-119397080413)

<br>

For the "Network settings",choose the custom VPC that we created,for subnet choose My subnet1|App Tier1(an app private subnet in AZ1),for "Firewall (security groups)",select existing security group
and choose webserver security group.
<br>
![private_instance5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/55bb1d9d-a880-42f4-91ac-08fe1e19d125)

![Private_instance6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/886f2901-f68b-4f97-b4f5-04c671a7e7e5)


 Now the last step which involves attaching the EFS to the private instance,so all you will do is click on "Advance Details" above and scroll all the way down to an empty box called user data as seen above

 ```bash
#!/bin/bash
yum update -y
sudo yum install -y httpd httpd-tools mod_ssl
sudo systemctl enable httpd 
sudo systemctl start httpd
sudo amazon-linux-extras enable php7.4
sudo yum clean metadata
sudo yum install php php-common php-pear -y
sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y
sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
sudo yum install mysql-community-server -y
sudo systemctl enable mysqld
sudo systemctl start mysqld
echo "<yourEfsMountHere>:/ /var/www/html nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 0 0" >> /etc/fstab
mount -a
chown apache:apache -R /var/www/html
sudo service httpd restart
```
Note that in above script,the command  #!/bin/bash comprises of shebang(#!) and bin bash command(/bin/bash).The shebang command(#!) lets the terminal know that the programme is exscuting a script and (/bin/bash)the  lets the linux os recognize that we are trying to run a bash script
<br>

And before pasting above code into the user detail empty box,first edit the part "yourEfsMountHere>",to get this part navigate to your management console,on the search bar,type EFS and click your EFS to open it,once it opens click on attach to display your NFS client,copy the part that begins with fs and ends with .com,so the new script will look like 👇 
<br>

```bash
#!/bin/bash
yum update -y
sudo yum install -y httpd httpd-tools mod_ssl
sudo systemctl enable httpd 
sudo systemctl start httpd
sudo amazon-linux-extras enable php7.4
sudo yum clean metadata
sudo yum install php php-common php-pear -y
sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y
sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
sudo yum install mysql-community-server -y
sudo systemctl enable mysqld
sudo systemctl start mysqld
echo "fs-096a3d3f272ac3543.efs.ap-southeast-1.amazonaws.com:/ /var/www/html nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 0 0" >> /etc/fstab
mount -a
chown apache:apache -R /var/www/html
sudo service httpd restart
```
<br>

![Private_Instance7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/9e0d3893-bd0a-4d6f-ba96-0bdd8bb1c6d1)
And the user detail box will look like above
<br>

![Private_instance8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/36973f99-1f7b-418b-a6f7-6af3100c516a)

After successfully launching your instance you should see a display as shown 👆 

<br>

![Private_instance9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a47676e4-e911-4c0a-96e3-f1c6f023ae4a)
![Private_instance10](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/6d8e236c-8c86-424f-a034-380df92154e4)

![Private_instance11](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c50a20d0-0463-4e11-b3c0-42d113844eba)
![Private_instance12](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/2e985911-2f98-4884-810f-24add27a8223)

Now its time to create the second instance,follow similar step used in creating the first private instance above,the only difference is that under subnet,select the second private app tier subnet created in availabilty zone2 as seen in above 4 images.
<br>

![Private _instance13](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e84fea5e-1d50-434f-a41b-7131ab9e5d10)

Above is a display of all 3 instances including the two private instances that we just created

### Create a taget group
<br>

![Target_GP1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/469fa784-af5b-4725-b8d6-9d13b21cc4b5)

Next is to create a target group and put the two instances into the target group so that the application load balancer can route traffic to the target group 
On your aws management console,on the search bar type target group then click create target group at the bottom as shown above
<br>

![tg_gp3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/b5856c9d-8094-4f03-96f4-cbd4e4dbca32)
Choose your taget name as shown above
<br>

![tg_gp4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/3dd96f38-b651-4d91-adc1-99e00ed38035)

Choose the VPC that we previously created and also choose HTTP1 as shown above
<br>
![TG_GP2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/409ba9f2-1c35-4a77-8d75-7d0ae3b44bfb)

 Under choose a target group,select instances as shown above
<br>
![TG_GP5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/9b3b09b6-63a6-4cf8-b313-cc3dfbcd9fb1)
Under success codes add 301 and 302 as shwon above
<br>
![TG_GP6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/010d669e-4188-4979-b4e2-0adda7e38a3a)
Next check the boxe next to the two private instances that we created and click include as pending as shown above
<br>
![TG_GP7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/9ee4b755-4698-46cb-90d7-fe2919301a87)
Above are the target instances

### Creating Application load balancer
<br>

#### How Load balancers work
The way an Application load balancer works is such that when  a client makes a request to your application,the listeners that you configure your load balancer will receive requests that match the protocol that you configure when your created the load balancer,now the receiving listener listens to the request to see if it matches the rule that you specified,if yes it will route the traffic to the specific target group
<br>
#### How to create load balancers
<br>

![ALB1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a5ec5677-7d66-4782-8501-ac813b614cd5)

Now that we have been able to create two instances in private subnet and a target group that contains the two instances,its now time to create an Application load balancer
In your AWS managemnent console,on the search bar type EC2,when the EC2 page opens on the left tab scroll down untill you see "load balancing",click on "load balancers" and click create Application load balancer as seen above
<br>

![ALB_2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e2274210-36f5-47bc-9013-50fe57a68537)

Under Load balancer types,choose Application load balancers as seen above
<br>
![ALB_3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/84a6f95e-2c3f-411e-af51-f8d2eb2da707)

Next give a name to your Application load balancer,under "scheme" choose internet-facing(we choose this because user will be interacting with ALB from the internet) as shown above
<br>

![ALB_4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/4ed74bc5-afda-440f-b33a-5586bc7b0bf3)

Under "Network mapping" choose your vpc that your earlier created,under "mappings" check the boxes next to the two avalaibility zones and for each availability zone,choose public subnet 1 and public subnet 2 respectively as shown above
<br>

![ALB_5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/3f47a1be-15a7-4987-87be-589f9a0b2f14)


Under security groups,remove the default security group  and select the Application load balancer "security group" and under "Listeners and routing" leave the http:80 as default and click on drop-down arrow next to target group and select the target group we previously created as seen above
<br>
Next leave every other options as default and click create Application load balancer
<br>

![ALB_6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/5177b624-6a0f-47ff-8740-24b12d6bed3a)

![ALB_7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/ae0e0d89-7777-463f-8b2f-7fbae60c01ec)

Now wait for few seconds for the Application load to provision,and under "state" check to see when its reads "Active"  as seen above
<br>

![ALB_8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/0908a261-24b4-4c73-8b85-6c823c61fa55)

The final step to copy the "DNS Name" copy the link and paste it on a new tab and you will see your site is displayed and this time it is dispalyed with the DNS name as seen above




