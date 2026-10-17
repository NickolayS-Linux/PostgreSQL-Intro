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

<img width="462" height="41" alt="изображение" src="https://github.com/user-attachments/assets/42e385e1-84ce-41a0-b5bc-47a3ba30daf1" />

Теперь установим образ PostgreSQL из Docker Hub:

<img width="686" height="347" alt="изображение" src="https://github.com/user-attachments/assets/8c20bbbc-80ee-4d1d-a84b-e4ccfb1bbea3" />

После завершения установки PostgreSQL образ готов к запуску.

Чтобы запустить контейнер PostgreSQL, выполним следующую команду, указав созданный ранее каталог для хранения данных:


Подключимся к PG  сначала с хоста
<img width="1107" height="310" alt="изображение" src="https://github.com/user-attachments/assets/ed793c2b-e9d3-415e-985d-e49dbaa95122" />
