# gmox-kintex-7

**Chip** XC7K160T-FBG484.

The project is still in-progress. Switching regulation connections for ``VCCINT``, ``MGTAVCC``, ``VCCAUX``, ``MGTAVTT`` need to be made in the schematic, though the libraries are all in place. Also, the ADC interface needs to be connected.

A note about the libraries: libraries in the **custom** folder are manually created using respective datasheets, while the libraries in the **bxl-to-cad** folder have been created using [Ultra Librarian](http://www.accelerated-designs.com/ultra-librarian/).

## Power supply considerations

Some helpful resources are listed below.

1. Xilinx Kintex-7 [datasheet](http://www.xilinx.com/support/documentation/data_sheets/ds182_Kintex_7_Data_Sheet.pdf).
2. Xilinx 7-series [PCB design guide](http://www.xilinx.com/support/documentation/user_guides/ug483_7Series_PCB.pdf).
3. Xilinx 7-series [Select I/O resources](http://www.xilinx.com/support/documentation/user_guides/ug471_7Series_SelectIO.pdf).
4. [Are all of the VCCINT, VCCAUX, VCCAUX_IO, VCCO, or GND pins in the FPGA connected internally?](http://www.xilinx.com/support/answers/22338.html)
5. TI power management solutions for Xilinx FPGAs [reference guide](http://www.ti.com/lit/sg/slyt563/slyt563.pdf).

##### Supported I/O standards for our test-board

1. LVCMOS25. Only HR I/O banks. ``VCCO = 2.5V``
2. LVCMOS18. Both HR and HP I/O banks. ``VCCO = 1.8V``
3. ~~LVDS. Only HP I/O banks. ``VCCO = 1.8V``~~
4. ~~LVDS25. Only HR I/O banks. ``VCCO = 2.5V``~~

In our test design, we've connected the HR banks to ``VCCO = 2.5V``, and the HP banks to ``VCCO = 1.8V``. Note, HR stands for High Range and HP for High Performance. Banks 13, 14, 15, 16 are all HR banks. Banks 33, 34 are HP banks.

![XC7K160T banks](https://github.com/stothe2/gmox-kintex-7/blob/master/img/banks.jpg)

##### Recommended bypass capacitor usage

|                                      | 330uF | 100uF |  47uF | 4.7uF |
| ------------------------------------ |:-----:|:-----:|:-----:|:-----:|
| ``VCCINT``                           |   2   |   0   |   0   |   0   |
| ``VCCBRAM``                          |   0   |   1   |   0   |   3   |
| ``VCCAUX``                           |   0   |   0   |   2   |   3   |
| ``VCCO`` bank 0                      |   0   |   0   |   1   |   0   |
| ``VCCO`` all other banks (per bank)  |   0   |   1   |   0   |   0   |

##### Power tree

![Voltage lines](https://github.com/stothe2/gmox-kintex-7/blob/master/img/voltage-rail.jpg)

## Configuration Pins

Some helpful resources are listed below.

1. Xilinx 7 series FPGAs configuration user guide [UG470](http://www.xilinx.com/support/documentation/user_guides/ug470_7Series_Config.pdf).

##### ``PROGRAM_B``

Input. Active-low reset to configuration logic.

##### ``DONE``

Bidirectional. High signal on ``FPGA_DONE`` indicates completion of configuration sequence. On our test-board, ``LED2`` indicates the status of this signal.

##### ``CCLK``

Input or Output. On our test-board this pin is left unconnected since we're only using the board in JTAG mode when the pin has high impedance.

##### ``M[2:0]``

Input. Since we're only using the test-board in JTAG mode, the pins are set to ``101``.

##### ``CFGBVS``

Input. On our test-board, this is tied high since banks 0, 13, and 14 are operational at 2.5V.

##### ``INIT_B``

Pulsing of ``INIT_B`` from Low to High indicates the completion of initialization at power-up. ``LED3`` indicates the status of this pin.

## ADC

Some helpful resources are listed below.

1. Xilinx application note [XAPP554](http://www.xilinx.com/support/documentation/application_notes/xapp554-xadc-layout-guidelines.pdf).

##### Power supply
``XADC_VCC`` can be powered by either ``VCCAUX`` or through another 1.8V regulated source. It is recommended that the latter be used. Jumper ``J1`` should be used to make the appropriate choice.

## To think about

1. Power supervisory circuit? How would it compare to a simple pullup resistor network?
2. Test conditions? Two of the proposed ones are (a) testing setup/hold time as a function of temperature using chain oscillators, and (b) testing stability of performance with temperature using counters. See [this](https://nepp.nasa.gov/respace_mapld11/talks/thu/MAPLD_C/1020%20-%20Sheldon.pdf) presentation to get a better sense.
3. Load regulation for linear regulators LM1086-2.5V and LM1086-1.8V?
4. ``FPGA_INIT_B``, ``CCLK``, and ``M[2:0]`` (especially for non-JTAG uses)?
5. A separate ground pool for ``XADC_GND``?
