Для начала задания и получения информации используем команды из методички 

<img width="653" height="179" alt="image" src="https://github.com/user-attachments/assets/f94abda5-0233-4825-98c2-8312ac0b5a8a" />

Из-за того что у меня на машине стоит "btefs" пришлось использовать пространство интернета для выполнения задания
Таким образом было выявлено что для данной стоит использовать команду (sudo chattr +C /swapfile), которая использовать только в данной ситуации.
Если не использовать данную команду, то btefs отключает функцию и swapon "упадёт" (Недопустимый аргумент)
А использование dd вместо fallocate даёт гарантию, что в файле не будет пустого пространства 

<img width="694" height="227" alt="image" src="https://github.com/user-attachments/assets/f7b326bb-53e7-463f-8667-1a22abf5fe35" />

<img width="648" height="174" alt="image" src="https://github.com/user-attachments/assets/6374be7a-b811-4923-b9a0-b1071a161c28" />

Теперь с помощью команды посмотрим значение swappiness. В нашем случае он 60, давайте снизим его до 10

<img width="392" height="141" alt="image" src="https://github.com/user-attachments/assets/c30a5c16-d74b-4823-84e9-1b443ca58581" />

С помощью последовательности команды мы можем убрать swap-file и вернуть значение zram

<img width="651" height="206" alt="image" src="https://github.com/user-attachments/assets/d6d65aff-e307-4b72-9175-caf36cec93ab" />

Таким образом мы выяснили, что корневая система моей ВМ(fedora) является - btrfs, где особенностью является
по умолчанию включённый zram-swap 
Что делают команды:
sudo chattr +C /swapfile - является обязательным для нас, отключает copy-on-write
sudo dd if=/dev/zero of=/swapfile bs=1M count=512 status=progress - заполняет файл реальными нулями
sudo chmod 600 - доступ только для root 
sudo mkswap - создаёт заголовок в указанной области
sudo swapon - активирует swap-file 
sudo swapoff - отключает swap
swappiness - на сколько стоит приоритет работы выгрузки анонимной страницы из ядра в swap. Изначально стоит 60, при 10 ядро держит
страницы в ОЗУ.

БД рассчитаны на читаемую задержку, если страница уходит в swap то время получения ответа может увеличится в разы.
Таким образом отключение swap полностью стопит процесс.
