# led and temp sync code

#include <NinjaIoT.h>

NinjaIoT iot;

void setup() {
  Serial.begin(115200);
  iot.connect("wifi-name", "wifi-pass", "UIDofIoTPlatform");   // Connect to NinjaIoT platform
  pinMode(D2, OUTPUT);    // D2 is my output for LED control
}

void loop() {
  iot.ReadAll();  //

  int lightValue = iot.GetValue("light");  // Get light sensor value from cloud 
  if (lightValue < 80) {      // this is for adjusting threshold as needed
    digitalWrite(D2, HIGH);    // Turn LED on
  } else {
    digitalWrite(D2, LOW);     // Turn LED off
  }

:# need to connect to cloud?
  // iot.SyncPWM("D2");

  delay(50);   // wait 50 milliseconds
}
