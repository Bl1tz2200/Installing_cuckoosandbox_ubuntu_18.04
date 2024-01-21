# Installing_cuckoosandbox_ubuntu_18.04
I will help you with installing cuckoo sandbox on ubuntu 18.04.

# Choose ubuntu
Be sure that you have ubuntu 18.04. On other versions my instructions wouldn't work. And be sure that you have much time. <br>
**If you interrupt the installation file it will make many errors and you will lose much more time to fix them.**<br>

# Starting
I will use virtualbox by the way of virtualization. <br>
Install linked file and run it:<br>
<br>
$ sudo -u *enter your user name* ./cuckoo_installer.txt *enter your internet interface*<br>
<br>
After that you need to wait. By default it will install win7 virtual machine.<br>
When code stopped and you see line:<br>
<br>
2024-01-21 07:37:36,655 \[cuckoo\] INFO: Starting Cuckoo Rooter (group=*group of your user*)!<br>
<br>
Don't close the window.<br>
The cuckoo has been succesfull installed but we need to do some more things to run it.<br>
<br>
# Next step
After upper chapter open new terminal window and go to ~/.cuckoo/conf.<br>
Find virtualbox.conf and change:<br>
<br>
machines = cuckoo1<br>
to<br>
machines = 192.168.56.1011<br>
<br>
In lines down change all cuckoo1 names to 192.168.56.1011. (If you already have \[192.168.56.1011\] down then just delete label \[cuckoo1\] and all between \[cuckoo1\] and \[192.168.56.1011\])<br>
<br>
Then find<br>
resultserver_ip =<br>
And add <br>
resultserver_ip = 192.168.56.1<br>
<br>
Make the same work with resultserver_port but add 0:<br>
resultserver_port = 0<br>
<br>
Save and exit<br>
<br>
Then open next file: routing.conf and change <br>
internet = none<br>
to<br>
internet = *your internet interface*<br>
<br>
It will give cuckoo more access and accuracy<br>
Save and exit<br>
<br>
Then open last file: reporting.conf<br>
Change state for \[mongodb\] from no to yes<br>
<br>
from<br>
enabled = no<br>
to<br>
enabled = yes<br>
<br>
Save and exit<br>
<br>
Then run:<br>
<br>
$ sudo cuckoo<br>
<br>
If you have done all right it won't give an error. Don't close the window<br>
<br>
Open the third window and run:<br>
<br>
$ sudo cuckoo web --host 127.0.0.1 --port 8080<br>
<br>
It will give you access to cuckoo from web interface. Don't close the window<br>
<br>
If you want to use cuckoo api run:<br>
<br>
$ sudo cuckoo api<br>
<br>
Don't close the window<br>
It will create cuckoo api on localhost:8090 by default. To find your api token check ~/.cuckoo/conf/cuckoo.conf<br>
<br>
# How to run it after suspend<br>
Well, you need to open at least 3 terminal windows:<br>
First window to give access, run:<br>
<br>
$ sudo cuckoo rooter --sudo --group *your username group*
<br>
Second window to start cuckoo, run:<br>
<br>
$ sudo vmcloak-vboxnet0<br>
$ sudo cuckoo<br>
<br>
And the third window to start web interface, run:<br>
<br>
$ sudo cuckoo web --host 127.0.0.1 --port 8080<br>
<br>
Or if you need api run:<br>
<br>
$ sudo cuckoo api<br>
<br>
# What after
If you didn't catch an error and opened the cuckoo web interface on your localhost:8080 you can use cuckoo sandbox to check file but it can make mistakes and don't see some stealthy viruses.<br>
To make your cuckoo sandbox more effective you should install some additions like moloch, suricata, volatility and other.<br>




