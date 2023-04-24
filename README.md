//library for servo, so we can code it to move
#include <Servo.h>

//variables made: we are linking each pin is hooked up to in the motor driver board 
int IN1 = 7;
int IN2 = 8;
int IN3 = 9;
int IN4 = 10;
//enA and enB are the speed control outputs on the motor controls
int enA = 6;
int enB = 5;
//trigger and echo are the input and output of the sensor, so we made them into pins on the arduino uno
int trig = 2;
int echo = 3;
//distance is made into a varibale with the int and duration is 
int lDist,rDist,fDist;

Servo myServo;


//setup for the basic coding of the arduino and motor control board
void setup() {
   myServo.attach(13);
    //making all pins on arduino uno connected to motor control pins(pinMode established output and inputs)
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);
    pinMode(enA, OUTPUT);
    pinMode(enB, OUTPUT);

    analogWrite(enA, 203);
    analogWrite(enB, 173);
    //speed control for each motor(enA and en8 are both connected to separate motors on robot, and have different speeds so it can go forward in a straight line)
    
     pinMode(trig, OUTPUT);
     pinMode(echo, INPUT);
    //for ultrasonic sensor, echo being the input of information, trigger(trig) being the output of information

    Serial.begin(9600);
    //Serial.begin monitors the ultrasonic sensor in the front of my robot(to monitor how close it is to certain objects)
    
}

//looping code to go on forever(continue to keep repeating)
void loop() {
  fDist = readDist();
  if (fDist > 50){
    Forward();
  }
  else {
    Stop();
    Backwards();
    chooseDir();
    }
  }
    
    
  
   
//with the void Forward, I'm making the basic coding for the robot to go forward with digitalwrite on pins 1 and 3 going high and 2 and 4 going low
void Forward() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2,HIGH);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, HIGH);
    
    
    
}

//with void Stop, digitalwrite controls the motors and makes it completely stop with all the pins being on LOW
void Stop() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, LOW);
}

//with void TurnLeft, digitalwrite controls the motors and makes it turn to the left by having IN1 and IN4 going LOW, and IN2 and IN3 going HIGH
  void TurnLeft() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, HIGH);
    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, LOW);
}

//with void TurnRight, digitalwrite controls the motors directions by making it go right by making each pin go low or high(seen down below)
void TurnRight() {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, HIGH);
}

//with void Backwards, digitalwrite controls the motors directions by making it go backwards by making each pin go low or high(down below in coding)
 void Backwards () {
   digitalWrite(IN1, HIGH);
   digitalWrite(IN2, LOW);
   digitalWrite(IN3, HIGH);
   digitalWrite(IN4, LOW);
 }
 
 int readDist(){
  int distance;
  long duration;
  //trig variable set to low, with waiting 0.010 miliseconds
  digitalWrite(trig, LOW);
  delayMicroseconds(10);
  digitalWrite(trig, LOW);
  
  //echo set to high and measuring the duration of the pulse through the echo pin
  duration = pulseIn(echo, HIGH);
  
  // Calculate the distance in centimeters based on the duration
  // The speed of sound is assumed to be 34,000 cm/s, and we divide by 2
  // since the sound wave travels to the object and back to the sensor
  distance = duration * 0.034/2;
  return distance;
 }
 
 void chooseDir(){
   myServo.write(0);
   delay(1000);
   lDist = readDist();
   delay(100);
   myServo.write(180);
   delay(1000);
   rDist = readDist();
   delay(100);
   myServo.write(90);
   delay(1000);
   if (lDist > rDist){
     TurnLeft();
   }
   else {TurnRight();}
 }

