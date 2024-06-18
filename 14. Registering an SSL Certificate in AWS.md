### Registering an SSL Certificate in AWS Certificate Manager
<br>
An SSL certificate will help to encrpty communication between visitors and websites It ensures that the data transmitted between the user's browser 
and the website's server remains confidential and cannot be intercepted or tampered with by unauthorized parties,this is also known as encryption in transit.
<br>
We will register for free SSL certificate and we will use the SSL certifcate to encrypt communication between web browser and our web severs
<br>

![SSL1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/8878efc3-5eba-4d01-bc5b-75a29d264f70)

To get the free SSL certificate fromm AWS navigate to your AWS management console,on the search bar type "Certificate Manager"  select "Request a certificate" as seen above
<br>
Check the box next to request a public certficate and click next
<br>
![SSL2](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/41441073-67ae-442f-864c-12c27fd158bb)

Under "Fully qualified domain name" and click "Add another sertificate" and this time type "*.your domain name" 1.e *.loalab.org as seen above
<br>
![SSL3](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/e40d2a8f-b6e1-4fd7-b644-d2673f83f77c)

Now the status above is showing issued,so I have been issued
