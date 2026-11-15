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
 
# опционально - сделаю ссылку на бинарный файл (пути могут отличаться), разместив его в каталоге, доступном в переменной $PATH
ln -s /usr/bin/wal-g /usr/local/bin/wal-g

