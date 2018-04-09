## Setting up a Mail Server

## Home

Setting up and maitaining a mail server is not work for the faint hearted. But we will show you a tool that will automate almost all the tasks for you. [mail-in-a-box](https://mailinabox.email/)

But mail in a box will not set itself up in Ubuntu 16.04 (our preferred OS for now). An easy solution is provided by [jirislav](https://github.com/mail-in-a-box/mailinabox/issues/758) [here](https://github.com/jirislav/mailinabox). Check on either of those locations how to set up mail-in-a-box in ubuntu 16.04 LTS.

That is easy, but it is far from the end.

**[⬅ cseco](http://github.com/cseco/cseco/tree/dev)** | **[⬅ resources](http://github.com/cseco/cseco/tree/dev/resources)** | **[⬆ back home](#home)** |

## SSL certificates
(They got a new name)
mail-in-a-box will give you self-signed certificates which will give you a problem with the browser.

You need to use [certbot](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx) to get other certificates. Install certbot and use it as shown in their page. You may have to also set the domain of this server in the certbot command if it does not give you that domain in the options

```sh
sudo certbot --nginx -d domain
```

Once that is done, remove the self-signed certificate and create links there that point to the new certificates. (Remember to change mail.cseco.co.ke to the domain for which the certificate was created. Or whichever place the certificate was saved)

```sh
rm /home/user-data/ssl/ssl_certificate.pem
rm /home/user-data/ssl/ssl_private_key.pem

ln -s /etc/letsencrypt/live/mail.cseco.co.ke/fullchain.pem  /home/user-data/ssl/ssl_certificate.pem
ln -s /etc/letsencrypt/live/mail.cseco.co.ke/privkey.pem /home/user-data/ssl/ssl_private_key.pem
```

How you log into the server
```sh
	ssh root@ip-address-server
```

**[⬅ cseco](http://github.com/cseco/cseco/tree/dev)** | **[⬅ resources](http://github.com/cseco/cseco/tree/dev/resources)** | **[⬆ back home](#home)** |

# DKIM
Now you are almost done, but you may still have a problem with the DKIM records that are created by mail-in-a-box. You may get an error like `DKIM record exists but its encording is no supported`. That means that you need to use a 1024 bits encoding rather than the 2048 bits encoding.

Run these commands (Remember to change cseco.co.ke to your own domain and mail to your sub-domain if you are setting it up for a sub-domain).

```sh
cd /etc/opendkim
sudo mkdir keys && cd keys
sudo mkdir cseco.co.ke && cd cseco.co.ke
sudo opendkim-genkey --bits=1024 -s mail -d cseco.co.ke
```

Again you have to replace the old key (Always remember to change cseco.co.ke). The key you are replacing may also not be `/home/user-data/mail/dkim/mail.private`. You can check for solutions to any problems [here](https://discourse.mailinabox.email/t/dkim-signature-header-exists-but-is-not-valid/1968/5)

```sh
cp /home/user-data/mail/dkim/mail.private /home/user-data/mail/dkim/mail.private.bac
rm /home/user-data/mail/dkim/mail.private
ln -s /etc/opendkim/keys/cseco.co.ke/mail.private /home/user-data/mail/dkim/mail.private

systemctl restart opendkim
```


`cat /etc/opendkim/keys/example.com/mail.txt` to get the DKIM key. You will not need everything in the file. See what part of it you need [here](https://discourse.mailinabox.email/t/dkim-signature-header-exists-but-is-not-valid/1968/5)

**[⬅ cseco](http://github.com/cseco/cseco/tree/dev)** | **[⬅ resources](http://github.com/cseco/cseco/tree/dev/resources)** | **[⬆ back home](#home)** |

## DNS
You will need to set up these records in the dns. See how to do that in [setting up server](See how to get DKIM from [Setting up Mail Server](https://github.com/cseco/cseco/blob/dev/resources/SERVER.md#dns)

**[⬅ cseco](http://github.com/cseco/cseco/tree/dev)** | **[⬅ resources](http://github.com/cseco/cseco/tree/dev/resources)** | **[⬆ back home](#home)** |