# e-picycle Ebike Black Box ebbb

Raspberry Pi Black Box  V 0.0.1

Grafana exported example of a working install - https://snapshot.raintank.io/dashboard/snapshot/pmG5r8diaoI567h7IozUxB1F2qoeefv1

##Parts Required:

* Raspberry Pi 3 (Raspberry Pi 2 will work however there is no onboard Bluetooth/Wifi)
* Cycle Analyst
* Cycle Analyst USB Serial TTY programing cable
* Power source for Raspberry Pi - DC-DC Converter eg 36v to 12v or 48v to 12v (depending on battery voltage)

##Software to install
`sudo apt-get install build-essential libi2c-dev i2c-tools python-dev libffi-dev`

`sudo pip install smbus-cffi`

`sudo pip install git+https://github.com/bivab/smbus-cffi.git`

`sudo apt-get install screen`

`sudo apt-get install python-dev`

`sudo apt-get install python-rpi.gpio`

`sudo apt-get install rcconf`

##InfluxDB
Visit https://portal.influxdata.com/downloads and download the latest ARM binary | Standalone Linux Binaries (ARM). At the time of writing - InfluxDB v1.2.1.

`wget https://dl.influxdata.com/influxdb/releases/influxdb-1.2.1_linux_armhf.tar.gz`

`tar xvfz influxdb-1.2.1_linux_armhf.tar.gz`

`sudo adduser influxdb`

`sudo tar xzf influxdb-1.2.1-1linux_armhf.tar.gz `

`cd influxdb-influxdb-1.2.1-1`

`sudo cp -R * /`

`sudo chown influxdb:influxdb -R /etc/influxdb`

`sudo chown influxdb:influxdb -R /var/log/influxdb`

`sudo mkdir -p /var/lib/influxdb`

`sudo chown influxdb:influxdb -R /var/lib/influxdb`

`sudo cp /usr/lib/influxdb/scripts/init.sh /etc/init.d/influxdb`

`sudo chmod 755 /etc/init.d/influxdb`

`sudo cp /usr/lib/influxdb/scripts/influxdb.service /etc/systemd/system`

Start InfluxDB
`/etc/init.d/influxdb start`

Start at every boot

`sudo apt-get install rcconf`

run rcconf and push space to get “*” at influxdb.

`rcconf`

###Create InfluxDB Database to store stats retreived from Cycle Analyst

`$ influx`

Connected to http://localhost:8086 version 0.12.0
InfluxDB shell 0.12.0
>

`CREATE DATABASE ebike`

##Create user

influx -username ebike -password ebike

* Grafana
Install Grafana and create a Datasource to InfluxDB, database named ebike (Newer built can be found here https://github.com/fg2it/grafana-on-raspberry)



`sudo apt-get install adduser libfontconfig`

`wget https://github.com/fg2it/grafana-on-raspberry/releases/download/v3.1.1-wheezy-jessie/grafana_3.1.1-1472506485_armhf.deb`

`sudo dpkg -i grafana_3.1.1-1472506485_armhf.deb`

`sudo /bin/systemctl daemon-reload`

## Start Grafana on boot
`sudo /bin/systemctl enable grafana-server`

`sudo /bin/systemctl start grafana-server`

### Open web browser to http:// ip of pi:3000


![Create a datasource](https://github.com/cws4204/e-picycle/blob/master/Grafana_influxDB_datasource%20example.png)

Import Dashboard or create your own


