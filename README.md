# Arduino_01
Светофор
```c++
int led_red = 2;
int led_yellow = 3;
int led_green = 4;
void setup()
{
  pinMode(led_red, OUTPUT);
  pinMode(led_yellow, OUTPUT);
  pinMode(led_green, OUTPUT);
}
void loop()
{
  digitalWrite(led_red, HIGH);
  delay(2000); 
  digitalWrite(led_yellow, HIGH);
  delay(700);
  digitalWrite(led_red, LOW);
  digitalWrite(led_yellow, LOW);
  digitalWrite(led_green, HIGH);
  delay(2000); 
  digitalWrite(led_green, LOW);
  digitalWrite(led_yellow, HIGH);
  delay(700);
  digitalWrite(led_yellow, LOW);
}
```

Кнопка
```c++
#define BUTTON 0
#define LED1 7
void setup() {
  pinMode (BUTTON, INPUT);
  pinMode (LED1, INPUT);
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:
  int btnVal = digitalRead(BUTTON);

  if (btnVal == 0){
    digitalWrite(LED1, HIGH);

  }
  else{
    digitalWrite(LED1, LOW);
  }

}
```
Термометр
``` c++
    // библиотека для работы с аналоговым термометром (Troyka-модуль)
    #include <TroykaThermometer.h>
    
     
    // создаём объект для работы с аналоговым термометром
    // и передаём ему номер пина выходного сигнала
    TroykaThermometer thermometer(A0);
    int led_red = 2;

    void setup()
    { 
      pinMode(led_red, OUTPUT);
      // открываем последовательный порт
      Serial.begin(9600);
    }
     
    void loop()
    {
      // считываем данные с аналогового термометра
      thermometer.read();
      Serial.print("Temperature is ");
      Serial.print(thermometer.getTemperatureC());
      // вывод показателей аналогового термометра в градусах Цельсия
      if (thermometer.getTemperatureC() <30){
        digitalWrite(led_red, HIGH);
      }
      else {
        digitalWrite(led_red, LOW);
      }


    
    }
```
Термометр+лампочка+индикатор
``` c++
 // библиотека для работы с аналоговым термометром (Troyka-модуль)
    #include <TroykaThermometer.h>
    #include <QuadDisplay.h>
   // Подключаем библиотеку для работы с дисплеем
    #include <QuadDisplay2.h>
// создаём объект класса QuadDisplay и передаём номер пина CS
    QuadDisplay qd(9);
 
    
     
    // создаём объект для работы с аналоговым термометром
    // и передаём ему номер пина выходного сигнала
    TroykaThermometer thermometer(A0);
    int led_red = 2;

    void setup()
    { 
      pinMode(led_red, OUTPUT);
      // открываем последовательный порт
      Serial.begin(9600);
      qd.begin();
    }
     
    void loop()
    {
      // считываем данные с аналогового термометра
      thermometer.read();
      Serial.print("Temperature is ");
      Serial.print(thermometer.getTemperatureC());
      // вывод показателей аналогового термометра в градусах Цельсия
      if (thermometer.getTemperatureC() <30){
        digitalWrite(led_red, HIGH);
      }
      else {
        digitalWrite(led_red, LOW);
      }
      qd.displayInt(thermometer.getTemperatureC());


    
    }

```
Сервопривод: вращение с потенциометром
``` C++
#include <Servo.h>
#define PTR_PIN A0



Servo myservo;  // create servo object to control a servo


int potpin = 0;  // analog pin used to connect the potentiometer

int val;    // variable to read the value from the analog pin


void setup() {

  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
  pinMode(PTR_PIN, INPUT);
}


void loop() {
  val = analogRead(PTR_PIN);
  val = analogRead(potpin);            // reads the value of the potentiometer (value between 0 and 1023)

  val = map(val, 0, 1023, 0, 180);     // scale it to use it with the servo (value between 0 and 180)

  myservo.write(val);                  // sets the servo position according to the scaled value

  delay(15);                           // waits for the servo to get there

}
```
Вращение двух моторов

``` c++
    // подключите один мотор к клемме: M1+ и M1-
    // а второй к клемме: M2+ и M2-
    // Motor shield использует четыре контакта 4, 5, 6, 7 для управления моторами 
    // 4 и 7 — для направления, 5 и 6 — для скорости
    #define SPEED_1      5 
    #define DIR_1        4
     
    #define SPEED_2      6
    #define DIR_2        7
     
    void setup() {
      // настраиваем выводы платы 4, 5, 6, 7 на вывод сигналов 
      for (int i = 4; i < 8; i++) {     
        pinMode(i, OUTPUT);
      }
    } 
     
    void loop() {
      // устанавливаем направление мотора «M1» в одну сторону
      digitalWrite(DIR_1, LOW);
      // включаем мотор на максимальной скорости
      analogWrite(SPEED_1, 255);


      digitalWrite(DIR_2, HIGH);
      // включаем мотор на максимальной скорости
      analogWrite(SPEED_2, 255);
      
    }

```
Пульт (кнопка + это 21, - это 7, вперед 24, назад 82, влево 8, вправо 90, стоп 28)
``` c++

#include <IRremote.hpp>
#define IR_RECEIVE_PIN 2

void setup(){
  Serial.begin(9600);
  IrReceiver.begin(IR_RECEIVE_PIN);
}

void loop(){
   if (IrReceiver.decode()) {
      IrReceiver.resume(); // Enable receiving of the next value
      //Serial.println(IrReceiver.decodedIRData.decodedRawData, HEX);
      Serial.println(IrReceiver.decodedIRData.command);
  }
}
```
Работа с пультом, выполнение программ с пультом
```c++
#include <IRremote.hpp>

#define IR_RECEIVE_PIN 2
#define IR_BUTTON_PLUS 21
#define IR_BUTTON_MINUS 7
#define IR_BUTTON_CH_PLUS 71
#define IR_BUTTON_CH_MINUS 69
#define IR_BUTTON_PLAY_PAUSE 67

#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

void setup(){
  Serial.begin(9600);
  IrReceiver.begin(IR_RECEIVE_PIN);

  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
}

void loop(){
   if (IrReceiver.decode()) {
      IrReceiver.resume(); // Enable receiving of the next value
      int command = IrReceiver.decodedIRData.command;
      
      switch (command) {
        case IR_BUTTON_PLUS: {
          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_MINUS: {
          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_CH_PLUS: { // stop mototrs
          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_CH_MINUS: { 
          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed
          
          break;
        }
        case IR_BUTTON_PLAY_PAUSE: { // stop mototrs
          analogWrite(SPEED_1, 0); 
          analogWrite(SPEED_2, 0);  
          break;
        }
      }
```
Управление с джостика
```c++
    // подключите один мотор к клемме: M1+ и M1-
    // а второй к клемме: M2+ и M2-
    // Motor shield использует четыре контакта 4, 5, 6, 7 для управления моторами 
    // 4 и 7 — для направления, 5 и 6 — для скорости
    #include "IRremote.h"
    #define SPEED_1      5 
    #define DIR_1        4
     
    #define SPEED_2      6
    #define DIR_2        7
    #define pinX        A2  // ось X джойстика
    #define pinY        A1  // ось Y джойстика
    void setup() {
      Serial.begin(9600);
        pinMode(pinX, INPUT);
        pinMode(pinY, INPUT);
      // настраиваем выводы платы 4, 5, 6, 7 на вывод сигналов 
      for (int i = 4; i < 8; i++) {     
        pinMode(i, OUTPUT);
      }
        int X = analogRead(pinX);              // считываем значение оси Х
        int Y = analogRead(pinY);              // считываем значение оси Y
    } 
     
    void loop() {
      int X = analogRead(pinX);              // считываем значение оси Х
      int Y = analogRead(pinY);              // считываем значение оси Y
      Serial.print(X);                       // выводим в Serial Monitor
      Serial.print("\t");                    // табуляция
      Serial.println(Y);
      // устанавливаем направление мотора «M1» в одну сторону
      
      if(X>515)
      {
        digitalWrite(DIR_1, LOW);
        analogWrite(SPEED_1, 255);
      }
      else 
      {
        digitalWrite(DIR_1, HIGH);
        analogWrite(SPEED_1, 255);
      }
      /*
      digitalWrite(DIR_1, LOW);
      // включаем мотор на максимальной скорости
      analogWrite(SPEED_1, 255);


      digitalWrite(DIR_2, HIGH);
      // включаем мотор на максимальной скорости
      analogWrite(SPEED_2, 255);*/
      
    }

```
      
  }
}
```
