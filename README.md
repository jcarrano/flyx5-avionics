# FlyX5 Hardware #

This is the circuit board for the FlyX5 UAV controller.

![FlyX5 Revision 0 Board](images/DSC06301.JPG?raw=true "Manufactured board")

## Main board: flx_control ##

* Flight Stabilization and control.
* Tested. Works (except for errata listed below).

Features:

* Compact size: 54.5mm x 45.2mm
* Builtin buck converter: can be powered directly by batteries and provides 5V up to 1A.
* 3 Leds, 3 Buttons (2 programmable + reset).
* Microprocessor: TI Tiva-C (ARM M4F) with hardware floating point support.
* Supports up to 8 ESC. ESC ports can be configured as PWM or SPI.
* Radio-control port: 6 channels PWM input. Can be reconfigured as up to 3 duplex serial ports.
* Dedicated Serial Port.
* 2 Analog sense ports for battery sensing.
* Buzzer (with melodies)
* SD card slot.
* Expansion port (SPI+Power+2GPIO). Matches the pinout of a NRF2404+ module
* Gyro+Accelerometer: Invensense MPU-6500
* Magnetometer: Freescale MAG3110
* Altimeter: Freescale MPL3115A2
* Port for connecting ultrasonic ranger.

![3D rendering of PCB](images/top3d-2.png?raw=true "3D rendering of PCB")

Debugging and tinkering:

* JTAG port (can be programmed (and debugged) with a Tiva-C eval board and OpenOCD, no fancy HW required)
* Way too many testpoints.

### Errata ###

* On the first version, SDA and SCL lines for one I2C bus were reversed.
* The buzzer driver circuit is designed for magnetic buzzers. For piezo buzzers it requires a pull resistor. Newer versions should include a push-pull driver instead.
* The MCU has an errata, which has been worked around both in SW and HW.

## ESC controller board: flx_esc ##

SUPER experimental.

Features:

* Digital control via SPI: no more trimming/calibrating the PWM
* SPI allows reporting current motor speed (along with other parameters) back to control board.
* Uses a crystal for timing: no trimming or calibrating time.
* Processor: Kinetis KE02 (ARM M0+) allows for more advanced calculations (for example square root compensation for directly controlling thrust instead of speed)
