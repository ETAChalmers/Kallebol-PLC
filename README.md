## Project och källkod till Kallebolens PLC

IDE TwinCAT 3 (TE1000 XAE Engineering) https://www.beckhoff.com/en-en/products/automation/twincat/

Projektets syfte är att driva Elevation och Azimith axlarna, Börvärdena kommer matas in via ADS in till PLCn som sedan kommer realisera dem.

Elevation drivs med en EL7342 (endast en av två kanaler används) kopplat till en sunkigt linjärdon

Azimuth drivs med en AX5203 (endast en av två kanaler används) kopplat till en DFS-52L motor från SEW

## signaler till ADS

Alla signaler i ADS börjar med _MAIN._ (då de ligger i MAIN tasket)

| Signal        | rikting       | användning      |
| ------------- | ------------- | ------------- |
| Azimuth.EnableAzimuth             | ReadWrite | Starta Azimuth motor drivaren |
| Azimuth.Azimuth_Target_Position_Parabola | ReadWrite | Börvärde azimuth på parabolen |
| Azimuth.Azimuth_target_position   |ReadOnly|Börvärde motor|
| Azimuth.HMI_Azimuth|ReadOnly      |Parabolens azimuth vinkel|
| Azimuth.Azimuth_CurrentPosition   |ReadOnly|aktuella Motorsvinken|
| Azimuth.Azimuth_state             | ReadWrite | Nuvarande state i motordrivar statemachinen|
|----|----|----|
|Elevation.Enable            |ReadWrite| Sätt på strömmen till Elevation; om inte .Homed så körs homeing automatiskt|
|Elevation.Homed             |ReadOnly|Är axeln homead?|
|Elevation.Targetpos_mm      |ReadWrite|Börvärde som Linjäraxeln skall röra sig till|
|Elevation.Reset_requested   |ReadWrite||
|Elevation.Homeing_Error     |ReadOnly|Något gick fel i homeing sekvensen,ex timeout, typ att den inte hittade endstop|
|Elevation.Homeing_Wrong_direction|ReadOnly| Homeing felet var att axeln gick åt fel håll|
|Elevation.Error             |ReadOnly|Fel på något i Elevation drivningen|
|Elevation.Homeing           |ReadOnly|Elevation håller just nu på att homea|


