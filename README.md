# FLsun-V400
Everything you need for quality prints.

There have been many topics and posts around a few common faults of this machine.
To adress these I would like to add a knowledgebase and get all the printers out there to work as they should.
My writing will assume you have an inkling of an idea of the workings of both Cura as 3dprinting.

Some of the common issues out there:
1: The white stuff at the nozzle > This is a silicone glue to keep the sock on the heatblock and nothing to worry about.
2: Nozzle dragging > This is one of the biggest frustrations to users out there and it seems to revolve around proper calibration and software setting.
For the sake of simplicity I will only use CURA (5.1 at this time) as a reference.
3: Top layer quality > this one is a direct connect to #2 and will resolve itself when following my next steps.
4: Belt tension, there are many different opinions around this one, but there is an option to set them all equally.


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

 - Add the following line in Cura at the start GCODE after G28 to actually load the bed mesh for the print, please use the following: 
   <code>BED_MESH_PROFILE LOAD=default</code> > if you use a different naming convention for your printers config, please use that name instead.
 - Please find the profile I use in cura and feel free to import it: https://github.com/Eyreon/FLsun-V400/blob/main/Cura%20profile%20for%20PLA%20and%20PLA%2B.curaprofile I would like to thank @Amazon62 for sharing his work.



When you have done this you will probably have noticed that the time is wrong, for you to correct this you can follow another github by Guilouz, this will also offer you the option to go full vanilla Klipper and add some other features to the machine like an ADXL accelerometer.

Follow this link: https://github.com/Guilouz/Klipper-Flsun-Speeder-Pad


On to the fun stuff!
Some handy improvements for your V400 that will make this machine even better!

Some people that print high temp materials might want to build an enclosure, there are a few options here.
To reduce any cold drafts you can use side walls on 2/3 openings, you can find a nice setup for those here and thank you @JohnJacky for this awesome design.
https://www.printables.com/model/322917-flsun-v400-enclosure-cut-pla-version

If you want to go full enclosure you can add these doors designed and tested by the wonderful and talented @Amazon62 leave this guy a tip for his hardships!
https://www.printables.com/model/329660-flsun-v400-door-hinges-doors-updated/comments

If you decide to go for a full enclosure I would advice to do somethign about the ventilation of the printer, this will require some modding but is mandatory to avoid overheating of the motherboard.
https://www.printables.com/model/325471-flsun-v400-upper-plate-risers and https://www.printables.com/model/323798-flsun-v400-top-cover-cut-version again designed by the awesome @JohnJacky.


