# Use dm-logger to log a network attachment process

This process was developed to work specific equipment. It should be possible to adapt the general principle to other dm-logger debug tasks

# Equipment used
* Raspberry Pi 4 
* with latest raspberry pi os and 
* Sierra Mobile Broadband Package for Linux (MPBL) drivers (in this case R23)
* Sierra EM9191 card development board
* Suitable dm-logger application
* Filter file "default_qxdm_plus_5G.cfg"

# Procedure

It's important to timestamp every event so that if there is an issue with the log the process taken can be debugged.

Open two Linux terminals. 
* First terminal to run the dm-logger tool
* Second terminal will be used for Serial communication with the modem (AT commands)



1. First terminal: type the following - this should prepend data/time to the command line 
  1.1 export PROMPT_COMMAND="echo -n \[\$(date +%Y-%m-%d' '%H:%M:%S)\]\ "
2. First terminal: change to the directory where you copied dm-logger and "default_qxdm_plus_5G.cfg" e.g 
  2.1 cd dm-logger/bin/
  2.2 ls contains files default_qxdm_plus_5G.cfg and dm-loggerrpi

