# docker-alpine
Пустой docker контейнер c Linux Alpine

## Установка из проекта arhone

Создание директории проекта
```
cd /srv
sudo mkdir docker-alpine
sudo chown $USER:$USER docker-alpine
```

Клонирование проекта
```
git clone https://github.com/arhone/docker-alpine.git ./docker-alpine
```

## Установка из своего проекта после форка

Создания deploy ключа для git

Имя файла указать docker-alpine (первый вопрос в ssh-keygen)
```
cd ~/.ssh/
ssh-keygen
```

```
nano config
```
Добавить в файл config
```
Host docker-alpine.github.com
    HostName github.com
    IdentityFile ~/.ssh/docker-alpine
```

Скопировать и добавить ключ в git, в ваш репозиторий
```
cat ~/.ssh/docker-alpine.pub
```

Создание директории проекта
```
cd /srv
sudo mkdir docker-alpine
sudo chown $USER:$USER docker-alpine
```

Клонирование проекта
```
git clone git@docker-alpine.github.com:ВАШ_ПРОЕКТ/docker-alpine.git /srv/docker-alpine
```

## Настройка
Копирование общего примера файла настроек в локальную версию файла
```
cp .env.example .env
```

Сборка и запуск контейнера

Используется docker compose v2 [Установка](https://github.com/arhone/debian-server-guide/blob/main/docker.md)
```
sudo docker compose -f docker-compose.yml up -d --build --remove-orphans
```

## Управление
Войти в контейнер
```
sudo docker exec -it docker-alpine-01 /bin/sh
```

Остановка/Запуск контейнера
```
sudo docker stop docker-alpine-01
sudo docker start docker-alpine-01
```

Просмотр логов контейнера
```
sudo docker logs --tail 50 --follow --timestamps docker-alpine-01
```

## Deploy
Загрузка и разворачивание проекта на удалённом сервере
```
. deploy.sh username@example.com
```

### Разрешить команду docker-compose без sudo
```
sudo visudo
```
Добавить запись
```
username ALL=NOPASSWD: /usr/bin/docker-compose
```


## Cron в контейнере
Пример команды
```
docker exec docker-alpine-01 /srv/docker-alpine/cron/example.sh
```

Открыть редактор заданий cron на host машине
```
crontab -e
```

Добавить запись
```
* * * * * docker exec docker-alpine-01 /srv/docker-alpine/cron/example.sh > /dev/null 2>&1
```

В файле /srv/docker-alpine/logs/example.cron.txt должна появится текущая дата
