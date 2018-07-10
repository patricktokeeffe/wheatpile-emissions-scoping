# Data sets

### Plume dispersion calculations

An [Excel&trade; workbook](GaussCalcs_CO2.xlsx) put together by Dr. Brian Lamb
for estimating required point-source tracer delivery rates to attain meaningful
concentration differences. 


### 2018 June 5

Combined CO2/PM tracer release test, Paccar ETB roof top. Collected data has
not been adjusted for analyzer calibration discrepancies since unit #1 had to 
be swapped out with a new unit, #3 (it began reporting erratic, unexplainable 
values).

* [Collected data (.zip)](20180605_roof_test/20180605_roof_test.zip)
* [Data summary (.xlsx)](20180605_roof_test/20180605_roof_test.xlsx)

The downwind gas analyzer was located ~10 meters (6-7 paces) from the point
release of CO<sub>2</sub>. Winds were consistently from the East. Upwind sonic
anemometer and gas analyzer were located almost 3 meters from the point
release source.

![Students conducting simultaneous aerosol point release; instrumentation
visible in the background](20180605_roof_test/IMG_20180605_133234.jpg)

We were able to observe the plume from ~10 meters (6-7 paces):

![Observed CO2 tracer plume](20180605_roof_test/xy_wd_co2.png)

Some additional time-series plots:

![Time series of PM2.5 concentration](20180605_roof_test/ts_pm25.png)

![Time series of CO2 concentration](20180605_roof_test/ts_co2.png)

![Time series of difference in CO2 concentration](20180605_roof_test/ts_deltaco2.png)

![Time series of wind direction](20180605_roof_test/ts_wd.png)

#### Notes on wind direction

##### Airmar compass declination

In general, the "mobile suite" compact weather station (Airmar 150WX) produces
better wind direction data with respect to magnetic north. The electronic
compass used to output True North-corrected wind direction data is subject to
local noise and is less reliable than using a current, site-specific, but 
constant declination value. 

Observe the small noise levels and large outliers in the magnetic declination
inferred from Airmar 150WX magnetic compass readings:

![Time series of inferred site magnetic declination](file://20180605_roof_test/delta_wd_true_mag.png)

##### Standard deviation formula choice

These data were collected using the Campbell Scientific proprietary wind speed
weighted algorithm to calculate standard deviation of wind direction. This is
in contrast to the Yamartino algorithm, which is the EPA-compliant choice for
use with straight-line Gaussian dispersion plume transport models (*WindVector,
CRBasic Program Reference for CR1000.Std.32. Campbell Scientific Inc.*)

Recalculating the standard deviation of wind direction from 10 Hz anemometer
data using the Yamartino algorithm is a relatively straightforward procedure;
refer to online sources for more details. 


### 2018 May 6-9th

Data collected by co-located LI-840A units #1 and 2, inside Paccar ETB 417.

![Analyzers sampling in pass-through mode](20180506_co2_prep/IMG_20180506_134854.jpg)

Performance data ([zip archive](20180506_co2_prep/2018-05-06_Licor_comparison.zip)) was evaluated with Excel:

| CO2   | Licor #1   | Licor #2    |
|-------|------------|-------------|
| mean  |419.0423738 | 412.2458884 |
| stdev | 10.2546315 | 10.1936601  |

Regression eqn: `y = 0.9876x - 1.6`

![Scatterplot of measurements from LI-840A units #1 and #2](20180506_co2_prep/2018_05_10_12_56_46_2018_05_09_Licor_cross_compare.xlsx_Excel.png)

