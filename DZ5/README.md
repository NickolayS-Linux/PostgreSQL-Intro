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

Скачать и установить скачаю и установлю скаченный выше файл;

Устанавливаем утилиту WAL-G из пакета pool_w_wal-g_wal-g_2.0.1-1_amd64.

   <img width="1295" height="192" alt="изображение" src="https://github.com/user-attachments/assets/bd9e1571-0e6d-4048-a7f5-0f54f46b6f40" />
 
   <img width="1295" height="462" alt="изображение" src="https://github.com/user-attachments/assets/258c283b-2658-4bc8-bcf9-566a8b89128b" />

Выполню дополнительные действия:

    touch /var/lib/postgresql/walg.log /var/lib/postgresql/walg-bootstrap.log

    chown postgres:postgres /var/lib/postgresql/walg.log /var/lib/postgresql/walg-bootstrap.log
 
опционально - сделаю ссылку на бинарный файл (пути могут отличаться), разместив его в каталоге, доступном в переменной $PATH

    ln -s /usr/bin/wal-g /usr/local/bin/wal-g

В домашнем каталоге пользователя postgres:

    ```
    su - postgres
    postgres@PGWork:~$ pwd
    /var/lib/postgresql
    ```
1. Создам каталог walgdata для РК данных СУБД PostgreSQL:
   
    ```
    mkdir walgdata
    ```
    <img width="1295" height="138" alt="изображение" src="https://github.com/user-attachments/assets/f78f23dd-0877-4e8f-ba3a-22260a3793f7" />

2. Создам файл конфигурации .walg.json для утилиты WAL-G содержащий следующие данные:
   
   nano .walg.json
   ```
    {
        "WALG_COMPRESSION_METHOD": "brotli",
        "WALG_DELTA_MAX_STEPS": "5",
        "WALG_FILE_PREFIX": "/var/lib/postgresql/walgdata",
        "PGDATA": "/var/lib/postgresql/16/main",
        "PGHOST": "/var/run/postgresql/.s.PGSQL.5432"
    }
    ```
    <img width="1295" height="116" alt="изображение" src="https://github.com/user-attachments/assets/383baa13-60bf-44fe-96ec-30abae730d02" />

   ```
    Пояснения к дериктивам указанных в файле настроек:
    WALG_COMPRESSION_METHOD определяет применяемый метод сжатия данных brotli
    WALG_DELTA_MAX_STEPS определяет, сколько разностных резервных копий (между ранее созданной резервной копией и текущим состоянием) может быть между полными резервными копиями
    WALG_FILE_PREFIX определяет расположение каталога данных WAL-G /var/lib/postgresql/walgdata
    PGDATA определяет расположение каталога данных СУБД PostgreSQL /var/lib/postgresql/16/main
    PGHOST определяет расположение информационного файла сервиса СУБД PostgreSQL
    ```
   
3. Вношу изменения в файл конфигурации СУБД PostgreSQL /var/lib/postgresql/16/main/postgresql.auto.conf

    ```
    cat >>  /var/lib/postgresql/16/main/postgresql.auto.conf << EOL
    wal_level = replica
    archive_mode = on
    archive_command = '/usr/bin/wal-g wal-push "%p" 2>&1 | tee -a /var/lib/postgresql/walg.log'
    archive_timeout = 60
    restore_command = '/usr/bin/wal-g wal-fetch \"%f\" \"%p\" 2>&1 | tee -a /var/lib/postgresql/walg.log'                                                                            
    EOL
   
    ```
    
 4. Перезапускаю сервис СУБД PostgreSQL для применение изменений.

    ```
    postgres@PGWork:~$ systemctl restart postgresql.service
    ```
    <img width="1295" height="90" alt="изображение" src="https://github.com/user-attachments/assets/b12bb8a8-bfa3-4d83-8b2a-2171bc1e1fe8" />

5. Выполняю проверку каталога walgdata.

   ```
   postgres@cs-db-001:~$ wal-g backup-list
   ```
   <img width="1295" height="78" alt="изображение" src="https://github.com/user-attachments/assets/87b24588-4281-467b-9201-6b8177c2133d" />


**Создание резевной копиии (РК) и восстановление из неё.**

6. Выполняю РК СУБД PostgreSQL с использованием утилиты WAL-G.

   ```
   postgres@PGWork:~$ /usr/local/bin/wal-g backup-push /var/lib/postgresql/16/main/
   ```
   <img width="1295" height="319" alt="изображение" src="https://github.com/user-attachments/assets/5a421b32-905d-4a33-8270-03e35a3423a5" />

7. Останавливаю СУБД PostgreSQL.

   ```
   sudo systemctl stop postgresql.service
   ```
   <img width="1295" height="111" alt="изображение" src="https://github.com/user-attachments/assets/62b304c0-8e0b-4f7a-a757-05d79015a00e" />

8. Перемещаю каталог данных СУБД PostgreSQL.

   ```
   cp -r /var/lib/postgresql/16/main /var/lib/postgresql/16/savedata
   rm -rf /var/lib/postgresql/16/main/*
   ```   
   <img width="1295" height="77" alt="изображение" src="https://github.com/user-attachments/assets/90d44656-5902-4361-a8ad-a1c4554e8932" />

9. Восстанавливаю каталог данных СУБД PostgreSQL с использованием утилиты WAL-G.

   ```
   wal-g backup-fetch /var/lib/postgresql/tantor-se-16/data LATEST
   ```
   <img width="1295" height="148" alt="изображение" src="https://github.com/user-attachments/assets/ea66657f-ca2f-4678-be18-4f454e7581d2" />

10.  Создам в каталоге данных СУБД PostgreSQL файл recovery.signal для запуска восстановления.

   ```
   touch /var/lib/postgresql/16/main/recovery.signal
   ```
   <img width="1295" height="66" alt="изображение" src="https://github.com/user-attachments/assets/e4ae05f4-075b-40e9-a361-2e5945519fcd" />

11. Запускаем  СУБД PostgreSQL и проверяем работу сервиса и доступ к СУБД.

   ```
   sudo systemctl start postgresql.service
   ```
   <img width="1295" height="122" alt="изображение" src="https://github.com/user-attachments/assets/29742e3e-6acb-465d-9b29-3d013aa434f6" />

12. Проверяем работу сервиса и доступ к СУБД.

   ```
   sudo systemctl status postgresql.service
   ```
