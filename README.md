# CIRCUIT-INNOVATORS
SPARK-A-THON
#include <LiquidCrystal.h>
LiquidCrystal lcd(12,11,5,4,3,2);
void setup()
{
  Serial.begin(9600);
  lcd.begin(16,2);
}
void loop()
{
  //water temperature
  pinMode(14, INPUT);
  float sig;
  sig =analogRead(14);
  float voltage=((sig-0.5)/1024)*5;
  float temp =voltage*100;
 
  delay(500);
  //temperature end
  
  //turbidity of water
  pinMode(15, INPUT);
  int turbidity;
  int turl;
  turbidity=analogRead(A1);
  turl= map(turbidity,0,471,0,5);
  delay(500);
  //turbidity end
  
  //TDS sensor as potentiometer
  pinMode(16,INPUT);
  int TDS;
  int TDS1;
  TDS=analogRead(A2);
  TDS1=map(TDS,0,1023,0,2000);
  delay(500);
  //TDS sensor end
  
  //PH sensor replaced by potentiometer
  pinMode(17,INPUT);
  float PH;
  float PH1;
  PH=analogRead(A3);
  PH1=map(PH,0,1023,0,14);
  delay(500);
  //PH sensor end
  
  //IR Sensor
  pinMode(18, INPUT);
  float signal;
  signal = analogRead(A4);
  
  //IR end
  
  Serial.print("temperature:"); 
  Serial.println(temp);
  Serial.print("TURBIDITY:"); 
  Serial.println(turl);
  Serial.print("TDS:");
  Serial.println(TDS1);
  Serial.print("PH:");
  Serial.println(PH1);
  Serial.print("colour:");
  Serial.println(signal);
  //LCD for drinking use
  pinMode(6,INPUT);
  int dis;
  dis=digitalRead(6);
  if (dis==LOW)
  {
    if (turl>=4 && TDS<600 && (PH1>=6.5 && PH1<7.2))
    {
      
      
   lcd.setCursor(1,0);
      lcd.print("Safe to use");
      Serial.println("Safe to Use");
    }
      else
      {       
      
   lcd.setCursor(1,0);
      lcd.print("Dangerous");
      Serial.println("Dangerous");
        delay(1000);
      }
    
  }
      dis=digitalRead(6);
      if (dis==HIGH)
      {
        //LCD display for temperature
       lcd.setCursor(1,0); lcd.print("TEMPERATURE");
       lcd.setCursor(3,1); lcd.print(temp);
        delay(1000);
        lcd.clear();
        //LCD display for Turbidity
   lcd.setCursor(1,0); lcd.print("TURB");
    lcd.setCursor(7,0); lcd.print(turl);
        delay(500);
        lcd.clear();
         //LCD display for pH
         lcd.setCursor(1,0); lcd.print("PH");
         lcd.setCursor(7,0); lcd.print(PH1);
         delay(500);
         lcd.clear();
        
  //LCD display for TDS
   lcd.setCursor(1,0); lcd.print("TDS");
    lcd.setCursor(7,0); lcd.print(TDS1);
        delay(500);
        lcd.clear();
          
  if (signal>=0 && signal <=512){
    lcd.setCursor(1,0); lcd.print("black water");
       
  }
  else{
    lcd.setCursor(1,0); lcd.print("trans water");
   delay(500);
    lcd.clear();
  }
       
   }

}
   
