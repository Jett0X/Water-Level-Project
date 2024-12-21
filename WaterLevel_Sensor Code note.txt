//Arduino water level sensor code
// Sensor pins pin D6 LED output, pin A0 analog Input
//Arduino water level sensor code
#include <LiquidCrystal_I2C.h> // Library for LCD
LiquidCrystal_I2C lcd(0x27, 16, 2); // I2C address 0x27, 16 column and 2 rows

#include <math.h>

#define sensorPin A0
#define lowOutput  2       ////Inputing Variables
#define mediumOutput  3
#define highOutput  4

void setup() {
  Serial.begin(9600);
  pinMode(lowOutput , OUTPUT);
  pinMode(mediumOutput , OUTPUT);
  pinMode(highOutput , OUTPUT);              //// Function all the
  digitalWrite(lowOutput, LOW);               ///  Components
  digitalWrite(mediumOutput, LOW);
  digitalWrite(highOutput, LOW);

  lcd.init(); // initialize the lcd
  lcd.backlight();
}
void loop() {
  int sensorValue = analogRead(sensorPin);

  if (280 > sensorValue) {        ///Value of normal Water Level
    digitalWrite(lowOutput, HIGH);
    digitalWrite(highOutput, LOW);   ///Functions of the Water Level
    digitalWrite(mediumOutput, LOW);
    Serial.print("\nFlow Velocity of the River: 60.39111971");   ///Inputing the Eq'n of the Formula
    //LCD write
    lcd.setCursor(0, 0);         // move cursor to   (0, 0)
    lcd.print(" Flow Velocity:");        // print message at (0, 0)
    lcd.setCursor(0, 1);
    lcd.print(" 60.39111971");        // print message at (0, 0)
    delay(150);

  }  else if (564 > sensorValue) {    ///Value of Half of the river Water Level/Blue
    digitalWrite(mediumOutput, HIGH);
    digitalWrite(highOutput, LOW);
    digitalWrite(lowOutput, LOW);
    Serial.print("\nFlow Velocity of the River: 64.25657553");   ///Inputing the Eq'n of the Formula
    //LCD write
    lcd.backlight(); //open the backlight 
    lcd.setCursor(0, 0);         // move cursor to   (0, 0)
    lcd.print(" Velocity of the River:");        // print message at (0, 0)
    lcd.setCursor(0, 1); 
    lcd.print(" 64.25657553");        // print message at (0, 0)
    delay(150);

  } else if (640 > sensorValue) {  //Full Value of the Water Level/RED
    digitalWrite(highOutput, HIGH);
    digitalWrite(mediumOutput, LOW);
    digitalWrite(lowOutput, LOW);
    Serial.print("\nFlow Velocity of the River: 71.18277757");    ///Inputing the Eq'n of the Formula
    //LCD write
    lcd.backlight(); //open the backlight 
    lcd.setCursor(0, 0);         // move cursor to   (0, 0)
    lcd.print(" Velocity of the River:");        // print message at (0, 0)
    lcd.setCursor(0, 1); 
    lcd.print(" 71.18277757");        // print message at (0, 0)
    delay(150);
  } else {
    digitalWrite(highOutput, LOW);
    digitalWrite(mediumOutput, LOW);  /// Ouput of the Sensor
    digitalWrite(lowOutput, LOW);
  }
  delay(100);

}
