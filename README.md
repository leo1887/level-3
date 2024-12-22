#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

// Display-Konfiguration
#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET -1 // Reset-Pin (nicht benötigt bei I2C)
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

void setup() {
  // Initialisierung des Displays
  if (!display.begin(SSD1306_PAGEADDR, 0x3C)) { // Standard I2C-Adresse
    Serial.begin(9600);
    delay(500);
    Serial.println(F("Serial connection started!"));

    Serial.println(F("SSD1306-Display konnte nicht initialisiert werden!"));
    for (;;);
  }

  display.clearDisplay();
  drawStepByStepNikolausHaus();  // Zeichnet das Haus schrittweise
}

void loop() {
  // Keine kontinuierliche Logik erforderlich
}

void drawStepByStepNikolausHaus() {
  // Hausgröße
  int width = 30; // Breite des Hauses
  int height = 20; // Höhe des Hauses
  
  // Berechnung der Verschiebung, um das Haus zu zentrieren
  int centerX = SCREEN_WIDTH / 2;
  int centerY = SCREEN_HEIGHT / 2;

  // Verschieben des Hauses weiter nach unten (doppelter Wert)
  int startX = centerX - width / 2; // Start X Koordinate des Hauses
  int startY = centerY + height / 2 + 20; // Start Y Koordinate des Hauses (doppelt nach unten verschoben)

  // Schritt 1: Boden von rechts nach links
  display.drawLine(startX + width, startY, startX, startY, SSD1306_WHITE);
  display.display();  // Anzeige aktualisieren
  delay(700); // Verzögerung zwischen den Linien (0,7 Sekunden)

  // Schritt 2: Linke Kante von unten nach oben
  display.drawLine(startX, startY, startX, startY - height, SSD1306_WHITE);
  display.display();  // Anzeige aktualisieren
  delay(700); // Verzögerung zwischen den Linien

  // Schritt 3: Obere Kante von links nach rechts
  display.drawLine(startX, startY - height, startX + width, startY - height, SSD1306_WHITE);
  display.display();  // Anzeige aktualisieren
  delay(700); // Verzögerung zwischen den Linien

  // Schritt 4: Rechte Dachhälfte von oben nach unten
  display.drawLine(startX + width / 2, startY - height - 10, startX + width, startY - height, SSD1306_WHITE);
  display.display();  // Anzeige aktualisieren
  delay(700); // Verzögerung zwischen den Linien

  // Schritt 5: Linke Dachhälfte von unten nach oben
  display.drawLine(startX, startY - height, startX + width / 2, startY - height - 10, SSD1306_WHITE);
  display.display();  // Anzeige aktualisieren
  delay(700); // Verzögerung zwischen den Linien

  // Schritt 6: Diagonale links oben nach rechts unten
  display.drawLine(startX, startY - height, startX + width, startY, SSD1306_WHITE);
  display.display();  // Anzeige aktualisieren
  delay(700); // Verzögerung zwischen den Linien

  // Schritt 7: Rechte Kante von unten nach oben
  display.drawLine(startX + width, startY, startX + width, startY - height, SSD1306_WHITE);
  display.display();  // Anzeige aktualisieren
  delay(700); // Verzögerung zwischen den Linien

  // Schritt 8: Diagonale von rechts oben nach links unten
  display.drawLine(startX + width, startY - height, startX, startY, SSD1306_WHITE);
  display.display();  // Anzeige aktualisieren
  delay(700); // Verzögerung zwischen den Linien
}


