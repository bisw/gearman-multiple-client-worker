# gearman-multiple-client-worker

This is a simple bash script which will create two daemon service which will run everymoment as well as on system roobot. If you are using gearman, then it is very important to use gearman parallel functionality. So to achieve that goal we need to run multiple worker as well as multiple client of gearman parallaly. That what this service will do, by default it will launch 10 worker and 10 client instance and they will run parallaly. This is tested with 16.04.


## MODIFICATION
Gearman client service
1. PROG_PATH="/var/www/html/gearman" : Path of your gearman repo.
2. PROG="client.php" : Gearman client script
3. PROG_ARGS="" : leave it
4. PID_PATH="/var/run" : leave it
5. FA_CLIENTS=10 : By default 10 gearman client will launch. You can modify FA_CLIENTS variable according to your requirement.


Gearman worker service
1. PROG_PATH="/var/www/html/gearman" : Path of your gearman repo.
2. PROG="worker.php" : Gearman worker script
3. PROG_ARGS="" : leave it
4. PID_PATH="/var/run" : leave it
5. FA_WORKERS=10 : By default 10 gearman worker will launch. You can modify FA_WORKERS variable according to your requirement.


##INSTALL:

Connect to your server via SSL as root because only as root we can use service start/stop/reload for the seperate daemons. On Ubuntu we need to do the following to make a script into a daemon this way and also run them on system reboot.

1) put gearman-client and gearman-worker into /etc/init.d/ folder
2) sudo chmod +x /etc/init.d/gearman-client
3) sudo chmod +x /etc/init.d/gearman-worker
4) sudo update-rc.d /etc/init.d/gearman-client defaults
4) sudo update-rc.d /etc/init.d/gearman-worker defaults
5) sudo systemctl daemon-reload


Now gearman-client and gearman-worker is ready to use.
Services for gearman-client
Start service: sudo service gearman-client start
Stop service: sudo service gearman-client stop
Restart service: sudo service gearman-client restart/reload

Services for gearman-worker
Start service: sudo service gearman-worker start
Stop service: sudo service gearman-worker stop
Restart service: sudo service gearman-worker restart/reload


Note: if you modify service script, sudo systemctl daemon-reload is needed. In case you modify in you gearman script, in that case you have to restart gearman-client and gearman-worker to effect latest code.
