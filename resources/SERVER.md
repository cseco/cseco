## Setting up a Server

Our chosen VPS host is [upcloud](http://upcloud.com/). And this because they have a free one month trial without any restrictions - a very attractive offer. Log in to you account, go to servers. Then deploy server. Once the server is deployed you will get a password to log in to the server with as root. But you will need to change this to a safer practice - disable root login using password. 

How you log into the server
```sh
	ssh root@ip-address-server
```

Buy a domain from [godaddy](https://www.godaddy.com/) or [sasahost](sasahost.co.ke) (for .ke domains)

Change the nameservers for the domain you bought to [1984](https://www.1984hosting.com/). This will give us a central place to control our domains which be buy from different places, only going back there to renew them. Here are the [1984](https://www.1984hosting.com/) nameservers:
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

## DNS
You will need to set up these records in the dns

### A
Host | ttl    | points to                                                                                  
-- | ---------- | ------ 
@  | 3600    | your ip
mail  | 3600    | where you'll set up your mail server 

### CNAME
Host | ttl    | points to                                                                                  
-- | ---------- | ------ 
ftp  | 3600    |@
www  | 3600    | @ 

### MX
Host | ttl    | points to                                                                                  
-- | ---------- | ------  
@  | 3600    |server sending mail on your behalf
mail  | 3600    | server sending mail on your behalf

### TXT 
(example from gospelsounders.org - mails are sent from mail server at mail.cseco.co.ke) Change accordingly
See how to get DKIM from [Setting up Mail Server](https://github.com/cseco/cseco/blob/dev/resources/MAILSERVER.md#dkim) 
Host | ttl    | points to                                                                                  
-- | ---------- | ------  
gospelsounders.org.  | v=spf1 a mx include:mail.cseco.co.ke ~all  
mail._domainkey.gospelsounders.org.  | DKIM 

**[⬅ cseco](#https://github.com/cseco/cseco/tree/dev)** | **[⬅ resources](#https://github.com/cseco/cseco/tree/dev/resources)** | **[⬆ back home](#home)** |
