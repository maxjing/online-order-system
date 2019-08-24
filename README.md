# online-order-system with wechat
sell - Spring boot based 

Here we use the account of WeChat public platform and the account of WeChat open platform.
You need to apply for some permissions yourself.
The permissions currently used are:
WeChat public account login payment authority, message push permission. Login and message push can use test accounts in development documents.
As for the payment authority, you need to find a friend to borrow an account.
I am developing the video of Liao’s brother, and I need to have a payment permission test. You can read this document:
https://github.com/Pay-Group/best-pay-sdk/blob/master/doc/borrowAccount.md  
There is also the login permission of the WeChat open platform, which also needs to be authenticated by itself. 

  
Two open source SDKs were used
Links:  
https://github.com/Wechat-Group/weixin-java-tools  
https://github.com/Pay-Group/best-pay-sdk 


# linux service set up

centos7 set up

cd /ets/systemd/system  
touch AAA.service

vim AAA.service  
```
[Unit]  
Description=AAA #Description  
After=syslog.target network.target  #dependency  

[Service]  
Type=simple  

ExecStart=/usr/bin/java -jar /opt/javaapps/AAA.jar  
ExecStop=/bin/kill -15 $MAINPID   

User=root  
Group=root   

[Install]  
WantedBy=multi-user.target  
```

How to use?  
systemctl start AAA or  
systemctl start AAA.service  
if changed:  
run systemctl daemon-reload, then systemctl start sell.service  

stop service:  
systemctl stop AAA or 
systemctl stop AAA.service  

star when boot:   
systemctl enable AAA or  
systemctl enable AAA.service   

disable start when boot:  
systemctl disable AAA or  
systemctl  disable AAA.service  


# Summary  
 
## Wechat 
Template message, authorization, payment and refund   

## Token Authentication   
Used in the seller's login management system
I have blocked it in aop because I don't have an authentication account on WeChat open platform and can't log in.
You can go to cn.chenhaoxiang.aspect.SellerAuthorizeAspect to liberate the note on the class. 

## WebSocket Message
After the buyer places an order, there is a message to the buyer and play music.   

## Redis Seession adn distributed lock  
Redis cache, pay attention to add, delete, change the update cache, otherwise there will be unpredictable consequences
Here, if there is a purchase of goods, you can use Redis' distributed locks.

