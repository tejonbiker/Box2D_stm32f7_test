# Box2D_stm32f7_test
An example of how well Box2D can run on a MCU Nucleo-F767ZI

## Hardware Overview
You will need the following:
- STM32 Nucleo-F767ZI Board (ARM Cortex M7 with Floating Point Hardware)
- ili9341 Arduino UNO layout 8 bit interface
- Micro USB cable

### Prepare the Hardware

1. Plug the ili9341 Shield into the nucleo144 board (with the Arduino UNO pins compatible)
2. Plug the Micro USB into the Nucleo144 Board
3. Plug the USB Type A in the computer
4. Proceed to the software

## Software
This will require the following software:
- [MCUFRIEND_kbv (parallel 8 bit ili9341 Driver)](https://github.com/prenticedavid/MCUFRIEND_kbv)
- [Adafruit-GFX-Library (Graphics Routines)](https://github.com/adafruit/Adafruit-GFX-Library)
- [Box2D (Physics Engine)](https://github.com/erincatto/box2d)
- [STM32CubeIDE (For Building)](https://www.st.com/en/development-tools/stm32cubeide.html)

### Improving things
Box2D, GFX Library and MCUFRIEND_kbv are taken from github, but only Box2D is used directly from github source code.

GFX Library and MCUFRIEND_kbv are not used directly, a glue-class was created for this libraries to support framebuffer transfers and framebuffer writing instead of drawing directly to the display (avoiding a lot of flickering and improving transfer times to the display), the downside of this method is the amount of RAM usage (320x240x2 bytes = 153600 bytes), limiting the test for higher end Microcontrollers. 

## Building the existing project
1. Clone this repo:
   
   `git clone https://github.com/tejonbiker/Box2D_stm32f7_test`

2. Update submodules

   `git submodule update --init --recursive`

3. Download, install and open STM32CubeIDE
4. Import project folder (expand this)
5. Build the project (expand this)
6. Program the MCU
7. Push the "User" button to switch example
8. Enjoy :D

## Shifting to another STM32 MCU 
MCUFRIEND_kbv library have a lot of support for anothers boards (including anothers nucleo stm32 boards) and MCUs, [(See here)](https://github.com/prenticedavid/MCUFRIEND_kbv/blob/6792ce7caffc75b89a95ae659a0e98bd43d98258/utility/mcufriend_shield.h#L691), MCUFriend Library init the GPIOs by itself, is not required to do nothing in .ioc STM32CubeIDE file for pin definitions, you will only need a pin definition for push button for switching the demo. 

If you board is not listed in the boards section you can check for your MCU model, but pay attention to pin definitions for the display.

If you MCU is not listed you will need modify things to migrate to the new MCU. 

If you don't like framebuffer, you can try directly the MCUFRIEND_kbv library, without the glue class. 

In the new project inside the STM32CubeIDE add the following flags in: (elabrote a lot more) 

1. Flag1
2. Flag2
3. Flag3

Pay attention to target optimization (path to optimizations), (debug flag) will dramatically slow the performance but will allow a more friendly debugging (will not "optimized out" a lot of variables), (Speed flag) will screase speed but a lot of symbols will be "optimized out", change acordingly to the used case. 

## Binary ready to go!!!
A binary is also added, you can program it with STM32CubeProgrammer to the board. 

