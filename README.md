# ESP-01S-GPIO4
ESP-01S Non-Glitch modification for Driving Relay Modules.

This shows to properly modify an ESP-01S module such that when used with its associated single Relay module it prevents the relay activating during start up initialization.

The modification changes the function of header pin 4 from being being a module enable EN signal to being GPIO4 direct from the ESP8266 chip.

It requires cutting one track, one solder bridge, and soldering of a single wire link.

Underneath the PCB you need to cut a track in order to isolate the header pin 4 used for module enable (EN).

![BoardMod Bottom](https://github.com/user-attachments/assets/4f80f260-76f7-40ae-9664-03d4d01e21ea)

ON top of the PCB, put a big solder bridge between the leg of a capacitor and resistor.
You may want to use a hair wire to do the bridging but it is possible with a big solder blob.
(This bridge connects the ESP8266 EN signal to VCC).

Now connect the ESP8266 pin 16 (GPIO). (its the pin right on the corner of the IC) to the now isolated header pin 4.
Use a single strand from a piece of standard wire. Tin one end of that wire and very carefully attach it to pin 16.
Use minimal solder for this so that you don't acidentally solder bridge to the adjacent pin).
Then thread a small piece of insulation (stripped from a larger piece of solid core wire) over the strand.
Then wrap the strand around the base of header pin 4 and solder into place.

![BoardMod Top](https://github.com/user-attachments/assets/0d163eb5-c0b8-4b34-87c5-04ebe924fa2f)

For the relay module, you just need to cut a single track and reroute the relay drive signal from the GPIO0 header pin
to the new GPIO4 header pin (previously used for module EN).

Now for your Arduino code, simply change the relay output signal pin used from 0 (GPIO0) to 4 (GPIO4).

Now when powering up, (or when the module is reset), the relay no longer glitches during start up.
