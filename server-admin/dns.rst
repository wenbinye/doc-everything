
We have already discussed how to setup DHCP server in Ubuntu .This tutorial will explain how to release and renew a DHCP IP address in Ubuntu 10.04 (Lucid)/9.10 (Karmic)/9.04(Jaunty)
Release a DHCP ip address in Ubuntu 10.04 (Lucid)/9.10 (Karmic)/9.04(Jaunty)

Open the terminal and run the following command

sudo dhclient -r

Renew a DHCP ip address in Ubuntu 10.04 (Lucid)/9.10 (Karmic)/9.04(Jaunty)

Open the terminal and run the following command

sudo dhclient

or

sudo dhclient eth0

Note:- eth0 is your Ethernet interface

