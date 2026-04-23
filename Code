#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,16,2);

// Pin
#define BTN_ONOFF 2
#define BTN_EMG   3
#define POT_PIN   A0

#define ENA 5
#define IN1 6
#define IN2 7

// Status
bool motorState = false;
bool emergency = false;

int speedPWM = 0;

// Debounce
unsigned long lastBtn1 = 0;
unsigned long lastBtn2 = 0;
const int debounce = 200;

// Timer
unsigned long startRun = 0;
unsigned long runTime = 0;

void setup() {
  pinMode(BTN_ONOFF, INPUT_PULLUP);
  pinMode(BTN_EMG, INPUT_PULLUP);

  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);

  lcd.init();
  lcd.backlight();

  stopMotor();
}

void loop() {

  // ===== BUTTON ON/OFF =====
  if(digitalRead(BTN_ONOFF) == LOW && millis() - lastBtn1 > debounce){
    lastBtn1 = millis();

    if(!emergency){
      motorState = !motorState;

      if(motorState){
        startRun = millis() - runTime;
      } else {
        stopMotor();
      }
    }
  }

  // ===== BUTTON EMERGENCY =====
  if(digitalRead(BTN_EMG) == LOW && millis() - lastBtn2 > debounce){
    lastBtn2 = millis();

    emergency = !emergency;

    if(emergency){
      motorState = false;
      runTime = 0;
      stopMotor();
    }
  }

  // ===== MOTOR CONTROL =====
  if(motorState && !emergency){
    int adc = analogRead(POT_PIN);

    speedPWM = map(adc,0,1023,80,255);

    analogWrite(ENA, speedPWM);
    digitalWrite(IN1,HIGH);
    digitalWrite(IN2,LOW);

    runTime = millis() - startRun;
  }
  else{
    speedPWM = 0;
    stopMotor();
  }

  displayLCD();
}

// =======================
void stopMotor(){
  analogWrite(ENA,0);
  digitalWrite(IN1,LOW);
  digitalWrite(IN2,LOW);
}

// =======================
void displayLCD(){

  lcd.setCursor(0,0);

  if(motorState) lcd.print("ON ");
  else           lcd.print("OFF");

  lcd.setCursor(5,0);
  if(emergency) lcd.print("EMG:ON ");
  else          lcd.print("EMG:OFF");

  lcd.setCursor(0,1);
  lcd.print("S:");

  if(speedPWM < 100) lcd.print("0");
  if(speedPWM < 10) lcd.print("0");
  lcd.print(speedPWM);

  lcd.print(" ");

  lcd.print("T:");
  lcd.print(runTime/1000);
  lcd.print("s   ");
}
