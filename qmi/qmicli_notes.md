# Experiment using qmicli

# Equipment
* RPi4
* Bullesye Raspberry OS
* M.2 adapter
* EM7455

# Install qmicli

```
sudo apt-get install qmicli
```

# manual qmicli
https://www.freedesktop.org/software/libqmi/man/latest/qmicli.1.html

# Testing
Now make sure the module is ready, this can be done using the following command.
```
sudo qmicli -d /dev/cdc-wdm0 --dms-get-operating-mode
[/dev/cdc-wdm0] Operating mode retrieved:
        Mode: 'online'
        HW restricted: 'no'
```

sudo qmicli -p -d /dev/cdc-wdm0 --device-open-net='net-raw-ip|net-no-qos-header' --wds-start-network="apn='YOUR_APN',username='YOUR_USERNAME',password='YOUR_PASSWORD',ip-type=4" --client-no-release-cid
