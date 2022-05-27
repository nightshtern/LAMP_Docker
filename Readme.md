# LAMP in Docker
## _Installing LAMP in Docker containers with Ansible_

Данный playbook разворачивает стек LAMP  с запущенным в нем CMS Bitrix, готовым к инсталляции.
### Используемое ПО  
- Apache
- Nginx
- PHP 7.4.29 в качестве модуля Apache
- MySQL
- Docker
- Ansible

В качестве хостовой ОС используется Ubuntu 20.04

## Порядок установки

Установим Ansible:
```sh
sudo apt install -y ansible
```
Установим модуль Ansible community.docker:
```sh
ansible-galaxy collection install community.docker
```

Вносим домен/ip-адресс сервера в файл hosts.ini:

```sh
cd  ~/LAMP_Docker
nano hosts.ini ansible_user=root
```
При желании можно изменить переменные для MySQL:
```sh
nano configs/docker-compose.yml
```
>MYSQL_ROOT_PASSWORD: 'password'

>MYSQL_DATABASE: 'bitrix'

>MYSQL_USER: 'bitrix'

>MYSQL_PASSWORD: 'passwd'

Для изменения доменного имени в конфигурации Apache и Nginx необходимо изменить переменную servername в файле playbook.yml:

```sh
  vars:
    servername: "example.ru"

```

Запуск playbook'a Ansible:
```sh
ansible-playbook playbook.yml -i hosts.ini
```
После выполнения вышеперечисленных действий на серер установяться в Docker-контерйнерах web-сервер Apache с модулем PHP, БД MySQL, Nginx для редиректа запросов и CMS Bitrix, полностью готовая к установке сайта.
