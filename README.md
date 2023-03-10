![image](https://user-images.githubusercontent.com/44564923/213299517-0aafb2f5-020b-4a4b-a91f-2f02d9a7c2b8.png)
# FLsun-V400 new user guide.
Everything you need to know as a new V400 owner for quality prints.

Now this is not a guaranteed method but it covers most of the issues out there and staying close to FlSun stock as much as possible, nor will this talk about what happens with a lack of maintenance.

There have been many topics and posts around a few common shortcomings of this machine.
To adress these I would like to create knowledgebase and get all the printers out there to work as they should.
My writing will assume you have an inkling of an idea of the workings of both Cura and 3d printing,
additionally I will add useful links to builds for the printer and advanced user posts.

# some facts and misconceptions:

 - Out of the box the printer is solid hardware wise, you might need to spend some time on belt tuning but other than that its fine.
 - Eventually you might get sick of the bed and want to get an upgrade.
 - The stock slicer profile isn't bad but there are better profiles as this document will point out.
 - Marketing states 400mm/s, in reality you never really get these speeds and if you do the quality will drop depending on model, there are mechanical laws we cannot cross or things will break.


# Some of the common issues out there:

- The white stuff at the nozzle? > This is a silicone glue to keep the sock on the heatblock and nothing to worry about.
-  Nozzle dragging > This is one of the biggest frustrations to users out there and it seems to revolve around proper calibration and software setting.
For the sake of simplicity I will only use CURA (5.1 at this time) as a reference.
- Top layer quality > this one is a direct connection to the above and will resolve itself with the following steps.
- Belt tension, there are many different opinions around this one, but there is an option to set them all equally.
- Layer shifts, mostly belt and speed related.
- "Why can't I SSH login with flsun user and password", this one is mentioned further down, when we talk flashing the FLSun stock 'open image'.
- Poor bed adhesion after a short time.


# First steps:

When you set up your printer you will probably have noticed that the time is set wrong, to correct this you can follow another github by Guilouz, this will also offer you the option to go full vanilla Klipper and add some other features to the machine like an ADXL accelerometer.
Follow this link: https://github.com/Guilouz/Klipper-Flsun-Speeder-Pad

Lets start with using the FLSUN recovery image that enables SSH and access to the printers firmware.
The image can be found here: https://flsun3d.com/pages/speeder-pad > Select V400, then put it on a microSDcard using Belena etcher or some other tool as described in above guide.


# calibration:

This will be your bread and butter!
The printers probing is a bit flawed in the stock state so we'll want to edit printer.CFG to resolve this.
This is why we set up the recovery image earlier so we can SSL to the speederpad.

 - Make sure to probe with your bed heated at the temperature you will mostly print at and let it soak for about 15 minutes.
 - Change the bed mesh to 9x9 in the config.
 - Change the bed mesh points to 5 from 3. The first point that this sensor takes is always wrong.

 - Probe and Z-offset calibration: https://www.klipper3d.org/Probe_Calibrate.html
 - Delta calibration: https://www.klipper3d.org/Delta_Calibrate.html
 - Belt tuning: follow this great video that explains everything! https://www.youtube.com/watch?v=DR-R_uKlo0A > printable tool found here > https://drive.google.com/drive/folders/1cPqHoQqRYM4s4bfQF_XUy9ShHSPXlSST

# Slicer settings: 

 - Add the following line in Cura at the start GCODE after G28 to actually load the bed mesh for the print, please use the following: 
   <code>BED_MESH_PROFILE LOAD=default</code> > if you use a different naming convention for your printers config, please use that name instead.
 - Please find the profile I use in cura and feel free to import it: https://github.com/Eyreon/FLsun-V400/blob/main/Cura%20profile%20for%20PLA%20and%20PLA%2B.curaprofile I would like to thank @Amazon62 for sharing his work.
 - For nozzle dragging the main advice is to use gyroid infill, 15% for small prints and 25% for large print for a smooth top surface, Delta's don't do well with regular infill due to the way the effector moves.
 - In some cases a z-hop of .5/.8 mm is advised however the profile I use does not require this and creates quality prints.
 - A great print tuning guide here: https://ellis3dp.com/Print-Tuning-Guide/

 - If you've tried everything else and don't get consistent quality, consider a Bondtech CHT 0.4mm or 0.6mm nozzle instead. If you go for a larger nozzle, you will need to adjust pressure advance with a pressure advance tower and potentially  the main change in the slicer is the "line width" to something in the 0.5 to 0.62 range, though you also increase your layer heights for faster prints and thicker layer lines as well. You may also need to change your flow rate as well.


# Filament:

Forget all you know about filament from your old printer, the V400 is fast so it eats through spindles like crazy.
Due to the above you need to set temperature and flow accordingly, having said this I strongly urge you to print temperature towers and flow towers, only then will you be able to determine the right settings for your filament.

# Bed adhesion:

 - After some time this could be a thing for some of users, to counter this: 
   Mix a Light amount of dish soap with warm water and scrub the surface wit a rough sponge perhaps following with alcohol, this should remove any debris and some grease that got stuck on the surface. 

 - The bed temperature is usually 3-5 degrees below what Klipper shows, so consider slightly bumping the bed temp up by about 5 degrees if you are still getting poor adhesion - an entered value of 65C seems to work pretty well

  - Adding that pressure advance calibration is one of the most important ones to do and it's fairly straightforward and can fix ringing and odd looking corners on prints. I believe the stock value is 0.02 if you ever want to go back to it after messing with it.

# Advanced users:

Dan Nault has graced us with a complete re-work of stock image on the V400.
His work is recorded over at his Gtihub and you might want to dig in to it if you make detailed prints.
Find his repo here: https://github.com/danorder/OEM-VANILLA-V400-Klipper-


# The good stuff:

Some handy improvements for your V400 that will make this machine even better!

Some people that print high temp materials might want to build an enclosure, there are a few options here.
To reduce any cold drafts you can use side walls on 2/3 openings, you can find a nice setup for those here and thank you @JohnJacky for this awesome design.
https://www.printables.com/model/322917-flsun-v400-enclosure-cut-pla-version

If you want to go full enclosure you can add these doors designed and tested by the wonderful and talented @Amazon62 leave this guy a tip for his hardships!
https://www.printables.com/model/329660-flsun-v400-door-hinges-doors-updated/comments

If you decide to go for a full enclosure I would advice to do something about the ventilation of the printer, this will require some modding but is mandatory to avoid overheating of the motherboard.
https://www.printables.com/model/325471-flsun-v400-upper-plate-risers and https://www.printables.com/model/323798-flsun-v400-top-cover-cut-version again designed by the awesome @JohnJacky.

If you get sick of the textured bed there are other options out there from a high quality product from China (YES ITS TRUE!) to the good old whambam plates for V400.
Chinese quality plate found here: https://fr.aliexpress.com/item/1005004704770888.html?spm=a2g0o.order_list.order_list_main.5.21ef5e5bA4ru9y&gatewayAdapt=glo2fra&fbclid=IwAR181Uo8kQeK4by4LinQ7yQvpdIrPIqmV8EYL6W-IN-1eDoofl2kJ5Zf55A

For better overhangs there is an improved fanduct out there, if you own a resin printer use that to print these: https://www.printables.com/model/291550-flsun-v400-improved-fanduct/files?fbclid=IwAR3GSVYO-2vj4ZLZz9CZFkRwCVIPRUOB_Ve5Hu148csf0PxKwyvwWEzRPyk


# Special thanks go to the following people:

- Amazon62 for the door design and testing, support him here: https://www.printables.com/social/308844-amazon62/about
- @Johnjacky for the enclosure panels and risers, support him here: https://www.printables.com/social/346712-johnjacky/about
- @Dennis G. Gignac for making a great tutorial on belt tensioning.
- A special thanks to @danorder for completely tuning this machine for crazy detail: https://github.com/danorder
- Thanks for the work on the guide to get the stock image up to vanilla Klipper: https://github.com/Guilouz/Klipper-Flsun-Speeder-Pad
