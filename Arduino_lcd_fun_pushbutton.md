#include <LiquidCrystal.h>
LiquidCrystal lcd(6,7,10,11,12,13);
int push1=2;
int push2=3;
void setup(){
  lcd.begin(16,2);
  lcd.print("HI");
  delay(1000);
  pinMode(push1,INPUT_PULLUP);
  pinMode(push2,INPUT_PULLUP);
  lcd.setCursor(0,0);// this will clear what was there at 0,0 position and writes the new text; So no need to lcd.clear() but it can overwrite only if new text is longer.
   //if not then the old text will still pertain after the new text's end .
  lcd.print("Truth or Dare");
  delay(1000);// Always delay after display in lcd or else we won't see the text unless it is in infinite loop-> void loop()
}
void loop(){
  lcd.clear();
 
  if (digitalRead(push1)==0){
    lcd.print("Good move, Go");//only first 16 characters in first line
  //if more characters it won't go to next line, it just gets cut
    lcd.setCursor(0,1);
    lcd.print("eat the banana");
    delay(2000);}
  else if(digitalRead(push2)==0){
    lcd.print("what is the");
    lcd.setCursor(0,1);// first parameter is column, second one is row
    lcd.print("biggest lie of u");
    delay(2000);}
  }
  
