# gantrywarmer
The alu-steel combination in Ratrig vcore4 forms a bimetallic structure that bows because the hotend blows hot air at it. On a 400, the bow from 22 to 250 is about 180um on my printer. The proper way to fix this would be hardware changes, such as a different gantry material (titanium, steel) or changing the airflow (reversing the fan), or gantry heaters. Personally, fan reversal works wonders for me, the bow drops to less than 20um.

On-the-fly height measurement with beacon might be another way to compensate for the slow drift. That does not fix the root cause but lessens some effects especially on the first layer.

The gantry bow is different from hotend expansion. The time constants with hotend expansion seem relatively short, in the order of seconds, whereas the gantry bow is a slower process that starts within a few seconds but continues for tens of minutes.

The standard heatsoaking with the bed or enclosure heater does not add the hotend effect on the gantry, and thus is not effective to reduce this specific error. This software is a POC to study what the effect would be if the gantry was pre-heated / heat-soked by moving the head back&forth over the length of the gantry while keeping it as hot as is practical.

The code is nowhere near production quality. This is just POC meant for studying the phenomenon. It has only been tried&tested on PLA with cold bed, where it seems to produce reasonable first layers with a 0.3mm first layer height and a 0.4mm nozzle.

The macro "START_PRINT" is a modified version of the code in RatOS, see https://github.com/Rat-OS/RatOS

## Use
To use this routine, clone the repo wherever, and include the "printer.cfg" from that location. An example:

`[include local/gantrywarmer/printer.cfg]`

The path is relative to your "real" `printer.cfg` file. The include should be towards the end of your `printer.cfg` file, so that the values are not overriden.

To change the time or the Y postion of the soaking, edit the file `start_print.cfg`:
```	
#Customizations for POC
	{% set gantry_heat_soak_time = 1200 %}
	{% set gantry_heat_soak_Y = 410 %}
``` 

