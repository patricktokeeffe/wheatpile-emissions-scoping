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

## Documentation

* [Preparatory checklists](doc/prep.md)
* [Operating procedures](doc/usage.md)
* [Data product details](doc/data.md)
* [Initial setup notes](doc/setup.md)

## Data stuff

See [here](data/) for:

* Example plume calculations
* Validation test data & results
* Analyzer calibration audit data & results


## References

* Airmar Technology Corp. *PB100 WeatherStation Technical Manual.* Revision 1.007.
  Online: <http://www.airmartechnology.com/uploads/installguide/PB100TechnicalManual_rev1.007.pdf>

* Airmar Technology Corp. *Ultrasonic WeatherStation Instrument Owner's Guide &
  Installation Instructions.* Revision 2016 Jan 28.
  Online: <http://airmartechnology.com/uploads/InstallGuide/17-461-01.pdf>

* Alicat Scientific. *MC/MCD Mass Flow Controller Manual.* Rev 42, 2017 May 22.
  Online: <https://www.alicat.com/documents/manuals/Gas_Flow_Controller_Manual.pdf>

* Campbell Scientific, Inc. *CR1000 Measurement and Control System Operator's
  Manual.* Revision 2018 Feb. 
  Online: <https://s.campbellsci.com/documents/us/manuals/cr1000.pdf>

* Campbell Scientific, Inc. *CRBasic Program Reference: WindVector.* Version
  CR1000.Std.32. CRBasic Editor.

* Campbell Scientific, Inc. *CSAT3B Three-Dimensional Sonic Anemometer.* Revision
  2018 Mar. Online: <https://s.campbellsci.com/documents/us/manuals/csat3b.pdf>

* Campbell Scientific, Inc. *GPS16X-HVS GPS Receiver Instruction Manual.*
  Revision 2017 Oct. Online: <https://s.campbellsci.com/documents/us/manuals/gps16x-hvs.pdf>

* TSI Incorporated. *DustTrak II Aerosol Monitor Model 8530/8531/8532/8530EP
  Operation and Service Manual.* Revision P, 2017 Jan. Online:
  <http://www.tsi.com/uploadedFiles/_Site_Root/Products/Literature/Manuals/8530-8531-8532-DustTrak_II-6001893-web.pdf>

