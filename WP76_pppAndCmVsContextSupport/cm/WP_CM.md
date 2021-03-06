# Scope
Capture Qualcomm debug using Legato cm (cm data connect) to activated context 3  
Capture Qualcomm debug using Legato cm (cm radio) to observe automatic context 1 connection following radio on  

## Equipment
RPi4 Bullseye os  
WASP PCA + WP7607  
```
Firmware Version:              SWI9X07Y_02.37.03.00 73df45 jenkins 2020/04/08 10:59:14
Bootloader Version:            SWI9X07Y_02.37.03.00 73df45 jenkins 2020/04/08 10:59:14
MCU Version:                   002.015
PRI Part Number (PN):          9908663
PRI Revision:                  001.002
Carrier PRI Name:              GENERIC
Carrier PRI Revision:          002.095_000
SKU:                           1104192
```
EE PAYG SIM - note network RAT is LTE - we suspect different behaviour when RAT is 2G or 3G. RAT alternatives will be the subject of other tests  

## Procedure

RPI -> Start the capture
```
sudo ./dmcapture.sh -a arm -d /dev/ttyUSB0 -l  -f filters/MC7xxx_GSM_GPRS_EDGE_WCDMA_LTE_DATA_EVDO_SMS.sqf -o testWP76_cm.qmdl
```

RPI-> shell into the WP->  and then start context 3
```
ssh root@192.168.2.2
```

Check the context settings - note the index
```
root@swi-mdm9x28-wp:~# cm data
Index:                         3
APN:                           everywhere
PDP Type:                      IPV4
Connected:                     no
Auth type:                     PAP
User name:                     eesecure
Password:                      secure
```

Activate context 3
```
cm data connect
```


## Results

After the successful connection -  (ignore context 2 that's me messing with at+cgact)

RPI-> 
```
minicom root@192.168.2.2
```


Check the contexts and modem reported IP addresses

```
> at+cgact?
> +CGACT: 1,1
> +CGACT: 2,1
> +CGACT: 3,1

> AT+CGPADDR
> +CGPADDR: 1,100.67.208.145
> +CGPADDR: 2,0.0.0.0
> +CGPADDR: 3,100.66.238.50
```

[Qualcomm debug raw data](./testWP76_cm.qmdl)

Qualcomm debug decode
![Sierra DM log decode](./WP_CM_QualcomDMDecode_1.png)


# Initial radio startup

RPI-> shell into the WP  
```
ssh root@192.168.2.2
```
WP-> Radio off  
```
cm radio off
```


RPI -> Start the capture  
```
sudo ./dmcapture.sh -a arm -d /dev/ttyUSB0 -l  -f filters/MC7xxx_GSM_GPRS_EDGE_WCDMA_LTE_DATA_EVDO_SMS.sqf -o testWP76_cmRadioOn.qmdl
```

[Qualcomm debug raw data](./testWP76_cmRadioOn.qmdl)

WP-> Radio on  
```
cm radio on
```

Check to see if context 1 auto activated
```
at+cgact?
+CGACT: 1,1
+CGACT: 2,0
+CGACT: 3,0

AT+CGPADDR
+CGPADDR: 1,100.73.205.66
+CGPADDR: 2,0.0.0.0
+CGPADDR: 3,0.0.0.0
```



 

