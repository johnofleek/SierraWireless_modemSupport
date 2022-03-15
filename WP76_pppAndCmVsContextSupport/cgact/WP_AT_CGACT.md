## Equipment
RPi4 Bullseye os  
WASP PCA + WP7607  
EE PAYG SIM - note network RAT is LTE - we suspect different behaviour when RAT is 2G or 3G. RAT alternatives will be the subject of other tests  



# Capture modem Qualcomm debug

## dm capture - SHELL 1

Captures the raw qualcom data from the WP76

```
sudo ./dmcapture.sh -a arm -d /dev/ttyUSB0 -l  -f filters/MC7xxx_GSM_GPRS_EDGE_WCDMA_LTE_DATA_EVDO_SMS.sqf -o testWP76_AT_CGACT.qmdl
Write Filter: filters/MC7xxx_GSM_GPRS_EDGE_WCDMA_LTE_DATA_EVDO_SMS.sqf -> /dev/ttyUSB0
Log messages: /dev/ttyUSB0 -> testWP76_AT_CGACT.qmdl
```

## Test command sequence - via USB AT command port - SHELL 2

Try to activate context 3 and check the result  
```
sudo minicom -D /dev/ttyUSB2
CTRL A n CTRL A n
```


```
ati9
at+cgdcont?
at+cgact?
at+cgauth?
at+ksrat?
AT+CGPADDR
AT+CGACT=1,2
AT+CGPADDR
```

**Results**

[See testWP76_AT_CGACT.qmdl](testWP76_AT_CGACT.qmdl) for raw qualcom data


The following is at command capture
```
[2022-03-14 11:56:52.843] ati9
[2022-03-14 11:56:53.504] Manufacturer: Sierra Wireless, Incorporated
[2022-03-14 11:56:53.504] Model: WP7607
[2022-03-14 11:56:53.504] Revision: SWI9X07Y_02.37.03.00 73df45 jenkins 2020/044
[2022-03-14 11:56:53.504] IMEI: 359779080470764
[2022-03-14 11:56:53.504] IMEI SV: 14
[2022-03-14 11:56:53.504] FSN: V3048285141510
[2022-03-14 11:56:53.504] +GCAP: +CGSM
[2022-03-14 11:56:53.505]
[2022-03-14 11:56:53.505] OK
[2022-03-14 11:56:58.796] at+cgdcont?
[2022-03-14 11:56:59.338] +CGDCONT: 1,"IPV4V6","everywhere","0.0.0.0.0.0.0.0.0.0
[2022-03-14 11:56:59.338] +CGDCONT: 2,"IP","everywhere","0.0.0.0",0,0,0,0
[2022-03-14 11:56:59.338] +CGDCONT: 3,"IP","everywhere","0.0.0.0",0,0,0,0
[2022-03-14 11:56:59.339]
[2022-03-14 11:56:59.339] OK
[2022-03-14 11:57:05.628] at+cgact?
[2022-03-14 11:57:06.348] +CGACT: 1,1
[2022-03-14 11:57:06.348] +CGACT: 2,0
[2022-03-14 11:57:06.348] +CGACT: 3,0
[2022-03-14 11:57:06.348]
[2022-03-14 11:57:06.348] OK
[2022-03-14 11:57:12.276] at+cgauth?
[2022-03-14 11:57:13.061] +CGAUTH: 1,0
[2022-03-14 11:57:13.061] +CGAUTH: 2,1,"eesecure"
[2022-03-14 11:57:13.061] +CGAUTH: 3,1,"eesecure"
[2022-03-14 11:57:13.061]
[2022-03-14 11:57:13.061] OK
[2022-03-14 11:57:19.853] at+ksrat?
[2022-03-14 11:57:20.473] +KSRAT: 0
[2022-03-14 11:57:20.473]
[2022-03-14 11:57:20.473] OK
[2022-03-14 11:57:25.781] AT+CGPADDR
[2022-03-14 11:57:26.420] +CGPADDR: 1,10.15.33.37
[2022-03-14 11:57:26.420] +CGPADDR: 2,0.0.0.0
[2022-03-14 11:57:26.420] +CGPADDR: 3,0.0.0.0
[2022-03-14 11:57:26.420]
[2022-03-14 11:57:26.420] OK
[2022-03-14 11:57:32.310] AT+CGACT=1,2
[2022-03-14 11:57:32.909] OK
[2022-03-14 11:57:38.510] AT+CGPADDR
[2022-03-14 11:57:39.061] +CGPADDR: 1,10.15.33.37
[2022-03-14 11:57:39.062] +CGPADDR: 2,0.0.0.0
[2022-03-14 11:57:39.062] +CGPADDR: 3,0.0.0.0
[2022-03-14 11:57:39.062]
[2022-03-14 11:57:39.062] OK

[2022-03-14 12:09:39.908] at+cgact?
[2022-03-14 12:09:43.009] +CGACT: 1,1
[2022-03-14 12:09:43.009] +CGACT: 2,1
[2022-03-14 12:09:43.009] +CGACT: 3,0
[2022-03-14 12:09:43.009]
[2022-03-14 12:09:43.009] OK

```

# Context 2 AT command deactivate
Results - disconnect
[See testWP76_AT_CGACT_Discon.qmdl](testWP76_AT_CGACT_Discon.qmdl) for raw qualcom data


```
at+cgact?
+CGACT: 1,1
+CGACT: 2,1
+CGACT: 3,0

OK
at
[2022-03-14 12:09:33] OK
[2022-03-14 12:09:39.908] at+cgact?
[2022-03-14 12:09:43.009] +CGACT: 1,1
[2022-03-14 12:09:43.009] +CGACT: 2,1
[2022-03-14 12:09:43.009] +CGACT: 3,0
[2022-03-14 12:09:43.009]
[2022-03-14 12:09:43.009] OK
[2022-03-14 12:11:08.192] at+cgact=2,0
[2022-03-14 12:11:18.360] ERROR
[2022-03-14 12:11:21.920] at+cgact?
[2022-03-14 12:11:24.761] +CGACT: 1,1
[2022-03-14 12:11:24.761] +CGACT: 2,1
[2022-03-14 12:11:24.761] +CGACT: 3,0
[2022-03-14 12:11:24.761]
[2022-03-14 12:11:24.761] OK
[2022-03-14 12:11:39.190] at+cgact=0,2
[2022-03-14 12:11:47.163] ERROR
[2022-03-14 12:11:48.871] at+cgact?
[2022-03-14 12:11:52.026] +CGACT: 1,1
[2022-03-14 12:11:52.026] +CGACT: 2,0
[2022-03-14 12:11:52.026] +CGACT: 3,0
[2022-03-14 12:11:52.026]
[2022-03-14 12:11:52.026] OK
[2022-03-14 12:11:53.993] at+cgact=0,2
[2022-03-14 12:12:04.067] OK

[2022-03-14 12:12:58.974] at+cgact?
[2022-03-14 12:13:02.946] +CGACT: 1,1
[2022-03-14 12:13:02.947] +CGACT: 2,0
[2022-03-14 12:13:02.947] +CGACT: 3,0
[2022-03-14 12:13:02.947]
[2022-03-14 12:13:02.947] OK
```


# Other things we could try
```
AT$QCPDPP=<cid>, <auth_type>, <password>, <username>
<auth_type>
0 = None-Username and password not required
1 = PAP-Username and password accepted
2 = CHAP-Username and password (secret) accepted
```
