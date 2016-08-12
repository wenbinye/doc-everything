http://www.debian.org/doc/manuals/repository-howto/repository-howto#id3032359
http://askubuntu.com/questions/529/how-to-set-up-an-apt-repository

apt-get install python-software-properties

sudo apt-get install software-properties-common

Step 1: On the PPA's overview page, look for the heading that reads Adding this PPA to your system. Make a note of the PPA's location, which looks like:

ppa:gwibber-daily/ppa

Step 2: Open a terminal and enter:

sudo add-apt-repository ppa:user/ppa-name

Replace ppa:user/ppa-name with the PPA's location that you noted above.

add-apt-repository -y ppa:nginx/stable
