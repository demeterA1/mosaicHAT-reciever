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

## 3. software
full code is [here](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/code/sketch_may26a.ino)

   ### arduinoIDE
   pro jiné arduina se budou muset použít jiné knihovny pro tisk text. To je kvůli tome, že Arduino R3 obsahuje v sobě knihovnu "wiring_private.h", kterou arduino R4 nemá
   #### libraries for arduino R4
      #include <SoftwareSerial.h>
      #include <Wire.h> 
      #include <TFT_eSPI.h>
      #include <SPI.h>
   #### libraries for arduino R3
      #include <SoftwareSerial.h>
      #include <Wire.h> 
      #include <LCDWIKI_GUI.h> //Core graphics library
      #include <LCDWIKI_SPI.h> //Hardware-specific library
   #### spuštění mosaicHAT a TFT_eSPI knihovny
      SoftwareSerial mosaicSerial = SoftwareSerial(8, 7);; // RX, TX of software serial (mosaicHAT connection)
      TFT_eSPI tft = TFT_eSPI();  // Invoke library
   #### void setup
      void setup() {
     pinMode(8,INPUT); //RX of software serial, input mode
     pinMode(7,OUTPUT); //TX of software serial, output mode
     mosaicSerial.begin(9600);// Software Serial connects to mosaicHAT
     Serial.begin(9600);  // default Serial connects to a computer via USB
     pinMode(2, INPUT_PULLUP);

     int x = 5;
     float y = 3.255;   // temp values
     char z[] = "Hello TFT!";

     tft.init();
     tft.setRotation(1);  // set up if its landscape (1) or portrait(0)
     tft.fillScreen(TFT_BLACK);  // fill screen black
     tft.setTextColor(TFT_YELLOW, TFT_BLACK);  //set up text color and the backround
     tft.setTextSize(2);   //set up text size

     tft.drawString(String("x = ") + x, 10, 20);   //test printing on display
     tft.drawString(String("y = ") + String(y, 2), 10, 50);  //mezera je 30 mezi řádky
     tft.drawString(String("z = ") + z, 10, 80);

     Serial.println("Hellow world!");
  
     delay(1000);
     tft.fillScreen(TFT_BLACK); //clear the screen again
      }
   RX (reciever) a TX (transmiter) jsou tady z pohledu arduina tedy obráceně než na mosaicHAT.

   #### globalní promněnné
      String nmea_string,sreadString;
      String Latitude,Longitude,Latitude_direction,Longitude_direction,Quality_indicator,SVs_Number,Height,Geoid_separation,Quality_indicator_string; //nmea message   elements
      String quality_string_array [6]={"No Fix","GNSS fix","DGPS","","RTK","RTK Float"}; //string meanings of quality indicator values
      bool nmea_flag=false,button_flag=false,push_button=true;
      int separator_indices[14];
      int page=0,disp_counter=100000;
   nmea_string a spread_string jsou na uložení zprávy z mosaicHAT. stringy Latitude, Longitude, atd. jsou na přesné informace z nmea_stringu. button_flag, push_button a int page jsou promněnné k tlačítku a nejsou nutné mít.

   #### void loop
      void loop()
      {
         while (mosaicSerial.available())
         {
          char c;
          delay(2) ; //delay to allow buffer to fill
          if (mosaicSerial.available() >0)
          {
               c = mosaicSerial.read();  //gets one byte from serial buffer
              sreadString += c; //makes the string sreadString  
          } 
        } 
        if(sreadString!="" )
        {
          Serial.println(sreadString);
          nmea_flag=true;
          nmea_string=sreadString;
        }
        sreadString="";
  
        if(nmea_flag)
        {
          int c=0;
          for(int i=0;i<nmea_string.length();i++)
          {
            if(nmea_string[i]==',')
            {
              separator_indices[c]=i;
              c++;
            }
          }

          //parse nmea message into its important elements
          Quality_indicator= nmea_string.substring(separator_indices[5]+1,separator_indices[6]);
          SVs_Number= nmea_string.substring(separator_indices[6]+1,separator_indices[7]);
          Height=nmea_string.substring(separator_indices[8]+1,separator_indices[9]);
          Geoid_separation=nmea_string.substring(separator_indices[10]+1,separator_indices[11]);
          Latitude= nmea_string.substring(separator_indices[1]+1,separator_indices[2]);
          Longitude=nmea_string.substring(separator_indices[3]+1,separator_indices[4]);
          Latitude_direction= nmea_string.substring(separator_indices[2]+1,separator_indices[3]);
          Longitude_direction=nmea_string.substring(separator_indices[4]+1,separator_indices[5]);

          nmea_flag=false;
        }

        disp_counter++; 

        // reducing update rate to avoid screen flickering

        if(disp_counter >= 50000)      //this if is so that it doesnt flicker and only refreshes every few seconds
        {
          tft.fillScreen(TFT_BLACK);

          Quality_indicator_string = quality_string_array[Quality_indicator.toInt()];

          tft.drawString(String("Q = ")+Quality_indicator_string, 10, 20);      // printing all the values
          tft.drawString(String("SV num = ")+SVs_Number, 10, 50);  //mezera je 30 mezi řádky
          tft.drawString("Latitude = "+String(Latitude) + Latitude_direction, 10, 80);
          tft.drawString("Longitude = "+String(Longitude) + Longitude_direction, 10, 120);
          tft.drawString(String("Height = ")+Height+"m", 10, 150);  //mezera je 30 mezi řádky
          tft.drawString(String("Geoid_separation = ")+Geoid_separation+"m", 10, 180);

          disp_counter = 0;
           }
      }

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
   základ programu je z [instructables](https://www.instructables.com/Building-a-GNSS-Receiver-Using-MosaicHAT-and-Ardui/)\
   [datasheets](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/datasheets/datasheets.md) pro součástky
   
