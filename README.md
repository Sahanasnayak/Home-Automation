# Home-Automation
Using Bluetooth module(HC-05) and AMR voice app, different loads are turned ON/OFF on voice command.
code:The code is developed in Arduino IDE
#include<SoftwareSerial.h>
int led1=3;
int led2=4;
const int txpin=1;
const int rxpin=0;
String readmsg;
//char c;
SoftwareSerial BT(rxpin,txpin);
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
   BT.begin(9600);
   pinMode(led1,OUTPUT);//TV
  pinMode(led2,OUTPUT);//AC
  
   
}

void loop() {
  // put your main code here, to run repeatedly:
  while(BT.available()){
  delay(10);
   char c=BT.read();
  readmsg+=c;
  }
  if(readmsg.length()>0){
if(readmsg=="*TV#"){
  digitalWrite(led1,HIGH);
  digitalWrite(led2,LOW);
  delay(100);
      Serial.println("TV is on");
    }
    else if(readmsg=="*AC#"){
   digitalWrite(led2,HIGH);
   digitalWrite(led1,LOW);
   delay(100);
    Serial.println("AC is on");
   }
   else if(readmsg=="*bye#"){
     Serial.println("power saving mode");
    digitalWrite(led2,HIGH); 
    digitalWrite(led1,HIGH); 
    delay(100);
    }
  
    Serial.println(readmsg);
    readmsg="";

}
}
