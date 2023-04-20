#include <Servo.h>
//

//
int IN1 = 7;
int IN2 = 8;
int IN3 = 9;
int IN4 = 10;

//
int enA = 6;
int enB = 5;

//
int trig = 2;
int echo = 3;

//
long duration;
int distance; 

Servo myservo;


//
void setup() {
   myservo.attach(13);
    //
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);
    pinMode(enA, OUTPUT);
    pinMode(enB, OUTPUT);
    //
    
    analogWrite(enA, 203);
    analogWrite(enB, 173);
    //
    
     pinMode(trig, OUTPUT);
     pinMode(echo, INPUT);
    //
    
   
    
    Serial.begin(9600);
    //
}

//
void loop() {
   
   
    digitalWrite(trig, LOW);
    delayMicroseconds(10);
    digitalWrite(trig, LOW);
    duration = pulseIn(echo, HIGH);
    distance = duration * 0.034/2;
    
    Serial.print("Distance");
    Serial.print(distance);
    //
    
    
    
  
   
//
void Forward() {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, LOW);
    
    
    
}

//
void Stop() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, LOW);
}

//
  void TurnLeft() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, HIGH);
    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, LOW);
}

//
void TurnRight() {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, HIGH);
}

//
 void Backwards () {
   digitalWrite(IN1, LOW);
   digitalWrite(IN2, HIGH);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, HIGH);
 }

