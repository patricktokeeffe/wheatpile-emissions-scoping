# Wheatpile Emissions Scoping Study

Source code and documentation for wheat pile emission study scoping hardware.
There are two main components:

* A stationary site located upwind with
    * Fine aerosol (PM<sub>2.5</sub>) monitor ([DustTrak 8530; TSI](http://www.tsi.com/DUSTTRAK-II-Aerosol-Monitor-8530/))
    * Carbon dioxide (CO<sub>2</sub>) analyzer ([LI-840A; LICOR Biosciences](https://www.licor.com/env/products/gas_analysis/LI-840A/))
    * 3D ultrasonic anemometer ([CSAT3B; Campbell Scientific](https://www.campbellsci.com/csat3b))
    * GPS receiver ([GPS16X-HVS; Garmin](https://www.campbellsci.com/gps16x-hvs))
    * Regulated point-release of CO<sub>2</sub> via multiple mass flow controllers ([Alicat brand](https://www.alicat.com/product/gas-mass-flow-controllers/))
* A mobile station with
    * Fine aerosol (PM<sub>2.5</sub>) monitor ([DustTrak 8530; TSI](http://www.tsi.com/DUSTTRAK-II-Aerosol-Monitor-8530/))
    * Carbon dioxide (CO<sub>2</sub>) analyzer ([LI-840A; LICOR Biosciences](https://www.licor.com/env/products/gas_analysis/LI-840A/))
    * Compact weather station (T/RH/DP/P/WS/WD) with integral GPS ([150WX; Airmar Technologies](http://www.airmartechnology.com/productdescription.html?id=155))

Programmable dataloggers ([CR1000; Campbell Scientific](http://www.campbellsci.com/cr1000))
acquire and store data to internal memory media. Raw measurements are stored on
their acquisition time base (10Hz for sonic data, 1Hz otherwise) and aggregated
to 1-min values. Data is retained to CompactFlash memory; there is no telemetry
component.


## Quick Start

**TODO**

### Tracer release station

* Setup the monitoring tripod (short plastic gray & black tripod)
    * Attach sonic anemometer to 1.5" cross arm and connect data cable
    * Attach 10ft black aerosol tube to DustTrak inlet 
    * Attach 10ft PFA gas tube to orange coupler on CO2 analyzer inlet
* Setup the instrument enclosure (blue cooler)
    * Connect power strip to extension cord (from generator)
    * Connect data cable to sonic anemometer
    * Place GPS receiver on gray magnetic mounting plate
* Setup the release station (large stainless steel tripod)
    * Strap CO2 release tanks upright against tripod mast
    * Install CO2 tank regulators
        * **TODO** add heat tape notes
    * Use ~12ft coupler tubes to connect regulators to associated flow controller:
      small one for 20 SLPM, large one for 50 SLPM (mismatch may cause freeze-up)
    * Connect ~8ft leader tubes to flow controller outlets

### Plume monitoring station

* Enclosure goes in flatbed pickup with ext cord to inverter
* Inverter goes inside vehicle, using 12V accessory port

> Starting the vehicle will cut inverter output and cause the DustTrak and
> logger to restart. If the DustTrak is sampling when this occurs, it will
> automatically recover back into sampling mode.


## Data Products 

[See here](doc/data.md) for data product specifications.


## Prep checklists

### Scouting visit prep

* [x] prep both DustTrak II units w/ PM<sub>2.5</sub> & PM<sub>10</sub> inlets
* [x] verify Kestrel weather meter working OK, print user manual

### Data systems

#### Tracer release station

CO2 (tracer) point-source release equipment

* [x] pure CO2 tanks *ordered (4) 50# tanks*
* [x] regulator *order one new, other from IAQ*
    * [x] test for regulator freeze-up *does frost over but direct sunlight is
          sufficient to prevent freezing; tested up to full range 20+50 SLPM*
    * [ ] install heat tape on new regulator
* [x] digital flowmeter *one 50SLPM from 415, other 20LPM from IAQ*
* [x] DustTrak II w/ PM2.5 inlet *unit #1 (s/n 8530150710)*
    * [ ] verify logger program has correct det. scaling from IAQ study
* [x] Licor LI-840A CO2/H2O analyzer + pump *unit #2 (s/n HGA-2573)
    * [x] validate analog voltage scaling range
    * [x] add backup analog measurement CO2 only
* [x] GPS unit (*s/n 1A4171474*)
    * [x] verify programmed for use with CR1000
* [ ] Campbellsci datalogger *s/n 50905*
    * [x] check for latest firmware *32.02*
    * [ ] replace lithium battery (is below 3V)
    * [ ] finish program
* [ ] extension cord & power strip
* [x] small Honda generator *bought Honda EU2200 generator*
    * [ ] test operation

#### Plume monitoring vehicle

Probably an open-bed pick-up.. except motor pool only has those in towing size.

* [x] DustTrak II w/ PM2.5 inlet *unit #2 (s/n 8530152108)*
    * [x] verify logger program has correct det. scaling from IAQ study
    * [x] needs internal battery back from unit #1
* [x] Licor LI-840A CO2/H2O analyzer + pump *unit #1 (s/n HGA-1666)*
    * [x] validate analog voltage scaling range *set to 0-2500ppm/0-5V*
    * [x] add backup analog measurement CO2 only
* [x] Airmar unit for WX+GPS *150WX from IAQ*
    * [x] verify NMEA sentence config
* [x] Campbellsci datalogger *s/n 67138*
    * [x] check for latest firmware *32.02*
    * [ ] finish program
* [x] cigarette-lighter inverter *black 400W unit*
    * [x] verify operates OK on internal DC socket
* [x] road worthy enclosure that sufficiently elevates inlets and is securable to vehicle

### Logger program

* [ ] incorporate DustTrak analog scaling from IAQ


## Initial Setup Notes

### Wiring

See this [Word document](wiring.docx). *Sorry, it's a .docx because we can edit
it, print it neatly, and still get basic diffs.*

### Instrument Configuration

#### LI-840A

The logger program sends a configuration command at start-up which enables the 
correct settings for serial communication with the analyzer.

Additionally, use the [manufacturer software](https://www.licor.com/env/products/gas_analysis/LI-840A/software.html)
to configure the *DAC Output* to 5V range and *DAC 1 Source* to *CO2* (0-2500 ppm).

#### 150WX

Use [Airmar WeatherCaster](http://www.airmartechnology.com/software-downloads.html)
to disable all NMEA0183 sentences *except* `WIMDA` and `GPRMC`. Keep the
default 1Hz (`0:01.00`) interval.

#### GPS16X-HVS

If necessary, use `SNSRXCFG_270.exe` (available upon request from lab tech) to
configure the GPS receiver as detailed in *Appendix A. Changing GPS16X-HVS
Settings*.


## References

* Campbell Scientific, Inc. *CR1000 Measurement and Control System Operator's
  Manual.* Revision 2018 Feb. 
  Online: <https://s.campbellsci.com/documents/us/manuals/cr1000.pdf>

* Campbell Scientific, Inc. *CRBasic Program Reference: WindVector.* Version
  CR1000.Std.32. CRBasic Editor.

* Campbell Scientific, Inc. *CSAT3B Three-Dimensional Sonic Anemometer.* Revision
  2018 Mar. Online: <https://s.campbellsci.com/documents/us/manuals/csat3b.pdf>

* Campbell Scientific, Inc. *GPS16X-HVS GPS Receiver Instruction Manual.*
  Revision 2017 Oct. Online: <https://s.campbellsci.com/documents/us/manuals/gps16x-hvs.pdf>

* Airmar Technology Corp. *PB100 WeatherStation Technical Manual.* Revision 1.007.
  Online: <http://www.airmartechnology.com/uploads/installguide/PB100TechnicalManual_rev1.007.pdf>

* Airmar Technology Corp. *Ultrasonic WeatherStation Instrument Owner's Guide &
  Installation Instructions.* Revision 2016 Jan 28.
  Online: <http://airmartechnology.com/uploads/InstallGuide/17-461-01.pdf>

