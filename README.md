# gmox-kintex-7

## ADC

Some helpful sources are listed below.

1. Xilinx application note [XAPP554](http://www.xilinx.com/support/documentation/application_notes/xapp554-xadc-layout-guidelines.pdf).

##### Power supply
``XADC_VCC`` can be powered by either ``VCCAUX`` or through another 1.8V regulated source. It is recommended that the latter be used. Jumper ``J1`` should be used to make the appropriate choice.
