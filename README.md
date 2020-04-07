# bitrix_vagrant
Автоматическая настройка виртуальной машины с общей папкой, настроенным Xdebug, возможностью увеличить размер диска виртуальной машины в конфиге.
# Скорость сайта на виртуальной машине
В некоторых случаях скорость сайта на виртуальной машине может не понравится. Об этом лучше знать заранее. На виртуальной машине используется общая папка `VirtualBox`, это замедляет файловые операции. Лучшу всего виртуальная машина будет работать на `SSD` диске в `Linux`. В случае `Windows` виртуальную машину может замедлять антивирус, служба индексирования, `Superfetch`, обновление `Windows`. Можно настроить исключения антивируса, отключить неактуальные службы. Можно с помощью диспетчера задач проверять нагрузку на процессор и использование жесткого диска, посмотреть какие приложения мешают и правильно их настроить. Также сайт могут замедлять зависшие бизнес-процессы, лучше их удалить. И если просто запущены бизнес-процессы которые не критически важны во время разработки, тоже можно удалить.
# Использование
Установите новый [Virtualbox](https://www.virtualbox.org/wiki/Downloads) согласно инструкции на странице загрузки. Или хотя бы старый:
```
sudo apt update && sudo apt install virtualbox
```

Установите новый [Vagrant](https://www.vagrantup.com/downloads.html) из скачанной x64 версии deb файла:
```
wget https://releases.hashicorp.com/vagrant/2.2.7/vagrant_2.2.7_x86_64.deb
sudo dpkg -i vagrant_2.2.7_x86_64.deb
```
Обратите внимание что в системных репозиториях более старые версии Vagrant, лучше не устанавливать через apt.
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
Первый запуск виртуальной машины требует подождать некоторого времени для полной автоматической настройки, последующие запуски той же машины будут происходит быстрее.
После включения виртуальной машины в командной строке вернётся стандартное приглашение ввода команд, тогда откройте в браузере ip-адрес `192.168.33.10`.
Установите сайт через интерфейс браузера.
После установки сайта в той же командной строке завершите настройку общей папки выполняя отдельно построчно команды:
```
cd c7
vagrant reload
```
Нужно подождать завершения автоматического копирования файлов сайта в общую папку.
Файлы сайта появятся в папке `www` которую можно открыть в удобной `IDE`.
При необходимости виртуальную машину можно выключить:
```
vagrant halt
```
Повторное включение выполняется командой: 
```
vagrant up
```
Нужно знать что каждая виртуальная машина Vagrant использует конфиг `Vagrantfile` из отдельной нынешней папки и принимает команды вызываемые при нахождении в этой же папке. То есть чтобы отдать команды другой машине нужно создать другую папку с другим `Vagrantfile` и перейти в неё.
# Дополнительная информация
Если нужно поменять ip-адрес `192.168.33.10`, это можно сделать в `Vagrantfile`, нужно брать локальные адреса из диапазона `192.168.0.0 - 192.168.255.255` но избегая крайних значений (без `0`,`1`,`255`). Крайние значения могут быть заняты роутером или системными программами. Можно запускать несколько виртуальных машин одновременно.

В `Vagrantfile` строка `vb.memory = "1024"` указывает на использование одного гигабайта оперативной памяти, если в основной системе много памяти то можно выделить виртуальной машине и больше.

В `Vagrantfile` в строке `config.disksize.size = "80GB"` можно при необходимости указать и более крупный размер виртуального диска.

Если выполнить команду`vagrant` без параметров, то появится справочная информация со списком всех доступных команд. Иногда полезно увидеть состояние машин командами `vagrant status` и `vagrant global-status`. Если виртуальная машина создаётся не на Linux а на Windows, то можно или запускать те же bash-скрипты из консоли Git Bash, или использовать bat-файлы `rm_dot_git.bat` и `create_vm.bat`.

В виртуальную машину можно залогиниться командой `vagrant ssh`. Виртуальную машину можно перезагрузить командой `vagrant reload`. Полностью удалить виртуальную машину можно командой `vagrant destroy -f`.

Xdebug автоматически настраивается внутри виртуальной машины, нужно только настроить на стороне IDE [https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html](https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html)
