# New-obstacles-
const int trigPin = 2;  // Trigger pin of ultrasonic sensor
const int echoPin = 3;  // Echo pin of ultrasonic sensor
const int servoPin = 9;  // Pin for servo motor

#include <Servo.h>

Servo myServo;  // Create a servo object

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  myServo.attach(servoPin);  // Attach the servo to the pin
}

void loop() {
  int distance = getDistance();  // Get the distance to the obstacle
  if (distance < 20) {  // If the distance is less than 20cm
    avoidObstacle();  // Avoid the obstacle
  } else {
    moveForward();  // Move forward
  }
  delay(50);  // Wait for 50ms
}

int getDistance() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  int duration = pulseIn(echoPin, HIGH);
  int distance = duration * 0.034 / 2;
  return distance;
}

void avoidObstacle() {
  myServo.write(0);  // Turn the servo to 0 degrees (left)
  delay(500);  // Wait for 500ms
  myServo.write(180);  // Turn the servo to 180 degrees (right)
  delay(500);  // Wait for 500ms
}

void moveForward() {
  myServo.write(90);  // Turn the servo to 90 degrees (forward)
}
