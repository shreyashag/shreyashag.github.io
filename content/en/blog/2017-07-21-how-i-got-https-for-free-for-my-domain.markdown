---
date: "2017-07-21T00:00:00Z"
time: "2017-07-21 18:51:30"
title: How I got HTTPS for free for my domain
---
Getting https in important in today's world, it conveys authenticity and trust to the user visiting a website. From [what Google has to say about HTTPS](https://developers.google.com/web/fundamentals/security/encrypt-in-transit/why-https)-
* HTTPS protects the integrity of your website
* HTTPS protects the privacy and security of your users
* HTTPS is the future of the web

#### How can you get HTTPS for free? 
1. Go to [Cloudflare.com](https://www.cloudflare.com/a/sign-up) and create a new account.
2. After creating your account, register your domain name with Cloudflare. This can be done with a free plan for personal use.  DNS Records will be imported to Cloudflare when the domain is added. We need to ensure that we have enabled DNS and HTTP proxy for our records.  ![This (the orange cloud) means that we are using the CDN provided by Cloudflare for our domain.](/images/2017-07-21-how-i-got-https-for-free-for-my-domain-cloudflare.png)

In this step, you will also need to update the nameservers of the domain name to the ones provided by cloudflare. To do this, you will need to go to the control panel of your domain name registrar and edit the nameservers. For my domain it looks like this in the Godaddy>Manage Domains>Manage DNS>Nameservers.  
![This is how it looks on my GoDaddy Control panel](/images/2017-07-21-how-i-got-https-for-free-for-my-domain-godaddy-nameservers.png)
 <!-- {% include image name="godaddy-nameservers.png" caption="This is how it looks on my GoDaddy Control panel" %}   -->

This will probably take some time to reflect across the different servers across the world. This is called DNS Propogation. To learn more about DNS Propogation, [click here](). You can check the propogation status using some tool. Here is a website which I used [What's My DNS](https://www.whatsmydns.net/#NS/shreyashagarwal.in).

3. Once that is done, inside the Cloudflare panel, you need to go to the Crypto tab, and set SSL to flexible. I haven't tried setting it to a higher setting as of now, and it works in the setup I am using.  
Also set the  Always Use HTTPS slider to On.

That's it! In some time, the DNS servers will now point to Cloudflare for your domain name and Cloudflare will also have activated HTTPS for the domain name. You can start using https in your domain!

Here are a few other things you can do using Cloudflare-
* Enable DNSSEC - DNSSEC protects against forged DNS answers. DNSSEC protected zones are cryptographically signed to ensure the DNS records received are identical to the DNS records published by the domain owner.
* Enable caching, I've implemented a rule in Cloudflare to do this, 3 rules can be setup in Cloudflare.
* Auto-minify code for HTML, CSS and JS files.

We need to keep in mind that our domain will be served using CDN of Cloudflare. We got HTTPS for free and our now serving our pages using CDN, that can also provide for caching . Hooray!

I mentioned about my setup here, and I am using Jekyll and GitHub Pages which can be read on [my previous blog post.]({{ site.baseurl }}{% post_url 2017-07-19-welcome-to-my-blog %})

