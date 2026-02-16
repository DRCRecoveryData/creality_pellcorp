To install the latest Klipper with load cell sensor support, you need:

1. Perform hardware modifications according to the instructions (up to the software part) - 
	https://github.com/cryoz/K1_tenso_manual/tree/main

2. Root access is required (Enable Root Access section) - 
	https://guilouz.github.io/Creality-Helper-Script-Wiki/firmwares/install-and-update-rooted-firmware-k1/ 

3. After connecting to the printer via SSH, perform a factory reset by running the following commands in sequence:

	wget --no-check-certificate  https://raw.githubusercontent.com/pellcorp/creality/main/k1/services/S58factoryreset
	chmod +x S58factoryreset
	./S58factoryreset reset 

   After startup, wait for the printer to restart itself and reconnect to it via SSH

4. Next, you can run the automated installation with the following commands:

	git config --global http.sslVerify false

	git clone https://github.com/Sekilsgs2/creality_pellcorp.git /usr/data/pellcorp

	sync

	/usr/data/pellcorp/k1/installer.sh --install loadcell

 
   The script will perform an automated installation of Klipper and all required modules - after installation you need to restart.
   If the printer does not produce any errors, you can start calibrating the load cell sensors according to the instructions (section 4.4 Calibration) -
 
	https://github.com/cryoz/K1_tenso_manual/tree/main

   WARNING!!! In the loadcell.cfg file on these lines:
   dout_pin: leveling_mcu:PA0
   sclk_pin: leveling_mcu:PA2
   If you soldered wires to a different sensor with different pins - you need to change them to your pins, otherwise the printer head may crash into the table!
   

   After calibration, you can try to do HOME and try to print. You may need to adjust the Z Offset.
   There seems to be a bug in the load cell code itself - you cannot save the Z offset through the web interface - it complains about negative values - but you can manually enter the resulting offset in
   the loadcell.cfg file - mine turned out to be -0.1
   
   Warning - my nozzle cleaning script is used - it needs to be adjusted - you need to make changes to the head position (X, Y, Z) when cleaning. All settings are in the NOZZLE_CLEAR.cfg file

   If you have any questions or suggestions - write to Telegram - @estenkin


This repo also hosts the wiki:
Go to https://github.com/pellcorp/creality/wiki
