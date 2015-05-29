== Nessus Vulnerability Scanner ==

Nessus is a vulnerability scanner provided by Tenable Network Security. Like most vulnerability scanners, its primary function is to scan targeted systems over a network for various vulnerabilities and report them back to the user for their consideration. Nessus also has the added functionality of being able to easily integrate scan results into Rapid7's Metasploit Framework through its ability to import scans and/or the nessus connector for Metasploit.

It can be ran and installed on practically any OS (Windows, Linux, OSX, Solaris, FreeBSD)and comes in two flavors: A home feed for security researchers and a professional feed that must be purchased for commercial use. The popular Backtrack Linux distribution comes with Nessus Pre-installed, only requiring the proper licensing to get started.

===Licencing===
Home Feed: up to 16 IP Addresses <br />
Evaluation: up to 16 IP Addresses and up to 15 days <br />
Professional: no apparent limits <br />

== Getting Started on Backtrack ==

I am going to run through the basic instructions required to get started on Backtrack. The instructions may differ slightly on your distro of choice, but overall, it should be fairly similar.

1. Backtrack 5, 5R1 and 5R2 all come with Nessus pre-installed and integrated into the Application/Backtrack menu system. For this purpose, I'm going to skip the actual installation process. However, if you are interested in installing Nessus on your distribution or choice, installation packages can be found [here](http://www.tenable.com/products/nessus/select-your-operating-system).

2. Next you will need to register your nessus installation with Tenable as either a home or professional feed and get the license key to actually use the product. This page for [Nessus](http://www.tenable.com/products/nessus/nessus-homefeed) will allow you to do so.

3. Ensure the system hosting your nessus instance has internet access -- you will need internet access to update nessus plugins initially as well as for licensing the installation.

4. After getting your license in your e-mail inbox, open up a terminal window and input the following:
 /opt/nessus/bin/nessus-fetch --register [license key]

This submits your license to Tenable.

5. Next you have to add a user to nessus. The first user you add will usually be the admin user. On backtrack this can be done via the backtrack menu (Vulnerability Asessment > Vulnerability Scanners > Nessus > nessus user add. Follow the on-screen prompts.

6. Next start the nessus server by "nessus start" under the vulnerability scanners menu.

option: If you want nessus to start on boot on backtrack enter the following command in a terminal window: "update-rc.d nessusd default"

7. Next, you will need to open a web browser to access the management interface for nessus. By default, nessus listens on port 8834 and will only accept HTTPS connections. So you will have to point your web browser to:
 https:\\[nessus server ip]:8834
note: the nessus management interface requires javascript and flash to run. upon first login to the management interface you may have to wait a moment or two. Nessus does a lot of background housekeeping and initialization on first login, so be patient.

[Tools](../tools.md)
