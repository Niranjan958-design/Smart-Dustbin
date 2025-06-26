# Project Overview

This project automates a dustbin to open the lid automatically when someone approaches using an ultrasonic sensor and servo motor.

## Aurdino code for Smart-Dustbin
#include <Servo.h>   //servo library
Servo servo;     
int trigPin = 5;    
int echoPin = 6;   
int servoPin = 7;
int led= 10;
long duration, dist, average;   
long aver[3];   //array for average


void setup() {       
    Serial.begin(9600);
    servo.attach(servoPin);  
    pinMode(trigPin, OUTPUT);  
    pinMode(echoPin, INPUT);  
    servo.write(0);         //close cap on power on
    delay(100);
    servo.detach(); 
} 

void measure() {  
 digitalWrite(10,HIGH);
digitalWrite(trigPin, LOW);
delayMicroseconds(5);
digitalWrite(trigPin, HIGH);
delayMicroseconds(15);
digitalWrite(trigPin, LOW);
pinMode(echoPin, INPUT);
duration = pulseIn(echoPin, HIGH);
dist = (duration/2) / 29.1;    //obtain distance
}
void loop() { 
  for (int i=0;i<=2;i++) {   //average distance
    measure();               
   aver[i]=dist;            
    delay(10);              //delay between measurements
  }
 dist=(aver[0]+aver[1]+aver[2])/3;    

if ( dist<50 ) {
//Change distance as per your need
 servo.attach(servoPin);
  delay(1);
 servo.write(0);  
 delay(3000);       
 servo.write(150);    
 delay(1000);
 servo.detach();      
}
Serial.print(dist);
} 
## 🧰 Components Used
- Arduino Uno
- HC-SR04 Ultrasonic Sensor
- SG90 Servo Motor
- Jumper Wires
- 9V Battery
- Breadboard

## 🔌 Circuit Connections
| Component         | Arduino Pin |
|------------------|-------------|
| Ultrasonic Trig  | 9           |
| Ultrasonic Echo  | 10          |
| Servo Signal     | 3           |
| VCC and GND      | 5V/GND      |

## 🚀 How to Run
1. Connect the circuit as per the diagram.
2. Upload the `SmartDustbin.ino` file using Arduino IDE.
3. Power the Arduino using USB or a 9V battery.

## 📄 License
This project is open-source under the MIT License.

## Circuit Diagram
https://circuitdigest.com/sites/default/files/circuitdiagram_mic/Smart-Dustbin-Circuit.jpg

