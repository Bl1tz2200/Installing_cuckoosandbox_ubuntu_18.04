# Installing_cuckoosandbox_ubuntu_18.04
I will help you with installing cuckoo sandbox on ubuntu 18.04.

# Choose ubuntu
Be sure that you have ubuntu 18.04. On other versions my instructions wouldn't work. And be sure that you have much time. <br>
**If you interrupt the installation file it will make many errors and you will lose much more time to fix them.**<br>

# Installing
I will use virtualbox by the way of virtualization. <br>
Install linked file and run it:<br>
<br>
$ sudo -u *enter_your_user_name* ./cuckoo_installer.txt *enter_your_internet _nterface*<br>
<br>
After that you need to wait. By default it will install win7 virtual machine.<br>
After that we can say that cuckoo has been succesfull installed but we need to do some more things to run it.<br>
<br>
# Next step
After upper chapter open new terminal window and go to ~/.cuckoo/conf.<br>
Then open file: routing.conf and change: <br>
<br>
internet = none<br>
to<br>
internet = *your internet interface*<br>
<br>
It will give cuckoo more access and accuracy<br>
Save and exit<br>
<br>
Then open reporting.conf<br>
Change state for \[mongodb\] from no to yes<br>
<br>
from<br>
enabled = no<br>
to<br>
enabled = yes<br>
<br>
Save and exit<br>
(If your cuckoo don't see mongodb bu sure, that you have started it (sudo systemctl start mongodb))
<br>
# Starting
Run rooter command to give cuckoo access:
<br>
$ cuckoo rooter --sudo --group *your_username_group*<br>
<br>
Remember to don't close terminal or cuckoo won't start<br>
<br>
Then open new terminal and run:<br>
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

# How to increase accuracy
If you run your first check you will see, that cuckoo warning about those functions that cannot be malicious (dns time.microsoft, some teredo functions)<br>
That can give you wrong report thats why I recommend you configurate your VM that cuckoo use to check.<br>
To do this you should run vmcloak clone command to make new image of VM:<br>
<br>
$ sudo vmcloak clone win7x64cuckoo win7x64cuckoo_configured<br>
<br>
By next step you will need to configure it by vmcloak:<br>
<br>
$ sudo vmcloak modify --vm-visible --vrde win7x64cuckoo_configured<br>
<br>
It will open your VM in new window that you will need to configure<br>
How to know what i need to configure? Easy<br>
You should run your cuckoo web interface, than check safe file or link.<br>
After that you should check the report: find where is the unnecessary information<br>
Than just google how to disable it<br>
<br>
After configurating the VM close VMBox window and stop vmcloak modify process in terminal by ^C<br>
Restart your ubuntu computer<br>
After restarting run command to make a snapshot of our VM:<br>
<br>
$ sudo vmcloak snapshot win7x64cuckoo_configured win7x64cuckoo_configured 192.168.56.102<br>
#You can choose any ip address between 192.168.56.102 - 192.168.56.255 (just be sure that ip is free)<br>
<br>
After that you should add our new snapshot to cuckoo (remember about chosen ip address):<br>
<br>
$ sudo cuckoo machine --add win7x64cuckoo_configured 192.168.56.102 --platform windows --snapshot vmcloak<br>
<br>
Now cuckoo is ready to start<br>
Everyone should do this because you can choose your rules: what do you want to see in report and what you don't want to see<br>
By careful configuration you can make perfect VMs to check different types of files<br>

# How to run it after suspend<br>
Well, you need to open at least 3 terminal windows:<br>
First window to give access, run:<br>
<br>
$ sudo cuckoo rooter --sudo --group *your_username_group*<br>
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




