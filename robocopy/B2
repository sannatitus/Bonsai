@echo off
setlocal enabledelayedexpansion

for /f "delims=" %%a in ('wmic os get localdatetime ^| find "."') do set datetime=%%a

set year=!datetime:~0,4!
set month=!datetime:~4,2!
set day=!datetime:~6,2!
set hour=!datetime:~8,2!
set minute=!datetime:~10,2!
set second=!datetime:~12,2!

mkdir D:\robocopy-log 2>nul
robocopy "D:\B2" "Z:\raw\CrabLab\CrabitatCam_daily\B2" /E /MOVE /MON:1 /LOG+:D:\robocopy-log\Robocopylog_!day!_!month!_!year!_!hour!!minute!.txt /v /tee
