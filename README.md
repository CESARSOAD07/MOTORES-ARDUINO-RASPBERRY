# MOTORES-ARDUINO-RASPBERRY

RASPBERRY

import serial
import time

ser = serial.Serial("/dev/ttyACM0", 9600, timeout = 1)

def driveMotor(drct1, drct2):
    valList = [str(drct1), str(drct2)]
    sendStr = ','.join(valList)
    ser.write(sendStr.encode('utf-8'))
    time.sleep(0.1)

while 1:
        print("Direccion1 = ")
        drct1 = input()
        print("Direccion2 = ")
        drct2 = input()

        driveMotor(drct1,drct2)
        
     
  ARDUINO
  
  int in1 = 5;
int in2 = 4;
int in3 = 3;
int in4 = 2;
int drct1Val, drct2Val;

void setup() {
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);

  Serial.begin(9600);

}

void loop() {
  while(!Serial.available() > 0){}
  if(Serial.available() > 0){
    drct1Val = Serial.parseInt();
    drct2Val = Serial.parseInt();
  }
  if(drct1Val == 1 && drct2Val == 1){
    Motor1a();
    Motor2a();
  }

  if(drct1Val == 1 && drct2Val == 0){
    Motor1a();
    Apagado2();
  }

  if(drct1Val == 1 && drct2Val == -1){
    Motor1a();
    Motor2b();
  }

  if(drct1Val == -1 && drct2Val == 1){
    Motor1b();
    Motor2a();
   }

  if(drct1Val == -1 && drct2Val == 0){
    Motor1b();
    Apagado2();
   }  

  if(drct1Val == -1 && drct2Val == -1){
    Motor1b();
    Motor2b();
   }  

  if(drct1Val == 0 && drct2Val == 1){
    Apagado1();
    Motor2a();
   }  

  if(drct1Val == 0 && drct2Val == 0){
    Apagado1();
    Apagado2();
   }  
}

void Motor1a(){
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);
  }

void Motor1b(){
  digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
  }  

void Motor2a(){
  digitalWrite(in3, HIGH);
  digitalWrite(in4, LOW);
  }

void Motor2b(){
  digitalWrite(in3, LOW);
  digitalWrite(in4, HIGH);
  }

void Apagado1(){
  digitalWrite(in1, LOW);
  digitalWrite(in2, LOW);
  }  

void Apagado2(){
  digitalWrite(in3, LOW);
  digitalWrite(in4, LOW);
  }  
