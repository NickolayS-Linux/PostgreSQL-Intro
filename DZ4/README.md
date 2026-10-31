**Домашнее задание

Высокая доступность: развертывание Patroni

Цель:

разворачивать отказоустойчивый кластер PostgreSQL для сохранения доступности сервиса при сбое узла
**

Поднял 3 виртуальные машины на базе Oracle Virtual Box (Лидер, реплика, синхр. реплика), настром плавающий адрес 
Лидер - 192.168.9.151
Реплика -  192.168.9.210
Синхрон. реплика - 192.168.9.220

<img width="466" height="424" alt="image" src="https://github.com/user-attachments/assets/3b47734f-e70e-492e-a4a6-966c2cfc23e1" />

Ставим на каждую ВМ пакета из репозиториЯ Ubuntu 24.04, PostgreSQL 16, Patroni 3.2.2-2 и etcd 3.4 

sudo apt install postgresql patroni python3-etcd etcd-server etcd-client pgbackrest prometheus-postgres-exporter

Нода PG, лидер:

<img width="1574" height="424" alt="image" src="https://github.com/user-attachments/assets/18630124-11ba-412c-9a83-be5850bdca40" />

Нода Node1, реплика:

<img width="1574" height="424" alt="image" src="https://github.com/user-attachments/assets/40f24c2b-be10-4676-a2db-596f2e47c1ad" />

Нода Node2, реплика:

<img width="1574" height="424" alt="image" src="https://github.com/user-attachments/assets/a9d48bfb-3fd6-4236-9768-ee4699c08fe9" />

