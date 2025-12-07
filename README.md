# REPORTE-NIVEL-DE-AGUA--SENSOR-ULTRASONICO-
## USO DEL SENSOR ULTRASONICO
### Reporte: Sensor utrasónico con Tarjeta ESP32

- Introducción
El sensor ultrasónico HC-SR04 es un dispositivo capaz de medir distancias utilizando ondas de sonido de alta frecuencia. Su funcionamiento se basa en el envío de un pulso ultrasónico y la detección del eco reflejado por un objeto. La ESP32, gracias a su velocidad y múltiples pines de entrada/salida, permite procesar esta señal con precisión.
- OBJETIVO
   - Simular el funcionamiento del sensor HC-SR04 con una ESP32.
   - Medir distancias en centímetros y visualizar el resultado en el monitor serial.
   - Analizar el comportamiento del sensor dentro del entorno virtual Wokwi

- Materiales Utilizados

  1. Sensor DHT22
  2. Tarjeta ESP32
  3. LCD 
  4. WOKWI SIMULATOR (https://wokwi.com)
![](https://github.com/Mayte-10/-DHT22-CON-LCD/blob/main/WhatsApp%20Image%202025-11-30%20at%2019.54.34.jpeg)

- PROCEDIMIENTO 

- Ingresar a  WOKWI SIMULATOR y seleccionar el microcontrolador ESP32

  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2021.14.00%20(1).jpeg)
  ![](https://github.com/Mayte-10/REPORTE-SENSOR-DTH22/blob/main/WhatsApp%20Image%202025-11-23%20at%2020.50.01.jpeg)

- Colocar el sensor ultrasonico y la LCD
- Realizar la conexión correspondiente
  
  ![](https://github.com/Mayte-10/REPORTE-SENSOR-ULTRASONICO-/blob/main/ULTRASONICO%20CONEXION%20SIMPLE.PNG)

- Colocar el siguiente código
  
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();

}

void loop()
 {
  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms
  lcd.clear();
  lcd.setCursor(3, 0);
  lcd.print("BIENVENIDOS");
  lcd.setCursor(2, 1);
  lcd.print("MODULO 5");
  delay(1000);
  lcd.clear();
  lcd.setCursor(2, 1);
  lcd.print("MAYTE TORRES");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia:");
  lcd.print(d);
  lcd.setCursor(14, 0);
  lcd.print("cm");
 
  delay(1000);
}
```
ADJUNTAR LAS LIBRERÍAS CORRESPONDIENTES 
![](https://github.com/Mayte-10/REPORTE-SENSOR-ULTRASONICO-/blob/main/LIBRERIAS.PNG)
- COMPILAR
![](https://github.com/Mayte-10/REPORTE-SENSOR-ULTRASONICO-/blob/main/COMPILAR%20SIMPLE%202.0.PNG)
  
- FUNCIONAMIENTO 
En la simulación de Wokwi se observa:
La pantalla LCD actualiza la distancia.
El sensor ultrasónico responde correctamente cuando se modifica la distancia en el simulador.
El HC-SR04 opera mediante dos pines principales:
- Trigger (TRIG): Genera un pulso de 10 µs para iniciar la medición.
- Echo (ECHO): Recibe el eco y regresa un pulso proporcional al tiempo de viaje.

  ![](https://github.com/Mayte-10/REPORTE-SENSOR-ULTRASONICO-/blob/main/DISTANCIA%20164%20CM.PNG)
   ![](https://github.com/Mayte-10/REPORTE-SENSOR-ULTRASONICO-/blob/main/MODULO%2005%20SIMPLE.PNG)
   ![](https://github.com/Mayte-10/REPORTE-SENSOR-ULTRASONICO-/blob/main/MAYTE%20TORRES%20SIMPLE.PNG)
   ![]( )


Realizó
Mayte Torres 
