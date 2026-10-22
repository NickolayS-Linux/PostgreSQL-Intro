**Домашнее задание

Спасение данных на внешнем диске

Цель:

переносить каталог данных PostgreSQL на внешний диск для расширения хранилища без потери данных.

Т.к. у меня нет внешнего жетского диска, я создам виртуальный жесткий диск. Важен же сам принцип )

Сделать его из файла-образа и подключить через loop-устройство.

**

Создам виртуальный диск и подключу его через loop устройство

<img width="1862" height="116" alt="изображение" src="https://github.com/user-attachments/assets/1ff7b980-1dde-4908-be22-b14a056519c8" />

Создадим файловую систему на нем:

<img width="1862" height="222" alt="изображение" src="https://github.com/user-attachments/assets/053a27e8-d016-462c-aff3-ab17dd4f5b8f" />

Создадим директория для монтирования диска:

<img width="1862" height="53" alt="изображение" src="https://github.com/user-attachments/assets/d9ab0d23-4b05-4569-b001-b6e990245933" />

И примантируем виртуальный диск:

<img width="1862" height="276" alt="изображение" src="https://github.com/user-attachments/assets/e0a221b1-29e2-4961-bbcf-91e2f7bd5c60" />

Посмотрим, что у нас есть в наличии:

<img width="1862" height="744" alt="изображение" src="https://github.com/user-attachments/assets/40cc3b6c-7dc9-4847-ae33-40488397c248" />

Данные присутствую, останавливаем postgresql, но перед этим получим текущий директорий:

<img width="1337" height="134" alt="изображение" src="https://github.com/user-attachments/assets/6ac1325f-9a89-46d5-9e35-2162904fea8a" />

И начинаем перенос:

начало
<img width="1337" height="286" alt="изображение" src="https://github.com/user-attachments/assets/983c15af-a376-4dcf-a56d-0fe0d957a493" />

конец
<img width="1337" height="286" alt="изображение" src="https://github.com/user-attachments/assets/4dd9ab37-b4e7-45c0-937a-7e3b43926646" />

Теперm создажим символическую ссылку,чтобы наш PG заработал в Docker, т.к. он изначально запускался для докумера, 
и проверим, данные которые перенесли на новый внешний диск:

<img width="1337" height="138" alt="изображение" src="https://github.com/user-attachments/assets/ca2ef961-e64f-4275-8914-1d9a083e6f66" />

<img width="1337" height="690" alt="изображение" src="https://github.com/user-attachments/assets/86aef0da-25ae-425a-b82e-2f9a06f085b1" />

Данные на месте, можно продолжать работу.

Спасибо за внимание. ДЗ закончено.

