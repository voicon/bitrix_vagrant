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
./rm_dot_git.sh
```
Для создания виртуальной машины запустите скрипт:
```
./create_vm.sh
```
Если действия выполняются не в Linux а в Windows то виртуальную машину можно создать скриптом:
```
create_vm.bat
```
Первый запуск виртуальной машины требует подождать некоторого времени для полной автоматической настройки, последующие запуски той же машины будут происходит быстрее.
После включения виртуальной машины в командной строке вернётся стандартное приглашение ввода команд, тогда откройте в браузере ip-адрес `192.168.33.10`.
Установите сайт через интерфейс браузера.
После установки сайта в той же командной строке завершите настройку общей папки выполняя отдельно построчно команды:
```
cd c7
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
Повторное включение также выполняется командой `vagrant up`, возможен и перезапуск `vagrant reload`. Полностью удалить машину можно командой:
```
vagrant destroy -f
```
Вообще нужно знать что каждая виртуальная машина использует конфиг `Vagrantfile` из отдельной нынешней папки, то есть чтобы отдать команды другой машине нужно создать другую папку с другим `Vagrantfile` и перейти в неё.
# Дополнительная информация
Если нужно поменять ip-адрес `192.168.33.10`, это можно сделать в `Vagrantfile`, нужно брать локальные адреса из диапазона `192.168.0.0 - 192.168.255.255` но избегая крайних значений (без `0`,`1`,`255`). Крайние значения могут быть заняты роутером или системными программами. Можно запускать несколько виртуальных машин одновременно. В `Vagrantfile` число `1024` указывает на использование одного гигабайта оперативной памяти, если в основной системе много памяти то можно выделить виртуальной машине и больше. 
Если выполнить команду`vagrant` без параметров, то появится справочная информация со списком всех доступных команд. Иногда полезно увидеть состояние машин командами `vagrant status` и `vagrant global-status`.
