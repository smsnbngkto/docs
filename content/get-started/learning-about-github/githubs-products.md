
#include <SoftwareSerial.h> 
SoftwareSerial module_bluetooth(0, 1); // pin RX | TX
char data = 0;             
#define enA 3
#define in1 4
#define in2 5
#define enB 11
#define in3 13
#define in4 12
int motorSpeedA = 0;
int motorSpeedB = 0;
int state;
int Speed = 130; 



void setup() 
{
  Serial.begin(38400);         
  pinMode(enA, OUTPUT);
  pinMode(enB, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
}
void loop()
{
  if(Serial.available() > 0)  
  {
    data = Serial.read();Serial.print(data);    //Pembacaan dan ditampilkan data yang masuk   
    Serial.print("\n");
state = Serial.read();      
if(state > 10){Speed = state;
}

     
   // //Kondisi Data yang masuk      
    if(data == 'B'){
    motorSpeedA = 150; //Pengatur kecepatan motor; 0-255
    motorSpeedB = 150; //Pengatur kecepatan motor; 0-255
    analogWrite(enA, state); // Send PWM signal to motor A
    analogWrite(enB, state); // Send PWM signal to motor B
    // Set Motor A backward
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    // Set Motor B backward
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);
    
    }
    else if(data == 'F'){      
    motorSpeedA = 150; //Pengatur kecepatan motor; 0-255
    motorSpeedB = 150; //Pengatur kecepatan motor; 0-255
    analogWrite(enA, state); // Send PWM signal to motor A
    analogWrite(enB, state); // Send PWM signal to motor B
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    // Set Motor B forward
    digitalWrite(in3, LOW);
    digitalWrite(in4, HIGH);
    }
    else if(data == 'R'){      
    motorSpeedA = 80; //Pengatur kecepatan motor; 0-255
    motorSpeedB = 80; //Pengatur kecepatan motor; 0-255
    analogWrite(enA, state); // Send PWM signal to motor A
    analogWrite(enB, state); // Send PWM signal to motor B
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    // Set Motor B RIGHT
    digitalWrite(in3, LOW);
    digitalWrite(in4, HIGH);
    }
    else if(data == 'L'){      
    motorSpeedA = 80; //Pengatur kecepatan motor; 0-255
    motorSpeedB = 80; //Pengatur kecepatan motor; 0-255
    analogWrite(enA, state); // Send PWM signal to motor A
    analogWrite(enB, state); // Send PWM signal to motor B
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    // Set Motor B LEFT
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);
    }
    else if(data == 'S'){      
    motorSpeedA = 255; //Pengatur kecepatan motor; 0-255
    motorSpeedB = 255; //Pengatur kecepatan motor; 0-255
    analogWrite(enA, state); // Send PWM signal to motor A
    analogWrite(enB, state); // Send PWM signal to motor B
    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    // Set Motor B STOP
    digitalWrite(in3, LOW);
    digitalWrite(in4, LOW);
    } 
  }                            
 
}
