# P4-ULTRASONICO-LCD
## INTRODUCCION
### DESCRIPCION 
La **Esp32** la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor (**HC-SR04**) para adquir los valores de distancia a la cul se encuentra un cuerpo determidado; Cabe aclarar que esta practica se usara un simulador llamado WOKWI.
### MATERIAL A OCUPAR
Para realizar esta practica ocuparemos lo siguente:
-WORKI
-Tarjeta ESP 32
-Sensor HC-SR04
### Requisitos previos
Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.
## INSTRUCIOES DE ELAVORACION 
1.Abrir la terminal de programación y colocar la siguente programación:
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
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

  lcd.setCursor(0, 0);
  lcd.print("  Distancia: " + String(d) +"cm");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Ing. Electrico");
  lcd.setCursor(0, 1);
  lcd.print("Nestor Jimenez");
  delay(2000);
}

2. Se agrega la libreria #include <LiquidCrystal_I2C.h>.
![]
3. Hacer la conexion de **HC-SR04** con la **ESP32** y el **LCD 16X2 (I2C)** como se muestra en la siguente imagen.
![]
## INSTRUCCIONES DE OPERACION 

    1. Iniciar simulador.
    2. Visualizar los datos en el monitor serial.
    3. Colocar la distancia de trabajao del sensor **HC-SR04**
## RESUSLTADOS
Cuando haya funcionado, verás los valores dentro de display como se muestra en la sigiente imagen.
![]
