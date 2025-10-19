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

  int lightValue = iot.GetValue("light");  // Get light sensor value from cloud (replace "light" with your sensor variable name)

  if (lightValue < 100) {      // this is for adjusting threshold as needed
    digitalWrite(D2, HIGH);    // Turn LED on
  } else {
    digitalWrite(D2, LOW);     // Turn LED off
  }

  // If you still want to sync PWM brightness from the cloud for other purposes, comment this out or remove it:
  // iot.SyncPWM("D2");

  delay(50);   // wait 50 milliseconds
}
