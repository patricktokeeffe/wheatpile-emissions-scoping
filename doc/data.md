# Data Products

### Wheat pile dust emissions scoping study (spring 2018)

This document provides guidance for data handling.

## Data Retrieval

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


### Wind data: `*.tsfast.dat`

Primary data product.

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

### Trace gas data: `*.tsdata.dat`

Primary data product.

* Table name: tsdata
* Record interval: 1 second
* Aggregation: none; real-time measurements from CO2 analyzer & aerosol monitor

| Column name         | Units  | Description                    |
|---------------------|--------|--------------------------------|
| dusttrak2_analog_pm | mg/m^3 | aerosol concentration          |
| li840a_CO2          | ppm    | CO<sub>2</sub> mixing ratio    |
| li840a_H2O          | ppth   | H<sub>2</sub>O mixing ratio    |
| li840a_analog_CO2   | ppm    | CO<sub>2</sub> mixing ratio (analog data) |


### Aggregated data: `*.minutely.dat`

Complete data records from all analyzers, on a common time base. 

* Table name: minutely
* Record interval: 1 minute (closed left, labeled right &rarr; 10:25:00-10:25:59 is labeled 10:26:00)
* Aggregation: either average (Avg), median (Med), minimum (Min) or point-sample
  (Smp) as appropriate (*see 4th header row*)

| Column name          | Units | Description                    |
|----------------------|-------|--------------------------------|
| li840a_CO2           | ppm   | CO<sub>2</sub> mixing ratio    |
| li840a_H2O           | ppth  | H<sub>2</sub>O mixing ratio    |
| li840a_cell_T        | degC  | sample cell temperature        |
| li840a_cell_P        | kPa   | sample cell pressure           |
| li840a_dewpoint      | degC  | H<sub>2</sub>O dewpoint        |
| li840a_pwr_src       | Vdc   | power input                    |
| latitude_deg         | degreesN    | position latitude degrees component |
| latitude_min         | minutesN    | position latitude decimal minutes component |
| longitude_deg        | degreesE    | position longitude degrees component |
| longitude_min        | minutesE    | position longitude decimal minutes component |
| mag_variation        | degreesEofN | position magnetic variation |
| gps_ready            | unitless    | status indicator (10=ready) |
| csat3b_boardTemp     | degC        | sonic internal temperature  |
| csat3b_boardHumidity | %           | sonic internal humidity     |
| csat3b_inclinePitch  | degrees     | sonic pitch incline angle   |
| csat3b_inclineRoll   | degrees     | sonic roll incline angle    |
| csat3b_azimuth       | degreesEofN | sonic orientation wrt north |
| wnd_spd              | m/s         | mean horizontal wind speed  |
| rslt_wnd_spd         | m/s         | mean wind vector magnitude  |
| rslt_wnd_dir         | degreesEofN | resultant mean wind direction |
| std_wnd_dir          | degrees     | wind direction stdev per CSI algorithm |

