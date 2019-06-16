# load balanced multi country nordvpn/openvpn
## purpose of this repo

This repo has been created for something which started to be small and easy solution for NordVPN, but 
finally become quite sophisticated and useful (for me of course :)) solution for manage high available,
obfuscated, load balanced solution for my home Internel access...

I\'m using NordVPN solution, and I\'m quite happy of it, but it is easy to change it to use other VPN-s, 
ppp or/and pppoe... The only real different thing is that I'm using NordVPN API for finding the least
loaded servers, the closesed, obfuscated etc... 

It might be either use in any kind of load balancing connections, but then routing, and/or iptables
suppose to be corrected/changed

PS. During my lond time tests it looks like that simultaneus connections offers about 20% more in 
download capacity then during use of \"normal\" ISP connection

## Important links and prerequisites:

I used some sites for making it work, and for understand what is and why it suppose to be that very way :)
But any suggestion/encourage for correction/optimization/adding features is welcomed...
Becasue I'm system engineer, and not network one, and despite I understand this topic quite much, I had
to make myself understand why this way, and what is the difference between \"normal\" TCP/UDP eth connections, and
what are very important difference when VPN/ppp is used (for example in routing process)...

All of it works as butter on... yes, yes, really: rasbpian on Raspberry Pi 3 B+;

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
* -m - it will try to use NordVPN servers located in the nearest (from ping time perspective) countries (also with the least load)
* -H - obfuscated servers will be used (-M, -m and -H might be used together)
* -M - number of simultaneus connections (from 1 to 6 - restricted only becasue NordVPN restriction)
* -c - country in which NordVPN enpoint will be (other options are still possible: -M, -H)
* -v - for verbose use
* -h - short help of parameters and usage
* -o directory - is for storing all temporary files, and logs in mentioned directory 

## ToDo

- [ ] - checking if appropriate routing tables exists in iproute2/rt_tables - and manage them automatically
- [ ] - add option to connect to choosen country
- [ ] - implement cleaning from openvpn_cleaning into main script instead of current cleaning (which might not always be appropriate)
- [X] - cleaning of connections, ip rules and tables works inapropriately, needs to be corrected
- [X] - added help (-h), so then changed obsucation (hidening to capital H)
- [X] - automatically checking name for VPN connections (default is tun, but... who knows somebodys idea :))
- [X] - extra parameter for amount of simultaneus connections, default is 4
- [X] - checking how many vpn connections is open and stopping all of them, flushing related routing tables and removing related routing rules
- [X] - automatic nearest country servers collecting and using (checking and calculating ping statistics + load)
- [X] - add full automation to find best servers from the closesd locations around country script is run from (calculates ping statistics)

## Changelog (I'm using [git-release-notes](https://www.npmjs.com/package/git-release-notes))


* __Updated Changelog__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 14 Jun 2019 13:00:00 +0200
    
    EAD -&gt; refs/heads/1.0.0, refs/remotes/origin/1.0.0
    

* __Rewritten cleaning of all vpn connections, rules and routing tables__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 14 Jun 2019 12:59:34 +0200
    
    
    

* __Small update__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 14 Jun 2019 11:04:35 +0200
    
    
    Changelog
    

* __Updated parameters information in README__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 14 Jun 2019 11:04:01 +0200
    
    
    

* __Updated readme__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 14 Jun 2019 11:02:49 +0200
    
    
    Changelog
    

* __Added help (-h)__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 14 Jun 2019 11:01:44 +0200
    
    
    Changed obfuscation (-h) parameter to capital H (-H)
    
    Preparation for cleaning connections, ip rules and routes properly
    

* __Readme/Changelog update__

    [Kamoyl](mailto:kamoyl@outlook.com) - Sun, 2 Jun 2019 08:23:19 +0200
    
    
    

* __Small issues corrected - related to extra parameter: M, and with closed quotation__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 31 May 2019 12:33:00 +0200
    
    
    

* __Updated changelog__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 31 May 2019 09:52:29 +0200
    
    
    

* __Added autoamtically discovered path of scripts and template__

    [Kamoyl](mailto:kamoyl@outlook.com) - Fri, 31 May 2019 09:51:41 +0200
    
    
    Added automatically recognized tun device
    

* __Changelog__

    [Kamoyl](mailto:kamoyl@outlook.com) - Thu, 30 May 2019 11:50:10 +0200
    
    
    

* __README corrections__

    [Kamoyl](mailto:kamoyl@outlook.com) - Thu, 30 May 2019 11:48:15 +0200
    
    
    

* __Changelog__

    [Kamoyl](mailto:kamoyl@outlook.com) - Thu, 30 May 2019 11:44:11 +0200
    
    
    

* __Added extra script for looking into servers statistics__

    [Kamoyl](mailto:kamoyl@outlook.com) - Thu, 30 May 2019 11:42:12 +0200
    
    
    Added script for cleaning all openvpn connection, routing tables and rules - it
    is important for automatically find recommended but also THE CLOSEST servers
    
    Added full automation of finding closest servers
    
    Corrected looking for servers with standard vpn-s and obfuscated
    
    Some small issues corrections
    
    preparation for amount of openvpn connection moved to parameters
    

* __Tested against four connections at once__

    [Kamoyl](mailto:kamoyl@outlook.com) - Wed, 29 May 2019 21:21:56 +0200
    
    
    added .gitignore
    
    removed auth - but it is easy to add
    

* __Changelog__

    [Kamoyl](mailto:kamoyl@outlook.com) - Tue, 28 May 2019 18:43:17 +0200
    
    
    

* __Rewritten completely the whole code and did it smaller, and cleaner, and in one loop accordingly to a connection__

    [Kamoyl](mailto:kamoyl@outlook.com) - Tue, 28 May 2019 17:03:18 +0200
    
    
    removed separated iptables code, and stored it in main script
    
    slightly changed all notifications
    
    Prepare script for a parameter of amount of simultaneus connections
    
    made lots of cleaning
    

* __Added options to connect to different countries at once - funny results form IP localization services :)__

    [Kamoyl](mailto:kamoyl@outlook.com) - Tue, 28 May 2019 09:42:34 +0200
    
    efs/remotes/origin/initial, refs/heads/master
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
    
    


