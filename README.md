# led and temp sync code

#include <NinjaIoT.h>

NinjaIoT iot;

void setup() {
  Serial.begin(115200);
  iot.connect("wifi-name", "wifi-pass", "UIDofIoTPlatform");   // Connect to NinjaIoT platform
  pinMode(D2, OUTPUT);    // Set D2 as output for LED control
}

void loop() {
  iot.ReadAll();  // Read all values from the cloud

  int lightValue = iot.GetValue("light");  // Get light sensor value from cloud 
  if (lightValue < 80) {      // this is for adjusting threshold as needed
    digitalWrite(D2, HIGH);    // Turn LED on
  } else {
    digitalWrite(D2, LOW);     // Turn LED off
  }

:
  // iot.SyncPWM("D2");

  delay(50);   // wait 50 milliseconds
}
