# arduino-DEV-this

----
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,2,16);
int button =2;   // to store on or off value
int led = 13;
int buttonPC = 0;
boolean buttonPressed = false;
boolean setShowName = 0;
boolean setShowLight = 0;
void setup()
{
  
  // put your setup code here, to run once:
  pinMode(led, OUTPUT);
  pinMode(2,INPUT);
  pinMode(8,OUTPUT);
  pinMode(13,OUTPUT);
  Serial.begin(9600);

}
void loop()
{
button = digitalRead(2);

if(buttonPressed == true && button == 1){
 delay(1000);
 buttonPressed = false; 
}

if(button == 0 && buttonPressed == false){
  buttonPressed = true;
  buttonPC = buttonPC +1;
  Serial.println(buttonPC);
}

if((buttonPC >2) && (setShowLight == 0)){
 Serial.println(setShowName);
  showLight(); 
 setShowLight = true;
}

if((buttonPC > 4) && (setShowName == 0)){
    Serial.println("showName start");
    digitalWrite(13,HIGH);
  showName("david Put","000000");
  Serial.println("showName start 2");
  setShowName = 1; 
}

// laat tijd controleren
  checkTime();
}

void checkTime(){
  
}

void sendData(){
  
}

void showLight(){
  Serial.println("licht gaat aan");
  digitalWrite(8,HIGH);
}

void showName(String namePerson, String numberPerson){
  Serial.println("david start");
    Serial.println(namePerson);
  // LCD schermpje
  lcd.init();
  lcd.backlight();
  lcd.clear();  
  lcd.home();
  lcd.print(namePerson);
  lcd.setCursor(0,1);
  lcd.print(numberPerson);
    Serial.println("showName end");
}
