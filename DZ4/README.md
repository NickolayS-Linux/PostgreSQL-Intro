**Домашнее задание**

**Высокая доступность: развертывание Patroni**

**Цель:**

**разворачивать отказоустойчивый кластер PostgreSQL для сохранения доступности сервиса при сбое узла**


Поднял 3 виртуальные машины на базе Oracle Virtual Box (Лидер, реплика, синхр. реплика), плавающий адрес:

Лидер - 192.168.9.151

Реплика -  192.168.9.210

Синхрон. реплика - 192.168.9.220

VIP - 192.168.9.10

<img width="466" height="424" alt="image" src="https://github.com/user-attachments/assets/3b47734f-e70e-492e-a4a6-966c2cfc23e1" />

Ставим на каждую ВМ пакета из репозиториЯ Ubuntu 24.04, PostgreSQL 16, Patroni 3.2.2-2 и etcd 3.4 

sudo apt install postgresql patroni python3-etcd etcd-server etcd-client pgbackrest prometheus-postgres-exporter

Нода PG, лидер:

<img width="1574" height="424" alt="image" src="https://github.com/user-attachments/assets/18630124-11ba-412c-9a83-be5850bdca40" />

Нода Node1, реплика:

<img width="1574" height="424" alt="image" src="https://github.com/user-attachments/assets/40f24c2b-be10-4676-a2db-596f2e47c1ad" />

Нода Node2, реплика:

<img width="1574" height="424" alt="image" src="https://github.com/user-attachments/assets/a9d48bfb-3fd6-4236-9768-ee4699c08fe9" />

Пакеты установлены, начинаем настройку отказоустойчивого кластера PG

**Настраиваем etcd на PG**

<img width="1574" height="275" alt="image" src="https://github.com/user-attachments/assets/b16505c6-2885-4902-9813-facdf714b51d" />

Настраиваем etcd на Node1

<img width="1574" height="353" alt="image" src="https://github.com/user-attachments/assets/7de4ce6d-9727-4d3c-9eea-54430be69157" />

Настраиваем etcd на Node2

<img width="1574" height="355" alt="image" src="https://github.com/user-attachments/assets/926d8812-187d-4044-b1fb-c713debb9149" />

Проверим:

<img width="1574" height="122" alt="image" src="https://github.com/user-attachments/assets/d250b471-4269-429b-bcde-ba0b43b48a23" />

<img width="1574" height="122" alt="image" src="https://github.com/user-attachments/assets/46f5a3c2-cb7a-40c2-afb9-d653ecf88e28" />

Настраиваем Patroni, конифгу приложу дополнительно в личном кабинете ДЗ.

<img width="1574" height="231" alt="image" src="https://github.com/user-attachments/assets/2c2244be-98a0-460d-8fbe-53bef1b32b59" />

Установим VIP-Manager

<img width="1574" height="231" alt="image" src="https://github.com/user-attachments/assets/93e1b5e6-4667-4315-83f7-4afa3a8bd677" />

Проверим как меняется Лидер, остановкой основного, потом второго. Запуска основного и остановку всех реплик

<img width="1574" height="233" alt="image" src="https://github.com/user-attachments/assets/34e5c2a7-3b53-4eab-8e1f-a3225efdb14b" />

В следующем слайде я лома плику. Потом восстанваливаю

<img width="1574" height="257" alt="image" src="https://github.com/user-attachments/assets/8253986a-aae5-4f64-88f4-7d23817a7d7d" />

Выключение Лидера и переключение на вторую ноду как видим задержки не большие, добавление записей продолжилось, после переключение. 

Реплика стала мастером (vip-manager так же сработал корректно)

<img width="1574" height="344" alt="image" src="https://github.com/user-attachments/assets/18177e57-a444-4f29-a15e-c9c7f68c390d" />

<img width="1574" height="718" alt="image" src="https://github.com/user-attachments/assets/82797070-f0a1-474b-80cf-fd7b3376de67" />

<img width="1574" height="635" alt="image" src="https://github.com/user-attachments/assets/d9c8828b-d557-41c7-a9bf-eb544f6d2f42" />

Все записи (34) на месте )

ДЗ выполнено

