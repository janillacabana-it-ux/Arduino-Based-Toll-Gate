
#include <SPI.h>
#include <MFRC522.h>
#include <Servo.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

#define SS_PIN 10
#define RST_PIN 9
MFRC522 rfid(SS_PIN, RST_PIN);

Servo gateServo;
LiquidCrystal_I2C lcd(0x27, 16, 2);

#define buzzer 6
#define servoPin 7

// Registered RFID UIDs
byte alonaUID[] = {0x77, 0x0A, 0x32, 0x25};
byte jukenUID[] = {0x35, 0x9C, 0x87, 0xE0};

void showWelcome() {
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Welcome to SRCB");
  lcd.setCursor(0, 1);
  lcd.print("Please scan ID");
}

boolean compareUID(byte *tagUID, byte *knownUID) {
  for (byte i = 0; i < 4; i++) {
    if (tagUID[i] != knownUID[i]) return false;
  }
  return true;
}

void setup() {
  Serial.begin(9600);
  SPI.begin();
  rfid.PCD_Init();

  pinMode(buzzer, OUTPUT);

  gateServo.attach(servoPin);
  gateServo.write(0);

  lcd.init();
  lcd.backlight();

  showWelcome();
}

void loop() {
  if (!rfid.PICC_IsNewCardPresent()) return;
  if (!rfid.PICC_ReadCardSerial()) return;

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Welcome!");

  if (compareUID(rfid.uid.uidByte, alonaUID)) {
    lcd.setCursor(0, 1);
    lcd.print("Alona Abar");
    grantAccess();
  }
  else if (compareUID(rfid.uid.uidByte, jukenUID)) {
    lcd.setCursor(0, 1);
    lcd.print("Juken Tubal");
    grantAccess();
  }
  else {
    lcd.setCursor(0, 1);
    lcd.print("Access Denied");
    digitalWrite(buzzer, HIGH);
    delay(2000);
    digitalWrite(buzzer, LOW);
    showWelcome();
  }

  rfid.PICC_HaltA();
}

void grantAccess() {
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Scan Successful");
  lcd.setCursor(0, 1);
  lcd.print("You can enter!");

  digitalWrite(buzzer, HIGH);
  gateServo.write(90);   // Open gate
  delay(4000);

  digitalWrite(buzzer, LOW);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Gate Closing...");
  gateServo.write(0);    // Close gate
  delay(2000);

  showWelcome();
}
