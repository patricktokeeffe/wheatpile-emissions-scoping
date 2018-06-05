# Data Product Details

### Wheatpile Emissions Scoping Study

This document provides guidance for data handling; see also [Operating Procedures](sop.md).

## Data Retrieval


### TSI DustTrak

> Refer to the DustTrak user manual [listed here](../README.md#references).

Data files are stored to internal memory and may be retrieved with a USB flash
memory card via the *Data* submenu. The files are written to a folder with the
unit's serial number. The labels on each unit are:

| Location                   | DustTrak unit      |
|----------------------------|--------------------|
| stationary (release) site  | #1, s/n 8530150710 |
| mobile (monitoring) site   | #2, s/n 8530152108 |


### CR1000 Datalogger

> Refer to the CR1000 user manual [listed here](../README.md#references).

Data files are written to CompactFlash media. To safely retrieve the memory card:
1. Locate the card holder on the right-hand side of the logger
2. Press the large white *Eject* button
3. Wait until the solid green light indicates all data is written to card
4. Open the lid and press to eject

Use a USB memory card adapter to retrieve files from the memory card. Files are
stored in a binary format ("TOB3") and must be converted to plain-text ("TOA5")
using CardConvert. The CardConvert utility is included with all Campbell software 
packages, including the no-cost [PC200W](https://www.campbellsci.com/pc200w).

> Refer to the CardConvert user documentation for file conversion instructions.

Recommended destination file options:
* File format: *ASCII Table Data (TOA5)*
* File Processing
    * [ ] Use Filemarks
    * [ ] Use Removemarks
    * [ ] Use Time
    * [ ] Convert Only New Data
* File Naming
    * [x] **TimeDate Filenames**
        * [ ] Use Day of Year
    * [ ] Create New Filenames
    * [ ] Append to Last File
* TOA5-TOB1 Format
    * [x] **Store Record Numbers**
    * [x] **Store TimeStamp**
    * [ ] Midnight is 2400

## Importing Data Files

Data files are in the "TOA5" format (Campbell Scientific), a multi-header
comma-separated values file. If you use the excellent
[pandas](http://pandas.pydata.org) Python library, try this:

```python
import pandas as pd

df = pd.read_csv('/path/to/data/file.dat',
                 index_col=0, # timestamps in first column
                 parse_dates=True, # iso8601
                 header=1, # 1st line metadata 2nd headers
                 skiprows=[2,3], # 3rd units 4th agg type
                 # Table 129 (p484) in CR1000 manual rev. 4/13/15
                 # https://s.campbellsci.com/documents/us/manuals/cr1000.pdf
                 na_values=['NAN', -7999, 7999], keep_default_na=False)
```

You can also open files with Microsoft Excel&trade; and use *Text-to-columns*
with a *comma* separator, but you'll probably want a real data reduction 
solution to process the 10hz data files.

## Table Definitions

Data is recorded in Pacific Daylight Time (Z-0700).

| Column prefix | Instrument description   |
|---------------|--------------------------|
| csat3b_*      | 3D ultrasonic anemometer ([CSAT3B; Campbell Scientific](https://www.campbellsci.com/csat3b)) |
| dusttrak2_*   | Fine aerosol (PM<sub>2.5</sub>) monitor ([DustTrak 8530; TSI](http://www.tsi.com/DUSTTRAK-II-Aerosol-Monitor-8530/)) |
| li840a_*      | Carbon dioxide (CO<sub>2</sub>) analyzer ([LI-840A; LICOR Biosciences](https://www.licor.com/env/products/gas_analysis/LI-840A/)) |
| gps_*         | GPS receiver ([GPS16X-HVS; Garmin](https://www.campbellsci.com/gps16x-hvs)) |
| m150wx_*      | Compact weather station (T/RH/DP/P/WS/WD) with integral GPS ([150WX; Airmar Technologies](http://www.airmartechnology.com/productdescription.html?id=155)) |


### Stationary (release) site

These files can be identified by the text "`CPU:tracer-stationary.cr1`" in the
first header line.

#### Turbulence data: `*.tsfast.dat`

Primary data product (1/2).

* Table name: tsfast
* Record interval: 100 milliseconds
* Aggregation: none; real-time measurements from ultrasonic anemometer

| Column name       | Units | Description                                  |
|-------------------|-------|----------------------------------------------|
| csat3b_Ux         | m/s   | wind vector streamwise component, into array |
| csat3b_Uy         | m/s   | wind vector horizontal crosswise component   |
| csat3b_Uz         | m/s   | wind vector vertical component               |
| csat3b_sonicTemp  | degC  | ultrasonic (virtual) temperature             |
| csat3b_diag       | arb   | sensor diagnostic word                       |

#### Gas & aerosol data: `*.tsdata.dat`

Primary data product (2/2).

* Table name: tsdata
* Record interval: 1 second
* Aggregation: none; real-time measurements from CO2 analyzer & aerosol monitor

| Column name         | Units  | Description                    |
|---------------------|--------|--------------------------------|
| dusttrak2_analog_pm | mg/m^3 | aerosol concentration          |
| li840a_CO2          | ppm    | CO<sub>2</sub> mixing ratio    |
| li840a_H2O          | ppth   | H<sub>2</sub>O mixing ratio    |
| li840a_analog_CO2   | ppm    | CO<sub>2</sub> mixing ratio (analog data) |
| instant_WS          | m/s    | instantaneous horizontal wind speed |
| instant_WD          | degreesEofN | instantaneous wind direction   |


#### Aggregated data: `*.minutely.dat`

Complete data records from all analyzers and the GPS, on a common time base. 

* Table name: minutely
* Record interval: 1 minute (closed left, labeled right &rarr; 10:25:00-10:25:59 is labeled 10:26:00)
* Aggregation: either average (Avg), median (Med), minimum (Min) or point-sample
  (Smp) as appropriate (*see 4th header row*)

| Column name          | Units  | Description                   |
|----------------------|--------|-------------------------------|
| dusttrak2_analog_pm  | mg/m^3 | aerosol concentration         |
| li840a_CO2           | ppm    | CO<sub>2</sub> mixing ratio   |
| li840a_H2O           | ppth   | H<sub>2</sub>O mixing ratio   |
| li840a_cell_T        | degC   | sample cell temperature       |
| li840a_cell_P        | kPa    | sample cell pressure          |
| li840a_dewpoint      | degC   | H<sub>2</sub>O dewpoint       |
| li840a_pwr_src       | Vdc    | power input                   |
| gps_latitude_deg     | degreesN    | position latitude degrees component |
| gps_latitude_min     | minutesN    | position latitude decimal minutes component |
| gps_longitude_deg    | degreesE    | position longitude degrees component |
| gps_longitude_min    | minutesE    | position longitude decimal minutes component |
| gps_mag_variation    | degreesEofN | position magnetic variation |
| gps_ready            | unitless    | status indicator (10=ready) |
| csat3b_boardTemp     | degC        | sonic internal temperature  |
| csat3b_boardHumidity | %           | sonic internal humidity     |
| csat3b_inclinePitch  | degrees     | sonic pitch incline angle   |
| csat3b_inclineRoll   | degrees     | sonic roll incline angle    |
| csat3b_azimuth       | degreesEofN | sonic orientation wrt north |
| csat3b_wnd_spd       | m/s         | mean horizontal wind speed  |
| csat3b_rslt_wnd_spd  | m/s         | mean wind vector magnitude  |
| csat3b_rslt_wnd_dir  | degreesEofN | resultant mean wind direction |
| csat3b_std_wnd_dir   | degrees     | wind direction stdev per CSI algorithm |
| li840a_analog_CO2    | ppm         | CO<sub>2</sub> mixing ratio (analog data) |


### Mobile (plume monitoring) site

These files can be identified by the text "`CPU:tracer-mobile.cr1`" in the
first header line.

#### Gas, aerosol & position data: `*.tsdata.dat`

Primary data product.

* Table name: tsdata
* Record interval: 1 second
* Aggregation: none

| Column name          | Units  | Description                    |
|----------------------|--------|--------------------------------|
| dusttrak2_analog_pm  | mg/m^3 | aerosol concentration          |
| li840a_CO2           | ppm    | CO<sub>2</sub> mixing ratio    |
| li840a_H2O           | ppth   | H<sub>2</sub>O mixing ratio    |
| m150wx_P             | hPa    | barometric pressure            |
| m150wx_T             | degC   | ambient temperature            |
| m150wx_RH            | %      | relative humidity              |
| m150wx_DP            | degC   | dewpoint                       |
| m150wx_WS            | m/s    | wind speed                     |
| m150wx_WD            | degTN  | degrees East of True North     |
| m150wx_WD_mag        | degMN  | degrees East of Magnetic North |
| m150wx_latitude_deg  | degreesN | position latitude degrees component  |
| m150wx_latitude_min  | degreesN | position latitude minutes component  |
| m150wx_longitude_deg | degreesE | position longitude degrees component |
| m150wx_longitude_min | degreesE | position longitude minutes component |
| m150wx_mag_variaton  | degEofTN | position magnetic variation          |
| m150wx_gps_mode      | -        | status indicator (see manual)        |
| li840a_analog_CO2    | ppm      | CO<sub>2</sub> mixing ratio (analog data) |


#### Aggregated data: `*.minutely.dat`

Complete data records from all analyzers and the GPS, on a common time base. 

* Table name: minutely
* Record interval: 1 minute (closed left, labeled right &rarr; 10:25:00-10:25:59 is labeled 10:26:00)
* Aggregation: either average (Avg), median (Med) or point-sample
  (Smp) as appropriate (*see 4th header row*)

| Column name          | Units | Description                    |
|----------------------|-------|--------------------------------|
| dusttrak2_analog_pm  | mg/m^3 | aerosol concentration         |
| li840a_CO2           | ppm   | CO<sub>2</sub> mixing ratio    |
| li840a_H2O           | ppth  | H<sub>2</sub>O mixing ratio    |
| li840a_cell_T        | degC  | sample cell temperature        |
| li840a_cell_P        | kPa   | sample cell pressure           |
| li840a_dewpoint      | degC  | H<sub>2</sub>O dewpoint        |
| li840a_pwr_src       | Vdc   | power input                    |
| m150wx_P             | hPa    | barometric pressure            |
| m150wx_T             | degC   | ambient temperature            |
| m150wx_RH            | %      | relative humidity              |
| m150wx_DP            | degC   | dewpoint                       |
| m150wx_WS            | m/s    | wind speed                     |
| m150wx_WD            | degTN  | degrees East of True North     |
| m150wx_WD_mag        | degMN  | degrees East of Magnetic North |
| li840a_analog_CO2    | ppm      | CO<sub>2</sub> mixing ratio (analog data) |


