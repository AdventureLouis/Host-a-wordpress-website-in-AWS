### Creating Key Pair
![Projects_Achitecture](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/18ee33b9-6e66-4c91-a639-e0c97b4aa1ff)
There are several ways you can access or create your EC2 instance in AWS.Today we will be discussing  one of the ways which is through ssh.
<br>
before you can ssh into your EC2 instance you need key pairs and the these key pairs comprises of primary key and foreign key,in this lesson I will give more details
<br>
![key1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/4d274f5e-f93b-4659-99d0-50803d58166c)

![key2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/28339997-22af-4df4-8ee5-b330d9c42365)

To begin,in AWS management console,click on services and type key pair,at the top right corner click key pairs as shwon above
<br>

give a name to your key.Its important to note that MAC and Windows users have different specifications during creation
<br>
For MAC users or Windows users under  key pair type,you can either choose RSA or ED25519
<BR>

![Key3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c743c7ef-a187-4c49-b7a4-6fdd9105c387)


For MAC users under private key file format choose .pem,for Windows users choose .ppk as shown above,then click create.
After you click create two keys will be generated private and public key,when you click create you will be prompted to download the private key in your local machine
<br>
And the public key will be in AWS management console.So Whenever you need to ssh into your ec2 instanc,you will put the public key on the ec2 instance and you will use the private key 
that you previously downloaded to ssh into that instance

### For MAC/Linux Users
Navigate to wherever you have saved your primary key, in my case I saved it in my home directory 
<br>
![Key4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/f7b8c2eb-8bd0-404a-b9e0-5a5126f54f0a)

In order to enable permissions  for the key I will use command "chmod 400 mineEC2key.pem" as shown above

### For Windows Users
we will need to download PuTTY so as to able to make connections into EC2 instance.


