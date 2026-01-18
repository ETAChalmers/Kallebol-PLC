### Project och källkod till Kallebolens PLC
##Setup
IDE TwinCAT 3 (TE1000 XAE Engineering) Installera via Beckhoff package manager. Senaste TwinCAT XAE kommer installeras då, för att komma åt 4024.X behövs "remote package manager". Kom ihåg att lägga till "Outdated feed" i package manager och starta TC i 32-bitars läge då 4024 inte stödjs av 64-bitars sytem längre.

Video som visar lite bra https://www.youtube.com/watch?v=BZZ_3WDMTG4

XAE version 4024.66 (OBS ej 4026 då CX9020 inst stödjer högre runtime)

##Syfte
Projektets syfte är att driva Elevation och Azimith axlarna, Börvärdena kommer matas in via ADS in till PLCn som sedan kommer realisera dem.

Elevation drivs med en EL7342 (endast en av två kanaler används) kopplat till en sunkigt linjärdon

Azimuth drivs med en AX5203 (endast en av två kanaler används) kopplat till en DFS-52L motor från SEW

## signaler till ADS
För att någon axel skall funka skall "Enable" sickas till respektive mellan varje boot-up cykel


Alla signaler i ADS börjar med _MAIN._ (då de ligger i MAIN tasket)

| Signal        | rikting       |Datatyp| användning      |
| ------------- | ------------- |-------------| ------------- |
| Azimuth.EnableAzimuth             | ReadWrite |BOOL| Starta Azimuth motor drivaren |
| Azimuth.Azimuth_Target_Position_Parabola | ReadWrite |Float32| Börvärde azimuth på parabolen |
| Azimuth.Azimuth_target_position   |ReadOnly|Float32|Börvärde motor|
| Azimuth.HMI_Azimuth               |ReadOnly|Float32|Parabolens azimuth vinkel|
| Azimuth.Azimuth_CurrentPosition   |ReadOnly|Float32|aktuella Motorsvinken|
| Azimuth.Azimuth_state             | ReadWrite |int16| Nuvarande state i motordrivar statemachinen|
|----|----|----|
|Elevation.Enable            |ReadWrite|BOOL| Sätt på strömmen till Elevation; om inte .Homed så körs homeing automatiskt|
|Elevation.Homed             |ReadOnly|BOOL|Är axeln homead?|
|Elevation.Targetpos_mm      |ReadWrite|Float32|Börvärde som Linjäraxeln skall röra sig till|
|Elevation.Current_Position_mm|ReadWrite|Float32|Nuvarande position av Elevationaxeln|
|Elevation.Reset_requested   |ReadWrite|BOOL|Återställ axelfel|
|Elevation.Homeing_Error     |ReadOnly|BOOL|Något gick fel i homeing sekvensen,ex timeout, typ att den inte hittade endstop|
|Elevation.Homeing_Wrong_direction|ReadOnly|BOOL| Homeing felet var att axeln gick åt fel håll|
|Elevation.Error             |ReadOnly|BOOL|Fel på något i Elevation drivningen|
|Elevation.Homeing           |ReadOnly|BOOL|Elevation håller just nu på att homea|


