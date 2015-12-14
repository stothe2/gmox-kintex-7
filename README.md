# gmox-kintex-7

**Chip** XC7K160T-FBG484.

## Power supply considerations

Some helpful sources are listed below.

1. Xilinx Kintex-7 [datasheet](http://www.xilinx.com/support/documentation/data_sheets/ds182_Kintex_7_Data_Sheet.pdf)
2. Xilinx 7-series [PCB design guide](http://www.xilinx.com/support/documentation/user_guides/ug483_7Series_PCB.pdf)
3. Xilinx 7-series [Select I/O resources](http://www.xilinx.com/support/documentation/user_guides/ug471_7Series_SelectIO.pdf)
4. [Are all of the VCCINT, VCCAUX, VCCAUX_IO, VCCO, or GND pins in the FPGA connected internally?](http://www.xilinx.com/support/answers/22338.html)

##### Supported I/O standards for our test-board

1. **LVCMOS25** Only HR I/O banks. ``VCCO = 2.5V``
2. **LVCMOS18** Both HR and HP I/O banks. ``VCCO = 1.8V``
3. ~~**LVDS** Only HP I/O banks. ``VCCO = 1.8V``~~
4. ~~**LVDS25** Only HR I/O banks. ``VCCO = 2.5V``~~

Note, HR stands for High Range and HP for High Performance. Banks 13, 14, 15, 16 are all HR banks. Banks 33, 34 are HP banks.

## ADC

Some helpful sources are listed below.

1. Xilinx application note [XAPP554](http://www.xilinx.com/support/documentation/application_notes/xapp554-xadc-layout-guidelines.pdf).

##### Power supply
``XADC_VCC`` can be powered by either ``VCCAUX`` or through another 1.8V regulated source. It is recommended that the latter be used. Jumper ``J1`` should be used to make the appropriate choice.
