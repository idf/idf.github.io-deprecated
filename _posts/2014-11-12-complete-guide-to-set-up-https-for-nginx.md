---
layout: post
title: "Complete Guide to Set Up HTTPS for Nginx"
description: "In 10 Minutes"
category: Computer Science
tags: [HTTPS, Nginx, Server]
---
{% include JB/setup %}

##What is HTTPS?
HTTPS is superman version of HTTP. Okay, actually it's secure version of HTTP with super awesomeness. It's a communications protocol for secure communication, with security features from SSL/TLS with the old dark magic of private/ public key encryption. Everything ranging from the head to toe (i.e. header and loads) in the HTTPS message is encrypted. It's like a naked man (plain text) suddenly going into a dark tunnel and nobody can see him anymore. 

##Nginx
Nginx is a cool server and everyone who uses it never cares about the feather server anymore.  

To get the cool server: 

{% highlight bash %}
$ sudo apt-get update
$ sudo apt-get install nginx
{% endhighlight %}

##Generate private key and certificate
Do the generation: 

{% highlight bash %}
$ sudo mkdir /etc/nginx/ssl
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt
{% endhighlight %}
Enther the information accordingly. Some samples:

{% highlight bash %}
Country Name (2 letter code) [AU]:SG
State or Province Name (full name) [Some-State]:Singapore
Locality Name (eg, city) []:Singapore
Organization Name (eg, company) [Internet Widgits Pty Ltd]: Hack Me If You Can
Organizational Unit Name (eg, section) []:Hack Me If You Can
Common Name (e.g. server FQDN or YOUR name) []:your_domain.com
Email Address []:admin@your_domain.com
{% endhighlight %}
Configure your Nginx:

{% highlight bash %}
$ cd /etc/nginx/sites-available/
$ sudo emacs default
{% endhighlight %}
HTTPS URLs begin with "https://" and use port 443 by default, whereas HTTP URLs begin with "http://" and use port 80 by default.
Add something to the server block to:

{% highlight bash %}
server {
        listen 80 default_server;
        listen [::]:80 default_server ipv6only=on;

        listen 443 ssl;

        root /usr/share/nginx/html;
        index index.html index.htm;

        server_name your_domain.com;
        ssl_certificate /etc/nginx/ssl/nginx.crt;
        ssl_certificate_key /etc/nginx/ssl/nginx.key;

        location / {
                try_files $uri $uri/ =404;
        }
}
{% endhighlight %}

Then restart your server:

{% highlight bash %}
$ sudo service nginx restart
{% endhighlight %}
Bang! It's done. Visiting your site:

{% highlight bash %}
https://your_domain.com
{% endhighlight %}
Now you see me:  
![pic](/assets/img/2014-11/1.png)

BANG! You get your HTTPS is less than 10 minutes!
![pic](/assets/img/2014-11/yeah2.gif)

##Make your HTTPS website trusted 
Do you notice that the `https` is crossed out by a red line? Browser will issue some warnings when clients visit your site with your self-signed certificate SSL. This is expected. It is telling you that the browser cannot verify the identity of the server because your certificate hasn't been signed by a certificate authority that the browser has been configured to trust. 
![pic](/assets/img/2014-11/untrusted.png)
To solve this problem, you need to get your HTTPS certificate signed. (Actually you can stop here if you don't wanna talk to certificate authority and you like the red line).

##Signing the Certificate
Warning - it takes some time and costs you some cash. But if you're rich and awesome, why not keep on going?
In this step, you need to generate a CSR and submit to some authorities to get it signed.

###Generate a CSR (Certificate Signing Request):

{% highlight bash %}
$ openssl x509 -x509toreq -in nginx.crt -out nginx.csr -signkey nginx.key
{% endhighlight %}

###Submit Request
First you need to ensure that you can access `admin@your_domain.com` since the authority will send confirmation information regarding the signing approval to that email and verify that you have the ownership of the domain.  

You can submit your CSR to [geotrust.com](https://www.geotrust.com/) and it costs you some pocket money. Or if you have a domain name bought in [gandi.net](https://www.gandi.net/), then you can get a free SSL certificate from [here](http://wiki.gandi.net/en/ssl/standard/free).

After submission, verification of email account, BANG! You get your signed certificate: 
![pic](/assets/img/2014-11/cert.png)

###Update Your Cert and Let the Show Begin
Replace the original `nginx.crt` with your new `nginx.crt` signed and then restart your server and see all the amazingness happens:
![pic](/assets/img/2014-11/perfect.png)


##Force HTTPS
So far, the HTTPS is successfully set up, and you can access your website by both `http://your_domain.com` and `https://your_domain.com`.  
If you don't like HTTP or you wanna be cool, you can force all the connections to HTTPS rather than HTTP/HTTPS hybrid. Fire up your editor can do some hacks in Nginx:

{% highlight bash %}
$ cd /etc/nginx/sites-available/
$ sudo emacs default
{% endhighlight %}
Update the site config file and separate original 1 server into to 2 server blocks:

{% highlight bash %}
server {
        listen 80 default_server;
        listen [::]:80 default_server ipv6only=on;

        server_name your_domain.com;
        return 301 https://$server_name$request_uri;
}

server {
        listen 443;
        ssl on;
        root /usr/share/nginx/html;
        index index.html index.htm;

        server_name your_domain.com;
        ssl_certificate /etc/nginx/ssl/nginx.crt;
        ssl_certificate_key /etc/nginx/ssl/nginx.key;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
                proxy_set_header X-Forwarded-Proto https;
                # Uncomment to enable naxsi on this location
                # include /etc/nginx/naxsi.rules
        }
{% endhighlight %}
Some explanations: the first virtual server listening to port 80 (i.e. HTTP) will return HTTP status code 301 (i.e. moved) and redirect to another virtual server listening to port 443 (i.e. HTTPS), redirecting the client to `https://` version of your site. 

Now the server only serve on https, no more http. 

Have fun and enjoy the awesomeness.
![pic](/assets/img/2014-11/yeah.gif)