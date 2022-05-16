- 👋 Hi, I’m @chander2022
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
chander2022/chander2022 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->


--- STEPS FOR  installing Nagios in Amazon Linux-----

yum install httpd php
yum install gcc glibc glibc-common
yum install gd gd-devel

adduser -m nagios
passwd nagios

groupadd nagcmd
usermod -a -G nagcmd nagios
usermod -a -G nagcmd apache

mkdir ~/downloads
cd ~/downloads

wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.0.8.tar.gz
wget http://nagios-plugins.org/download/nagios-plugins-2.0.3.tar.gz

tar zxvf nagios-4.0.8.tar.gz
cd nagios-4.0.8
./configure --with-command-group=nagcmd
make all
make install
make install-init
make install-config
make install-commandmode

vim /usr/local/nagios/etc/objects/contacts.cfg
  (configure email address)

make install-webconf

htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin  

service httpd restart 

service nagios reatart 

===NAGIOS PLUGIN====
cd ~/downloads
tar zxvf nagios-plugins-2.0.3.tar.gz
cd nagios-plugins-2.0.3
./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
make install
chkconfig --add nagios
chkconfig nagios on
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

http://<IP>/nagios


----Adding Linux clients

vi  /usr/local/nagios/etc/nagios.cfg

#Add line
cfg_file=/usr/local/nagios/etc/objects/client.cfg

cd /usr/local/nagios/etc/objects

cp  localhost.cfg   client.cfg

vi client.cfg
#add ip address 
# replace localhost with clientname

service nagios reatart 



