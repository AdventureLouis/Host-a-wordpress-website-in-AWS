### Elastic File System Creation(EFS)
![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/fd7ea12a-7f50-48da-8ca3-c14ab78da092)
The EFS is a scalable file storage service in AWS,it is designed to create shared file storage for EC2 instances and other AWS services
<br>
Now we will create a file system with mount target in the Datasebase subnet in each availability zone
<br>
After creating the and put our application code into the file system so that the webserver can pull the application code from the same location
<br>
![EFS](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/05789778-01c0-4aab-bb5b-a0daf612232d)

Now lets create the EFS,in the AWS management console click on services and select EFS as shown above
<br>
![EFS2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/8165515e-0760-4f8f-9963-d742ffcb2f9f)

Next click create File system as shown above
<br>
![EFS3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/231e9732-c54a-42bb-9319-4bf48e40292f)
![EFS4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a8dfc4e6-8114-4fcd-90dc-d262d48474da)
![EFS5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/fd0d0159-e42f-419f-a92c-d94fdf24d060)


Next click customize as shown above,next type your file name,next if you you dont want to incure extra cost uncheck the Enable automatic backups box 
<br>

And click Next,Under network,select your default VPC as shown above
<br>
![EFS6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/55d689a2-9883-4682-b419-c40ba95bc263)

Under mount targets,there are two Availability zones,click on the drop down arrow next to Subnet ID and select private subnet3|Database Tier1  and for the second Availability zones,also clcik on the drop down next to Subnet ID and select private subnet4|Database Tier2 as shown above
<br>
![EFS7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e3a70296-7833-42b6-8405-cf803624de12)

Under security group,delete the default security group,for the first Availability zone,select the EFS security group and for the second Availability zone select the EFS security group again as shown above
<br>
![EFS8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a065cf97-d25f-4cb2-ab1e-fa4a235469f3)

![EFS9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/d9b502f9-4fb6-4287-9069-54870715a5af)

![EFS10](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/544b45a3-020a-4f7c-9e64-10179962fc6a)

![EFS11](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/9c51dc49-970a-462b-a032-8e775beb6f85)


Click Next,for the file policy leave it as default and click next,then click create to create the EFS
<br>
![EFS12](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a49dad62-438b-4edb-a92a-8f619be5afa6)

Now wait for a while for EFS state is available as shown above
<br>
![EFS13](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/51cdacd6-cedb-4462-a961-af6a87320162)

click on the file system and at the top right corner click Attach
<br>

![EFS14](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c43e0abd-e3d5-4534-9caa-eafd3eef117b)


After clicking on attach you will see your mount info as shown above,we will need the info later
