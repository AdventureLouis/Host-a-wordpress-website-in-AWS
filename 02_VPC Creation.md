### Creating the VPC

![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/665af6d8-77aa-4ef0-ac2e-6d5cefb3273e)

VPC Stands for private virtual cloud,every resources that will be created in this projects will be inside the VPC
<br>
Login to AWS management console,and while in your management console,at the top right corner,select your region,in this case my region is Singapore and this is becauese during  creation of this project 
the HK region is not enabled on my account
<br>
So while you are in aws management console,on the search  bar type VPC and this can be shown in diagram below
![VPC](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/b944b405-59fe-4c23-b8eb-f5d76bda5877)
<br>
Once the VPC page is open on the left corner select My VPCs and click create VPC,Select VPC only,on IPV4 CIDR Block,type 10.0.0.0/16,on tenancy tab,select default and click create VPC
this can be illustrated in two diagrams below
![VPC1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/37297fe5-5c8d-46e0-bdec-61b142217d47)

![VPC2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/84e6634d-a2a1-49df-96eb-cade8c2eb8c7)
<br>
After creating the VPC,another important step is to enable the DNS Hostnames,this will help to ensure that after compoleting all configurations you can access your site with DNS hostnames
To achieve this,check the box next to the VPC and select the drop down on actions menu,the select Edit vpc settings,next check the box next to Enable DNS Hostname

![VPC4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/81adabb1-23b8-4f47-b90e-99432437ebd4)

![VPC5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/1364d718-2617-40a2-b65e-9b0926323347)

### Create internet Gateway
Still on the VPC page,scroll down on the left part and select Internet gateway,select create internet gateway on the top left part,give a name to your internet gateway and select create internet gateway at the bottom
<br>
![igw2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e4406199-7ee4-401a-8a92-a64746286609)

![IGW1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/4627c6c7-bbdb-4194-9b5f-d5f539b728d7)
If we observe below we will notice that the newly created internet gateway is deatched
![IGW3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/9172b8e8-0ef7-42ef-9c71-eca480178c4f)
<BR>
Now to attache the internet gateway,check the box next to internet gateway,click on actions tab at the top and on the drop down select attach to VPC,the next box that appears select the VPC that was created earlier,it is also important to note that only one internet gateway cam be attached to a VPC

![Screenshot 2024-05-29 at 4 00 06 PM](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a9004a55-5cf2-4d95-b26b-42a0f2603cc4)

![IGW5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/1ed250ca-aa38-4cdd-8059-5b5722ecafbc)
As can be seen 👇 we have attached the internet gateway to the VPC,now instances on the VPC will have access to the internet
![IGW6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/cf627904-ebe7-4ae8-bd4d-578e82d3f819)


### Create Public Subnets
Still under VPC service,on the left part select subnets and at the top left select create subnet,on VPC id select your VPC,give the subnet a name,on the availaibility zone select Asia pacific(Singapore)/ap-southeast-1a on IPv4 subnet CIDR block type 10.0.0.0/24 and select create subnet at the bottom righ corner,all this is illustrated in 2 diagrams 👇 

![subnet1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/f5d80519-6628-42f9-8ba2-329151d22ee4)

![subnet2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/796014e1-f1c7-4956-8935-d9d68d0cfe6e)

<br>
I will create a second public subnet in a second availaibility zone,give it a name,now select the second availabilty zone Asia pacific(Singapore)/ap-southeast-1b,on IPv4 subnet CIDR block type 10.0.1.0/24

![subnet3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/9c465b80-ec3f-41dc-b84c-13cac667fc9f)
<br>
Now we can see below the two public subnets and they are in two different availability zones

![subnet4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/1c47c71d-f5dd-4ecb-8cbb-f418ad9d53d5)

![subnet5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/eb706ceb-7e21-4580-b07b-65e8864943e1)
<br>
Now in the next step,I will modify the IP Settings of the public subnets that I just created,to do this check the box of the first public subnet and select Actions menu at the top right corner and on the drop down select Edit subnet settings,under Auto-assign IP settings check the box next to Enable auto-assign public IPv4 address and click save at the bottom right,and this will be done for the two public subnets as shown 👇 

![subnet6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/225e51f0-6300-4c0c-95c8-2497a38647a1)

![subnet7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/7ec9453c-fb07-4bbd-9e54-942f0d9041e1)

![subnet8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/af0d7f22-192c-4f48-9c60-4a3474621715)

![subnet9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/04c1a665-4a74-4f7c-a394-c187ce7da705)

### Route Table creation
In the following steps I will create table,create the public routes and associate the public subnets we previously created to the route tables.
So while still on the VPC service on the left part,select route tables and at the top right corner click create route tables and give the route table a name and at the bottom click create route table
![route1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e8408492-e5d8-4ac4-8792-9567be104c1a)

![route2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/fc788ece-b1fc-4aa5-8372-b838be4ab50a)
Next we will add a route to the public route table,check the box next to the public route we just created,click on route tab at the bottom and click edit routes,
now a new dialog box will appaear,click add route,under destination select  0.0.0.0/0 and this symbol implies route anywhere,under target select internet gateway and select the internet gateway that was previously created.
![route3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/7a4ed108-8256-4d1d-b605-bf94c219c4b2)
Next lets associate the public route table to our two public subnet so that that the public subnet can have access to the internet,so to do this,check the box next to route table and at the bottom click on the subnet Association menu and click edit subnet associations.

![route4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/dea36000-916d-4748-ad63-7c43d6e957c7)

![route5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e656430e-4f1a-4be6-a76d-c819d46aa521)
finally check the box next two the two public subnets and click save,this can be see in above diagram

![route6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/2b113ef5-530e-467c-9eee-359495b5083d)
As seen above the two public subnets have been associated  to the route table

### Creating 4 Private Subnets
In this step we will be creating four private subnets,two in each availabilty zone
Still on the VPC service on the left part select subnets and click create subnets at the top right corner,select your VPC,type the name of the first private subnet,select the first availabily zone and the IPV4 CIDR Block is 10.0.2.0/24
<br>
for the second private subnet type the name of the second private subnet,select the second availabily zone and IPV4 CIDR Block is 10.0.3.0/24
<br>
for the third private subnet type the name of the third private subnet,select the first availabily zone and IPV4 CIDR Block is 10.0.4.0/24
<br>
for the fourth private subnet type the name of the fourth private subnet,select the second availabily zone IPV4 CIDR Block is 10.0.5.0/24
<br>
Below is a diagram on how the 4 private subnets where created
![Private_subnet1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/af49f06d-1750-40ca-9f5f-3d66b71ba428)

![Private_subnet2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/05b7cd69-c7a0-40d0-ae13-46b0d2fd20a1)

![private_subnet3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/26391d58-079a-4da2-a46b-b4dfc6568692)

![Private_subnet4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/66bcd658-bd69-4fe5-8823-bad383705d9c)

![Private_subnet5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/597acf86-b4de-4684-b592-8b23ae18266e)

In the diagram above,we can see the last 4 private subnets that was created and they all have different IPv4 CIDR blocks,this is very important to have

### Route tables for Private subnets
Now we will create two route tables for our private subnets,recall that when we created the VPC it authomatically created a route table for us,so this route table will be used for two private subnets and a new route table will be created to handle the remaining two private subnets

![Private_route_table1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/d7d1a7aa-6fee-445d-9bf6-dd5102f28f3e)
so as seen in above diagram,our VPC has two route tables but we only created  the Public_Route_table1,other one came by default when we created the VPC,
![private_routeTable2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/ec7a09f6-f80e-44d8-a4b5-c1a1cdaa5417)
so we will rename that default route table to a private route table1 as seen above
![Private_routeTable3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/60b7db8c-adc2-4274-839e-d0eb7cc1e355)
Now lets create a second private route table as seen above
![PrivateRouteTable4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a47c841e-2ef3-41e0-90ab-707080c73f13)
Finally as seen above we now have 3 route tables,2private and 1 Public route table
Now the next step is to attach the first private route table that we created to the the private subnet in our first availability zone

![Private_routeTable5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/0e48e46f-71f3-4c4c-badd-07b9cc4ec1fa)

![Private_routeTable6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/4acfac57-4777-4b1f-802f-0b4f679d63c7)
And to do check the box next to the private_route_table2 and below  on subnet associations click edit subnet association 

![PrivateRouteTable7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/1965678f-ea19-427f-a570-ea9c7bde1105)

Next as seen above check the boxes for App Tier and Database Tier in first Availability zones

![PrivateRouteTable8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e02d2afb-ad2e-446b-ae17-d586b2578fe4)
So as seen above,we have successfully attached one route table to 2 private subnets

Now the next step is to repeat same process for the remaining private_route_table1 which is the default route table,and the reason I have decided to use the default route table is because by default it is attached to our main route table

![PrivateRoutetABLE9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/b931a0e5-1bcb-46a8-992b-fffeb687e4b1)
so check the box next to the private route table1,click on Edit subnet associations  as shown above

![PrivateRouteTable10](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/187c6fc7-73cb-4897-a592-d56e880946b8)
and check the boxes App Tier and Database Tier in second Availability zones as shown above




