Скрипт который мы ввели из методички поможет нам выделить в цикле по 10 МБ и записать байт в каждую страницу, это сделано чтобы
ядро выделяло место на физ память.

Состояние памяти до запуска

<img width="655" height="122" alt="image" src="https://github.com/user-attachments/assets/983e849e-4c6a-4d2b-85b1-b902b9c24008" />

И запуск с ограничениями

<img width="653" height="141" alt="image" src="https://github.com/user-attachments/assets/4db70626-9536-42d7-b9a4-ffa06f28ad74" />

Данная команда позволяет установить максимальный размер виртуальной памяти для процесса и потоков. Но запуск без лимита безопаснее, потому что действует только на процесс и его потомков, жесткое ограничение из-за -> ()
ООМ killer не сработает.

Процесс упал в кол-во памяти потому что часть лимита занято python, библиотеками и структурами утилиты.

<img width="503" height="37" alt="image" src="https://github.com/user-attachments/assets/71361f51-1e0e-4b1c-9ba6-c822e5fd1ca4" />

<img width="406" height="67" alt="image" src="https://github.com/user-attachments/assets/f535d92a-4567-4edf-a63b-4aa21164951e" />
