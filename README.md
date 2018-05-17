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
to 1-min values. Data is only retained in logger memory; there is no telemetry
component.


## Quick Start

**TODO**


## Data Products 

**TODO**


## Prep checklists

### Scouting visit prep

* [x] prep DustTrak II w/ PM 2.5 inlet, extra battery
* [x] verify Kestrel weather meter working OK, print user manual

### Data systems

#### Stationary site

CO2 (tracer) point-source release equipment

* [x] ~~pure CO2 tanks~~ *ordered (4) 50# tanks*
* [x] regulator *possibly two*
* [ ] digital flowmeter *possibly two*
* [x] ~~DustTrak II w/ PM2.5 inlet~~ *unit #1*
* [ ] Licor LI-840A CO2/H2O analyzer + pump
* [ ] Campbellsci datalogger
    * [ ] check for latest firmware *32.02*
    * [ ] load program
* [ ] extension cord & power strip
* [ ] small Honda generator *order or buy?*

#### Plume monitoring vehicle

Probably an open-bed pick-up.. except motor pool only has those in towing size.

* [x] ~~DustTrak II w/ PM2.5 inlet~~ *unit #2*
    * [ ] needs internal battery back from unit #1
* [ ] Licor LI-840A CO2/H2O analyzer + pump
* [ ] Airmar unit for WX+GPS
* [x] Campbellsci datalogger *s/n 50905*
    * [x] check for latest firmware *32.02*
    * [ ] load program
* [x] cigarette-lighter inverter
    * [ ] verify operates OK on internal DC socket
* [x] road worthy enclosure that sufficiently elevates inlets and is securable to vehicle


