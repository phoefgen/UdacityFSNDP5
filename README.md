# this file will complete the operations to setup the sever as per the requirements

# fix sudo error:
echo '127.0.0.1 ip-10-20-1-61' >> /etc/hosts

# add the grader user
adduser grader

# enable sudo access, by placin the new user in the sudoers grou
adduser grader sudo

# update software installed:
apt-get update
apt-get upgrade

# configure timezone:
dpkg-reconfigure tzdata

#change ssh port to 2200:
vim /etc/sshsshd_config

# setup firewall
ufw allow 2200/tcp
ufw allow http
ufw allot ntp
ufw enable

# Install Apache:
apt-get install apache2
apt-get install libapache2-mod-wsgi

# add this line to the apache config:
vim /etc/apache2/sites-enabled/000-default.conf

# >>  WSGIScriptAlias / /var/www/html/myapp.wsgi
apache2ctl restart

# install DB, setup a normal user called catalog
apt-get install postgres
su postgres
createuser catalog
psql
\password catalog
# enter password
