**Домашнее задание**

**Установлено: на хостовую машину Ubuntu 24.04.**

Установка и настройка PostgteSQL в контейнере Docker

**Цель:**

разворачивать PostgreSQL в контейнере для быстрого создания воспроизводимого окружения разработки;

На хосте установлено:

- PostgreSQL 16.14 on x86_64-pc-linux-gnu, compiled by gcc (Debian 12.2.0-14+deb12u1) 12.2.0, 64-bit, и postgresql-client

- Docker version 29.1.3, build 29.1.3-0ubuntu3~24.04.2

- Docker Compose version v5.6.0

- Каталог для хранения данных будет использоваться $HOME/docker/volumes/postgres

Приступим к выполнению ДЗ

Пока изолированная среда не запущена, в ней нет никаких данных. Нам это не подходит, поэтому создаем Docker Postgres Volume – каталог для хранения данных:

<img width="1107" height="24" alt="изображение" src="https://github.com/user-attachments/assets/e64b3e5e-9763-4929-878a-713f00a7bf49" />

Теперь установим образ PostgreSQL из Docker Hub:

<img width="686" height="347" alt="изображение" src="https://github.com/user-attachments/assets/8c20bbbc-80ee-4d1d-a84b-e4ccfb1bbea3" />

После завершения установки PostgreSQL образ готов к запуску.

Чтобы запустить контейнер PostgreSQL, выполним следующую команду, указав созданный ранее каталог для хранения данных:

<img width="1107" height="57" alt="изображение" src="https://github.com/user-attachments/assets/20cedaf9-1e70-4db2-a904-22d994ff8796" />

Подключимся к контейнеру через Docker и проверим подключенный каталог:

<img width="552" height="42" alt="изображение" src="https://github.com/user-attachments/assets/507b5dc4-2556-47d2-93b7-97d2379d85d5" />

Подключимся клиентом к PG хоста

<img width="1107" height="310" alt="изображение" src="https://github.com/user-attachments/assets/ed793c2b-e9d3-415e-985d-e49dbaa95122" />

Подключитесь из контейнера с клиентом к контейнеру с сервером и создайте таблицу с данными о перевозках.

Но сначала создадим в Docker сеть и назовем её pg_net

<img width="600" height="44" alt="изображение" src="https://github.com/user-attachments/assets/3a6d52b9-884f-415f-86c5-b47b7be79421" />

Но сначала на сервере создаим еще одну БД и назовем test1

<img width="685" height="189" alt="изображение" src="https://github.com/user-attachments/assets/28975f90-8f90-474a-b7b1-5874aadf43e4" />

после этого как создали сеть для Docker, подключимся к серверу

<img width="1052" height="336" alt="изображение" src="https://github.com/user-attachments/assets/6ec628fc-3bfb-482f-ad81-db29d266d2b3" />

Клиент видит созданныую БД. Сетевая связанность работает.

Теперь переключимся на БД dz2, создадим таблицу  заполним её:

<img width="685" height="62" alt="изображение" src="https://github.com/user-attachments/assets/6f9cb890-af7a-4449-8e70-258797c522e5" />

<img width="810" height="385" alt="изображение" src="https://github.com/user-attachments/assets/0769f8bc-3164-4148-8599-134309dff039" />


