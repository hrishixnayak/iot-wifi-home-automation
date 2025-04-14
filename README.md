// 🔹 Blynk Template Info (replace with your actual values)
#define BLYNK_TEMPLATE_ID "TMPL3lXbVhKeU"
#define BLYNK_TEMPLATE_NAME "Home Automation"
#define BLYNK_AUTH_TOKEN "tsbSOm1Fp1sUireXSL4cQmV0nAeixioc"

// 🔹 Include Libraries
#include <WiFi.h>
#include <WiFiClient.h>
#include <BlynkSimpleEsp32.h>

// 🔹 Wi-Fi Credentials
const char* ssid = "IC_IITP";        
const char* password = "iciitp@9911";

// 🔹 LED Pins
const int ledPins[] = {18, 19, 22, 23};  
const int numLeds = 4;

// 🔹 Setup
void setup() {
  Serial.begin(115200);
  delay(100);

  Serial.println("🔌 Booting...");
  Serial.println("Setting up LED pins...");

  for (int i = 0; i < numLeds; i++) {
    pinMode(ledPins[i], OUTPUT);
    digitalWrite(ledPins[i], LOW);  // Turn OFF all LEDs initially
  }

  Serial.print("📶 Connecting to Wi-Fi: ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("\n✅ Wi-Fi Connected!");
  Serial.print("📡 ESP32 IP Address: ");
  Serial.println(WiFi.localIP());

  // 🔹 Connect to Blynk
  Blynk.config(BLYNK_AUTH_TOKEN);
  Blynk.connect();
}

// 🔄 Loop
void loop() {
  Blynk.run();
}

// 🔹 Blynk LED Control
BLYNK_WRITE(V1) {
  int value = param.asInt();
  digitalWrite(ledPins[0], value);
  Serial.print("🔴 LED 1 (GPIO 18) = ");
  Serial.println(value);
}

BLYNK_WRITE(V2) {
  int value = param.asInt();
  digitalWrite(ledPins[1], value);
  Serial.print("🟠 LED 2 (GPIO 19) = ");
  Serial.println(value);
}

BLYNK_WRITE(V3) {
  int value = param.asInt();
  digitalWrite(ledPins[2], value);
  Serial.print("🟢 LED 3 (GPIO 22) = ");
  Serial.println(value);
}

BLYNK_WRITE(V4) {
  int value = param.asInt();
  digitalWrite(ledPins[3], value);
  Serial.print("🔵 LED 4 (GPIO 23) = ");
  Serial.println(value);
}
