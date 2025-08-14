# GNSS MosaicHAT reciever
![mosaicHAT_logo_withText](https://github.com/user-attachments/assets/fa5d2720-5744-4d43-ac49-5d1017e8f0d1)
![arduinologo](https://github.com/user-attachments/assets/ebccc210-ea41-4441-a85b-deffee34c085)



## 1. motivation
tohle je manual pro přijímač satelitu, který ti řekne podle nich tvoji pozici. Budeme používta [GNSS](https://en.wikipedia.org/wiki/Satellite_navigation)(Global Navigation Satellite System) anténu, která přijímá signál ze satelitů, [MosaicHAT](https://github.com/septentrio-gnss/mosaicHAT/tree/master) což je součástka, která ti zpracovává signál a dá ti různé data ohledně tve pozice a pozice satelitů. Aby jsme vytiskly naše informace použijeme Arduino UNO R4 wifi. Připojení k wifi použijem na to, aby mosaicHAT se připojil k [RTK](https://en.wikipedia.org/wiki/Real-time_kinematic_positioning)(Real-time kinematic positioning) stanicím, které nám zpřesní naši pozici.

## 2. hardware
   ### list součástek
         1x mosaicHAT
         1x GNSS antena
         1x arduino UNO R4 wifi
         2x 9v baterie
         2x klip na 9v baterie
         1x displej(bylo by lepší použít menší displej, protože ten který jsme použili má až moc vysokou spotřebu)
         1x tlačítko(nepotřebný)
         1x přepínač
         kable
   ### MosaicHAT
   je to Open Source GPS/GNSS HW PCB HAT, který integruje <a href="https://www.septentrio.com/en/products/gnss-receivers/rover-base-receivers/receivers-module/mosaic">Septentrio's mosaic-X5</a> GNSS module se        základní komunikací, která může být s raspberry pi systémem.
   Cílem tohodle je docílit jednodušího HW prototypování pomocí mosaic-X5 GNSS modul využívající počítačový ecosystém poskytující raspberry pi. MosaicHAT můžete použít sám od sebe a připoijt o k počítači pomocí      usb.

   ![mosaicHAT_features](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/pictures/mosaicHAT_features.png)

   #### mosaic-X5
   <a href="https://www.septentrio.com/en/products/gnss-receivers/rover-base-receivers/receivers-module/mosaic">Septentrio's mosaic-X5</a> více pásmový, více konstilační GNSS přijímač v       modulu pro povrchovou         montáž s nízkým výkonem a širokou škálou rozhraní, navrženém pro aplikace na masovém trhu, jako je robotika a autonomní systémy, schopný sledovat všechny konstelace globálního navigačního satelitního systému      (GNSS) podporující současné i budoucí signály. Díky jedinečné vestavěné technologii AIM+ pro zmírnění rušení nabízí Septentrio výkonnostní benchmark v hromadném trhu stavebních bloků GNSS polohování.

   #### arduino UNO R4 wifi
   Je to Arduino UNO R4 s ESP32 pro připojení k wifi a bluetooth.
   ![ard-abx00087_02-504363431](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/pictures/ard-abx00087_02-504363431.jpg)

   #### gnss antena
   Aby bylo možné využít z více signálů a konstelací, které deska mosaicHAT má, doporučuje se zakoupit schopnou vícepásmovou anténu. Na trhu existuje několik výrobců GNSS antén (např.            Maxtenna, Tallysman atd.). Pro více informací můžete také kontaktovat společnost Septentrio. Existují také různé typy antén, z nichž každá je vhodná pro různé aplikace (např. robotika,        větší stroje atd.). Jistě, čím větší anténa, tím lepší výkon můžete získat, ale není to jen o velikosti, ale také o kvalitě samotných anténních prvků.

   Ujistěte se, že máte správnou propojku, abyste mohli také nastavit správné napětí v závislosti na zvolené anténě GNSS.
   
   ![vant_jumper_new](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/pictures/vant_jumper_new.jpg)

   NOTE: deska mosaicHAT obsahuje pouze jeden regulátor napětí (3,3V). 5V linka je přímo připojena ke zdrojům energie. Protože raspberry Pi i USB napájejí 5V, jejich použití pro napájení by nemělo představovat žádnou hrozbu. Napájení přes externí napájecí headery by však mělo být prováděno opatrně. Podložka VANT (Antenna voltage) mozaikového modulu je přímo připojena k externímu pinu +5V. NENÍ CHRÁNĚN PROTI VYŠŠÍMU NAPĚTÍ. Podle mozaikového hardwarového manuálu VANT akceptuje napájení 3V až 5,5V. Při použití externího napájecího zdroje se ujistěte, že není větší než 5 V. Pokud je požadován zdroj více než 5V, ujistěte se, že jsou dvě propojky PWR připojeny k pinu 3V3 nebo odstraněny. Napájení VANTu vyšším napětím by mohlo modul POŠKODIT. Na následující 
   
fotografii je anténa Tallysman připojena k mosaicHAT. Propojka je umístěna pro napájení antény 5V.
![antenna_connected](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/pictures/antenna_connected.jpg)

## Q&A
   ### 1. je možné použít jiné arduino
         ano ale je třeba dbát na knihovny, protože starší knihovny pujdou jenom na arduino R3 a ne na R4.
   ### 2. mosaicHAT funguje jenom když je připojen k počítači a ne když je jenom s arduinem a displejem
         zkontroluj zapojení a program. pokud tohle máte správně je možné, že displej má až moc vysokou spotřebu. Je dobré si to proměřit multimetrem.
   ### 3. mám připojený mosaicHAT k počítači, pro kontrolu funkčnosti, ale nechytá žádný signál ze satelitů
         zkontrolujte umístění antény. Pokuď bude v uzavřeném prostoru a nebude minimálně u otevřeného okne, tak bude mít hodně zkreslené hodnoty
         nebo je rovnou nebude vidět
   ### 4. během 5 minut mi naběhly jenom 2 satelity je s tím neco špatně?
         někdy to může trvat i 15 minut než získanete svojí pozici. Záleží na tom kde je umístěna antena.
         Pokuď je někde v ulici a je obklopena budovami tak bude mít větší potíže najít aspoň 4 satelity z 1 konstilace pro výpočet polohy.
         
         
   můj email pokuď máte na mě další otázky: adam.demeter.cz@gmail.com

## sources
   informace o mosaicHAT jsou z mosaicHAT [github](https://github.com/septentrio-gnss/mosaicHAT) by septentrio\
   originální nnávod je z [instructables](https://www.instructables.com/Building-a-GNSS-Receiver-Using-MosaicHAT-and-Ardui/)\
   [datasheets](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/datasheets/datasheets.md) pro součástky
   
