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


