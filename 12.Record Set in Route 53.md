### Create a record Set in Route 53

To create the record set,navigate to your AWS management console,on the search bar type Route 53 and after its displayed,click on hosted zone above
<br>
![Route53_4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/9b06a1fe-6e63-4da3-bea8-cfdcfce05c1b)

Next click the domain name you just created and at the top click create record
<br>

![Route53_5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/3c0750c0-1cff-4a52-b377-90002aa1b780)

Under record name type "www",toggle the "alias" menu to open ,then click on the drop-down and select  "Alias to application and Classic Load Balancer",under "region" select your region
Under "choose load balancer" you will see the Load balancer that we just created and select it,"under routing policy" choose simple routing
<br>

![Screenshot 2024-06-18 at 4 57 10 PM](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/96a62c9c-dfd0-447a-8233-46f9a1280a89)

Now to view with domain name typw www.your domain name 1.e www.loalab.org as shown above
<br>

![Route53_7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/fd908d3d-34aa-4250-b222-ab0ff94deafc)

![Route53_8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/2428becb-e1da-4e3d-a61d-fe74be06426e)

Note that anytime our domain name is changed with need to also go into our settings and change it there,to fix this paste your domain name (www.loalab.org)in the browser 
and type /wp-admin in front of it 1.e www.loalab.org/wp-admin
this will take you to the admin page of your wordpress ,select "Settings" > "General", 
paste the A record name that you created on Route 53 on "WordPress Address (URL)" and "Site Address (URL)" with "http://" in the beginning. Save changes.

<br>

![Route53_9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/69cf9225-83a3-4066-8f94-c042c0f5bcba)

Finally you will be prompted to login,now login in again and your will see the admin page of your website is displayed with your domain name
