# GNSS MosaicHAT reciever
![mosaicHAT_logo_withText](https://github.com/user-attachments/assets/fa5d2720-5744-4d43-ac49-5d1017e8f0d1)

## 1. motivation
tohle je manual pro přijímač satelitu, který ti řekne podle nich tvoji pozici. Budeme používta [GNSS](https://en.wikipedia.org/wiki/Satellite_navigation)(Global Navigation Satellite System) anténu, která přijímá signál ze satelitů, [MosaicHAT](https://github.com/septentrio-gnss/mosaicHAT/tree/master) což je součástka, která ti zpracovává signál a dá ti různé data ohledně tve pozice a pozice satelitů. Aby jsme vytiskly naše informace použijeme Arduino UNO R4 wifi. Připojení k wifi použijem na to, aby mosaicHAT se připojil k [RTK](https://en.wikipedia.org/wiki/Real-time_kinematic_positioning)(Real-time kinematic positioning) stanicím, které nám zpřesní naši pozici.

## 2. hardware
   ### 2.1 list součástek
         1x mosaicHAT
         1x GNSS antena
         1x arduino UNO R4 wifi
         2x 9v baterie
         2x klip na 9v baterie
         1x displej
         1x tlačítko(nepotřebný)
         1x přepínač
         kable
   ### 2.2 navod   
      budeme potřebovat GNSS antenu, kterou připojíme na mosaicHAT
      mosaicHAT připojíme na arduino UNO R4 Wifi
      budeme připojení k wifi, aby se mohl mosaicHAT připojit na RTK stanice
      informace z mosaicHAT budou vytištěny na displej
      tlačítko je nepotřebné a je spíše jen na výpomoc u vypisování
      na BOM jsou všechny potřebné součástky a kde je sehnat
      budeme potřebovat 2 9v baterie, na arduinoa a na GNSS satelit
![GNSS reciever2_bb](https://github.com/user-attachments/assets/091bfd6d-fe38-4b7f-b4d9-f5461a4b392f)

## 3. software

   mosaicHAT se bude must nastavit přes stránky septentrio ( http://192.168.3.1 ) \
   a přes RXcontrol je nastaven k RTK stanicím

## sources
   mosaicHAT [github](https://github.com/septentrio-gnss/mosaicHAT) by septentrio
   
