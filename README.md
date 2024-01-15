# KuberNet
## Задание1
### Docker 
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

### Kuber
1. Перейти на платформу «Play with Kubernetes» (https://labs.play-with-k8s.com/) и зарегистрироваться.
2. Первым шагом является инициализация кластера. Выполните на master пункт 1 из приветствия:
```
kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16 
```
Это займет пару минут, в течение которых вы увидите большую активность в терминале.
В конце вы увидите что-то вроде этого:
![image](https://github.com/user-2305/KuberNet/assets/95847398/88eba9fa-17ba-4fc7-948c-df7bc62ac7ab)
Скопируйте всю строку, начинающуюся kubeadm join из первого терминала, и вставьте ее во второй и третий терминалы.
Пример:
```
kubeadm join 192.168.0.23:6443 --token wng5kx.myjvi1p3vc25i62s \
--discovery-token-ca-cert-hash sha256:dd8138809bf8c943a198c2fe1b394393074da8da50b4c5a6069fb9bd10bb472f
```
Теперь нужно инициализировать сеть кластера в первом терминале, выполнив предписание №2 из сохраненного приветствия:
```
kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml
```
Ваш кластер настроен!

