#include <Adafruit_NeoPixel.h>
#define PIN            6
#define NUMPIXELS      200

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

char text;
char jsptext();
boolean startRead = false;
boolean plz;

void setup(){
  Serial.begin(115200);
    pixels.begin(); // This initializes the NeoPixel library.
}

void loop(){
   plz=true;
  jsptext();
  Serial.print("plz:");
  Serial.println(text);
if(text=='1'){
  Serial.println("ok");
  for(int i=0;i<NUMPIXELS;i++){

    // pixels.Color takes RGB values, from 0,0,0 up to 255,255,255
    pixels.setPixelColor(i, pixels.Color(100,0,0)); // Moderately bright green color.
    pixels.show(); // This sends the updated pixel color to the hardware.
  }
    for(int i=0;i<NUMPIXELS;i++){

    // pixels.Color takes RGB values, from 0,0,0 up to 255,255,255
    pixels.setPixelColor(i, pixels.Color(0,0,0)); // Moderately bright green color.
    pixels.show(); // This sends the updated pixel color to the hardware.
  }
}
 else if(text=='0'){
    Serial.println("nono");
    pixels.begin();
    pixels.show();
      for(int i=0;i<NUMPIXELS;i++){

    // pixels.Color takes RGB values, from 0,0,0 up to 255,255,255
    pixels.setPixelColor(i, pixels.Color(50,50,200)); // Moderately bright green color.

    pixels.show(); // This sends the updated pixel color to the hardware.

  }
  }
}
//Arduino UNO <-> ORANGE BOARD 1:1 rx/tx communication
char jsptext(){
while(plz){
if (Serial.available()) {
    char c = Serial.read();
    if(c=='<'){
    startRead = true;
    }else if(startRead){
        if(c != '>'){ //'>' is our ending character
          text = c;
        }
       else{
        Serial.println(text);
          //got what we need here! We can disconnect now
          startRead = false;
          plz = false;
        }
      }
    }  
}
}
