full code is [here](https://github.com/demeterA1/mosaicHAT-reciever/blob/main/code/sketch_may26a.ino)

   ### arduinoIDE
   pro jiné arduina se budou muset použít jiné knihovny pro tisk textu. To je kvůli tome, že Arduino R3 obsahuje v sobě knihovnu "wiring_private.h", kterou arduino R4 nemá
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
  8 je TX na mosaicHAT a 7 je RX
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
