

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

**Изучение уровней изоляции**

Создам базу данных OTUS и подключусь к ней, а так же создам таблицу и заполню её некоторыми данными:

<img width="1316" height="268" alt="image" src="https://github.com/user-attachments/assets/8e43e1cf-4f05-41d8-b476-ccbbf8993085" />

Мспользуем эту таблицу для учёта перевозок бананов и кофе.

Проверю текущий уровень изоляции с помощью команды:

<img width="1316" height="161" alt="image" src="https://github.com/user-attachments/assets/ddced2f1-a1c1-419a-b69d-2ded44f64b2f" />

В первой сесси так же переключимся на БД OTUS, и выполним следующую команду:

<img width="1407" height="134" alt="image" src="https://github.com/user-attachments/assets/9fc1ae11-971c-4a63-ba62-d23534dc5a70" />

Во второй сессии выполним:

<img width="1407" height="140" alt="image" src="https://github.com/user-attachments/assets/24febfa0-f3db-4fdc-9f7f-7a56a6f9f4e7" />

Почему не видим. пояснения: Мы получили два разынх результата. в одной транзакции, так как не было commit вы первой сессии.

Завершу первую транзакцию с помощью commit; и снова выполню select * from shipments во второй сессии. 

<img width="1407" height="161" alt="image" src="https://github.com/user-attachments/assets/ac9b3668-47bf-4ec3-8790-0beeb02cd539" />

Сейчс видно запись, которую добавили в первой сессии;

Почему видим. Пояснения: Транзакция завершилась, и поэтому мы увидили запись во второй сессии;

Почему это важно: мы изучал уровни изоляции, чтобы понять, как данные видны разным пользователям.

**Эксперименты с уровнем изоляции Repeatable Read**

Установим другой уровень изоляции в обеих сессиях:

<img width="834" height="28" alt="image" src="https://github.com/user-attachments/assets/d6110ce6-1171-49d2-a72a-caa0ba664d65" />

<img width="412" height="115" alt="image" src="https://github.com/user-attachments/assets/91363740-84c7-4adb-b0f7-3d8382286d80" />

Выполним в первой сессии следующее:

<img width="834" height="271" alt="image" src="https://github.com/user-attachments/assets/05905179-203e-43f1-b71d-ccea49d2897c" />

Видим, что в начатой транзакции запись добавлена.

Выполним команду во второй сессии:

<img width="834" height="181" alt="image" src="https://github.com/user-attachments/assets/10bc29d5-65d2-42e4-a002-2728c9af66a5" />

Запись мы не видим;

Потому что в **Repeatable Read** не повторяющееся чтение не возможно.

Теперь в первой сессии мы сделаем commit, и проверим вторую сессию:

<img width="834" height="246" alt="image" src="https://github.com/user-attachments/assets/ca717313-d14f-4d9e-87f0-825fae4224e1" />

Вторая сессия:

<img width="834" height="187" alt="image" src="https://github.com/user-attachments/assets/d69aae8a-b03a-4750-8012-982040360fd5" />

Любые новые строки (фантомы), добавленные другими транзакциями позже, для нас физически не существуют до тех пор, пока мы не завершите текущую транзакцию 

(COMMIT или ROLLBACK) и не откроете новую.

Теперь мы сделаем во второй сесии commit, и получим записи:

<img width="834" height="247" alt="image" src="https://github.com/user-attachments/assets/17132cdc-4d86-4781-8061-a0f6a950d56c" />

Мы увидели запись добавленную в первой сессии.

Почему мы увидели запись. Потому, что мы закончили свою теущую транзакция командой commit. Снимок обновился и мы видим реальные данные.

Почему это важно: Мы экспериментировали с уровнями изоляции, чтобы понять, как они влияют на видимость данных.
