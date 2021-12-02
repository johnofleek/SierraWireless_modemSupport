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

Check operator selection
```
at+cops?
+cops: 0,0,"EE",7
```

Set the APN on context 5 leave context 1 blank
```
at+cgdcont=5,"IP","everywhere"
at+cgdcont?
+CGDCONT: 1,"IPV4V6","","0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0",0,0,0,0
+CGDCONT: 5,"IP","everywhere","0.0.0.0",0,0,0,0
```
Set authentication parameters for context 5

```
AT+CGAUTH=5,1,"eesecure","secure"
at+cgauth?
+CGAUTH: 1,0
+CGAUTH: 5,1,"eesecure"
```

Start debug log
```
sudo ./dmcapture.sh -a arm9 -d /dev/ttyUSB0 -l \
 -f filters/MC7xxx_GSM_GPRS_EDGE_WCDMA_LTE_DATA_EVDO_SMS.sqf -o testrc76_c5.qmdl
```


Activate context 5

```
AT!SCACT=1,5
```

