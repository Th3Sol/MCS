### Ultrasonic Sensor

```cpp
const int trigPin = 11;
const int echoPin = 9;

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance:");
  Serial.print(distance);
  Serial.println(" cm");
}
```

---

### DC Motor

```cpp
int motorPin = 3;

void setup() {
  pinMode(motorPin, OUTPUT);
  Serial.begin(9600);
  Serial.println("speed 0 to 255");
}

void loop() {
  if (Serial.available()) {
    int speed = Serial.parseInt();
    if (speed >= 0 && speed <= 255) {
      analogWrite(motorPin, speed);
    }
  }
}
```

---

### Stepper Motor

```cpp
// Includes the Arduino Stepper Library
#include <Stepper.h>

// Define the number of steps per revolution
const int stepsPerRevolution = 2048;

// creates an instance of Stepper class
// Pins entered in sequence IN1-IN2-IN3-IN4 for proper step sequence
Stepper myStepper(stepsPerRevolution, 8, 10, 9, 11);

void setup() {
  // Nothing to do (Stepper library sets pins as outputs)
}

void loop() {
  // Rotate CW slowly at 5 RPM
  myStepper.setSpeed(5);
  myStepper.step(stepsPerRevolution);
  delay(1000);

  // Rotate CCW quickly at 10 RPM
  myStepper.setSpeed(10);
  myStepper.step(-stepsPerRevolution);
  delay(1000);
}
```

---

### DHT Sensor

```cpp
#include <dht.h>    // include library

#define outPin 7    // Define pin number to which the sensor is connected

// Creates a DHT object
dht DHT;

void setup() {
  Serial.begin(9600);
}

void loop() {
  int readData = DHT.read11(outPin);

  float t = DHT.temperature;  // Read temperature
  float h = DHT.humidity;     // Read humidity

  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.print("°C  ");
  Serial.print((t * 9.0) / 5.0 + 32.0);
  Serial.println("°F");

  Serial.print("Humidity = ");
  Serial.print(h);
  Serial.println("%");
  Serial.println(" ");

  delay(1000); // wait one second
}
```
