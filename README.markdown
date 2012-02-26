# Horribly Overengineered Nixie Clock

This is a "horribly overengineered" Nixie clock as the "clock" part could have been achieved far cheaper
and far easier. However, the end result (that there is an actual physical clock) is merely a side effect;
the main motivation for me was to use this project as means to learn something new. To this end, I've used
a fairly expensive ARM microcontroller and the mainboard also includes both USB and Ethernet connectivity.

There are two PCBs in this project: a driver board housing two Nixie tubes with their corresponding drivers
and a mainboard with the uC and other circuitry. The driver board is designed to fit into the 5x5 cm limit
and the mainboard fits the 5x10 cm limit of ITead Studio/Seeed Studio. A full kit with 6 digits would consist
of one mainboard PCB and three driver PCBs.

## BOM

The key components are:

  * ИН-12 Nixie tubes
  * К155ИД1 drivers
  * [Taylor Electronics HVPS-V](http://www.tayloredge.com/storefront/SmartNixie/PSU/index.html) high voltage power supply
  * [NXP LPC1764](http://ics.nxp.com/products/lpc1000/lpc17xx/~LPC1764/) ARM Cortex-M3 microcontroller
  * [Micrel KSZ8001L](http://www.micrel.com/page.do?page=product-info/fastether_trans.jsp) Ethernet PHY

