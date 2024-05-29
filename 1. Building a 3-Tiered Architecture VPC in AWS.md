##  Building a 3-Tiered Architecture VPC in AWS
Below is a bird's eye view of the overall architecture for this project
![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/2ac7a870-bd55-495b-9415-1449b4945b7b)
By using the above architectural diagram, we will build a three-tiered VPC, also note that for this project 2 different availability zones will be used, 👇 I will illustrate the three tiers
<br>
(a)**Tier 1** - 2 public subnets created in separate availability zones, and these subnets will hold resources like NAT gateway and the load balancer
<br>
(b)**Tier 2** - 2 private subnets in separate  availability zones and these subnets will hold resources like webservers and auto-scaling groups
<br>
(c) **Tier 3**- 2 private subnets in separate  availability zones, and these subnets will hold resources like Database
