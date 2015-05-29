==Armitage Tool==

Armitage is a free and open-source front-end to the Metasploit framework Developed by Raphael Mudge and Strategic Cyber LLC. The motto and design goal of Armitage is "fast and easy hacking". This is achieved by an easy to navigate GUI, integration of db_autopwn by way of Armitage's Hail Mary along with easy host management and network pivoting through exploited hosts. Armitage also boasts collaborative capability through its deconfliction server in combination with msfrpcd, as well as attack automation via the cortana scripting engine.

==Red Teaming==

Red Teaming allows multiple members of a pentest team or red team to collaborate during an engagement.It also reduces duplication of effort, attacker footprint and chances of destabilizing controlled hosts through multiple users exploiting the same host repeatedly -- you know who has sessions on the system, and can pass sessions or have different users interact with a single session as necessary.

The architecture relies on armitage's deconfliction server to manage connections from armitage clients and in turn proxy/manage connections to msfrpcd and in turn to the controlled host(s)

to summarize, in order to perform red teaming, the system that will be acting as a server has two components:
msfrpcd (metasploit framework RPC daemon)
armitage deconfliction server (connection manager for armitage clients, and proxy to msfrpcd)


the method of doing this is in fact already scripted through the script teamserver.sh available on fastandeasyhacking.com

the script handles all the fun of the lovecraftian summoning of msfrpcd, generating an SSL cert for deconfliction server and summarily telling java to use the SSL cert on the deconfliction connection, then Here are the basic steps to do this:

1. install the latest backtrack release
2. dhclient ethX && apt-get update && apt-get -y upgrade && cd /pentest/exploit/framework && msfupdate && startx (get an ip address, patch all the things, svn up metasploit/armitage and start X)
3. terminal window: current directory will be /pentest/exploit/framework
cd data/armitage
4. cp teamserver /pentest/exploit/framework/data/armitage
5. chmod u+x teamserver && ./teamserver [ip address] [deconfliction server password you want to use]
6. tell clients connection information: ip address:port username:password
7. ???
8. profit.

***NOTE: Don't try to start msfrpcd and the deconfliction server yourself. The teamserver.sh script is made available for a reason and protects you in the event that the deconfliction server setup process changes (This is per Raphael Mudge himself). Take it from somebody that did NOT RTFM. Don't do this, and you will avoid much crying, wailing and gnashing of teeth.***

==Cortana== 

Cortana is the scripting engine for armitage and can be used to automate several tedious tasks in armitage. There are several scripts made available by Raphael and other contributors as well as the script recorder built into Armitage itself for recording manual operations you perform on a host for automation.

[A collection of Cortana scripts that you may use with Armitage and Cobalt Strike](https://github.com/rsmudge/cortana-scripts cortana-scripts github)

==References==

[Manual from Raphael Mudge](http://www.fastandeasyhacking.com/manual)
[Training from Raphael Mudge](http://www.fastandeasyhacking.com/training)

==Raphael Mudge== 
Red Team for Multiple regions: NE-CCDC, MA-CCDC, creator of Red Team Tool:[Armitage](http://www.fastandeasyhacking.com)
[@armitagehacker](https://twitter.com/armitagehacker)

[Tools](../tools.md)
