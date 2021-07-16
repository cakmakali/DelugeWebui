#Deluge BitTorrent Client on Ubuntu 16.04/14.04 (use raw version)

sudo add-apt-repository ppa:deluge-team/ppa

sudo apt-get update -y

sudo apt-get install deluge-webui deluged -y

sudo adduser --system --gecos "Deluge Service" --disabled-password --group --home /var/lib/deluge deluge

sudo gpasswd -a your-user-name deluge

sudo nano /etc/systemd/system/deluged.service        #Copy and paste the following lines into the file. 14-34 between
---------------------------------------------------
[Unit]
Description=Deluge Bittorrent Client Daemon
After=network-online.target

[Service]
Type=simple
User=deluge
Group=deluge
UMask=007

ExecStart=/usr/bin/deluged -d

Restart=on-failure

# Configures the time to wait before service is stopped forcefully.
TimeoutStopSec=300

[Install]
WantedBy=multi-user.target
-------------------------------------------------

systemctl start deluged

systemctl enable deluged

sudo nano /etc/systemd/system/deluge-web.service      #Copy and paste the following texts into the file. 41-59 between
-------------------------------------------------
[Unit]
Description=Deluge Bittorrent Client Web Interface
After=network-online.target

[Service]
Type=simple

User=deluge
Group=deluge
UMask=027

ExecStart=/usr/bin/deluge-web

Restart=on-failure

[Install]
WantedBy=multi-user.target
---------------------------------------------

systemctl start deluge-web

systemctl enable deluge-web

your-server-ip:8112
