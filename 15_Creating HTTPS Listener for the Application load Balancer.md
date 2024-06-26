### Create an HTTPS listener
<br>

![Listener1](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/14d6e398-1758-441d-9e17-2047d13fe8d2)

In your AWS management console,on the search bar type EC2,under EC2 page on the left pane under Load balancing,
click load balancer and you will see the load balancer we prevously created Now check the box next to the Load balancer you previously created and click the "Listeners and rules" tab and click as seen above
<br>

![Listener4](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/a087f48a-11b8-4c88-828f-1e34053eeb0c)

<br>
Now we will change the "Protocol" to "HTTPS" (443), on "Default actions", select "Forward" (determines how incoming requests are processed and forwarded to the target group).

<br>

![Listener5](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/8739ac18-9d53-4358-a00e-f1e66b2e5dc8)

Under security policy,select the default recommended policy,under "Default SSL/TLS server certificate" select ACM(AWS Certificate manager) and click add shown above
<br>

![Listener6](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/ccd9cec7-23d9-43b3-b490-b9310fdb0fbd)

![Listener7](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/48cb7702-0673-4ecb-960d-1c1212af7a88)

Now we have to edit our HTTP listener to redirect HTTP traffic to HTTPS. To do that, select the "HTTP: 80" on "Listener ID" and click "Actions" > "Edit listener". On the edit page, 
click "Remove" on the "Default actions" and then select "Redirect", type 443 in front of the HTTPS protocol. Save changes.
<br>

![Listener8](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/c97909e5-f545-4185-b758-82f3d80a91b1)
As seen above our domain name now has https in front of it
<br>
![Listener9](https://github.com/AdventureLouis/Host-a-wordpress-website-in-AWS/assets/161846069/4865e5ea-30f1-473c-99c4-d73721b1155d)

The final step is to edit our website to also have https,so to do this in front of the domain name add /wp-admin

