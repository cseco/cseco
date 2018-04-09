## Setting up a Server

Our chosen VPS host is [upcloud](http://upcloud.com/). And this because they have a free one month trial without any restrictions - a very attractive offer. Log in to you account, go to servers. Then deploy server. Once the server is deployed you will get a password to log in to the server with as root. But you will need to change this to a safer practice - disable root login using password. 

How you log into the server
```sh
	ssh root@ip-address-server
```

Buy a domain from [godaddy](https://www.godaddy.com/) or [sasahost](sasahost.co.ke) (for .ke domains)

Change the nameservers for the domain you bought to [1984](https://www.1984hosting.com/). This will give us a central place to control our domains which be buy from different places, only going back there to renew them. Here are the 1984 nameservers:
- ns0.1984.is
- ns1.1984hosting.com
- ns1.1984.is
- ns2.1984hosting.com
- ns2.1984.is

With the domain in place, you can now go back to upcloud, select you server, then IP, and change the Reverse DNS Name to your domain

You can install dig in linux and test your set up using 
```sh
 dig -x ip-address
```

for reverse DNS, and

```sh
 dig  domain
```