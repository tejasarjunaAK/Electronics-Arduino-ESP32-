#include <Keypad.h>
#include <LiquidCrystal.h>
LiquidCrystal lcd(13,12,8,9,10,11);
char keys[4][4]={{'1','2','3','+'},{'4','5','6','-'},{'7','8','9','*'},{'C','0','=','/'}};
byte rowpins[4]={7,6,5,4};
byte colpins[4]={3,2,1,0};
float Numbers[4]={0.0,0.0,0.0,0.0};
int num_index=0;
byte row=4; //only byte works for keypad
byte col=4;//only byte is working int not working
int start=0;
float answer=0.0;
char operators[4]={0,0,0,0};
int char_index=0;
bool current_number=true;
String string ="";
bool current_char=false;
Keypad K= Keypad(makeKeymap(keys),rowpins,colpins,row,col);
void setup(){
 //I removed Serialmonitor and so no Serial.begin() as I am using 0,1 pins for lcd
  lcd.begin(16,2);
  lcd.print("calculator ready");
  delay(1000);
  lcd.clear();}
void loop(){              
  char keytouch=K.getKey();

  if ((keytouch <='9')&&(keytouch>='0')){
    if(current_number==true){
      string =string+keytouch;  
      lcd.print(keytouch);
      current_char=false;}
    
    else{
      Numbers[num_index]=string.toFloat();
      string="";
      num_index+=1;
      string=string+keytouch;
      lcd.print(keytouch);
      current_number=true;
      current_char=false;
    }}
 
   else if((keytouch=='+')||(keytouch=='-')||(keytouch=='/')||(keytouch=='*')){
    if (current_char==false){
        lcd.print(keytouch);
        current_number=false;
        operators[char_index]=keytouch;
        char_index+=1;
        current_char=true;
    }
}

  else if(keytouch=='C'){
    answer=0.0;
    num_index=0;
    char_index=0;
    string="";
    for(int h=0;h<4;h++){
      Numbers[h]=0;}
    current_number=true;
    current_char=false;
    for(int j=0;j<4;j++){
      operators[j]=0;}
    lcd.clear();}
  else if(keytouch=='='){
    Numbers[num_index]=string.toFloat();
      string="";
    
for(int i = 0; i < char_index; i++) {
    if(operators[i] == '*') {
        Numbers[i] = Numbers[i] * Numbers[i+1];
        for(int j = i+1; j < num_index; j++) Numbers[j] = Numbers[j+1];
        for(int j = i; j < char_index-1; j++) operators[j] = operators[j+1];
        num_index--;
        char_index--;
        i--; 
    }
    else if(operators[i] == '/') {
        Numbers[i] = Numbers[i] / Numbers[i+1];
        for(int j = i+1; j < num_index; j++) Numbers[j] = Numbers[j+1];
        for(int j = i; j < char_index-1; j++) operators[j] = operators[j+1];
        num_index--;
        char_index--;
        i--;
    }
}
answer = Numbers[0];
for(int i = 0; i < char_index; i++) {
  if(operators[i] == '+') {
    answer += Numbers[i+1];
  }
  else if(operators[i] == '-') {
    answer -= Numbers[i+1];
  }
}   num_index=0;// 
    char_index=0;
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print(answer);
}}
