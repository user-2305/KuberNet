# KuberNet

Для создания образа и контейнера из Dockerfile, вам потребуется выполнить следующие шаги:

1. Установите Docker на вашей операционной системе.

2. Создайте Dockerfile в вашем проекте.
```
FROM node:7
ADD app.js /app.js
ENTRYPOINT ["node", "app.js"]
```
3. Откройте терминал и перейдите в директорию, где находится ваш Dockerfile.

4. Выполните следующую команду, чтобы собрать образ из вашего Dockerfile:
```
docker build -t <имя_образа> .
```
Пример:
```
docker build -t replica_set .
```

5. Авторизуйтесь в Docker Hub. Выполните следующую команду для аутентификации:
```bash
docker login
```

6. Теперь, чтобы загрузить образ на Docker Hub, используйте команду `docker tag` для присвоения тегу образа, который указывает на репозиторий Docker Hub:
```bash
docker tag <имя_локального_образа> <имя_репозитория>/<имя_образа>:<тег>
```
Пример:
```bash
docker tag replica_set user2305/replica_set:v1
```

7. Выполните команду `docker push`, чтобы загрузить образ на Docker Hub:
```bash
docker push <имя_репозитория>/<имя_образа>:<тег>
```
Пример:
```bash
docker push user2305/replica_set:v1
```
