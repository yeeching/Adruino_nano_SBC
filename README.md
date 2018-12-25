# Adruino_nano_SBC
Using Arduino nano SBC with IBT-2 motor driver to control DC Motor
/*........................
  BTS7960 Motor Driver Test
  Written By :Yeeching Lee
  Code for :

      File Name: IBT-2-003
  File location: D:/2018-06DOC/Arduino/IBT-2-003
           Date: 2018-12-24
        Version: 001
         Author: Yeeching Lee
         
    Description: IBT-2 Motor Control Board driven by Nano Arduino.  
IBT-2 Driver Pin Assignment:
    1: RPWM : Clockwise PWM Signal
    2: LPWM : Count clockwise PWM Signal
    3: R_En : Enable ("Active High")
    4: L_En : Enable ("Active High")
    5: R_IS : Current Sense
    6: L_IS : Current Sense
    7: Vcc  : +5VDC in
    8: Gnd  : Gnd

LPWM input PWM signal or "H", Motor run clockwise
RPWM input PWM signal or "H", Motor run count clockwise  
  
*/
int RPWM=5;  // Turn Right (clockwise) control PWM pin
int LPWM=6;  // Turn Left (count clockwise) control PWM pin

int R_EN=7;  // Right Enable pin
int L_EN=8;  // Left Enable pin

void setup() {
  for(int i=5;i<9;i++){   // DO pin 5 ~ pin 8 set to OUTPUT
   pinMode(i,OUTPUT);
  }
   for(int i=5;i<9;i++){
   digitalWrite(i,LOW);  // disable D5 ~ D8
   Serial.println(" === MOTOR STOP  ===");
  }
   delay(1000);
   Serial.begin(9600);  // For debug display purpose
  }
void loop() {
  Serial.println(" ----------------------------------------------- ");
  Serial.println("  ====== MOTOR READY TO RUN ======");
  Serial.println(" ----------------------------------------------- ");
  Serial.println();
  digitalWrite(R_EN,HIGH);  // Enable
  digitalWrite(L_EN,HIGH);
delay(500);


// Turn Right
 Serial.println();
 Serial.println(" ----Motor Turn Clockwise  --- ");
 Serial.println();
for(int i=0;i<255;i=i+5){
  Serial.print(" 01  Turn Clockwise Speed Up +++ : ");

  Serial.print(" i=");Serial.println(i);
  digitalWrite(R_EN,HIGH);  // Enable
  digitalWrite(L_EN,HIGH);
  analogWrite(LPWM,i);
  analogWrite(RPWM,0);
  delay(100);
}
 Serial.println(" --------------------------------- ");
 Serial.println();
delay(500);

for(int i=255;i>0;i=i-5){
  Serial.print(" 02   Turn Clockwise Speed Down --- : ");
  Serial.print(" i=");Serial.println(i);
  digitalWrite(R_EN,HIGH);  // Enable
  digitalWrite(L_EN,HIGH);
  analogWrite(LPWM,i);
  analogWrite(RPWM,0);
  
  delay(100);
}
delay(500);

// Disable All
  Serial.println("=== Motor disable : STOP ====");
  digitalWrite(R_EN,LOW);
  digitalWrite(L_EN,LOW);

  delay(500);
  Serial.println("=== Motor enable : Ready to run ====");
  digitalWrite(R_EN,HIGH);  // Enable
  digitalWrite(L_EN,HIGH);

delay(1000);

// Turn Left
  Serial.println();
  Serial.println(" --------------------------------- ");
 Serial.println();
for(int i=0;i<255;i=i+5){
  Serial.print(" 03 Turn Count ClockWise Speed Up +++: ");
   Serial.print(" i=");Serial.println(i);
  digitalWrite(R_EN,HIGH);  // Enable
  digitalWrite(L_EN,HIGH);
  analogWrite(RPWM,i);
  analogWrite(LPWM,0);
  delay(100);
}
 Serial.println(" --------------------------------- ");
 Serial.println();
delay(500);
for(int i=255;i>0;i=i-5){
  Serial.print(" 04 Turn Count ClockWise Speed Down ---: ");
   Serial.print(" i=");Serial.println(i);
  digitalWrite(R_EN,HIGH);  // Enable
  digitalWrite(L_EN,HIGH);
  analogWrite(RPWM,i);
  analogWrite(LPWM,0);
  delay(100);
}

delay(1000);
 Serial.println();
 Serial.println(" --------------------------------- ");
 Serial.println(" ............ next run ........... ");
 Serial.println();
}
