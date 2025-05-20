# GNSS MosaicHAT reciever
návod

## 1. motivation

tohle je manual pro přijímač satelitu, který ti řekne podle nich tvoji pozici. Budeme používta [GNSS](https://en.wikipedia.org/wiki/Satellite_navigation)(Global Navigation Satellite System) anténu, která přijímá signál ze satelitů, [MosaicHAT](https://github.com/septentrio-gnss/mosaicHAT/tree/master) což je součástka, která ti zpracovává signál a dá ti různé data ohledně tve pozice a pozice satelitů. Aby jsme vytiskly naše informace použijeme Arduino UNO R4 wifi. Připojení k wifi použijem na to, aby mosaicHAT se připojil k [RTK](https://en.wikipedia.org/wiki/Real-time_kinematic_positioning)(Real-time kinematic positioning) stanicím, které nám zpřesní naši pozici.

## x. součástky
   
   budeme potřebovat GNSS antenu, kterou připojíme na mosaicHAT\
   mosaicHAT připojíme na arduino UNO R4 Wifi\
   budeme připojení k wifi, aby se mohl mosaicHAT připojit na RTK stanice\
   informace z mosaicHAT budou vytištěny na displej\
   tlačítko je nepotřebné a je spíše jen na výpomoc u vypisování\
   na BOM jsou všechny potřebné součástky a kde je sehnat\
   budeme potřebovat 2 9v baterie, na arduinoa a na GNSS satelit

## x. software

   mosaicHAT se bude must nastavit přes stránky septentrio ( http://192.168.3.1 ) \
   a přes RXcontrol je nastaven k RTK stanicím
