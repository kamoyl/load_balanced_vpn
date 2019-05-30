# load balanced multi country nordvpn/openvpn
## purpose

This repo has been created for something which started to be small and easy solution for NordVPN, but 
finally become quite sophisticated and useful (for me of course :)) solution for manage high available,
obfuscated, load balanced solution for my home Internel access...

I'm using NordVPN solution, and I'm quite happy of it, but it is easy to change it to use other VPN-s, 
ppp or/and pppoe... The only real different thing is that I'm using NordVPN API for finding the least
loaded servers, the closesed, obfuscated etc... 

It might be either use in any kind of load balancing connections, but then routing, and/or iptables
suppose to be corrected/changed

## Important links and prerequisites:

I used some sites for making it work, and for understand what is and why it suppose to be that very way :)
But any suggestion/encourage for correction/optimization/adding features is welcomed...
Becasue I'm system engineer, and not network one, and despite I understand form this topic quite much, I had
to make myself understand why ths way, and what is the difference between "normal" TCP/UDP eth connections, and
what are very important difference when VPN/ppp is used (for example in routing)...

All of it works as butter on... yes, yes, really: rasbpian on Raspberry Pi 3 B+:

[Detailed and good description, but... not for ppp kind](http://www.system-rescue-cd.org/networking/Load-balancing-using-iptables-with-connmark/)\
[Not as detailed as previous one, and without routing configuration](https://blog.khax.net/2009/12/01/multi-gateway-balancing-with-iptables/)\
[Many useful details of how to configure openvpn to use more then one connection](https://serverfault.com/questions/821583/routes-for-two-openvpn-connections-different-hosts-in-the-same-client)\
[Some of examples of public NordVPN API](https://blog.sleeplessbeastie.eu/2019/02/18/how-to-use-public-nordvpn-api/)

There were many ideas of what to use to make it works: iptables with CONNMARK, routing with nexthoop, routing rules etc.
I tried to use some of them, and during it have tested most of them and it looks like it finally works, and works 
appropriately - so there is HA (doesn't matter if one will fail, it will still work), and combined performance with load
balancing using statistically spreaded packet sending ...

I know - that it might be better scripted (for example to use list of lists to manage easily amount of connections), 
but slowly I will try to add some more features and also optimize code little bit.

I also used NordVPN API to get some extra information on the fly, so NORMAL internet connection suppose to work
before start 'em, but... there is easy workaround: download first this file [zipped all config files for openvpn](https://nordvpn.com/api/files/zip),
and then use those files as connection parameters data...

## HowTo

just run: openvpn_automatic_HP - the rest will be done automatically; by default - the best (least load), not
obfuscated, Netherlands servers are used, but, when use:
* -m - it will try to use NordVPN servers located in nearest countries (also with the least load)
* -h - obfuscated servers will be used (-m and -h might be used both)
* -v - for verbose use
* -o directory - is for storing all temporary files, and logs in mentioned directory 

## ToDo

- [ ] - Checking if appropriate route tables exists in iproute2/rt_tables - and manage them automatically
- [X] - checking how many vpn connections is open to close also this one which will not be started (if there were 4 previously, and now there are three, fourth one won't be stopped
- [X] - finished nearest country servers collecting and using (checking and calculating ping statistics + load)
- [X] - add full automation to find best servers from the closesed locations around country script is run from (calculates ping statistics)

## Changelog (I'm using [git-release-notes](https://www.npmjs.com/package/git-release-notes))


* __Added options to connect to different countries at once - funny results form IP localization services :)__

    [Kamoyl](mailto:kamoyl@outlook.com) - Tue, 28 May 2019 09:42:34 +0200
    
    efs/remotes/origin/master, refs/remotes/origin/HEAD, refs/heads/master
    few more issues corrected
    
    some cleaning
    

* __small correction to README__

    [Kamoyl](mailto:kamoyl@outlook.com) - Mon, 27 May 2019 11:58:27 +0200
    
    
    

* __Added zipped nordvpn/openvpn config files link__

    [Kamoyl](mailto:kamoyl@outlook.com) - Mon, 27 May 2019 11:56:07 +0200
    
    
    

* __Corrected one weird sentence in README__

    [Kamoyl](mailto:kamoyl@outlook.com) - Mon, 27 May 2019 11:52:36 +0200
    
    
    

* __Corrected break lines in README__

    [Kamoyl](mailto:kamoyl@outlook.com) - Mon, 27 May 2019 11:50:57 +0200
    
    
    

* __Added a bit of description and help in slightly polished README__

    [Kamoyl](mailto:kamoyl@outlook.com) - Mon, 27 May 2019 11:45:21 +0200
    
    
    

* __First commit, after move from code repo__

    [root](mailto:root@pi.dom.local) - Mon, 27 May 2019 10:22:36 +0200
    
    
    

* __Initial commit__

    [Kamil Czarnecki](mailto:kamoyl@outlook.com) - Mon, 27 May 2019 10:15:37 +0200
    
    


