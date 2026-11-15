**Домашнее задание**

**Бэкапы**

**Цель:**

**настроить надёжное резервное копирование и восстановление базы данных;**

Тестовый стенд имеет следующие характеристики:

    RAM - 8GB
    HDD - 8 GB
    CPU - 4 Cores
    OS - Ubuntu 24.04.TLS
    PostgreSQL СУБД 16.15

**Установка и настройка.**

pool_w_wal-g_wal-g_2.0.1-1_amd64.deb

Скачать и установить скачаю и установлюскаченный выше файл;

Устанавливаем утилиту WAL-G из пакета pool_w_wal-g_wal-g_2.0.1-1_amd64.

    <img width="1295" height="192" alt="изображение" src="https://github.com/user-attachments/assets/bd9e1571-0e6d-4048-a7f5-0f54f46b6f40" />
 
    <img width="1295" height="462" alt="изображение" src="https://github.com/user-attachments/assets/258c283b-2658-4bc8-bcf9-566a8b89128b" />

Выполню дополнительные действия:

    touch /var/lib/postgresql/walg.log /var/lib/postgresql/walg-bootstrap.log

    chown postgres:postgres /var/lib/postgresql/walg.log /var/lib/postgresql/walg-bootstrap.log
 
опционально - сделаю ссылку на бинарный файл (пути могут отличаться), разместив его в каталоге, доступном в переменной $PATH

    ln -s /usr/bin/wal-g /usr/local/bin/wal-g

В домашнем каталоге пользователя postgres:

    su - postgres

    postgres@PGWork:~$ pwd

    /var/lib/postgresql

1. Создам каталог walgdata для РК данных СУБД PostgreSQL.

    mkdir walgdata

    <img width="1295" height="138" alt="изображение" src="https://github.com/user-attachments/assets/f78f23dd-0877-4e8f-ba3a-22260a3793f7" />

2. Создам файл конфигурации .walg.json для утилиты WAL-G содержащий следующие данные:

    nano .walg.json

{

    "WALG_COMPRESSION_METHOD": "brotli",
    "WALG_DELTA_MAX_STEPS": "5",
    "WALG_FILE_PREFIX": "/var/lib/postgresql/walgdata",
    "PGDATA": "/var/lib/postgresql/tantor-se-16/data",
    "PGHOST": "/var/run/postgresql/.s.PGSQL.5432"
    
}

<img width="1295" height="116" alt="изображение" src="https://github.com/user-attachments/assets/850ed2a8-24a3-4324-b1c1-062f8d135eb2" />

Пояснения к дериктивам указанных в файле настроек:

    WALG_COMPRESSION_METHOD определяет применяемый метод сжатия данных brotli
    WALG_DELTA_MAX_STEPS определяет, сколько разностных резервных копий (между ранее созданной резервной копией и текущим состоянием) может быть между полными резервными копиями
    WALG_FILE_PREFIX определяет расположение каталога данных WAL-G /var/lib/postgresql/walgdata
    PGDATA определяет расположение каталога данных СУБД PostgreSQL /var/lib/postgresql/16/main
    PGHOST определяет расположение информационного файла сервиса СУБД PostgreSQL

3. Вносим изменения в файл конфигурации СУБД Тантор /var/lib/postgresql/tantor-se-16/data/postgresql.auto.conf

