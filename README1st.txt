Procedura kojom je instalirano:


Step 1
Update apt source list

sudo apt-get update


Step 2
Install Updates

sudo apt-get -y upgrade


Step 3
Install Python Dependencies for Odoo 11

sudo apt-get install python3-pip


Step 4
Odoo Web Dependencies

sudo apt-get install -y npm

sudo ln -s /usr/bin/nodejs /usr/bin/node

sudo npm install -g less less-plugin-clean-css

sudo apt-get install node-less


Step 5
Install PostgreSQL 9.6+

sudo apt-get install python-software-properties

sudo vim /etc/apt/sources.list.d/pgdg.list -y

add a line for the repository
deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main

wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

sudo apt-get update

sudo apt-get install postgresql-9.6


Step 6
Create Database user for Odoo

sudo su postgres

cd

createuser -s odoo

createuser -s ubuntu_user_nam

createuser -s Admin

exit
Step 7
Create Odoo user and group

sudo adduser --system --home=/opt/odoo --group odoo
Step 8
Install Gdata

cd /opt/odoo

sudo wget https://pypi.python.org/packages/a8/70/bd554151443fe9e89d9a934a7891aaffc63b9cb5c7d608972919a002c03c/gdata-2.0.18.tar.gz

sudo tar zxvf gdata-2.0.18.tar.gz

sudo chown -R odoo: gdata-2.0.18

sudo -s

cd gdata-2.0.18/

python setup.py install

exit
Step 9
Odoo 11 Download from GitHub

Get lastest Odoo 11 from github repository. Download the Zip file from URL : “https://github.com/odoo/odoo/tree/11.0″ . Transfer the same file to /opt/odoo directory on server through ftp. Otherwise follow the below steps
cd /opt/odoo

sudo apt-get install git

sudo su - odoo -s /bin/bash

git clone https://www.github.com/odoo/odoo --depth 1 --branch 11.0 --single-branch

exit
Step 10
Create Odoo Log File

sudo mkdir /var/log/odoo

sudo chown -R odoo:root /var/log/odoo
Step 11
Edit Odoo configuration file

sudo vim /etc/odoo.conf

#Copy and paste below content in config file , write correct addons paths

[options]

; This is the password that allows database operations:

; admin_passwd = admin

db_host = False

db_port = False

db_user = odoo

db_password = False

logfile = /var/log/odoo/odoo-server.log

addons_path = /opt/odoo/addons,/opt/odoo/odoo/addons

Save and Exit the file. Now run the below command on terminal to grant ownership.

sudo chown odoo: /etc/odoo.conf
Step 12
WKHTMLTOPDF ( Supported Version 0.12.1 ) for Odoo

sudo apt-get -f install

sudo wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb

sudo dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb

sudo cp /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage

sudo cp /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
Step 13
Now Start Odoo Server

cd /opt/odoo/odoo

./odoo-bin
Step 14
Go to web browser to access Odoo 11

http://localhost:8069

Your Feedback will be Appreciated. Thanks
FIXES
ISSUE 1 : E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)

SOLUTION
sudo rm /var/lib/apt/lists/lock

sudo rm /var/cache/apt/archives/lock

sudo rm /var/lib/dpkg/lock

