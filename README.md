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


