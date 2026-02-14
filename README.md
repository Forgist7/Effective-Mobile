# Effective Mobile — DevOps Test Task

Это простое веб-приложение, развернутое с использованием Docker и Docker Compose.
Приложение состоит из backend-сервиса (Python HTTP server) и nginx в роли reverse proxy.

### Использованные технологии
* Docker
* Docker Compose
* Python (http.server)
* Nginx (reverse proxy)
* Linux networking (bridge)

### Архитектура проекта:

Приложение состоит из двух сервисов:
* backend — Python HTTP-сервер (порт 8080, доступен только внутри Docker-сети)
* nginx — reverse proxy (порт 80, доступен с хоста)

#### Схема взаимодействия:
```text
Client
   ↓
localhost:80
   ↓
nginx (reverse proxy)
   ↓
backend:8080 (docker network)
```
Nginx принимает HTTP-запросы и проксирует их во внутреннюю Docker-сеть на backend-сервис.
#### Структура проекта:
```text
.
├── .env
├── README.md
├── backend
│       ├── Dockerfile
│       └── app.py
├── docker-compose.yaml
└── nginx
    └── nginx.conf
```
### Настройка и запуск
#### 1. Клонирование репозитория
```bash
git clone https://github.com/Forgist7/Effective-Mobile.git
```
#### 2. Запуск через Docker Compose
```bash
docker compose up -d --build
```
Проверка статуса контейнеров:
```bash
docker ps
```
Ожидаемый результат:
```bash
effective_backend   effective_mobile-backend   "python app.py"          backend   6 minutes ago   Up 6 minutes (healthy)   8080/tcp
effective_nginx     nginx:1.29-alpine          "/docker-entrypoint.…"   nginx     6 minutes ago   Up 6 minutes             0.0.0.0:80->80/tcp, [::]:80->80/tcp
```
### Проверка работоспособности
После запуска приложение доступно по адресу:
```
http://localhost
```
Проверка через curl:
```bash
curl http://localhost
```
Ожидаемый ответ:
```text
Hello from Effective Mobile!
```