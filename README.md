# gmox-kintex-7

## Power supply considerations

Some helpful sources are listed below.

1. Xilinx Kintex-7 [datasheet](http://www.xilinx.com/support/documentation/data_sheets/ds182_Kintex_7_Data_Sheet.pdf)
2. Xilinx 7-series [PCB design guide](http://www.xilinx.com/support/documentation/user_guides/ug483_7Series_PCB.pdf)
3. Xilinx 7-series [Select I/O resources](http://www.xilinx.com/support/documentation/user_guides/ug471_7Series_SelectIO.pdf)
3. [Are all of the VCCINT, VCCAUX, VCCAUX_IO, VCCO, or GND pins in the FPGA connected internally?](http://www.xilinx.com/support/answers/22338.html)

## ADC

Some helpful sources are listed below.

1. Xilinx application note [XAPP554](http://www.xilinx.com/support/documentation/application_notes/xapp554-xadc-layout-guidelines.pdf).

##### Power supply
``XADC_VCC`` can be powered by either ``VCCAUX`` or through another 1.8V regulated source. It is recommended that the latter be used. Jumper ``J1`` should be used to make the appropriate choice.
