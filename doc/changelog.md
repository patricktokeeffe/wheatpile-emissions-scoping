# Change Log / Version History

### Wheatpile Emissions Scoping Study

| Release date | Version | Stationary logger `ProgSig` | Mobile logger `ProgSig` |
|--------------|---------|-----------------------------|-------------------------|
| 2018 June 5  | 0.1     | 44463                       | 40156  |
| 2018 July 10 | 1.0     | 47848                       | 8408   |
| 2018 July 20 | 2.0     | 18988                       | 8408   |


## Version 2.0

* By user special request, add grab sample of sonic anemometer components to
  1-minute data table


## Version 1.0

* Expose GPS position to users on front panel display. Shows minutes component
  of lat/long since degrees expected to remain relatively constant. 
* FIX: record all four aggregated wind values for sonic anemometer. Previously
  only first value (`csat3b_wnd_spd`) was retained in table `minutely`. (Data
  not recorded can be reconstructed from 10Hz anemometer data set.)
* FIX: add missing closing paren (no impact on program operation)
* Track datalogger wiring panel temperature, for quality assurance: adds new
  column `logger_panel_tmpr` to end of 1-min data tables
* FIX: step back custom menu so users first see a timestamp & card status, then
  press any key to obtain custom menu. Also, for stationary site only (because
  user can change azimuth value using keyboard display), hide present values
  behind a "View data" submenu


## Version 0.1

* Initial release used for validating testing and the following field sampling
  events:
    * June 12, 2018
    * June 22, 2018

