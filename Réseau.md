# WRITE_UP_CHALLENGE 
# Write by Harizo
## Network
Learn how to analyze and manipulate the most common protocols and services to turn them to your advantage.

### Prerequisites:
- Master a network analyzer;
- Know the most common application / network / transport protocols.

# FTP - Authentification
## Network capture analysis

#### State:
An authenticated file exchange carried out using the FTP protocol. Find the password used by the user.

open ch1.cpap on Wireshark

###### Tap filter
```sh
ftp
```
###### password is next to pass

# TELNET - authentification
## Network capture analysis
#### State: 
find the user's password in this TELNET session network capture.

open ch2.pcap on Wireshark

###### Tap filter
```sh
telnet
```
###### password is next to password:

# ETHERNET - trame
## Network capture analysis
#### State: 
Find the normally confidential data contained in this frame.
You will get:
```sh
00 05 73 a0 00 00 e0 69 95 d8 5a 13 86 dd 60 00
00 00 00 9b 06 40 26 07 53 00 00 60 2a bc 00 00
00 00 ba de c0 de 20 01 41 d0 00 02 42 33 00 00
00 00 00 00 00 04 96 74 00 50 bc ea 7d b8 00 c1
d7 03 80 18 00 e1 cf a0 00 00 01 01 08 0a 09 3e
69 b9 17 a1 7e d3 47 45 54 20 2f 20 48 54 54 50
2f 31 2e 31 0d 0a 41 75 74 68 6f 72 69 7a 61 74
69 6f 6e 3a 20 42 61 73 69 63 20 59 32 39 75 5a
6d 6b 36 5a 47 56 75 64 47 6c 68 62 41 3d 3d 0d
0a 55 73 65 72 2d 41 67 65 6e 74 3a 20 49 6e 73
61 6e 65 42 72 6f 77 73 65 72 0d 0a 48 6f 73 74
3a 20 77 77 77 2e 6d 79 69 70 76 36 2e 6f 72 67
0d 0a 41 63 63 65 70 74 3a 20 2a 2f 2a 0d 0a 0d
0a
```
You will need to change it to string using {http://www.unit-conversion.info/texttools/hexadecimal/}


```sh   
Authorization: Basic Y29uZmk6ZGVudGlhbA==
User-Agent: InsaneBrowser
Host: www.myipv6.org
Accept: */*

```
You will find that 
``` sh
Y29uZmk6ZGVudGlhbA== is a base64
```
You will have to decode it on {https://www.base64decode.org/}

# Authentification - twitter
#### State: 
A twitter authentication session was captured. Find the user's password in this network capture. You will have to decode it on

open ch3.pcap on wireshark

#### you will get
``` sh 
##...
Authorization: Basic dXNlcnRlc3Q6cGFzc3dvcmQ=
## ...
```
You will find that 
``` sh
dXNlcnRlc3Q6cGFzc3dvcmQ= is a base64
```
You will have to decode it on {https://www.base64decode.org/}


# Bluetooth - Fichier inconnu
### Google is your friend
#### States:
Your friend working at ANSSI has recovered an unreadable file from a hacker's computer. All he knows is that it came from an exchange between a computer and a phone. It's up to you to learn as much as possible about this phone.

The response is the SHA1 hash of the concatenation of the MAC address (in uppercase) and the phone name.
 ``` sh
 AB:CD:EF:12:34:56monTelephone -> 836eca0d42f34291c5fefe91010873008b53c129
 ```
 open ch18.bin on Wireshark
 
 Chek on Wireless then equipment Bluetooth
 The mac address is therefore not C6 4F B9 19 B3 0C
 
# CISCO  - Mot de passe
## Not all hashes are hashes.
#### States:
Find the "Enable" password

```sh
#...
username hub password 7 025017705B3907344E 
username admin privilege 15 password 7 10181A325528130F010D24
username guest password 7 124F163C42340B112F3830
#...
```
You must decode hub, admin, guest passwords with {https://www.ifm.net.nz/cookbooks/passwordcracker.html}

You just put what they have in common with :enable


 
# DNS - Transfert Zone
## Network capture analysis
##### State:
A careless administrator has set up a DNS service for the domain "ch11.challenge01.root-me.org"...
```sh
Hôte	challenge01.root-me.org
```
```sh
Protocole	DNS
```
```sh
Port	54011
```

## Answer:
You have to log in as a super user

```sh
harizo@harizo-TECRA-A50-C:~$ sudo su
[sudo] Mot de passe de harizo : 
root@harizo-TECRA-A50-C:/home/harizo# 
```
Then execute the command to find out the IP address of the DNS server to query.

```sh
root@harizo-TECRA-A50-C:/home/harizo# nslookup challenge01.root-me.org
```
```sh
##...
Non-authoritative answer:
Name:	challenge01.root-me.org
Address: 212.129.38.224          <---- the IP address of the DNS
Name:	challenge01.root-me.org
Address: 2001:bc8:35b0:c166::151
## ..
```

```sh
root@harizo-TECRA-A50-C:/home/harizo# dig @212.129.38.224 -p 54011 ch11.challenge01.root-me.org txt
```



## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
