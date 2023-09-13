#include <Arduino.h>
#include <Servo.h>

// Define the pins for the ultrasonic sensor
const int trigPin = 9;
const int echoPin = 10;

// Define the pins for the servo motor
const int servoPin = 11;

// Create a Servo object
Servo myServo;

// Define the variables for the distance and the threshold
int distance;
int threshold = 10;

// Setup function
void setup() {
  // Initialize the serial port
  Serial.begin(9600);

  // Initialize the ultrasonic sensor
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  // Initialize the servo motor
  myServo.attach(servoPin);

  // Set the servo motor to the closed position
  myServo.write(90);
}

// Loop function
void loop() {
  // Calculate the distance
  distance = calculateDistance();

  // Check the distance and open or close the lid accordingly
  switch (distance) {
    case 0:
      // The object is close, so open the lid
      myServo.write(0);
      break;
    case 1:
      // The object is far, so close the lid
      myServo.write(90);
      break;
    default:
      // The object is unknown, so do nothing
      break;
  }
}

// Function to calculate the distance
int calculateDistance() {
  // Clear the trigger pin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  // Set the trigger pin high for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Measure the time it takes for the echo pulse to return
  long duration = pulseIn(echoPin, HIGH);

  // Calculate the distance
  distance = duration * 0.034 / 2;

  return distance;
}
