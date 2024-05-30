### Creation of NAT Gateways
![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/91243397-a367-4ae8-accd-7df696ba4e4a)

The NAT Gateway is a service in AWS which  enables instances within the private subnet in the VPC to get access to the internet
Any instance in the public subnet with a public IP address will be able to access the internet and users from the internet will also be able to access that instance.
However,for private subnet any instance in it will not be able to access the internet and users from the internet will not be able to access the instance in the private subnet and as a result we want our applications to reside in the private subnet,this is good for best security practice.
subsequently are EC2 instance which will be residing in the private subnet through the help of a NAT Gateway will be able to access the internet to download security patches and upgrades and users from the internet will not be able to access your EC2 instance.
Now we will lunch the 
NAT Gateway to our public Subnets 1 and 2

### Create NAT Gateway
![NGW1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/cd4fb66c-e412-40f1-8cd7-d01bb0733303)
![NGW2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/f1c244e0-5133-4b7f-8e24-00b1d209a606)
![NGW3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/5902d75d-d577-4d2c-b01d-628dcddf36fb)

Before creating NAT Gateway,we will first allocate two IP Addresses for the NAT Gateways that will be lunched in public subnet1 and public subnet2
One of the purposes for creating elastic IP addresses is due to consistency as this will help to ensure that all outbound traffic from our instances have consistent IP.
In order to create the elastip IP's on the left part of the VPC service,scroll that and click Elastic IPs and at the top left corner,select Allocate Elastic IP address and repeat it twice so we can have two elastic ips for the public subnet
![NGW4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/2186e845-3e0b-4ec8-b019-9c82758dec52)

Now to create NAT Gateway,still on the VPC service,scroll down and click NAT gateways and the top left right corner click create NAT gateway
as shown above
![NGW5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/24ff6688-5f83-4862-8f98-a214fbc717cb)

![NGW6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/7610101d-d604-4e92-8c6e-ea9f7ee068b2)

Now while the Create NAT Gateway page is open,under NAT gateway settings,give a name to your NAT gateway,under subnet,select public subnet1 we priviously created,under connectivity type,leave it at public,under Elastic IP allocation ID,click on the drop down on select one of elastic IP's we previously created and click Create NAT gateway at the buttom right and the steps is shown above
Now that we have created the NAT Gateway,another important step is to update the route table associated to the private subnets so that internet bound traffic will be pointed to the NAT gateway
![NGW7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/b0f147ed-b179-4c8e-b04f-d331bd029d10)
![ngw8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/18976ed9-d665-4401-82fe-2b7b8b56e119)

so to do that,we navigate back to our route tablea by clicking on route tables on the left part,now select the first private route table and at the bottom click on routes tab,next click edit routes and click add routes,under destination select 0.0.0.0/0,under target select NAT Gateway ,then select the Nat Gateway we previously created and click save changes,as shown in above diagrams

![NGW10](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/d8fd8ece-a9ef-4dea-92f5-fd6f2c8f7b58)
![NGW9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/630d7840-17e4-4d17-a7ec-89db1f5bb49a)
![NGW11](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/5907beff-9418-40f4-a186-7ec2e4cb2e26)

Next we will create a second NAT Gateway and repeat as shown above,and this time we will implemnent on second public subnet and update the route on the private_route_table2.
so now that we have successfully created a NAT Gateway,instances in our peivate subnet will be able to download security patches
