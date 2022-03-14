# RetroNinja NLQHD-SATA
<img src="rev2\images\NLQHD-SATA_Rev2_render_top.png" alt="Render top" width="500"/><br/>

A SATA-disk interface for the Commodore IEC-bus based on the NLQHD-lite design by Jochen Adler a.k.a. NLQ. The original design, documentation, firmware and source code can be found at [nlq.de](http://nlq.de).

## NLQ-HD
The NLQHD disk interface is a JiffyDOS compatible hard disk controller for the IEC bus. It was designed by Jochen Adler who also wrote the firmware. It supports a partition size of up to 128GB. Larger hard drives can be used but the partition size can not be greater than 128GB. 
The file system used is FAT32 so with a SATA-USB adapter it's easy to unplug and connect the SATA drive to a computer for quick file transfers.  
It should work with all Commodore 8-bit computers using an IEC bus. The drive can in theory be used with a stock kernal in the computer but the standard commands for navigating directories uses the command channel and are pretty cumbersome to use. A JiffyDOS kernal or one of it's derivatives such as S-JiffyDOS or JaffyDOS is pretty much required.

## NLQHD-SATA
This SATA version is a somewhat simplified design in that it doesn't have the same level of over-voltage protection as the original design has. The reason is that I wanted to keep the size of the design down (70x58mm) to fit in a 3D-printed enclosure. It also can't be powered by 1541-II PSU so the protection is less necessary than on the original design. I recommend that this version is powered using a decent quality 12V DC adapter with a center positive barrel connector.  
I have also removed the debugging/programming dip switches so the programming software for the C64 can't be used for flashing the firmware. I don't think it's safe to use so don't even try to use it!  
Instead I have added an ICSP programming header so that the firmware can be programmed in circuit using any AVR programmer such as AVR-ISP, USBASP or even an Arduino (Arduino as ISP). More importantly I've also added a JMH330 PATA-SATA bridge so that the interface can be used with more available and reliable SSD drives without an extra adapter. All SATA drives should be possible to use, from older 3.5" rotational drives to the newer 2.5" SSD drives. 
I replaced the sometimes hard-to-find 5 Volt regulator with integrated components based around an LM2596 voltage regulator. These have unfortunately also became harder to find from reliable sources at the time of writing but are easy to find on eBay or AliExpress. 3.3V and 1.8V voltage regulators have been added to drive the SATA bridge.  
I have made a separate front panel for the control buttons and LEDs. It connects to the mainboard using a 5 pin connector and can easily be replaced by a different panel if you need a different shape.  

<br/>
<img src="rev2\images\NLQHD-SATA_Rev2_render.png" alt="Render top" width="500"/><br/>

I have also created a simple front panel board with buttons and status LEDs.  
This separate board should be pretty easy to modify to suite your own needs.
<img src="rev2\images\photo.jpg" alt="Render top" width="500"/><br/>

## Mainboard BOM

|Parts|Device|Value|Qty|
|-----|-----|-----|-----|
|C101, C102, C103, C104, C201, C202, C203, C204, C205, C206, C301|Ceramic capacitor 0805|100n|11|
|C11, C12|Ceramic capacitor 0805|100p|2|
|C207, C208, C209, C210|Ceramic capacitor 0805|10n|4|
|C211|Ceramic capacitor 0805|1u 10V|1|
|C401|Electrolytic capacitor SMD 6.3X7.7|100u 25V|1|
|C403|Electrolytic capacitor SMD 6.3X7.7|220u 10V|1|
|C404|Ceramic capacitor 0805|10n(*)|1|
|C501, C502, C601, C602|Polarized tantalum capacitor 1206|10uF 10V|4|
|C9, C10, C212, C213|Ceramic capacitor 0805|22p|4|
|D1, D401|Schottky diode 3A SOD-123FL|S34|2|
|D12|General purpose diode SOD-323F|1N4148WSF|1|
|J1, J2|DIN-6 Female PCB-mount||2|
|J3|Molex 22-pin SATA host connector|0470184000|1|
|J4|DC Barrel Jack|PJ-002A|1|
|J5|Shrouded male JST header|5-pin, 2.0mm|1|
|J6|Pin header|2x3-pin, 2.54mm|1|
|JP1|Jumper or power switch|2-pin, 2.54mm|1|
|L1|Inductor 10x11mm|33uH|1|
|R11|Resistor 0805|10k|1|
|R201|Resistor 0805|12k|1|
|R202|Resistor 0805|47k|1|
|R203|Resistor 0805|1M|1|
|R401|Resistor 0805|1k (*)|1|
|R402|Resistor 0805|3k1/0R(*)|1|
|R5, R6|Resistor 0805|100R|2|
|SW1|Tact. switch right angle|6.0x5.0x8.5mm|1|
|U1|Microcontroller TQFP-44|ATmega1284(P)|1|
|U2|PATA-SATA bridge TQFP-64|JMH330|1|
|U3|Hex buffers/drivers SOIC14|74LS07|1|
|U4|Switching regulator TO263-5|LM2596 (AP1501A)|1|
|U5|Volt regulator 3.3V SOT-223|LD1117-3.3|1|
|U6|Volt regulator 1.8V SOT-223|LD1117-1.8|1|
|Y1|Crystal ECX-32|8MHz|1|
|Y2|Crystal ECX-32|25MHz|1|

(*) Only for Adjustable LM2596.
If using a fixed 5V LM2596: Do NOT install R401 and C404 and use a 0 Ohm resistor at R402

There are several variants of 6-pin DIN connectors with different foot prints. I have tried to accommodate them all in one single foot print. Let me know if you have a DIN connector that still doesn't fit this board.
