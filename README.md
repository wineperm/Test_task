# Инструкция по использованию и настройке проекта

## Обзор проекта

Этот проект представляет собой Dockerized веб-приложение, развернутое с использованием Ansible для автоматизации развертывания. Проект включает в себя следующие компоненты:

- **PHP-FPM**: Контейнер для обработки PHP-скриптов.
- **NGINX**: Контейнер для веб-сервера.
- **MySQL**: Контейнер для базы данных.
- **phpMyAdmin**: Контейнер для управления базой данных через веб-интерфейс.

## Структура проекта

```
Test_task/
    ├── ansible/
    │   ├── inventory
    │   ├── playbook.yml
    │   └── roles/
    │       ├── docker/
    │       │   ├── files/
    │       │   │   └── docker-compose.yml
    │       │   └── tasks/
    │       │       └── main.yml
    │       ├── nginx/
    │       │   ├── files/
    │       │   │   └── Dockerfile
    │       │   ├── tasks/
    │       │   │   └── main.yml
    │       │   └── templates/
    │       │       └── nginx.conf.j2
    │       └── php/
    │           ├── files/
    │           │   ├── Dockerfile
    │           │   ├── index.php
    │           │   └── test_db.php
    │           └── tasks/
    │               └── main.yml
```

## Основные файлы и их назначение

- **ansible/inventory**: Файл инвентаря Ansible, содержащий информацию о серверах.
- **ansible/playbook.yml**: Playbook Ansible для автоматизации развертывания.
- **ansible/roles/docker/files/docker-compose.yml**: Файл конфигурации Docker Compose для запуска всех контейнеров.
- **ansible/roles/nginx/files/Dockerfile**: Dockerfile для создания контейнера NGINX.
- **ansible/roles/nginx/templates/nginx.conf.j2**: Шаблон конфигурации NGINX.
- **ansible/roles/php/files/Dockerfile**: Dockerfile для создания контейнера PHP-FPM.
- **ansible/roles/php/files/index.php**: Основной PHP-скрипт.
- **ansible/roles/php/files/test_db.php**: Скрипт для тестирования подключения к базе данных.

## Как использовать проект

### Установка Ansible

Убедитесь, что у вас установлен Ansible. Вы можете установить его с помощью pip:

```bash
pip install ansible
```

### Настройка инвентаря

Откройте файл `ansible/inventory` и убедитесь, что информация о сервере верна. Пример:

```ini
[web]
89.169.157.40 ansible_user=qwerty ansible_ssh_private_key_file=/home/qwerty/.ssh/id_ed25519
```

### Запуск Playbook

Запустите Playbook Ansible для развертывания проекта на удаленном сервере:

```bash
ansible-playbook -i ansible/inventory ansible/playbook.yml
```

## Как настроить и кастомизировать проект

### Настройка Docker Compose

Откройте файл `ansible/roles/docker/files/docker-compose.yml` и измените конфигурацию по необходимости. Например, вы можете изменить версии образов Docker или переменные окружения.

### Настройка PHP-скриптов

Откройте файлы `ansible/roles/php/files/index.php` и `ansible/roles/php/files/test_db.php` и измените их по своему усмотрению.

### Настройка конфигурации NGINX

Откройте файл `ansible/roles/nginx/templates/nginx.conf.j2` и измените конфигурацию NGINX. Например, вы можете изменить корневую директорию или настройки логов.

### Настройка Playbook Ansible

Откройте файл `ansible/playbook.yml` и измените задачи по необходимости. Например, вы можете добавить новые задачи для установки дополнительных пакетов или изменения конфигурации.

## Примеры кастомизации

### Изменение версии PHP

Откройте файл `ansible/roles/php/files/Dockerfile` и измените строку `FROM php:8.2-fpm` на нужную версию PHP.

### Изменение конфигурации MySQL

Откройте файл `ansible/roles/docker/files/docker-compose.yml` и измените переменные окружения для MySQL:

```yaml
environment:
  MYSQL_ROOT_PASSWORD: new_password
  MYSQL_DATABASE: new_database
  MYSQL_USER: new_user
  MYSQL_PASSWORD: new_password
```

### Добавление нового PHP-скрипта

Создайте новый файл в директории `ansible/roles/php/files/` и добавьте его в Playbook Ansible:

```yaml
- name: Copy new PHP script
  copy:
    src: new_script.php
    dest: "{{ project_path }}/app/new_script.php"
```

## Заключение

Этот проект предоставляет базовую структуру для развертывания Dockerized веб-приложения с использованием Ansible. Вы можете легко настроить и кастомизировать его под свои нужды, изменяя конфигурационные файлы и Playbook Ansible.
