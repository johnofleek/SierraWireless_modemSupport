The scope of this repo is to document Sierra Wireless debug mechansims that use the Qualcom / Sierra DM usb serial port 

# dmlogger
Notes and procedures for the Sierra Wireless dm-logger application. 
At the time of writting the following version was available.
```
./dm-loggerrpi
dm-logger v1.0.2106.0
```
This version seems to be specific to the EM9191 5G module

The dm-logger application can be obtained from the Sierra Wireless source on a page 
headed *Mobile Broadband Package for Linux (SDK, Drivers, Documentation)* currently 
[here](https://source.sierrawireless.com/resources/airprime/software/mbpl/mbpl-software-latest/#sthash.robx6zei.O6UUKym6.dpbs)

Download MBPL_Tools_R23_ENG4.bin.tar or similar latest version
The tool has been precmpiled for a number of targets as follows - pick the one you need and copy it to your target

```
dm-loggerarm
dm-loggerarm64
dm-loggerarm64linaro
dm-loggerhosti686
dm-loggerhostx86_64
dm-loggermipseb
dm-loggerrpi
```

## Debug EM9191 5g network attach using dmlogger
This [note](./dmlogger-attach.md) is aimed at capturing network attach debug information using dmlogger and the EM9191 on a Raspberry Pi.

# dmcapture
This is an older toolset.  
It is bundled with the Sierra Linux QMI SDK. It can be downloaded from the [source](https://source.sierrawireless.com/) by searching for "Linux QMI SDK".  
The version I used came from tarball "SLQS04.00.27.bin.tar"  folder I\tools\logging\dm

## Debug RC7620 failing to activate data connection
This [note](./cmcapture_rc76xx_1.md) documents a method I used to capture log files 


