# Tracktire
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
long duration;
int distance; 




//setup for the basic coding of the arduino and motor control board
void setup() {
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);
    pinMode(enA, OUTPUT);
    pinMode(enB, OUTPUT);
    //making all pins on arduino uno connected to motor control pins(pinMode esatblished output and inputs)
    
    analogWrite(enA, 203);
    analogWrite(enB, 173);
    //speed control for each motor(enA and en8 are both connected to seperate motors on robot, and have different speeds so it can go forward in a straight line)
    
     pinMode(trig, OUTPUT);
   pinMode(echo, INPUT);
    //for ultra sound sensor, echo being the input of information, trigger(trig) being the output of information
    
    Serial.begin(9600);
    //Serial.begin monitors the ultra sound sensor in the front of my robot(to monitor how close it is to certain objects)
}

//looping code to go on forever(continue to keep repeating)
void loop() {
   
   
    digitalWrite(trig, LOW);
    delayMicroseconds(10);
    digitalWrite(trig, LOW);
    duration = pulseIn(echo, HIGH);
    distance = duration * 0.034/2;
    
    Serial.print("Distance");
    Serial.print(distance);
    //prints the distance of objects away from the sensor in the Monitor library tab on the left
    
    
    
    //the "if" and "else" statements below are for the ultra sound sensor to sense if there are obstacles in front of it, and if so they have to do something to get out of that sitation
   if (distance < 30) {
     Stop();
     delay(500);
     Backwards();
      delay(1000);
     TurnRight();
      (750);
     Forward();
     delay(2000);
    } 
    else {
     Forward ();
      delay(5000);
    }
}

//with the void Forward, I'm making the basic coding for the robot to go forward with digitalwrite on pins 1 and 3 going high and 2 and 4 going low
void Forward() {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, LOW);
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

//
 void Backwards () {
   digitalWrite(IN1, LOW);
   digitalWrite(IN2, HIGH);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, HIGH);
 }

