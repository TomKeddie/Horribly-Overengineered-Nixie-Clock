# Horribly Overengineered Nixie Clock

This is a "horribly overengineered" Nixie clock as the "clock" part could have been achieved far cheaper
and far easier. However, the end result (that there is an actual physical clock) is merely a side effect;
the main motivation for me was to use this project as means to learn something new. To this end, I've used
a fairly expensive ARM microcontroller and the mainboard also includes both USB and Ethernet connectivity.

There are two PCBs in this project: a driver board housing two Nixie tubes with their corresponding drivers
and a mainboard with the uC and other circuitry. The driver board is designed to fit into the 5x5 cm limit
and the mainboard fits the 5x10 cm limit of ITead Studio/Seeed Studio. A full kit with 6 digits would consist
of one mainboard PCB and three driver PCBs.

(The firmware will appear here as soon as there is something usable.)

## BOM

The key components are:

  * ИН-12 Nixie tubes
  * К155ИД1 drivers
  * [Taylor Electronics HVPS-V](http://www.tayloredge.com/storefront/SmartNixie/PSU/index.html) high voltage power supply
  * [NXP LPC1764](http://ics.nxp.com/products/lpc1000/lpc17xx/~LPC1764/) ARM Cortex-M3 microcontroller

Rev A:
  * [Micrel KSZ8001L](http://www.micrel.com/page.do?page=product-info/fastether_trans.jsp) Ethernet PHY

Rev B:
 
  * [Micrel MIC4680](http://micrel.com/index.php/en/component/joodb/article/41-step-down-internal-switches/24-mic4680.html) buck regulator
  * [Micrel KSZ8051RNL](http://micrel.com/index.php/en/component/joodb/article/13-phys/10-ksz8051rnl.html) Ethernet PHY

## Truth table for module

Note that for ease of routing the truth table doesn't match 74(1)41/K155ID1:

<table>
  <tr><th>Num</th> <th>A</th> <th>B</th> <th>C</th> <th>D</th></tr>
  <tr><td>0</td><td>H</td><td>L</td><td>H</td><td>L</td></tr>
  <tr><td>1</td><td>H</td><td>L</td><td>L</td><td>H</td></tr>
  <tr><td>2</td><td>L</td><td>H</td><td>H</td><td>L</td></tr>
  <tr><td>3</td><td>H</td><td>H</td><td>H</td><td>L</td></tr>
  <tr><td>4</td><td>L</td><td>H</td><td>L</td><td>L</td></tr>
  <tr><td>5</td><td>H</td><td>H</td><td>L</td><td>L</td></tr>
  <tr><td>6</td><td>L</td><td>L</td><td>H</td><td>L</td></tr>
  <tr><td>7</td><td>L</td><td>L</td><td>L</td><td>H</td></tr>
  <tr><td>8</td><td>L</td><td>L</td><td>L</td><td>L</td></tr>
  <tr><td>9</td><td>H</td><td>L</td><td>L</td><td>L</td></tr>
</table>

## Errata for Rev A

  * SWDCLK is not routed to JTAG. Oops.
  * P0[28] does not have an external pull-up. Note to self: read the datasheet. Twice.
  * Either LPC parts in general [do not like the cheap-o "tube" 32.768 kHz crystals](http://mbed.org/forum/mbed/topic/1110/) or 
    I can't figure out the proper load capacitance without an actual datasheet. Will switch to a SMD crystal if Rev B ever comes.
  * `RESET` was very flaky until I soldered a 1 μF capacitor to GND across it.
  * Ethernet chip went up in smoke. Oops.
  * No proper way to mount a heatsink on the 7805, and the HVPS audibly complains about low voltages that keep the heat of '05 in check.

## Changelog for Rev B

  * SWDCLK is properly routed.
  * Added a switch-mode 5V power supply based on [Micrel MIC4680](http://micrel.com/index.php/en/component/joodb/article/41-step-down-internal-switches/24-mic4680.html)
  * Changed the Ethernet PHY to [Micrel KSZ8051RNL](http://micrel.com/index.php/en/component/joodb/article/13-phys/10-ksz8051rnl.html)
  * Changed the RTC crystal
  * Added power and USB LEDs.

## Errata for Rev B

  * RTC still won't oscillate. I haven't given up on it yet, as I have a proper datasheet now.
  * Ethernet still doesn't work, but at least didn't go up in smoke. Might just be my bad soldering or a software issue.


