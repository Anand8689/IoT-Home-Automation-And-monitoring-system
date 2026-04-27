#define BLYNK_PRINT Serial
#define BLYNK_TEMPLATE_ID "TMPL3bO8OovHN"
#define BLYNK_TEMPLATE_NAME "home automation and monitoring system"

#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

// Auth & WiFi
char auth[] =  "UZNfEMO3HKwc7rkAxOB3xTyx9MO8gq0-";
char ssid[] = "Redmi 13C";
char pass[] = "9619358320";
BlynkTimer timer;
void sendSensor();

// Blynk control   
BLYNK_WRITE(V0) { digitalWrite(27, param.asInt()); }
BLYNK_WRITE(V1) { digitalWrite(26, param.asInt()); }
BLYNK_WRITE(V4) { digitalWrite(33, param.asInt()); }
BLYNK_WRITE(V5) { digitalWrite(14, param.asInt()); }
void setup()
{ 
  Serial.begin(115200);

  pinMode(27, OUTPUT);
  pinMode(26, OUTPUT);
  pinMode(25, OUTPUT);
  pinMode(13, OUTPUT);
  pinMode(33, OUTPUT); //relay
  pinMode(32, OUTPUT); //triger
  pinMode(39, INPUT); //vn ir
  pinMode(34, INPUT); //pir
  pinMode(35, INPUT); // utr echo
  pinMode(14, OUTPUT);
  digitalWrite(33, HIGH);   //  Relay OFF at start

WiFi.begin(ssid, pass);

while (WiFi.status() != WL_CONNECTED) {
  delay(500);
  Serial.print(".");
}

Serial.println("\nWiFi Connected");

Blynk.config(auth);
Blynk.connect();
timer.setInterval(1000L, sendSensor); // 1 second
}

void loop()
{
  Blynk.run();
  timer.run();
}
void sendSensor()
{
  long duration;
  float distance;

  // Trigger
  digitalWrite(32, LOW);
  delayMicroseconds(2);
  digitalWrite(32, HIGH);
  delayMicroseconds(10);
  digitalWrite(32, LOW);

  // Read echo
  duration = pulseIn(35, HIGH, 20000);

  if(duration == 0){
    Serial.println("No echo");
    return;
  }

  // Convert to distance (this is your analog value)
  distance = duration * 0.034 / 2;
  if (distance < 20 && distance > 0) {
  digitalWrite(25, HIGH);   // ON
} else {
  digitalWrite(25, LOW);    // OFF
}

float percentage = (1 - (distance / 200.0)) * 100.0;

// Limit range
if (percentage > 100) percentage = 100;
if (percentage < 0) percentage = 0;
Blynk.virtualWrite(V6, percentage);
Blynk.virtualWrite(V3, distance);
  int pirState = digitalRead(34);
  int irState = digitalRead(39);

  // Send correct value to Blyn
  Blynk.virtualWrite(V7, pirState);
  Blynk.virtualWrite(V8, !irState);
}

## Working
The ESP32 connects to WiFi and communicates with the Blynk app. Users can control devices and monitor sensor data in real-time.

## Author
Anand Pandey
