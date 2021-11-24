Notes on how to use dm-logger to log a network attachment process

This process was developed to work specific equipment. It should be possible to adapt the general principle to other dm-logger debug tasks

# Equipment used
* Raspberry Pi 4 
* with latest raspberry pi os and 
* Sierra Mobile Broadband Package for Linux (MPBL) drivers (in this case R23)
* Sierra EM9191 card development board

# Procedure

It's important to timestamp every event so that if there is an issue with the log the process taken can be debugged.

Open two Linux terminals. 
* First terminal will be used for Serial communication with the modem (AT commands)
* Second terminal to run the dm-logger tool

