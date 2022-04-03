# Xiao_rp2040_ADXL_Klipper
Configuration for XIAO RP2040 for Input Shaper/ADXL usage on Klipper
---

Usage of XIAO RP2040 Mcu : 
https://wiki.seeedstudio.com/XIAO-RP2040/ 

for Input shaper acclerometer for Klipper firmware of 3d printers. For use with ADXL345 pcbs.
https://www.klipper3d.org/Measuring_Resonances.html


Firmware:
---

SSH from Klipper directory on PI.
```
cd ~/klipper
```

Use command : make menuconfig 
Setup with below settings.
Press Q to save.
____________________________
- uncheck extra low-level options
- Architecture: Raspberry Pi RP2040
- Communication Interface: USB
___________________________
![image](https://user-images.githubusercontent.com/94410881/161407288-0ed898fe-4e68-40b4-bd45-d2981ff111e7.png)
____________________________

Enter in SSH : 
```
make clean
make
```             
               
![image](https://user-images.githubusercontent.com/94410881/161407322-2eee11eb-5346-41fd-be4d-69338c560a5a.png)
__________________________
WINSCP
----
https://winscp.net/eng/index.php


Using WINSCP connect to PI via local IP. 
Navigate to /klipper/out folder 
Download klipper.uf2 to known directory on PC
![image](https://user-images.githubusercontent.com/94410881/161407378-d7902dbe-5efb-41e3-9598-915eb46d732c.png)

__________________________

XIAO RP2040. 
---

While holding "B" Button , connect XIAO to USB to PC that has "klipper.uf2" file. 
More info: https://wiki.seeedstudio.com/XIAO-RP2040/

![image](https://user-images.githubusercontent.com/94410881/161407423-73daff7c-3f78-403b-b8db-df9fb036657b.png)


After XIAO is available on PC. 


Copy "klipper.uf2" to XIAO. 

Once complete, disconnect from PC. 

___________________________________

VERIFYING FLASH:
---

Connect XIAO to Raspberry Pi. 
From SSH , use command : 
```

ls /dev/serial/by-id/*

```

3d printer MCU and XIAO as Klipper should display. 
XIAO is now flash with klipper FM. 

_______________________________

WIRING ADXL :
---

![image](https://user-images.githubusercontent.com/94410881/161407023-dd86fc24-776a-4541-8163-0d1ca7f7424a.png)


Images are of ADXL wired for VCC , NOT 3v3. Wire accordingly. 

Use this resource if unsure:

https://klipper.discourse.group/t/raspberry-pi-pico-adxl345-portable-resonance-measurement/1757



![image](https://user-images.githubusercontent.com/94410881/161407548-3307d8fe-df5a-47bb-a56b-0e31875a1555.png)
![image](https://user-images.githubusercontent.com/94410881/161407540-dafd24a6-14c4-4b85-a269-b0317c822869.png)
![image](https://user-images.githubusercontent.com/94410881/161407767-9217da2d-0f61-47c0-9d34-5df5b6f7805e.png)
![image](https://user-images.githubusercontent.com/94410881/161407778-94ee89a1-89e9-4a65-8b89-63da0b4f1bb8.png)



KLIPPER CONFIG:
---

Find Xiao serial by using : 

```
ls /dev/serial/by-id/*
```

Enter this address in the "mcu" section below within your printer config. 

Save and restart after editing printer.cfg file. 

![image](https://user-images.githubusercontent.com/94410881/161407123-e0ffffb4-7f40-4a2e-834c-f13651e20d52.png)
____________________________________

Testing:
--- 

Instructions with more detail are found at: 
https://www.klipper3d.org/Measuring_Resonances.html

ACCELEROMETER_QUERY will fail on first attempt. This is normal. 

Use 
```
ACCELEROMETER_QUERY 
```

in console to verify communication to ADXL :
Klipper should report:
![image](https://user-images.githubusercontent.com/94410881/161407591-f7b02d88-e3da-45aa-ae50-43a772b115d1.png)

Use 
```
MEASURE_AXES_NOISE
```
to measure noise of ADXL. 

![image](https://user-images.githubusercontent.com/94410881/161407797-b30ecfa5-af03-43d7-9d52-a282aafe655d.png)

![image](https://user-images.githubusercontent.com/94410881/161407793-070e4950-c8fa-436f-8a6b-961617915dbc.png)





 



