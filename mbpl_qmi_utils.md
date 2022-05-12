# MBPL on raspberry pi

Sierra have supplied a set of tools / demo apps as source and prebuilt binary


# lite-qmi-connection-manager

In this case

* Host is Raspberry Pi 4
* Modem is RC7620
* Sierra qmi drivers have been built and installed on the Host
* From MBPL_SDK_R23_ENG4-lite\SampleApps\lite-qmi-connection-manager the prebuilt binary application is in use *lite-qmi-connection-managerrpi*
* modem must usb composition must include RMNET

For example (EM7455)
```
at!usbcomp=1,1,0000010D
OK

REBOOT

at!usbcomp?
Config Index: 1
Config Type:  1 (Generic)
Interface bitmask: 0000010D (diag,nmea,modem,rmnet0)
```

## Testing
```
pi@raspberrypi:~/MBPL $ ls
lite-cm-daemon-readme.txt  lite-cm-daemonrpi  lite-qmi-connection-managerrpi
pi@raspberrypi:~/MBPL $ sudo ./lite-qmi-connection-managerrpi

lite-qmi-connection-manager v1.0.2108.1

Open transport "/dev/cdc-wdm0" in QMI mode
ModelID: RC7620
unpack_nas_GetHomeNetwork failed: 1037
Network Selection Preference: auto
SessionStatus (0:ipv4): Disconnected
SessionStatus (1:ipv6): Disconnected
SessionStatus (2:ipv4): Disconnected
SessionStatus (3:ipv6): Disconnected

Please select one of the following options or press <Enter> to exit:
1.      Start data session
2.      Start Multiple PDN data session
3.      Stop the currently active data session
4.      Display all the profiles stored on the device
5.      Display the settings for a particular profile stored on the device
6.      Create a profile on the device
7.      Modify the settings of an existing profile stored on the device
8.      Delete a profile stored on the device
9.      Scan available networks
10.     Enable QOS Event
11.     Disable QOS Event
12.     Request QOS Expaded
13.     Get QOS Information
14.     QOS Indication Register
15.     Get Packet Statistics
16.     Get Current Channel Rate
Option :
```

```
Option : 4

ID PDPType IPAddress           PrimaryDNS          SecondaryDNS        Auth ProfileName         APNName             UserName
1  0       0.0.0.0             0.0.0.0             0.0.0.0             0    eeb                 everywhere
5  0       0.0.0.0             0.0.0.0             0.0.0.0             1    ee                  everywhere          eesecure
```

