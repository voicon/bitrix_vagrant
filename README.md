# bitrix_vagrant
Автоматическая настройка виртуальной машины с общей папкой
# Использование
Установите [Virtualbox](https://www.virtualbox.org/wiki/Downloads) и [Vagrant](https://www.vagrantup.com/downloads.html).
Vagrant лучше установить из скачанного файла, потому что в репозиториях более старые версии.
Клонируйте репозиторий:
```
git clone https://github.com/abicorios/bitrix_vagrant
```
Удалите папку `.git`:
```
./rm_dor_git.sh
```
Перейдите в папку `c7`:
```
cd c7
```
Запустите виртуальную машину:
```
vagrant up
```
Если не установлены необходимые плагины, нужно согласиться (`y`) на их установку, потом ещё раз запустить виртуальную машину.
Первый запуск виртуальной машины требует подождать некоторого времени для полной автоматической настройки, последующие запуски той же машины будут происходит быстрее.
После включения виртуальной машины в командной строке вернётся стандартное приглашение ввода команд, тогда откройте в браузере ip-адрес `192.168.33.10`.
Установите сайт через интерфейс браузера.
После установки сайта в той же командной строке завершите настройку общей папки:
```
vagrant ssh
sudo -i
./run_after_site_install.sh
exit
exit
```
Файлы сайта появятся в папке `www` которую можно открыть в удобной `IDE`.
При необходимости виртуальную машину можно выключить:
```
vagrant halt
```
Повторное включение также выполняется командой `vagrant up`. Полностью удалить машину можно командой:
```
vagrant destroy -f
```
Вообще нужно знать что каждая виртуальная машина использует конфиг `Vagrantfile` из отдельной нынешней папки, то есть чтобы отдать команды другой машине нужно создать другую папку с другим `Vagrantfile` и перейти в неё.
# Дополнительная информация
Если нужно поменять ip-адрес `192.168.33.10`, это можно сделать в `Vagrantfile`, нужно брать локальные адреса из диапазона 192.168.0.0 -- 192.168.255.255 но избегая крайних значений (без 0,1,255). Крайние значения могут быть заняты роутером или системными программами. Можно запускать несколько виртуальных машин одновременно. В `Vagrantfile` число `1024` указывает на использование одного гигабайта оперативной памяти, если в основной системе много памяти то можно выделить виртуальной машине и больше. Плагины могут быть установлены глобально через командную строку:
```
vagrant plugin install vagrant-reload
vagrant plugin install vagrant-vbguest
```
Тогда не нужно будет подтверждать установку плагина для новых виртуальных машин. С другой стороны, если для какой-то виртуальной машины не нужна автоматическая установка `vbguest`, то лучше локально устанавливать через `Vagrantfile` для подходящих виртуальных машин.
