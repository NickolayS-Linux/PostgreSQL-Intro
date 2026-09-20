Выполнение домашнего задания №1. Курс Администрирование PostgreSQL. Экспертный уровень 

Установлено: на хостовую машину Ubuntu 24.04.

**Работа с уровнями изоляции транзакции в PostgreSQL**

**Цель:

настраивать уровни изоляции транзакций для проверки согласованности данных при конкурентном доступе;**

Установим PostgreSQL из пакетов с помощью команды apt install.

Устанавливаю последнию версию PostgreSQL:18

Использую скрипт автоматической настройки репозитория, который автоматически устанавливает официальный репозиторий PostgreSQL Apt

<img width="1316" height="638" alt="image" src="https://github.com/user-attachments/assets/101ee9ac-f88e-48ba-85e1-7d88087bccb6" />

Устанавливаю PostgreSQL:18 

<img width="1316" height="667" alt="image" src="https://github.com/user-attachments/assets/8d75d945-a839-4e26-a8a9-5a7c6782a692" />

Пакеты установились успешно. Начинаем выполнения домшнего задания

Подключаемся к серверу PostgreSQL:18

<img width="1316" height="229" alt="image" src="https://github.com/user-attachments/assets/6e8d5c5a-0dc7-4ba6-a318-954dd8c4d9e9" />

Установим режим auto commit в off:

<img width="1316" height="74" alt="image" src="https://github.com/user-attachments/assets/a04cdad0-e53b-4692-8e6b-b96dc0c0cd3b" />

Создам базу данных OTUS и подключусь к ней, а так же создам таблицу и заполню её некоторыми данными:

<img width="1316" height="268" alt="image" src="https://github.com/user-attachments/assets/8e43e1cf-4f05-41d8-b476-ccbbf8993085" />

Мспользуем эту таблицу для учёта перевозок бананов и кофе.

