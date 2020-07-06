---
layout: default
title: Netbox
parent: IT Applications
---

# Netbox
{: .no_toc }

IP Address Management and Datacenter Infrastructure Management
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Project Information

[https://github.com/netbox-community/netbox](https://github.com/netbox-community/netbox)

This is an active project with very responsive and friendly contributors.

## Installing Netbox

### Prerequisites

Before you begin, [create a new virtual machine](../../../../virtualization/vmware/building-a-new-virtual-machine.md#creation) with an [Ubuntu](../../../../linux/ubuntu.md) Linux core. Run apt update and apt upgrade to bring the system up-to-date. While Netbox provides documentation for both Centos and Ubuntu, I will just cover the Ubuntu side.

You can find the full documentation for this project at: [https://netbox.readthedocs.io/en/stable/installation/](https://netbox.readthedocs.io/en/stable/installation/)

Some information in this post is not included in the official documentation.

### Firewall

Due to the level of detail this system can provide, I like to limit the subnets that can access this system.

#### Enable the Firewall

```text
sudo ufw enable
```

#### Allow SSH to Putty from your subnet

```text
sudo ufw allow from x.x.x.x/24 to any port 22
```

####  Allow HTTP and HTTPS from your subnet

```text
sudo ufw allow from x.x.x.x/24 to any port 80
sudo ufw allow from x.x.x.x/24 to any port 443
```

### PostgreSQL

#### Install

```text
sudo apt update
sudo apt install -y postgresql libpq-dev
```

#### Configure

When configuring the database,  you are also going to create a user for the database. Be sure to change the password when you create the user.

```text
# sudo -u postgres psql
postgres=# CREATE DATABASE netbox;
CREATE DATABASE
postgres=# CREATE USER netbox WITH PASSWORD 'change-this-password';
CREATE ROLE
postgres=# GRANT ALL PRIVILEGES ON DATABASE netbox TO netbox;
GRANT
postgres=# \q
```

#### Test Connection

Test the connection by signing into the database with the username \(-U\) and password \(prompted after you try to connect\)

```text
psql -U netbox -W -h localhost netbox
```

One you have connected, type **\q** to exit

### Netbox

#### Install Prerequisites

This is slightly different from the official documentation with the inclusion of python3-testresources. This dependency was needed when using the upgrade script to upgrade Netbox from 2.7.3 to 2.7.4

```text
sudo apt install -y git python3 python3-pip python3-dev build-essential libxml2-dev libxslt1-dev libffi-dev libpq-dev libssl-dev redis-server zlib1g-dev python3-testresources
```

#### Clone the Git Repository

```text
sudo mkdir -p /opt/netbox/ && cd /opt/netbox/
sudo git clone -b master https://github.com/netbox-community/netbox.git .
```

#### Python requirements

```text
sudo pip3 install -r requirements.txt
```

#### Generate a Secret Key

You will use this in the configuration step.

```text
cd /opt/netbox/netbox
python3 generate_secret_key.py
```

Copy this key to a notepad temporarily to use later.

#### Configuration

```text
cd /opt/netbox/netbox/netbox/
sudo cp configuration.example.py configuration.py
sudo nano configuration.py
```

##### ALLOWED\_HOSTS

This will be what the server responds to when people are reaching out to it

```text
ALLOWED_HOSTS = ['netbox.example.com', '192.168.1.2']
```

##### DATABASE

Add the username and password for the Netbox user you created earlier for the database

```text
DATABASE = {
    'NAME': 'netbox',                   # Database name
    'USER': 'netbox',                   # PostgreSQL username
    'PASSWORD': 'change-this-password', # PostgreSQL password
    'HOST': 'localhost',                # Database server
    'PORT': '',                         # Database port (leave blank for default)
    'CONN_MAX_AGE': 300,                # Max database connection age
}
```

##### SECRET\_KEY

Scroll down under REDIS and you will see an area to post the secret key

##### BANNER\_TOP, BANNER\_BOTTOM, and BANNER\_LOGIN

These place a blue bar on the top of every page, bottom of every page, and only on the login screen. Choose the wording you would like to be used for each if desired.

##### LOGIN\_REQUIRED

If you would like to add an authentication piece to Netbox to help add an additional barrier to the information, you can change this value to True

##### PREFER\_IPV4

If you are generally using IPv4 for your devices, you can set this to True

##### TIME\_ZONE

You can set your time zone using the Region/City format. A list can be found here: [http://manpages.ubuntu.com/manpages/bionic/man3/DateTime::TimeZone::Catalog.3pm.html](http://manpages.ubuntu.com/manpages/bionic/man3/DateTime::TimeZone::Catalog.3pm.html)

When finished, press Ctrl+X then Y

#### Create The Netbox SuperUser

This account will be used to log in to the Netbox web GUI.

```text
# python3 manage.py createsuperuser
Username: admin
Email address: admin@example.com
Password:
Password (again):
Superuser created successfully.
```

#### Collect Static Files

```text
# python3 manage.py collectstatic --no-input

959 static files copied to '/opt/netbox/netbox/static'.
```

#### Test the Application

This is just to test and see if the application is working with a very basic web server. This is not what you will be using in production.

```text
# python3 manage.py runserver 0.0.0.0:8000 --insecure
Performing system checks...

System check identified no issues (0 silenced).
November 28, 2018 - 09:33:45
Django version 2.0.9, using settings 'netbox.settings'
Starting development server at http://0.0.0.0:8000/
Quit the server with CONTROL-C.
```

Open up a web browser on the server and test the connection using HTTP to port 8000. This will currently not work with a remote machine due to the ufw being enabled. If you want to quickly test, you can sudo ufw disable, test the site, then sudo ufw enable.

### Web Server

#### Install Nginx

```text
apt-get install -y nginx
```

#### Create the OpenSSL Config File

Only follow self-signed if you are hosting this locally and are not connecting this to the outside world. This is just to get HTTPS to work so you don't have a login form exposed to HTTP. If you are hosting this where others can access, follow proper PKI protocols.

```text
cd /etc/ssl/certs/
sudo nano cert.conf
```

Paste the following inside of nano and update all variables with asterisks around them. This will create a configuration first that will set up the defaults.

```text
[req]
default_bits       = 2048
default_keyfile    = cert.key
distinguished_name = *server.domain.tld*
req_extensions     = req_ext
x509_extensions    = v3_ca

[req_distinguished_name]
countryName                 = Country Name (2 letter code)
countryName_default         = *US*
stateOrProvinceName         = State or Province Name (full name)
stateOrProvinceName_default = *New York*
localityName                = Locality Name (eg, city)
localityName_default        = *Rochester*
organizationName            = Organization Name (eg, company)
organizationName_default    = *Company Name*
organizationalUnitName      = organizationalunit
organizationalUnitName_default = *IT Department*
commonName                  = Common Name (e.g. server FQDN or YOUR name)
commonName_default          = *localhost*
commonName_max              = 64

[req_ext]
subjectAltName = @alt_names

[v3_ca]
subjectAltName = @alt_names

[alt_names]
DNS.1   = *FQDN*
DNS.2   = *IP Address*
```

* Press **CTRL X** to exit
* Press **Y** to save

#### Generate The SSL Certificate and Key

This will generate a 10-year SSL cert for the machine.

> **NOTE: Do not do this on any public facing server. For public-facing, consider using Let's Encrypt:** [**https://www.nginx.com/blog/using-free-ssltls-certificates-from-lets-encrypt-with-nginx/**](https://www.nginx.com/blog/using-free-ssltls-certificates-from-lets-encrypt-with-nginx/)\*\*\*\*

```text
sudo openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout cert.key -out cert.crt -config cert.conf
```

You should be able to **ls** in **/etc/ssl/certs/** and make sure you see a .key and .crt.

#### Create the Netbox NGINX Site

```text
cd /etc/nginx/sites-available#
sudo rm default
sudo nano netbox
```

Paste the following in Netbox. This will create a HTTPS site on port 443 and a HTTP 301 redirect to the HTTPS site on port 80. Change the variable in asterisks

```text
server {
    listen 80;
return 301 https://$host$request_uri;
}

server{
    listen 443;
    server_name *server.example.com*;

    ssl_certificate             /etc/ssl/certs/cert.crt;
    ssl_certificate_key         /etc/ssl/certs/cert.key;

    ssl on;
    ssl_session_cache  builtin:1000  shared:SSL:10m;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:DHE-RSA-AES256-GCM-SHA512:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-SHA384;
    ssl_prefer_server_ciphers on;

    client_max_body_size 25m;

    location /static/ {
        alias /opt/netbox/netbox/static/;
    }

    location / {
        proxy_pass http://127.0.0.1:8001;
        proxy_set_header X-Forwarded-Host $server_name;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

#### Make Netbox Available

```text
cd /etc/nginx/sites-enabled/
sudo rm default
sudo ln -s /etc/nginx/sites-available/netbox
service nginx restart
```

#### Gunicorn

```text
pip3 install gunicorn
cd /opt/netbox
cp contrib/gunicorn.py /opt/netbox/gunicorn.py
```

#### Systemd Config

```text
cp contrib/*.service /etc/systemd/system/
systemctl daemon-reload
systemctl start netbox.service
systemctl start netbox-rq.service
systemctl enable netbox.service
systemctl enable netbox-rq.service
systemctl status netbox
```

The last command checks the status of the netbox application. Verify that it is running and that you are able to connect to it using HTTPS on your web browser. From here, you should be able to log in and start documentation.

> **NOTE: This is a reminder to check that UFW is enabled and filtering properly**


## Upgrading Netbox

### Locating Release Information

You can locate the latest release at [https://github.com/netbox-community/netbox/releases](https://github.com/netbox-community/netbox/releases). If the version posted is higher than the current version, you should be able to upgrade. Backup/Snapshot the computer before you upgrade the software as some updates may break.

{% embed url="https://github.com/netbox-community/netbox/releases" %}

### How To Upgrade

#### Cloning the Git Repository

```text
cd /opt/netbox
sudo git checkout master
sudo git pull origin master
sudo git status
```

#### Running The Upgrade Script

```text
sudo ./upgrade.sh
```

#### Restarting The Service

```text
sudo systemctl restart netbox
sudo systemctl restart netbox-rqworker
```


## Rack Documentation

The order of this flow is intentional as certain aspects have dependencies of information being in certain spots. Working this documentation top-down will help limit the amount of effort needed to document.

### Organization

#### **Region**

This is where you set up Campuses

* Log into Netbox
* Go to Organization/Regions
* Select Add
* Give the campus a name
* Select Create

#### **Sites**

This will be the building you are working in. You may have one or multiple buildings per campus.

* Log into Netbox
* Go to Organization/Sites
* Select Add
* Name the IDF the Campus-Room Number
* Create a slug to be similar to the name
* Select the correct Region \(Campus\) for the site
* Select Create at the bottom

### **Racks**

#### **Rack Roles**

These are the different purposes of your racks, whether that is audio/visual, data/infrastructure, etc.

* Log into Netbox
* Go to Organization/Rack Roles
* Select Add
* Give it a name and slug
* Color is optional
* Select Create

#### **Rack Groups**

A Rack Group is the MDF or IDF the racks are located in.

* Log into Netbox
* Go to Organization/Rack Roles
* Select Add
* Select the appropriate site \(building\) for the rack group
* Give the rack group a name \(Campus-RoomNumber is fine\)
* Select Creat**e**

#### **Racks**

This is where you document each individual rack. After a rack is set up, you can go back into this section to see its elevations and add devices.

* Log into Netbox
* Go to Organization/Racks
* Select Add
* Select the appropriate Site \(Building\)
* Give the rack a name \(Usually Building-Room-RackLetterOrNumber\)
* Select the appropriate group
* Give the appropriate role
* If the rack has an asset tag number, mark that down
* Select the correct type of rack under Dimensions
* Type in the correct height of the rack
* Select Create

### Device Manufacturers and Types

If you want to document racks well, it will relieve much stress to create device types and manufacturers first before populating your rack elevations. You can pre-configure device ports at the device type level instead of doing it for each device.

#### **Manufacturers**

This allows you to group device types by Manufacturer

* Log into Netbox
* Go to Devices/Manufacturers
* Select Add
* Give it a name
* Select Create

#### **Device Types**

This allows you to set up the device template. Once it is set up here, you don’t have to re-add all of the ports and connections.

* Log into Netbox
* Go to Devices/Device Types
* Select Add
* Choose the correct Manufacturer
* Type in the Model Number \(Or Brand + Model Number\)
* Enter the Part number/Service Tag if necessary
* Enter the correct Height in Rack Units
* Select Create

#### **Template Creation**

After you have created the device type, you can then go back and select the device type to set up the template that device type will use when added to racks.

* After you have created the device type go to Devices/Device Types
* Select the device type you would like to generate the template with
* Most of the ports you will be creating is the interface port for Data since you will likely be doing this for switches/routers.
  * Scroll down to the interfaces section
  * Select Add Interfaces at the bottom right
  * For name, give it a number in brackets like \[1-24\]
  * For type, give it the correct connection type, such as 1000Base-T
  * Add a stacking module if needed

**NOTE: Patch panels are a little different in this regard as you have to create both front and rear ports and connect the two together.**

#### **Device Roles**

Device roles allow you to color-code devices in the rack elevations

* Log into Netbox
* Go to Devices/Device Roles
* Select Add
* Give the device a name
* Choose a color different from the rest
* Unselect VM Role
* Select Create

#### **Platforms \(Operating Systems\)**

* Log into Netbox
* Go to Devices/Platforms
* Select Add
* Give it a name and Manufacturer
* Select Create

#### **Devices**

While you will want to follow the rest of these sections to create a device on your rack elevation, it is actually easier to do it from the rack than from Devices/Devices.

* Log into Netbox
* Go to Racks/Racks
* On the rack elevation, select the BOTTOM rack unit the device will be located on.
  * If it is 2U, it will sit on the bottom number and go up.
* Give the device a name that will be displayed on the elevation and role for the color
* Select the proper manufacturer and device type
* Give it a serial number and asset tag
* The site, rack, face, and position should autofil
* Select the appropriate platform
* Paste the config if desired
* Select Create
* Go back into the rack and open the device
* Scroll down to the interface and select the edit button
* Add the MAC Address of the interface
* If the interface is an OOB management, select the checkbox for OOB Management
* Select Update 


## IP Address Documentation

It is best to perform the Rack Documentation section of this system before moving to IP Address Management due to the dependencies required to document this information. Like Rack documentation, proceeding in the order documented here will help you complete all dependencies before moving onto specific devices.

### IPAM

#### VLAN Groups

This is how you can categorize different VLAN’s, such as DATA, VoIP, WiFi, Security.

* Log into Netbox
* Go to IPAM/VLAN Groups
* Select Add
* Leave site blank… not sure if there is any benefit right now for breaking up by site
* Name the VLAN Group
* Select Create

#### VLANs

This is how you can specify the different VLANs.

* Log into Netbox
* Go to IPAM/VLANs
* Select Add
* List the VLAN ID
* Name the VLAN
* Select the site it is on
* Select group it is a part of
* Select the role it is in
* Give it a description if needed
* Select Create

#### Aggregates

This is how you can specify the different IP Address blocks in use –This works for both private and public IP blocks.

* Log into Netbox
* Go to IPAM/Aggregates
* Select Add
* For Prefix, enter the CIDR notation of the block in use \(Example: 10.0.0.0/8\)
* Select the RIR for that address block
* Select Create

#### Prefix/VLAN Roles

This is how you can categorize the campus for each different IP Address blocks in use

* Log into Netbox
* Go to IPAM/Prefix/VLAN Roles
* Select Add
* Give it a name
* Select Create

#### Prefix/VLAN Roles

This is how you can categorize the campus for each different IP Address blocks in use

* Log into Netbox
* Go to IPAM/Prefixes
* Select Add
* For Prefix, enter the CIDR Notation \(should be the x.x.x.0/24 address for a CIDR notation\)
* Select the role if needed
* Give it a description
* If all addresses in the prefix are usable, select **Is a pool**
* Select the site
* Select the VLAN Group
* Select the VLAN
* Select Create

#### IP Addresses

There are two ways to enter IP Addresses. One is for internal addresses, one is for external addresses \(through NAT\). The internal device must have an IP address before the external IP address can be documented.

##### **Internal Addresses \(10.x.x.x\)**

##### **Static Addresses**

* Log into Netbox
* Go to Organization/Sites
* Select the campus
* Select the number above Racks on the right side
* Select the Rack the device is located in
* Select the device on the rack elevation
* Under the interfaces section, select the + next to the interface you would like to add an IP address
* Type in the Address in CIDR Notation
* Give it a DNS Name and description
* Select Create
* After the IP address is created, if you have not added a MAC address to that interface, edit the interface and add the MAC address.

##### **DHCP Address Blocks**

* Log into Netbox
* Go to IPAM/Prefixes
* Select the Address Block you want to change
* Select the IP Addresses tab
* Select Add an IP Address
* Select Bulk Create
* Type in a range in CIDR notation with the variable numbers in brackets \(like 10.0.1.\[10-220\]/24\)
* Change Status to DHCP
* Give it a proper role
* Give it a description

##### **External Addresses**

This will link an external address to an Internal address

* Log into Netbox
* Go to IPAM/Prefixes
* Select the Address Block you want to change
* Select the IP Addresses tab
* Select Add an IP Address
* Type in an external address in CIDR notation with the variable numbers in brackets \(like x.x.x.\[1-224\]/24\)
* Leave status as active
* Give it the external DNS name
* Give it a description
* Go down to NAT IP \(Inside\)
* Find the device in one of two ways
  * Locate the device by Site, Rack, Device, and IP – OR -
  * Select the By IP tab and locate the internal IP address.
* Select Create

#### Cable Paths

If you want to get real fancy, you can document which interfaces are connected to patch panel ports or switch ports. This is done by connecting the interfaces together in Netbox. You can define cable length, color, and type between the two. If this is defined, you can later run reports to see the cable patch all the way from the NOC to the end device.

* Log into Netbox
* Go to Organization/Sites
* Select the campus
* Select the number above Racks on the right side
* Select the Rack the device is located in
* Select the device on the rack elevation
* Under the interfaces section, next to the +, select the two arrows pointing to each other in a green icon.
* Select the type of interface it is going to
  * Interface – Direct connection to a switch or computer
  * Front port – The front side of a patch panel
  * Rear Port – the rear port of a patch panel
* Select the site, rack, and device the cable is going to
* Select the port it is going to under Name
* Define the type of cable, rough length if possible, color, and label.
* Select Connect

