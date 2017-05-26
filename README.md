#include <SPI.h>
#include <ESP8266WiFi.h>
#include <WiFiClient.h>
#include <ESP8266WebServer.h>
#include <ESP8266mDNS.h>
WiFiClient client;MDNSResponder mdns;

// Replace with your network credentials
const char* ssid = "*Your SSID*";
const char* password = "*Your Password*";

ESP8266WebServer server(80);
int gpio5_pin = LED_BUILTIN;

String webPage = "";


void setup(void){
     pinMode(gpio5_pin, OUTPUT);
  digitalWrite(gpio5_pin, HIGH);
  
  WiFi.begin(ssid, password);
  webPage += "<h1>Light Switches</h1><p>All Off <a href=\"alloff\"><button>Turn All Lights Off</button></a><br/>";
  webPage += "<p>Socket #1 <a href=\"socket1On\"><button>OfficeOn</button></a>&nbsp;<a href=\"socket1Dim\"><button>Office Dim</button></a>&nbsp;<a href=\"socket1Off\"><button>Office Off</button></a></p>";
  webPage += "<p>Socket #2 <a href=\"socket2On\"><button>Bedroom On</button></a>&nbsp;<a href=\"socket2Dim\"><button>Bedroom Dim</button></a>&nbsp;<a href=\"socket2Off\"><button>Bedroom Off</button></a></p>";
  webPage += "<p>Socket #3 <a href=\"socket3On\"><button>Living Room On</button></a>&nbsp;<a href=\"socket3Dim\"><button>Living Room Dim</button></a>&nbsp;<a href=\"socket3Off\"><button>Living Room Off</button></a></p>";
  //webPage += "<p>Datsun Sign <a href=\"DatOn\"><button>Datsun Sign On</button></a>&nbsp;<a href=\"DatOff\"><button>Datsun Sign Off</button></a></p>";
  webPage += "<h1>GPIO</h1><p>Datsun sign.. <a href=\"PinD1On\"><button>...Goes On</button></a>&nbsp;<a href=\"PinD1Off\"><button>...Goes Off</button></a></p>";
   server.begin();
    server.on("/", [](){
    server.send(200, "text/html", webPage);
  });
  
   server.on("/alloff", [](){
    server.send(200, "text/html", webPage);
    digitalWrite(gpio5_pin, LOW);
     socket1Off();
     delay(1000);
     socket2Off();
     delay(1000);
     socket3Off();
     delay(1000);
  });
   server.on("/socket1On", [](){
   server.send(200, "text/html", webPage);
   socket1On();
   delay(1000);
  });
       server.on("/socket1Dim", [](){
     server.send(200, "text/html", webPage);
    socket1Dim();
    delay(1000);
  });
     server.on("/socket1Off", [](){
     server.send(200, "text/html", webPage);
    socket1Off();
    delay(1000);
  });
   server.on("/socket2On", [](){
   server.send(200, "text/html", webPage);
   socket2On();
   delay(1000);
  });
       server.on("/socket2Dim", [](){
     server.send(200, "text/html", webPage);
    socket2Dim();
    delay(1000);
  });
     server.on("/socket2Off", [](){
     server.send(200, "text/html", webPage);
 socket2Off();
    delay(1000);
  });
     server.on("/socket3On", [](){
   server.send(200, "text/html", webPage);
   socket3On();
   delay(1000);
  });
       server.on("/socket3Dim", [](){
     server.send(200, "text/html", webPage);
    socket3Dim();
    delay(1000);
  });
     server.on("/socket3Off", [](){
     server.send(200, "text/html", webPage);
 socket3Off();
    delay(1000);
  });
    server.on("/PinD1On", [](){
    server.send(200, "text/html", webPage);
    digitalWrite(gpio5_pin, LOW);
    delay(1000);
  });
  server.on("/PinD1Off", [](){
    server.send(200, "text/html", webPage);
    digitalWrite(gpio5_pin, HIGH);
    delay(1000); 
  });
  
}

void loop() {
  // put your main code here, to run repeatedly:




 server.handleClient();
 client.stop();
}
void socket1On()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/groups/2");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("5000");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":true, \"bri\":240}"); 
}
void socket1Dim()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/lights/8");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("5000");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":true, \"bri\":100}"); 
}
void socket1Off()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/lights/8");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("150");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":false, \"bri\":100}"); 
}
void socket2On()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/groups/5");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("5000");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":true, \"bri\":240}"); 
}
void socket2Dim()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/groups/5");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("5000");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":true, \"bri\":100}"); 
}
void socket2Off()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/groups/5");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("5000");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":false, \"bri\":100}"); 
}
void socket3On()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/groups/1");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("5000");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":true, \"bri\":240}"); 
}
void socket3Dim()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/groups/1");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("5000");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":true, \"bri\":100}"); 
}
void socket3Off()
{
  client.connect("*Your Hue Bridge IP*", 80);
client.print("PUT /api/*Your Hue API Key Here*/groups/1");
client.println("/action HTTP/1.1");
    client.print("Host: ");
    client.println("*Your Hue Bridge IP*");
    client.print("Content-Length: ");
client.println("5000");
client.println("Content-Type: text/plain;charset=UTF-8");
    client.println();
client.println("{\"on\":false, \"bri\":100}"); 
}
