# REPORTE-NIVEL-DE-AGUA--SENSOR-ULTRASONICO-
## USO DEL SENSOR ULTRASONICO
### Reporte: Sensor utrasónico con Tarjeta ESP32

- Introducción
El sensor ultrasónico HC-SR04 es un dispositivo capaz de medir distancias utilizando ondas de sonido de alta frecuencia. Su funcionamiento se basa en el envío de un pulso ultrasónico y la detección del eco reflejado por un objeto.
- OBJETIVO
   - Simular el funcionamiento del sensor HC-SR04 con una ESP32.
   - Medir distancias en centímetros y visualizar el resultado en el monitor serial.
   - Además, se integraron LEDs como indicadores de nivel para representar el 25%, 50%, 75% y 100% de capacidad.

- Materiales Utilizados

  1. Sensor DHT22
  2. Tarjeta ESP32
  3. LCD
  4. LED DE COLORES 
  5. WOKWI SIMULATOR (https://wokwi.com)
![](https://github.com/Mayte-10/-DHT22-CON-LCD/blob/main/WhatsApp%20Image%202025-11-30%20at%2019.54.34.jpeg)

- PROCEDIMIENTO 

- Ingresar a  WOKWI SIMULATOR y seleccionar el microcontrolador ESP32

  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2021.14.00%20(1).jpeg)
  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2020.50.01.jpeg)

- Colocar el sensor ultrasonico y la LCD
- Realizar la conexión correspondiente
  
  ![]( )

- Colocar el siguiente código
  
```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
 //Pin digital 2 para el Trigger del sensor
const int Trigger = 4;
 //Pin digital 3 para el Echo del sensor
const int Echo = 15;
//Pin leds nivel  
const int led1 = 19;
const int led2 = 18;
const int led3 = 5;
const int led4 = 17;

long duration;
int distance;
int safetyDistance;
int porcentaje;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);
  pinMode(Trigger, OUTPUT);
  pinMode(Echo, INPUT);

  digitalWrite(Trigger, LOW);

  lcd.init();
  lcd.backlight();

  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);
}

void loop() {

  digitalWrite(Trigger, LOW);
  delayMicroseconds(2);

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trigger, LOW);

  duration = pulseIn(Echo, HIGH);

  distance = duration * 0.034 / 2;
  safetyDistance = distance;


  // CALCULO DE PORCENTAJE DE NIVEL
  
  if (safetyDistance >= 300 && safetyDistance <= 400) {
    porcentaje = 25;
  }
  else if (safetyDistance >= 200 && safetyDistance <= 299) {
    porcentaje = 50;
  }
  else if (safetyDistance >= 100 && safetyDistance <= 199) {
    porcentaje = 75;
  }
  else {
    porcentaje = 100;
  }

  //   LEDS SEGÚN NIVEL
  digitalWrite(led1, porcentaje >= 25 ? HIGH : LOW);
  digitalWrite(led2, porcentaje >= 50 ? HIGH : LOW);
  digitalWrite(led3, porcentaje >= 75 ? HIGH : LOW);
  digitalWrite(led4, porcentaje >= 100 ? HIGH : LOW);

  // MENSAJES EN LCD
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("BIENVENIDOS");
  lcd.setCursor(0, 1);
  lcd.print("MODULO 05");
  delay(1500);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Mayte Torres");
  lcd.setCursor(0, 1);
  lcd.print("Nivel Agua");
  delay(1500);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: ");
  lcd.print(distance);
  lcd.print("cm");

  lcd.setCursor(0, 1);
  lcd.print("Nivel: ");
  lcd.print(porcentaje);
  lcd.print("%");

  // Serial monitor
  Serial.print("Distancia: ");
  Serial.print(distance);
  Serial.print(" cm | Nivel: ");
  Serial.print(porcentaje);
  Serial.println("%");

  delay(2000);
}

```
ADJUNTAR LAS LIBRERÍAS CORRESPONDIENTES 
![](https://github.com/Mayte-10/REPORTE-SENSOR-ULTRASONICO-/blob/main/LIBRERIAS.PNG)
- COMPILAR
![]( )
  
- FUNCIONAMIENTO 
En la simulación de Wokwi se observa:
La pantalla LCD actualiza la distancia.
El sensor ultrasónico responde correctamente cuando se modifica la distancia en el simulador.
El HC-SR04 opera mediante dos pines principales:
- Trigger (TRIG): Genera un pulso de 10 µs para iniciar la medición.
- Echo (ECHO): Recibe el eco y regresa un pulso proporcional al tiempo de viaje.

  ![]( )
   ![]( )
   ![]( )
   ![]( )


Realizó
Mayte Torres 
