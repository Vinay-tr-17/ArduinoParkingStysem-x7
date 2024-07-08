/*#include <Servo.h>
Servo tap_servo;
int sensor_pin = 4;
int tap_servo_pin =5;
int val;
void setup(){
  pinMode(sensor_pin,INPUT);
  tap_servo.attach(tap_servo_pin);  
}
 
void loop(){
  val = digitalRead(sensor_pin);

  if (val==0)
  {tap_servo.write(0);
   delay(1000);
  }
  if (val==1)
  {tap_servo.write(180);
  
    }
}*/
/*#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
#include <Servo.h> 

// Initialize the LCD with the I2C address
// Replace the address with the correct one for your LCD module
LiquidCrystal_I2C lcd(0x27, 16, 2);  // Set the LCD address to 0x27 for a 16x2 display

Servo myservo1;

int IR1 = 2;
int IR2 = 4;

int Slot = 4;           //Enter Total number of parking Slots

int flag1 = 0;
int flag2 = 0;

void setup() {
  lcd.init();
   lcd.backlight();
  lcd.begin(16, 2);  // Initialize the LCD with 16 columns and 2 rows
  lcd.backlight();
  pinMode(IR1, INPUT);
  pinMode(IR2, INPUT);
  
  myservo1.attach(3);
  myservo1.write(100);

  lcd.setCursor (0,0);
  lcd.print("     ARDUINO    ");
  lcd.setCursor (0,1);
  lcd.print(" PARKING SYSTEM ");
  delay (2000);
  lcd.clear();  
}

void loop() { 

  if (digitalRead(IR1) == LOW && flag1 == 0) {
    if (Slot > 0) {
      flag1 = 1;
      if (flag2 == 0) {
        myservo1.write(0);
        Slot = Slot - 1;
      }
    } else {
      lcd.setCursor(0, 0);
      lcd.print("    SORRY :(    ");  
      lcd.setCursor(0, 1);
      lcd.print("  Parking Full  "); 
      delay (3000);
      lcd.clear(); 
    }
  }

  if (digitalRead(IR2) == LOW && flag2 == 0) {
    flag2 = 1;
    if (flag1 == 0) {
      myservo1.write(0);
      Slot = Slot + 1;
    }
  }

  if (flag1 == 1 && flag2 == 1) {
    delay (1000);
    myservo1.write(100);
    flag1 = 0, flag2 = 0;
  }

  lcd.setCursor(0, 0);
  lcd.print("    WELCOME!    ");
  lcd.setCursor(0, 1);
  lcd.print("Slot Left: ");
  lcd.print(Slot);
}
*/
#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
#include <Servo.h> 

// Initialize the LCD with the I2C address
// Replace the address with the correct one for your LCD module
LiquidCrystal_I2C lcd(0x27, 16, 2);  // Set the LCD address to 0x27 for a 16x2 display

Servo myservo1;

int IR1 = 2;
int IR2 = 4;

int Slot = 4;           //Enter Total number of parking Slots

int flag1 = 0;
int flag2 = 0;

void setup() {
  lcd.init();
  lcd.backlight();
  lcd.begin(16, 2);  // Initialize the LCD with 16 columns and 2 rows
  pinMode(IR1, INPUT);
  pinMode(IR2, INPUT);
  
  myservo1.attach(3); // Attach servo to pin 3
  myservo1.write(90); // Set initial position to 90 degrees
  
  lcd.setCursor (0,0);
  lcd.print("     ARDUINO    ");
  lcd.setCursor (0,1);
  lcd.print(" PARKING SYSTEM ");
  delay (2000);
  lcd.clear();  
}

void loop() { 
  if (digitalRead(IR1) == LOW && flag1 == 0) {
    if (Slot > 0) {
      flag1 = 1;
      if (flag2 == 0) {
        myservo1.write(0); // Open the barrier
        delay(3000); // Wait for 3 seconds
        Slot--; // Decrement slot count
      }
    } else {
      lcd.setCursor(0, 0);
      lcd.print("    SORRY :(    ");  
      lcd.setCursor(0, 1);
      lcd.print("  Parking Full  "); 
      delay (3000);
      lcd.clear(); 
    }
  }

  if (digitalRead(IR2) == LOW && flag2 == 0) {
    flag2 = 1;
    if (flag1 == 0) {
      myservo1.write(0); // Open the barrier
      delay(3000); // Wait for 3 seconds
      Slot++; // Increment slot count
    }
  }

  if (flag1 == 1 && flag2 == 1) {
    delay (1000);
    myservo1.write(90); // Close the barrier
    delay(1000); // Wait for 1 second
    flag1 = 0;
    flag2 = 0;
  }

  lcd.setCursor(0, 0);
  lcd.print("    WELCOME!    ");
  lcd.setCursor(0, 1);
  lcd.print("Slot Left: ");
  lcd.print(Slot);
}



Connections 
Ir 1 n = 2
Ir 2 n = 4
Sr n = 3
Sr y =5
Sr g= gnd
Ir 1 and 2 vcc = 5v
Ir 1 and 2 gnd = gnd
Lcd gnd = gnd 
Lcd vcc = 5v 
Sda = a4
Scl = a5
