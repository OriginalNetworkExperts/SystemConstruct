#include <SPI.h>
#include "WizFi250.h"
#include <ArduinoHttpClient.h>

char ssid[] = "hong";    // your network SSID (name)
char pass[] = "q1w2e3r4";          // your network password
const int http_port=8080;
int status = WL_IDLE_STATUS;       // the Wifi radio's status
int active=0;
String iotnum="cc000013";
WiFiClient client;
char server[] = "52.78.72.111";
HttpClient httpClient = HttpClient(client, server, http_port);

// Initialize the Ethernet client object


void printWifiStatus();

void setup()
{
    pinMode(6,INPUT);
    pinMode(10,OUTPUT);
    digitalWrite(10,1);
    Serial.begin(115200);
  WiFi.init();
  // check for the presence of the shield:
  if (WiFi.status() == WL_NO_SHIELD) {
    Serial.println("WiFi shield not present");
    // don't continue:
    while (true);
  }

  // attempt to connect to WiFi network
  while (status != WL_CONNECTED) {
    Serial.print("Attempting to connect to WPA SSID: ");
    Serial.println(ssid);
    // Connect to WPA/WPA2 network
    status = WiFi.begin(ssid, pass);
  }
  
  Serial.println("Connected to wifi");
  
  printWifiStatus();
}

void loop()
{
  int fronts=digitalRead(6);

  int iotactive;

  //test.jsp send active,iotnum 
    String s = "/test.jsp?active=";
        s.concat(active);
        s.concat("&iotnum=");
        s.concat(iotnum);
        Serial.println(s);
        
    httpClient.get(s);
    
    String response=httpClient.responseBody();
    Serial.print(response);
    
    delay(1000);
  if(response.equals("0")){
    digitalWrite(10,1);
    active=0;
        Serial.print("<");
        Serial.print(active);
        Serial.println(">");
  }
  //active=1 -> window security=1
  else if(response.equals("1")){
    Serial.println("1");
    Serial.print("@@@");
    Serial.print(fronts);
    Serial.println("@@@");
      if(fronts==0){
        digitalWrite(10,0);
        active=1;
        Serial.print("<");
        Serial.print(active);
        Serial.println(">");}
        else{
          Serial.println("plz");
        }
      }

     
    
  
}
//wifi connect
void printWifiStatus() {
  // print the SSID of the network you're attached to:
  Serial.print("SSID: ");
  Serial.println(WiFi.SSID());

  // print your WiFi shield's IP address:
  IPAddress ip = WiFi.localIP();
  Serial.print("IP Address: ");
  Serial.println(ip);

  // print the received signal strength:
  long rssi = WiFi.RSSI();
  Serial.print("signal strength (RSSI):");
  Serial.print(rssi);
  Serial.println(" dBm");
}
