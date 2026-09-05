# Sensor HC‑SR04 + Heltec LoRa 32 V3 → The Things Network


---

## Descripción general

Este repositorio contiene el **firmware completo** para un nodo LoRaWAN basado en la placa **Heltec WiFi LoRa 32 V3** (ESP32‑S3 + SX1262). El sistema adquiere mediciones de distancia desde un sensor ultrasónico **HC‑SR04** y las transmite de forma inalámbrica al servidor de **The Things Network (TTN)**.

---

## Hardware utilizado

| Componente | Modelo / Especificación |
| :--- | :--- |
| Placa de desarrollo | Heltec WiFi LoRa 32 V3 (ESP32‑S3) |
| Chip LoRa | SX1262 |
| Sensor ultrasónico | HC‑SR04 |
| Resistencias | 1 kΩ y 2 kΩ (para divisor de tensión) |

---

## Esquema de conexiones

| Pin del sensor | Pin del ESP32‑S3 | Observación |
| :--- | :--- | :--- |
| **VCC** | Pin **5V** | Alimentación directa desde la placa |
| **GND** | **GND** | Conexión a tierra común |
| **TRIG** | **GPIO 41** | Conexión directa (salida digital a 3.3 V) |
| **ECHO** | **GPIO 42** | Conexión mediante **divisor de tensión** (ver más abajo) |

---

## ⚠️ División de tensión para el pin ECHO

El pin **ECHO** del HC‑SR04 genera pulsos de **5 V** al detectar el retorno de la señal ultrasónica. Los pines del ESP32‑S3 solo soportan **3.3 V** como máximo; una conexión directa dañaría irreversiblemente el microcontrolador.

Para resolverlo se implementó un **divisor de tensión resistivo pasivo**:
