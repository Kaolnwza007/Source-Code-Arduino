# Source-Code-Arduino

#include <Servo.h>

int pirPin = 3;
int servoPin = 9;

int motionStatus = 0;
int pirState = 0;
int servoState = 0; 

Servo maServo;

void setup() {
  Serial.begin(9600);
  pinMode(pirPin, INPUT);
  maServo.attach(servoPin);
  maServo.write(0);
  delay(1000);
}

void loop() {
  motionStatus = digitalRead(pirPin);

  if (motionStatus == HIGH && pirState == LOW) {
    pirState = HIGH;  


    if (servoState == 0) {
      maServo.write(180);
      servoState = 1;
      Serial.println("Motion Detected → Servo 90°");
    } else {
      maServo.write(0);
      servoState = 0;
      Serial.println("Motion Detected → Servo 0°");
    }

    delay(500); 
  }

  if (motionStatus == LOW && pirState == HIGH) {
    pirState = LOW;
    Serial.println("Motion Ended");
  }
}
