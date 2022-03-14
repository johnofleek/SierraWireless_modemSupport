# Capture WP76 PPP over UART using context 2

## Equipment
RPi4 Bullseye os
WASP PCA + WP7607 

See [this](https://github.com/johnofleek/RPi_SierraWireless_PPP/blob/master/WP76xx_ppp_RPi_testing.md) for config and process details


## 1 Reboot the modem 

## 2 RPI SHELL 1 -> Start the syslog capture
```
tail -f /var/log/syslog
```

## 3 RPI SHELL 2 -> Start the Sierra / Qualcomm debug capture
```
sudo ./dmcapture.sh -a arm -d /dev/ttyUSB0 -l  -f filters/MC7xxx_GSM_GPRS_EDGE_WCDMA_LTE_DATA_EVDO_SMS.sqf -o testWP76_pppUC2.qmdl
```

## 4 RPI SHELL 3 -> Start the pppd capture
```
sudo pppd  /dev/ttyAMA0 115200  record WP76_pppd_ctx2.txt call pppWP76xx
```

## After connection via USB2 (not used for by pppd )

```
+CGACT: 1,1
+CGACT: 2,0
+CGACT: 3,0

OK

+CGAUTH: 1,0
+CGAUTH: 2,1,"eesecure"
+CGAUTH: 3,1,"eesecure"

OK

+CGPADDR: 1,100.76.58.254
+CGPADDR: 2,0.0.0.0
+CGPADDR: 3,0.0.0.0
```




Check the contexts and modem reported IP addresses after connection

```
at+cgact?


AT+CGPADDR

```

[Sierra DM log decode](./.png)

## Capture of pppd connection
```
pi@raspberrypi:~ $ sudo pppd  /dev/ttyAMA0 115200  record WP76_pppd_ctx2.txt call pppWP76xx
Script /usr/sbin/chat -v -f /etc/chatscripts/chatUpWP76xx finished (pid 2926), status = 0x0
Serial connection established.
using channel 1
Using interface ppp1
Connect: ppp1 <--> /dev/pts/3
sent [LCP ConfReq id=0x1 <asyncmap 0x0>]
rcvd [LCP ConfReq id=0x0 <asyncmap 0x0> <auth pap> <magic 0xd1eb66af> <pcomp> <accomp>]
sent [LCP ConfRej id=0x0 <magic 0xd1eb66af> <pcomp> <accomp>]
rcvd [LCP ConfAck id=0x1 <asyncmap 0x0>]
rcvd [LCP ConfReq id=0x1 <asyncmap 0x0> <auth pap>]
sent [LCP ConfAck id=0x1 <asyncmap 0x0> <auth pap>]
sent [LCP EchoReq id=0x0 magic=0x0]
sent [PAP AuthReq id=0x1 user="raspberrypi" password=""]
rcvd [LCP DiscReq id=0x2 magic=0xd1eb66af]
rcvd [LCP EchoRep id=0x0 magic=0xd1eb66af 00 00 00 00]
rcvd [PAP AuthAck id=0x1 ""]
PAP authentication succeeded
sent [IPCP ConfReq id=0x1 <addr 0.0.0.0> <ms-dns1 0.0.0.0> <ms-dns2 0.0.0.0>]
rcvd [IPCP ConfReq id=0x0]
sent [IPCP ConfNak id=0x0 <addr 0.0.0.0>]
rcvd [IPCP ConfNak id=0x1 <addr 100.76.58.254> <ms-dns1 109.249.185.228> <ms-dns2 109.249.185.229>]
sent [IPCP ConfReq id=0x2 <addr 100.76.58.254> <ms-dns1 109.249.185.228> <ms-dns2 109.249.185.229>]
rcvd [IPCP ConfReq id=0x1]
sent [IPCP ConfAck id=0x1]
rcvd [IPCP ConfAck id=0x2 <addr 100.76.58.254> <ms-dns1 109.249.185.228> <ms-dns2 109.249.185.229>]
Could not determine remote IP address: defaulting to 10.64.64.65
Script /etc/ppp/ip-pre-up started (pid 2933)
Script /etc/ppp/ip-pre-up finished (pid 2933), status = 0x0
replacing old default route to eth0 [10.10.10.1]
del old default route ioctl(SIOCDELRT): No such process(3)
local  IP address 100.76.58.254
remote IP address 10.64.64.65
primary   DNS address 109.249.185.228
secondary DNS address 109.249.185.229
Script /etc/ppp/ip-up started (pid 2936)
Script /etc/ppp/ip-up finished (pid 2936), status = 0x0
```