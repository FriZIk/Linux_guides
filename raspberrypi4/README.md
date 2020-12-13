# Установка Linux на RaspberryPi 

## Шаг I. Создание загрузочного образа
В 2020 году у Raspberry уже появился собственный лаунчер для создания загрузочных образов различных ос, скачиваем его (https://downloads.raspberrypi.org/imager/imager_1.4.exe) и запускаем. В появившемся окне выбираем нужную нам ОС (Ubuntu 20.04 LTS) и sd-карту. Жмём кнопку write и ждём окончания записи образа.

## Шаг II. Подключение к wifi после загрузки системы
После установки нужно настроить подключение к сети **wifi**, сделаем это с помощью команд:

```
sudo apt update
sudo apt install network-manager net-tools
sudo usermod -G netdev -a yourusername
sudo nmtui-connect SSID_NAME
```

Выясним полученный от роутера ip-адрес и проверим запущен ли ssh:

```
ifconfig
service ssh status
```
Теперь можно подключится к плате через ssh

## Шаг III. Установка PIORPi.GPIO и WiringPi
Теперь установим библиотеки wiringPI и RPi.GPIO для возможности работы с портами ввода/вывода:

```
# Установка wiring
cd /tmp
wget https://project-downloads.drogon.net/wiringpi-latest.deb
sudo dpkg -i wiringpi-latest.deb

# Установка RPi.GPIO
sudo apt install python3-pip
pip install RPi.GPIO
```

## Шаг IV. Установка ROS
Для установки **ROS** воспользуйтесь следующими командами:

```
sudo apt install ros-noetic-desktop-full
sudo pip install -U rosdep
sudo rosdep init
rosdep update
echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc ; source ~/.bashrc
roscore
```