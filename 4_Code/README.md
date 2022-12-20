#include <LiquidCrystal.h>  
LiquidCrystal lcd(7, 6, 5, 4, 3, 2);  
const int temp=A0;  
const int GAS=A1;  
const int GAS1=A2;  
const int BUZ=11;  
float tempc=0;  
float vout=0;  
int flag=0;  
int flag1=0;  
void setup()  
{  
  pinMode(temp,INPUT); // Configuring pin A0 as input  
  pinMode(GAS,INPUT);    
  pinMode(GAS1,INPUT);      
  pinMode(BUZ, OUTPUT);  
  Serial.begin(9600);  
  lcd.begin(16, 2);  
  lcd.setCursor(0,0);  
  lcd.print("TEMPERATURE: 00C");      
  lcd.setCursor(0,1);  
  lcd.print("NO HARMFUL GASES");  
  digitalWrite(BUZ, LOW);  
  }  
void loop()  
{  
vout=analogRead(temp);  
vout=(vout*500)/1023;  
tempc=vout;  
lcd.setCursor(13,0);  
lcd.print(tempc);  
lcd.setCursor(15,0);  
lcd.print('C');  
if(tempc>=32)  
{  
  digitalWrite(BUZ, HIGH);  
}  
  if(digitalRead(GAS)==LOW)  
  {  
  lcd.setCursor(0,1);  
  lcd.print("CARBON MONOXIDE ");  
  digitalWrite(BUZ, HIGH);  
  flag=1;  
  }  
  else  
  {  
  flag=0;  
  }  
  if(digitalRead(GAS1)==HIGH)  
  {  
  lcd.setCursor(0,1);  
  lcd.print("GASES: METHANE  ");  
  digitalWrite(BUZ, HIGH);  
  flag1=1;  
  }  
  else  
  {  
  flag1=0;  
  }  
  if((flag==0)&&(flag1==0)&&(tempc<32))  
  {  
  digitalWrite(BUZ, LOW);  
  lcd.setCursor(0,1);  
  lcd.print("NO HARMFUL GASES");      
  }  
  Serial.print("TEMPERATURE:");  
  Serial.println(tempc);  
  if(flag==1)  
  {  
  Serial.println("CARBON MONOXIDE DETECTED");      
  }  
  if(flag1==1)  
  {  
  Serial.println("METHANE DETECTED");      
  }    
  if((flag==0)&&(flag1==0))  
  {  
  Serial.println("NO HARMFUL GASES");      
  }  
  delay(1000);  
  
}  
