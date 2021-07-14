# Инструкция по настройке

Вначале нужно установить docker и ansible.

Установка docker:
```
 curl https://get.docker.com > /tmp/install.sh
 chmod +x /tmp/install.sh
 /tmp/install.sh
```

Установка ansible:
```
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible
```

Чтобы иметь доступ к контейнеру по ключу нужно на локальной машине сгенирировать пару ключей и передать в контейнер открытый ключ.

Генерация ключей:
```
ssh-keygen
```
После этого нужно создать папку key и скопировать в нее открытый ключи и переименовать его в **authorized_keys**
```
 mkdir ./manageNode/key
 cp ~/.ssh/id_rsa.pub <путь до cклонированного репозитория>/manageNode/key/authorized_keys
```
Теперь во время сборки образа открытый ключ будет скопирован в контейнер.

---

Чтобы проверить, что все работает, нужно зайти в папку **manageNode** и создать образ из Dockerfile:
```
 docker-compose build
```
Теперь можно запустить созданные контейнеры:
```
 docker-compose up -d
```
Флаг -d позволяет запустить контейнеры в фоне.

Теперь нужно зайти в папку ansible и кинуть ping к запущенным контейнерам:
```
 ansible all -m ping
```
или
```
 ansible-playbook playbooks/ping_all_servers.yml
```
Если ответ похож на это, значит все работает корректно:
```
node2 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
node3 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
node1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
``` 
или это
```
TASK [Ping my servers] ******************************************************************************************************************************
ok: [node1]
ok: [node2]
ok: [node3]
```
Чтобы остановить контейнеры и удалить их:
```
 docker-compose stop
 docker-compose rm
``` 
---
Если вдруг понадобилось авторизовываться с помощью пароля нужно добавить в Dockerfile:
```Dockerfile
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' etc/ssh/sshd_config
```
В файле **MANAGE_NODE** заменить *ansible_ssh_private_key_file : ~/.ssh/id_rsa* на *ansible_ssh_pass : 1234*