

# Домашнее задание к занятию «Docker. Часть 2»  Петров Петр

### Задание 1
Напишите ответ в свободной форме, не больше одного абзаца текста.
Установите Docker Compose и опишите, для чего он нужен и как может улучшить вашу жизнь.
### Решение 1
Docker Compose — это инструмент, который позволяет легко управлять многоконтейнерными приложениями в Docker. С его помощью можно описать архитектуру приложения в одном YAML-файле, что упрощает развертывание и управление зависимостями между контейнерами. Например, вы можете запускать веб-сервер, базу данных и кэш-сервер одновременно с одной командой. Это значительно ускоряет процесс разработки и тестирования, позволяет избежать конфликтов конфигураций и упрощает переносимость приложений между различными средами. В результате, Docker Compose делает жизнь разработчиков проще и эффективнее, позволяя сосредоточиться на написании кода, а не на настройке окружений.

### Задание 2
Выполните действия и приложите текст конфига на этом этапе.

Создайте файл docker-compose.yml и внесите туда первичные настройки:

version;
services;
networks.
При выполнении задания используйте подсеть 172.22.0.0. Ваша подсеть должна называться: <ваши фамилия и инициалы>-my-netology-hw.
### Решение 2
```
services:
  app:
    image: nginx
    networks:
      - petrovpg-my-netology-hw

networks:
  petrovpg-my-netology-hw:
    ipam:
      config:
        - subnet: 172.22.0.0/16

```
### Задание 3
Выполните действия и приложите текст конфига текущего сервиса:

Установите PostgreSQL с именем контейнера <ваши фамилия и инициалы>-netology-db.
Предсоздайте БД <ваши фамилия и инициалы>-db.
Задайте пароль пользователя postgres, как <ваши фамилия и инициалы>12!3!!
Пример названия контейнера: ivanovii-netology-db.
Назначьте для данного контейнера статический IP из подсети 172.22.0.0/24.
### Решение 3
```
version: '3.8'

services:
  netology-db:
    image: postgres:latest
    environment:
      POSTGRES_DB: petrovpg-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.10

networks:
  petrovpg-my-netology-hw:
    ipam:
      config:
        - subnet: 172.22.0.0/24
```
### Задание 4
Выполните действия:

Установите pgAdmin с именем контейнера <ваши фамилия и инициалы>-pgadmin.
Задайте логин администратора pgAdmin <ваши фамилия и инициалы>@ilove-netology.com и пароль на выбор.
Назначьте для данного контейнера статический IP из подсети 172.22.0.0/24.
Прокиньте на 80 порт контейнера порт 61231.
В качестве решения приложите:

текст конфига текущего сервиса;
скриншот админки pgAdmin.
### Решение 4
```
version: '3.8'

services:
  netology-db:
    image: postgres:latest
    container_name: petrovpg-netology-db
    environment:
      POSTGRES_DB: petrovpg-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.10

  petrovpg-pgadmin:
    image: dpage/pgadmin4
    container_name: petrovpg-pgadmin
    environment:
      PGADMIN_DEFAULT_EMAIL: petrovpg@ilove-netology.com
      PGADMIN_DEFAULT_PASSWORD: petrovpg12!3!!
    ports:
      - "61231:80"
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.20

networks:
  petrovpg-my-netology-hw:
    ipam:
      config:
        - subnet: 172.22.0.0/24

```
![image](https://github.com/user-attachments/assets/d4354705-5189-48f6-98df-dfee2c7ba2ad)
![image](https://github.com/user-attachments/assets/830986e3-0980-430e-8123-b6e7818effa2)
### Задание 5
Выполните действия и приложите текст конфига текущего сервиса:

Установите Zabbix Server с именем контейнера <ваши фамилия и инициалы>-zabbix-netology.
Настройте его подключение к вашему СУБД.
Назначьте для данного контейнера статический IP из подсети 172.22.0.0/24.
### Решение 5
```

version: '3.8'

services:
  petrovpg-netology-db:
    image: postgres:latest
    container_name: petrovpg-netology-db
    environment:
      POSTGRES_DB: petrovpg-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.10

  petrovpg-pgadmin:
    image: dpage/pgadmin4
    container_name: petrovpg-pgadmin
    environment:
      PGADMIN_DEFAULT_EMAIL: petrovpg@ilove-netology.com
      PGADMIN_DEFAULT_PASSWORD: petrovpg12!3!!
    ports:
      - "61231:80"
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.20

  petrovpg-zabbix-netology:
    image: zabbix/zabbix-server-pgsql:latest
    container_name: petrovpg-zabbix-netology
    environment:
      DB_SERVER_HOST: petrovpg-netology-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
      POSTGRES_DB: petrovpg-db
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.30

networks:
  petrovpg-my-netology-hw:
    ipam:
      config:
        - subnet: 172.22.0.0/24
```
### Задание 6
Задание 6
Выполните действия и приложите текст конфига текущего сервиса:

Установите Zabbix Frontend с именем контейнера <ваши фамилия и инициалы>-netology-zabbix-frontend.
Настройте его подключение к вашему СУБД.
Назначьте для данного контейнера статический IP из подсети 172.22.0.0/24.
### Решение 6
```
version: '3.9'

services:
  petrovpg-netology-db:
    image: postgres:latest
    container_name: petrovpg-netology-db
    environment:
      POSTGRES_DB: petrovpg-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.10

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin
    environment:
      PGADMIN_DEFAULT_EMAIL: petrovpg@ilove-netology.com
      PGADMIN_DEFAULT_PASSWORD: petrovpg12!3!!
    ports:
      - "61231:80"
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.20

  petrovpg-zabbix-netology:
    image: zabbix/zabbix-server-pgsql:latest
    container_name: petrovpg-zabbix-netology
    environment:
      DB_SERVER_HOST: petrovpg-netology-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
      POSTGRES_DB: petrovpg-db
    depends_on:
      - petrovpg-netology-db
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.30

  petrovpg-netology-zabbix-frontend:
    image: zabbix/zabbix-web-nginx-pgsql:latest
    container_name: petrovpg-netology-zabbix-frontend
    environment:
      DB_SERVER_HOST: petrovpg-netology-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
      POSTGRES_DB: petrovpg-db
      ZBX_SERVER_HOST: petrovpg-zabbix-netology
      PHP_TZ: Europe/Moscow
    ports:
      - "8080:8080"
    depends_on:
      - petrovpg-zabbix-netology
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.40

networks:
  petrovpg-my-netology-hw:
    driver: bridge
    ipam:
      config:
        - subnet: 172.22.0.0/24
```
### Задание 7
Выполните действия.

Настройте линки, чтобы контейнеры запускались только в момент, когда запущены контейнеры, от которых они зависят.

В качестве решения приложите:

текст конфига целиком;
скриншот команды docker ps;
скриншот авторизации в админке Zabbix.
### Решение 7
```
version: '3.9'

services:
  petrovpg-netology-db:
    image: postgres:latest
    container_name: petrovpg-netology-db
    environment:
      POSTGRES_DB: petrovpg-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.10
    restart: unless-stopped

  pgadmin:
    image: dpage/pgadmin4
    container_name: pgadmin
    environment:
      PGADMIN_DEFAULT_EMAIL: petrovpg@ilove-netology.com
      PGADMIN_DEFAULT_PASSWORD: petrovpg12!3!!
    ports:
      - "61231:80"
    depends_on:
      - petrovpg-netology-db
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.20
    restart: unless-stopped

  petrovpg-zabbix-netology:
    image: zabbix/zabbix-server-pgsql:latest
    container_name: petrovpg-zabbix-netology
    environment:
      DB_SERVER_HOST: petrovpg-netology-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
      POSTGRES_DB: petrovpg-db
    depends_on:
      - petrovpg-netology-db
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.30
    restart: unless-stopped

  petrovpg-netology-zabbix-frontend:
    image: zabbix/zabbix-web-nginx-pgsql:latest
    container_name: petrovpg-netology-zabbix-frontend
    environment:
      DB_SERVER_HOST: petrovpg-netology-db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: petrovpg12!3!!
      POSTGRES_DB: petrovpg-db
      ZBX_SERVER_HOST: petrovpg-zabbix-netology
      PHP_TZ: Europe/Moscow
    ports:
      - "8080:8080"
    depends_on:
      - petrovpg-netology-db
      - petrovpg-zabbix-netology
    networks:
      petrovpg-my-netology-hw:
        ipv4_address: 172.22.0.40
    restart: unless-stopped

networks:
  petrovpg-my-netology-hw:
    driver: bridge
    ipam:
      config:
        - subnet: 172.22.0.0/24
```
![image](https://github.com/user-attachments/assets/bc837245-c80b-44e8-b2c2-cedbd568a43b)

![image](https://github.com/user-attachments/assets/27072df9-97d2-4c45-934e-f3336220a793)

### Задание 8
Выполните действия:

Убейте все контейнеры и потом удалите их.
Приложите скриншот консоли с проделанными действиями.
### Решение 8

![image](https://github.com/user-attachments/assets/e6ceef27-b0d0-42a1-b8bd-168550b2a6df)

![image](https://github.com/user-attachments/assets/d59eab12-f5a9-4c88-bc31-4153337dc985)
