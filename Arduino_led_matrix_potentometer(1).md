//top row is row0 ; leftmost column is col0
int ROW[]={13,12,11,10};
int COL[]={7,5,4,3};

void setup(){
  for(int i=0;i<4;i++){
    pinMode(ROW[i],OUTPUT);
    pinMode(COL[i],OUTPUT);}}
void loop(){
  for(int i=0;i<4;i++){
    digitalWrite(ROW[i],HIGH);
    digitalWrite(COL[i],LOW);}
  int potent= analogRead(A1);
  int array[16];
  for (int i=0;i<=1024;i+=64){
    array[i/64]=i;}
  for(int j=0;j<1024/16;j++){
    if (array[j]>potent){
      int row=(j-1)/4;//takes the largest element smaller than potent
      int col=(j-1)%4;
      digitalWrite(ROW[row],LOW);
      digitalWrite(COL[col],HIGH);
      break;}}
