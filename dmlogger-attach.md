# Use dm-logger to log a network attachment process

This process was developed to work specific equipment. It should be possible to adapt the general principle to other dm-logger debug tasks

# Equipment used
* Raspberry Pi 4 
* with latest raspberry pi os and 
* minicom installed
* Sierra Mobile Broadband Package for Linux (MPBL) drivers (in this case R23)
* Sierra EM9191 card development board
* Suitable dm-logger application
* Filter file "default_qxdm_plus_5G.cfg"

# Procedure

It's important to timestamp every event so that if there is an issue with the log the process taken can be debugged.

Open two Linux terminals. The first terminal will be used with the dm-logger tool,
The second terminal will be used for Serial AT command communication with the modem 

<BR>


**First terminal:** prepend data/time to the command line by typing
1. *export PROMPT_COMMAND="echo -n \[\$(date +%Y-%m-%d' '%H:%M:%S)\]\ "*

**First terminal:** Begin recording command line by typing (use different filename for different sessions) 
1. *script terminal1.txt* 
1. Expected response --> *Script started, file is terminal1.txt* 

**First terminal:** change to the directory where you copied *dm-logger* and *default_qxdm_plus_5G.cfg* e.g 
1. *cd dm-logger/bin/*
1. Check the required files are present by typing *ls*
1. Response should contain files --> *default_qxdm_plus_5G.cfg* and *dm-loggerrpi* 
1. dm-loggerrpi needs to be executable - change permissions if necessary  


    

**Second terminal** prepend data/time to the command line by typing
1. *export PROMPT_COMMAND="echo -n \[\$(date +%Y-%m-%d' '%H:%M:%S)\]\ "*
    
**Second terminal:** Begin recording command line by typing (use different filename for different sessions) 
1. *script terminal2.txt* 
1. Expected response --> *Script started, file is terminal2.txt* 

**Second  terminal:** check modem is present 
 1. Type *ls /dev/ttyU** 
 1. Expected response is */dev/ttyUSB0  /dev/ttyUSB1  /dev/ttyUSB2* 
    
**Second terminal:** start minicom terminal session with modem 
1. *sudo minicom -D /dev/ttyUSB2* 
1. Turn on minicom extended time stamps (Ctrl A n twice) 
    1. Ctrl A n
    1. Ctrl A n 
    1. responses should look like this
```
[2021-11-25 11:54:26.393] at
[2021-11-25 11:54:27.092] OK
```
**Second terminal:** Check that QXDMLOGENABLE is set  
1. Type *at!custom?* 
1. Check response contains QXDMLOGENABLE 0x01    
1. If QXDMLOGENABLE is not set. Send command 
    1. Type *at!entercnd="A710"*
    1. Type *at!custom="QXDMLOGENABLE", 1*
    1. Reboot modem at+cfun=1,1 then retest as Type *at!custom?* 

**Second terminal:** turn radio off
1. Type *at+cfun=0*
    
**Second terminal:** check modem state
1. Type *at+creg=1*
1. Type *at+cereg=1*    
1. Type *at+cgdcont?*
1. Type *at+cops?*
    
**First terminal:** start dm-logging (assumes filter is on same path as dm-logger)
1. Type *./dm-loggerrpi /dev/ttyUSB1 -c default_qxdm_plus_5G.cfg -o test_log.qmdl    

**Second terminal:** Turn radio on
1. Type *at+cfun=1*
1. Type *at+cfun?* should return *+CFUN: 1*
1. Type *at+cops?*  Try this several times over the next 10 minutes
1. at+cfun=0
    
**First terminal:** stop dm-logging
1. Hit the *Enter* Key to stop logging
    
**First terminal:** exit script
1. *Ctrl D*
    
**Second terminal:** Exit minicom
1. *Ctrl A X Yes 

**Second terminal:** exit script
1. *Ctrl D*

 
Send the dm-logger log file (qdml) and the two terminal log files to your support contact
    
 
    
    



