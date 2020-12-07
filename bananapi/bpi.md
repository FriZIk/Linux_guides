# Установка Linux на BananaPi M3

## Шаг I. Подготовка к установке
1. Минимальный блок питания для запуска **5B/2A** (1.5 ампера не стартовало)
2. Подключать монитор и клавиатуру уже после того как загорится индикатор питания, иначе не хватит питания с блочком на 2А.(рекомендуемое питание 5В/3А)
3. Скачивание образа(armbian): https://mirrors.dotsrc.org/armbian-dl/bananapim3/archive/
4. Создавать образ через **Etcher**, через **win23diskImager** не работало

## Шаг II. Подключение к wifi после загрузки системы
После установки система предложит ввести новый пароль суперпользователя, а так же создать дополнительного пользователя. Далее нужно подключится к сети **wifi** с помощью команды:

```
sudo nmtui-connect SSID_NAME
```

Выясним полученный от роутера ip-адрес и проверим запущен ли ssh:

```
ifconfig
service ssh status
```

Теперь можно подключится к плате через ssh

## Шаг III. Установка PIORPi.GPIO
PIORPi.GPIO - Питоновская библиотека для работы с портами ввода/вывода:

```
git clone https://github.com/LeMaker/RPi.GPIO_BP -b bananapi
sudo apt-get update
sudo apt-get install python-dev
cd RPi.GPIO_BP
python setup.py install    
sudo python setup.py install #нужно запустить дважды это какая-то офигенная хитрость
```
Дополнительная дкоументация: https://github.com/LeMaker/RPi.GPIO_BP - Питоновская библиотека для **GPIO**

## Шаг IV. Установка Wiring

Сишная библиотека для работы с портами **GPIO**

```
git clone https://github.com/LeMaker/WiringBP -b bananapi
cd WiringBP/
sudo chmod +x ./build
sudo ./build
gpio readall #должна вывести таблицу GPIO
```

Для проверки работоспособности напишем и скомпилируем небольшую программу на языке **C**:

```
#include <wiringPi.h>
int main (void)
{
  wiringPiSetup () ;
  pinMode (0, OUTPUT) ;
  for (;;)
  {
    digitalWrite (0, HIGH) ; delay (500) ;
    digitalWrite (0,  LOW) ; delay (500) ;
  }
  return 0 ;
}
```

Для компиляции используем команду:

```
gcc blink.c -o blink -lwiringPi -lpthread # компиляция не работала как в гайде с LeMaker
```

Дополнительная документация: http://wiringpi.com/




