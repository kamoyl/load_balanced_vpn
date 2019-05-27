# load_balanced_vpn
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

All of it works on... yes, yes, really: Raspberry Pi 3 B+ on rasbpian:

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
before start 'em, but... it might be either changed having collected all nordvpn config files, and based on this start 
those scripts.

## HowTo

just run: openvpn_automatic_HP - the rest will be done automatically; by default - the best (least load), not
obfuscated, Netherlands servers are used, but, when use:
* -m - it will try to use NordVPN servers located in nearest countries (also with the least load)
* -h - obfuscated servers will be used (-m and -h might be used both)
* -v - for verbose use
* -o directory - is for storing all temporary files, and logs in mentioned directory 

## ToDo

- [ ] - finished nearest country servers collecting and using
- [ ] - add obfuscating nearest countries servers using
- [ ] - add full automation to find best servers from the closesed locations around country script is run from

## Changelog (I'm using [git-release-notes](https://www.npmjs.com/package/git-release-notes))

