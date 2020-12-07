# Установка nextcloud с помощью Snap пакета
Создание собственного облачного хранилища с помощью **Nextcloud** на сервере с ОС **Ubuntu 18.04**.

## Шаг I. Установка snap
Перед началом утсановки nextcloud необходимо установить сам **snap**:

```
sudo apt update
sudo apt install snapd
sudo snap install nextcloud
```

## Шаг II. Настройка администратора 
На вашей машине уже установлен **Nextcloud**. Теперь необходимо произвести настройку аккаунта администратора (логин и пароль), для этого выполним следующую команду (поля **login** и **password** следует заменить на свои):

```
sudo nextcloud.manual-install login password
```

## Шаг III. Настройка "доверенных доменов"
Нужно указать системе **домен** (или **ip адрес**), с которых будет идти подключение, делается это следующим образом:

```
sudo nextcloud.occ config:system:get trusted_domains
sudo nextcloud.occ config:system:set trusted_domains 1 --value=83.221.202.194:8000
sudo nextcloud.occ config:system:get trusted_domains
```

Система уже готова к использованию, для доступа к хранилищу теперь необходимо подключится по указанному адресу в браузере или приложении, но текущий каталог данных располагается в директории: **/var/snap/nexcloud/common/nextcloud/data**. Смена дефолтной директории рассмотрена в следующем шаге.

## Шаг IV. Cмена каталога данных
Для того что поменять расположение корневой директории, можно выполнить следующие шаги:

```
sudo nextcloud.occ config:system:set datadirectory --value=/wherever/you/ want
sudo nextcloud.occ config:system:get datadirectory # Проверяем 
chown root:root -R /wherever/you/ want
sudo snap connect nextcloud:removable-media
```
На этом всё, система готова к работе и настроена. (не рассмотрено разве что ssl соединение, в будущем буду добавлять).