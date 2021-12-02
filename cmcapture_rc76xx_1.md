# Stop modem manager
If mode manager is running it needs to be stopped so that the modem can be manually controlled via AT commands
```
sudo systemctl stop ModemManager
```
# Equipment used

Modem 
```
ati9
Manufacturer: Sierra Wireless, Incorporated
Model: RC7620
QTI baseline: MPSS.JO.2.0.2.c1.1-00073-9607_GENNS_PACK-1.416077.1.419248.1
Revision: SWI9X07H_00.08.19.00 725c0e jenkins 2021/09/08 14:36:45
IMEI: 353634110110227
IMEI SV: 18
FSN: 7Q0273850613B0
+GCAP: +CGSM
```

Raspberry pi 4  
EE PAYG SIM  

# AT command access
Install minicom

Start AT command session
```
sudo minicom -D /dev/ttyUSB2
```

## test using EE PAYG SIM

