### SSH Into the EC2 Instance
![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/91268826-0f55-4917-8409-700844546f96)
<br>
Now we will SSH into the EC2 Instance in the public subnet
<br>
![SSH_Into1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/dcb925f8-eaf4-497d-8e97-86821fe01b2e)
Navigate to your AWS managemnt console,ensure that you are in the region where you created your VPC,click on services and type EC2,
under resources,click on instances(running) as shown above.
<br>
![SSH_Into2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/8b36842c-e35b-455d-b8d0-7c8bad43c9ce)
Next you will see the setup server we just created,check on the box next to MySetupServer,then under details copy the Public IPv4 address
as shown above
<br>

#### SSH into the EC2 Instance from Terminal
##### For MAC/Linux users
![SSH_Into3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/bf1963b0-8896-45ad-b4a6-f599c27bdd93)

Open your terminal type ssh -i "name_of_the_keypair" ec2user@ec2-your_public_IPv4_address.your_region.compute.amazonaws.com

<br>

### For Windows users
<br>
For windows users ensure to install putty
<br>

![SSH_Into4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/dfa06fe5-21d6-4581-a6a0-06b3a58ace4a)

![SSH_Into5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/cb9fe7ae-1c36-4ad6-b186-12063515102f)




