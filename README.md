DeltaPVOutput
=============
A series of python scripts to use RS485 Serial from Delta G4 Inverter to PVOutput.org, and upload data to pvoutput.org

Hardware setup
==============
USB-RS485 modem
---------------
You need a RS485-USB modem like this one, which costs from about USD 2.50 and upwards.
This one works fine http://www.ebay.com/itm/USB-to-RS485-485-Converter-Adapter-ch340T-chip-Support-32-64-XP-Win7-Vista-/360615203160?pt=LH_DefaultDomain_0&hash=item53f6575158
Be aware it takes a couple of weeks to ship from China.

Cable
-----
Then you need a cable to connect your inverter with the USB-modem. Any normal network cable should work - if long distances, make sure your cable is a twisted pair (i.e. the normal round network cables)
This cable works:
![alt text](https://github.com/rsltrifork/DeltaPVOutput/raw/master/Cabel.jpg)
However, for long distances, you should use a round network cable, and instead of connecting wire 6 and 7, you should connect wire 7 and 8 (which are a twisted pair). On my inverter both 6,7 and 7,8 work.

Connecting Multiple Inverters
----------------------------
Just insert an normal, unmodified network cable connecting the inverters RS485 ports. No need for RS485 termination.
Set a unique RS485 ID for each inverter by using the buttons on the inverter. Preferably start with 1 and count upwards.

Machine
-------
I use a raspberry PI to run the program connected to my home network with a USB wifi dongle. It was amazingly easy to setup and came with drivers for both WIFI dongle and the USB-RS485 out of the box, when using the default "Wheezy" image.


Software setup
==============
Edit config file
-------------
Edit config.py, and insert your RS485 ID(s), so they match what is setup in your converters.
Edit config.py systemID(s) and API Key so they maych your account settings at pvoutput.org. Signing up is free.
Check connection
-------------
Check that you can connect by running:
python power-now.py

`python power-now.py
1: AC Power: 1203 W
2: AC Power: 1573 W
Total: AC Power: 2776 W

1: DC Power: 1250 W
2: DC Power: 1612 W
Total: DC Power: 2862 W`

Crontab
-------
You want to run DeltaPVOutput.py every 5 minutes to send data to pvoutput.org
type:
`crontab -e`

Enter this line:
`*/5 * * * * /home/pi/DeltaPVOutput/run.sh > /tmp/log.txt 2>&1`

Where `/home/pi/DeltaPVOutput/run.sh` is the path you have installed the scripts in.

Only thing left to do is lean back, and see the nice graphs on pvoutput.org while cursing the clouds!

Disclaimer
==========
The authors of this software and guide take no responsibility of how it works. It's purely for educational purposes.
The code may or may not work with different inverter models/firmware versions than the one it was created for.
Different versions of the Solivia inverter support different commands. A command from one inverter version may be
interpreted as something completely different in another version, potentially updating the inverter configuration,
leading to misconfiguration or possibly worse.
Using this software is your responsibility entirely.
