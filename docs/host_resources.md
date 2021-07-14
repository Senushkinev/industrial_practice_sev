Чтобы получить базовую информацию о доступных ресурсах хоста можно запустить host_resources.yml. Запускать нужно из папки ansible.
```
ansible-playbook playbooks/host_resources.yml
```
Если нужно узнать какую-то еще информацию о сервере стоит начать с модуля setup. 

Список хостов информацию о которых нужно узнать можно задать:
1. Через запятую.(2) 
2. Используя имена групп в которых они находятся.(3)
3. Если нужно узнать информацию о всех серверах можно написать all.(4)
```
1. ansible <список хостов> -m setup
2. ansible node1,node2 -m setup
3. ansible TWO_NODE,MANAGE_NODE3 -m setup
4. ansible all -m setup
```
   
Если вы ищите что-то конкретное и знаете поле в json файле, в котором оно находится можно добавить аргумент filter. В фильтре можно использовать простые регулярные выражения. 
```
ansible node1 -m setup -a "filter=ansible_os_family"
ansible node1 -m setup -a "filter=ansible_mem*"
ansible node1 -m setup -a 'filter=ansible_*_mb'
```
Если использовать аргумент gather_subset можно посмотреть уже сформированные множества фактов о сервере. Доступные множества all, min, hardware, network, virtual, ohai, facter. Множества можно задавать через запятую, так же с помощью ! можно исключать множества из коллекции с информацией.
```
ansible node1 -m setup -a "gather_subset=network,virtual"
ansible all -m setup -a 'gather_subset=!all,!any,facter'
```

Посмотреть свободное место на диске.
```
ansible node1 -m command -a "df -h"
```
Посмотреть все запущенные процессы на сервере и сколько они потребляют.
```
ansible node1 -m command -a "top -b -n 1"
```