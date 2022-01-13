# SW / RPi driver build manual

From  https://github.com/RPi-Distro/rpi-source

## Steps

Make sure the RPi file system is expanded

Dependencies  
```
sudo apt install git bc bison flex libssl-dev
```

Then install  
```
sudo wget https://raw.githubusercontent.com/RPi-Distro/rpi-source/master/rpi-source -O /usr/local/bin/rpi-source && sudo chmod +x /usr/local/bin/rpi-source && /usr/local/bin/rpi-source -q --tag-update
```

Then Run
```
rpi-source
```

Then from src/USB
```
make
```

Then 
```
make install
```

With RC7620 - I see
```
$ lsusb -t
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/4p, 5000M
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=xhci_hcd/1p, 480M
    |__ Port 1: Dev 2, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 1: Dev 3, If 3, Class=Vendor Specific Class, Driver=qcserial, 480M
        |__ Port 1: Dev 3, If 8, Class=Vendor Specific Class, Driver=qmi_wwan, 480M
        |__ Port 1: Dev 3, If 2, Class=Vendor Specific Class, Driver=qcserial, 480M
        |__ Port 1: Dev 3, If 0, Class=Vendor Specific Class, Driver=qcserial, 480M
        |__ Port 3: Dev 4, If 0, Class=Human Interface Device, Driver=usbhid, 1.5M
        |__ Port 3: Dev 4, If 1, Class=Human Interface Device, Driver=usbhid, 1.5M
        |__ Port 4: Dev 5, If 0, Class=Human Interface Device, Driver=usbhid, 1.5M
```

