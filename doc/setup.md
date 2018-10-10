# Initial Setup Notes

## Wheatpile emissions scoping study (spring 2018)

### Wiring

See this [Word document](../wiring.docx). *Sorry, it's a .docx because we can edit
it, print it neatly, and still get basic diffs.*

### Instrument Configuration

#### DustTrak II

The logger program expects the following configuration for the analog output
data channel: 0-1.0 mg/m<sup>3</sup> *over* 0-5000mV. 

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
