# Домашнее задание к занятию 4 «Работа с roles»
## Что нужно сделать

**Создайте в старой версии playbook файл requirements.yml и заполните его содержимым:**

```
---
  - src: git@github.com:AlexeySetevoi/ansible-clickhouse.git
    scm: git
    version: "1.13"
    name: clickhouse 
```

**При помощи ansible-galaxy скачайте себе эту роль.**

<img width="1085" height="155" alt="image" src="https://github.com/user-attachments/assets/8dd8d5d4-3fd7-4491-8503-de278d855a16" />


**Создайте новый каталог с ролью при помощи ansible-galaxy role init vector-role.**

<img width="1042" height="66" alt="image" src="https://github.com/user-attachments/assets/0c8b13ae-94f2-48df-8088-51876d4be3c5" />


**На основе tasks из старого playbook заполните новую role. Разнесите переменные между vars и default.**

Сделано.

**Перенести нужные шаблоны конфигов в templates.**

Сделано.

**Опишите в README.md обе роли и их параметры.**

[Документация Vector-role](https://github.com/vladmgb/hw-ansible-roles/blob/main/playbook/roles/vector-role/README.md)

[Документация Lighthouse-role](https://github.com/vladmgb/hw-ansible-roles/blob/main/playbook/roles/lighthouse-role/README.md)

**Повторите шаги 3–6 для LightHouse. Помните, что одна роль должна настраивать один продукт.**

Сделано.

<img width="902" height="335" alt="image" src="https://github.com/user-attachments/assets/6fd536cb-36b5-4849-a596-b5e828c1fd92" />


**Выложите все roles в репозитории. Проставьте теги, используя семантическую нумерацию. Добавьте roles в requirements.yml в playbook.**

Сделано

```
---
- src: https://github.com/AlexeySetevoi/ansible-clickhouse.git
  scm: git
  version: "1.13"
  name: clickhouse

- src: https://github.com/vladmgb/vector-role.git
  scm: git
  version: "v1.1"
  name: vector-role

- src: https://github.com/vladmgb/lighthouse-role.git
  scm: git
  version: "1.1"
  name: lighthouse-role

```

**Переработайте playbook на использование roles. Не забудьте про зависимости LightHouse и возможности совмещения roles с tasks.**



**Выложите playbook в репозиторий.**

Готово

**В ответе дайте ссылки на оба репозитория с roles и одну ссылку на репозиторий с playbook.**

[Ссылка на Lighthouse-role](https://github.com/vladmgb/lighthouse-role)

[Ссылка на Vector-role](https://github.com/vladmgb/vector-role)

[Ссылка на Playbook](https://github.com/vladmgb/hw-ansible-roles)
