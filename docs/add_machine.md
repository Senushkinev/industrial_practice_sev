Чтобы увеличить количество виртуальных docker-машин нужно добавить еще один managenode по шаблону в **manageNode/docker-compose.yml**.  
```
  <Уникальное имя сервиса>:
    container_name: <Уникальное имя контейнера>
    build: .
    networks:
      app_net:
        ipv4_address: 172.16.238.<Не занятый IP>
```

После добавления новой машин в docker-compose.yml нужно добавить информацию о нем в **ansible/inventory.txt** тоже по уже существующему шаблону. 
```
[<Уникальное имя группы>]
<Уникальное имя>   ansible_host=172.16.238.<Адресс контейнера из docker-compose.yml>
```

Чтобы ansible знал, где ключ для сервера, нужно добавить в машину в группу *MANAGE_NODES* в **ansible/inventory.txt**
```
[MANAGE_NODES]
<Добавить в группу имя группы новый машины>
```