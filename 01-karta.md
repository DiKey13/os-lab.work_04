Перед выполнением работ проверил нужные имеются ли нужные утилиты на моей машине. Проблем не обнаружено, всё что нужно уже было.

Для чтения и понимания следующей информации нам стоит знать что:
Колонка 1 - отвечает за адрес начала области
Колонка 2 - размер (КБ)
(r-xp) - код, (rw-p) - данные и имя файла/пометка.

echo $$

<img width="244" height="33" alt="image" src="https://github.com/user-attachments/assets/4bb28edd-a00f-4ebb-8ab1-89e2c807a907" />

cat /proc/$$/maps | head -20

<img width="910" height="360" alt="image" src="https://github.com/user-attachments/assets/e7037f63-ee1a-4dbd-8a3f-6a43688c5865" />

pmap $$

<img width="467" height="563" alt="image" src="https://github.com/user-attachments/assets/a55c11d1-35cf-4770-bb14-089dabcf64eb" />

pmap $$ | tail -1

<img width="308" height="35" alt="image" src="https://github.com/user-attachments/assets/3099a685-df86-45fe-a322-f26d19c806db" />

grep -E 'stack|libs' /proc/$$/maps

<img width="757" height="100" alt="image" src="https://github.com/user-attachments/assets/70588810-1d8b-4456-9dbb-c8fa08a57fa6" />

Мы можем заметить что (libc.so.6) не однократно повторяется, но имеется только в одном экземпляре.
Это потому что физическая страница является общее, а виртуальное пространство общее, что даёт нам
экономить пространство ОЗУ.
