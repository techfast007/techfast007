//code for covi bot
#include <Servo.h>
Servo myservo;
const int in1 = 2;
const int in2 = 4;
const int in3 = 5;
const int in4 = 7;
int LEFTsensor = A1;
int RIGHTsensor = A3;
#define en1 3
#define en2 6
int i = 0;
int M1_Speed = 150; // speed of motor 1
int M2_Speed = 150; // speed of motor 2
const int pushbutton = 8;
const int buzzer = 9;
void setup() {
 myservo.attach(12);
 Serial.begin(9600);
 pinMode(en1, OUTPUT);
 pinMode(en2, OUTPUT);
 pinMode (in1, OUTPUT);
 pinMode (in2, OUTPUT);
 pinMode (in3, OUTPUT);
 pinMode (in4, OUTPUT);
 pinMode(RIGHTsensor, INPUT);
 pinMode(LEFTsensor, INPUT);
 pinMode(pushbutton, INPUT);
 pinMode(buzzer, OUTPUT);
 myservo.write(0);
}
void loop() {
 int Right_Value = digitalRead(RIGHTsensor);
 int Left_Value = digitalRead(LEFTsensor);
 Serial.print(digitalRead(pushbutton));
 if (Right_Value == 0 && Left_Value == 0)
 {
 digitalWrite(in1, HIGH);
 digitalWrite(in2, LOW);
 digitalWrite(in3, HIGH);
 digitalWrite(in4, LOW);
 analogWrite(en1, M1_Speed);
 analogWrite(en2, M2_Speed);
 digitalWrite(buzzer, LOW);
 }
 // Right Turn
 else if ((Right_Value == 1) && (Left_Value == 0))
 {
 digitalWrite(in1, HIGH);
 digitalWrite(in2, LOW);
 digitalWrite(in3, LOW);
 digitalWrite(in4, HIGH);
 analogWrite(en1, M1_Speed);
 analogWrite(en2, M2_Speed);
 digitalWrite(buzzer, LOW);
 }
 // Left Turn
 else if ((Right_Value == 0) && (Left_Value == 1))
 {
 digitalWrite(in1, LOW);
 digitalWrite(in2, HIGH);
 digitalWrite(in3, HIGH);
 digitalWrite(in4, LOW);
 analogWrite(en1, M1_Speed);
 analogWrite(en2, M2_Speed);
 digitalWrite(buzzer, LOW);
 }
 // Stop
 else if ((Right_Value == 1) && (Left_Value == 1))
 {
 digitalWrite(in1, LOW);
 digitalWrite(in2, LOW);
 digitalWrite(in3, LOW);
 digitalWrite(in4, LOW);
 digitalWrite(buzzer, HIGH);
 delay(500);
 digitalWrite(buzzer, LOW);
 delay(400);
 if (i == 0)
 {
 for (i = 0 ; i < 180; i++)
 {
 myservo.write(i);
 delay(10);
 }
 }
 if (digitalRead(pushbutton) == HIGH)
 {
 if (!(i == 0))
 {
 for (i = 180 ; i > -1; i--)
 {
 myservo.write(i);
 delay(17);
 }
 i = 0;
 }
 digitalWrite(in1, HIGH);
 digitalWrite(in2, LOW);
 digitalWrite(in3, HIGH);
 digitalWrite(in4, LOW);
 analogWrite(en1, M1_Speed);
 analogWrite(en2, M2_Speed);
 digitalWrite(buzzer, LOW);
 delay(400);
 }
 else
 {
 digitalWrite(buzzer, HIGH);
 delay(100);
 digitalWrite(buzzer, LOW);
 delay(60);
 digitalWrite(buzzer, HIGH);
 delay(130);
 digitalWrite(buzzer, LOW);
 delay(60);
 digitalWrite(buzzer, HIGH);
 delay(150);
 digitalWrite(buzzer, LOW);
 delay(60);
 }
 }
}
