## list součástek
         1x mosaicHAT
         1x GNSS antena
         1x arduino UNO R4 wifi
         2x 9v baterie
         2x klip na 9v baterie
         1x displej(bylo by lepší použít menší displej, protože ten který jsme použili má až moc vysokou spotřebu)
         1x tlačítko(nepotřebný)
         1x přepínač
         kable
## zapojení
   |odkuď |kam |
|--------|----------|
|mosaicHAT RX | Arduino D7 |
|mosaicHAT TX | Arduino D8|
|mosaicHAT GND | Arduino GND|
|mosaicHAT +5V | Arduino 5V|
|--------|----------|
|baterie GND | Arduino GND|
|baterie +9V | Arduino VIN|
|--------|----------|
|displej GND | Arduino GND|
|displej 5V | Arduino 5V|
|displej reset | 1. převodník LV1|
|displej cs | 1. převodník LV2|
|displej dc | 1. převodník LV3|
|displej SDI(MOSI) | 1. převodník LV4|
|displej sck | 2. převodník LV1|
|displej SDO(MISO) | 2. převodník LV2|
|displej led | arduino 3,3V|
|displej led | 1. převodník LV|
|displej led | 2. převodník LV|
|--------|----------|
|1. převodník HV | arduino 5V|
|2. převodník HV | arduino 5V|
|1. převodník HV2 | arduino D4|
|1. převodník HV1 | arduino D5|
|1. převodník HV3 | arduino D3|
|1. převodník HV4 | arduino D11|
|2. převodník HV1 | arduino D13|
|2. převodník HV2 | arduino D12|
|1. i 2. převodník GND z LV a HV strany | arduino GND|
|--------|----------|
|pin tlačítka| arduino GND|
|pin tlačítka| arduino D2|


![GNSS reciever3_bb](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/fritzing/GNSS%20reciever4_bb.png)

