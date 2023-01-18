# FLsun-V400
Everything you need for quality prints

There have been many topics and posts around a few common faults of this machine.
To adress these I would like to add a knowledgebase and get all the printers out there to work as they should.

Some of the common issues out there:
1: The white stuff at the nozzle > This is a silicone pase to keep the sock on the heatblock and nothing to worry about.
2: Nozzle dragging > This is one of the biggest frustrations to users out there and it seems to revolve around proper calibration and software setting.
For the sake of simplicity I will only use CURA (5.1 at this time) as a reference.
3: Top layer quality > this one is a direct connect to #2 and will resolve itself when following my next steps.


Additionally I will add useful links to builds for the printer and advanced user posts.



Lets start with using the FLSUN recovery image that enables SSH and access to the printers firmware.

The image can be found here: 


calibration:

This will be your bread and butter!
The printers probing is a bit flawwed in the stock state so we will want to edit printer.CFG nto resolve this.

 - Make sure to probe with your bed heated at the temperature you will mostly print at and let it soak for about 15 minutes.
 - Change the bed mesh to 9x9 in the config.
 - Change the bed mesh points to 5 from 3. The first point that this sensor takes is always wrong.



 - Probe and Z-offset calibration: https://www.klipper3d.org/Probe_Calibrate.html
 - Delta calibration: https://www.klipper3d.org/Delta_Calibrate.html

Next is important! 

 - Add the following line in Cura at the start GCODE after G28 to actually load the meshes for the print, please use the following: 
   BED_MESH_PROFILE LOAD=default > if you use a different naming convention for your printers config, please use that name instead.



When you have done this you will probably have noticed that the time is wrong, for you to correct this you can follow another github by Guilouz, this will also offer you the option to go full vanilla Klipper and add some other features to the machine like an ADXL accelerometer.

Please follow this link: https://github.com/Guilouz/Klipper-Flsun-Speeder-Pad


