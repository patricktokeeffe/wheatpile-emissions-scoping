# Operating Procedures

### Wheatpile Emissions Scoping Study

This document gives an overview of equipment operation; see also [Data Products](data.md).

## Getting Started

### Stationary (tracer release) site

1. Position things
    * CO<sub>2</sub> tank **must** be operated in the upright position &rarr;
      setup the large tripod and strap it upright using a tie-down strap
    * Anemometer mounting boom (1.5" OD pipe) can be attached to either
      the large steel tripod or portable plastic tripod using U-bolt crossbrace
    * GPS receiver has magnetic mounting plate
    * Cooler containing datalogger & analyzers can be placed up to
        * 20ft from the sonic anemometer or GPS (data cable limits)
        * 10ft from gas/aerosol inlet location *(can find longer tubing, but
          would need to evaluate lag time and pump flow rates)*
2. Connect monitoring things
    1. Anemometer data cable **to** *SDM/Power* port on sensor head
    2. Teflon (gas) inlet tube **to** orange friction fitting on CO2
       analyzer inlet
    3. Conductive rubber (aerosol) inlet tube **to** DustTrak impactor
       (requires short length of smaller tubing used as a reducer fitting)
    4. Logger enclosure power cord **to** generator via
       extension cord
3. Connect CO<sub>2</sub> release things
    1. CO<sub>2</sub> tank **to** regulator (*don't forget the washer!*)
    2. Regulator **to** mass flow controller (10ft PFA tubing w/ double fittings)
    3. Mass flow controller **to** release tubing (20ft PFA tubing w/ single fitting)
4. Turn things on:
    1. Power strip in enclosure (bottom of cooler)
    2. Gas analyzer pump (right-side black plastic box)
    3. Aerosol monitor (DustTrak turns on automatically)
    4. Mass flow controller (automatic w/ power, 24Vdc)
5. Validate things
    1. Review DustTrak settings/performance:
        * analog output range 0-1.000 mg/^3 over 0-5V?
        * clock approximately matches logger (Pacific Daylight Time, Z-0700)?
        * flow rate is 3.0 LPM, even with extended inlet line?
        * evaluate background offset using inline zero filter
    2. Review values on logger keyboard display:
        * Does reported aerosol concentration match DustTrak? (only valid when
          DustTrak is conducting sample)
        * Does CO2 concentration make sense? (Is pump running?)
        * Are WS/WD reasonable? &rarr; use keyboard display to enter new value
          for sonic azimuth (changes are saved automatically)
    3. Program the flow controller for release settings ([see below](#setting-mfc-flow))


### Mobile (plume monitoring site)

1. Position things
    * blue enclosure can go in a vehicle or on the ground &rarr; it requires
      vehicle for power source (via 12V inverter) or a very long extension cord
      to plug directly into generator instead
    * it is *not* possible to adjust the height of the inlets or weather
      station (sorry)
2. Connect things
    1. Mast for weather station **to** gas inlet mast (data cable permanently
       routed inside PVC pipes)
    2. Weather station **to** weather station data cable
    3. Power cord **to** 12V inverter (or generator)
3. Turn things on:
    1. Power strip in enclosure (back bottom)
    2. Verify gas analyzer pump (left wall) is running
    3. Verify DustTrak II turned on automatically
    4. Verify logger has power, is running
4. Validate things
    1. Review DustTrak settings/performance:
        * analog output range 0-1.000 mg/^3 over 0-5V?
        * clock approximately matches logger (Pacific Daylight Time, Z-0700)?
        * flow rate is 3.0 LPM, even with extended inlet line?
        * evaluate background offset using inline zero filter
    a. Review values on logger keyboard display:
        * Does reported aerosol concentration match DustTrak? (only valid when
          DustTrak is conducting sample)
        * Does CO2 concentration make sense? (Is pump running?)
        * Are WS/WD reasonable? (requires GPS lock, which could take several
          minutes to acquire)

## Operations

### Setting tracer release flow <a name="setting-mfc-flow"/>

> Excerpted from the MFC user manual [listed here](../README.md#references):

Use the keyboard display on the mass flow controller to specify the desired
flow rate. Press <kbd>SETPT</kbd>, then use <kbd>SELECT</kbd> to choose the
decimal with the arrow and the <kbd>UP</kbd> and <kbd>DOWN</kbd> buttons to
change the value. Press <kbd>SET</kbd> to record your value. Press 
<kbd>CLEAR</kbd> to return to zero.
    
### Monitoring data

> See also the CR1000 user manual [listed here](../README.md#references).

Use the keyboard display attached to each logger to review current data values.
Scalars of interest (CO<sub>2</sub>, PM, and WS/WD) are shown directly on the
primary screen; additional values can be reviewed using standard methods. 


### Other Notes

* Starting the vehicle cuts the inverter's output and causes the DustTrak and
  logger to restart. However, if the DustTrak is sampling when this occurs, it
  will automatically recover back into sampling mode. The logger automatically
  recovers too.



