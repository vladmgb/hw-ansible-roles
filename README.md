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

<details>
<summary>Запустил playbook</summary>
  
 ```

vova@Mynote:/mnt/c/Users/Vova$ ansible-playbook -i hw-ansible-roles/playbook/inventory/prod.yml hw-ansible-roles/playbook/site.yml

PLAY [Install Clickhouse] **********************************************************************************************************
TASK [Gathering Facts] *************************************************************************************************************ok: [clickhouse-01]

TASK [clickhouse : Include OS Family Specific Variables] ***************************************************************************ok: [clickhouse-01]

TASK [clickhouse : include_tasks] **************************************************************************************************included: /mnt/c/Users/Vova/hw-ansible-roles/playbook/roles/clickhouse/tasks/precheck.yml for clickhouse-01

TASK [clickhouse : Requirements check | Checking sse4_2 support] *******************************************************************ok: [clickhouse-01]

TASK [clickhouse : Requirements check | Not supported distribution && release] *****************************************************skipping: [clickhouse-01]

TASK [clickhouse : include_tasks] **************************************************************************************************included: /mnt/c/Users/Vova/hw-ansible-roles/playbook/roles/clickhouse/tasks/params.yml for clickhouse-01

TASK [clickhouse : Set clickhouse_service_enable] **********************************************************************************ok: [clickhouse-01]

TASK [clickhouse : Set clickhouse_service_ensure] **********************************************************************************ok: [clickhouse-01]

TASK [clickhouse : include_tasks] **************************************************************************************************included: /mnt/c/Users/Vova/hw-ansible-roles/playbook/roles/clickhouse/tasks/install/yum.yml for clickhouse-01

TASK [clickhouse : Install by YUM | Ensure clickhouse repo installed] **************************************************************ok: [clickhouse-01]

TASK [clickhouse : Install by YUM | Ensure clickhouse package installed (latest)] **************************************************skipping: [clickhouse-01]

TASK [clickhouse : Install by YUM | Ensure clickhouse package installed (version 25.3.4.190)] **************************************ok: [clickhouse-01]

TASK [clickhouse : include_tasks] **************************************************************************************************included: /mnt/c/Users/Vova/hw-ansible-roles/playbook/roles/clickhouse/tasks/configure/sys.yml for clickhouse-01

TASK [clickhouse : Check clickhouse config, data and logs] *************************************************************************ok: [clickhouse-01] => (item=/var/log/clickhouse-server)
ok: [clickhouse-01] => (item=/etc/clickhouse-server)
ok: [clickhouse-01] => (item=/var/lib/clickhouse/tmp/)
ok: [clickhouse-01] => (item=/var/lib/clickhouse/)

TASK [clickhouse : Config | Create config.d folder] ********************************************************************************ok: [clickhouse-01]

TASK [clickhouse : Config | Create users.d folder] *********************************************************************************ok: [clickhouse-01]

TASK [clickhouse : Config | Generate system config] ********************************************************************************ok: [clickhouse-01]

TASK [clickhouse : Config | Generate users config] *********************************************************************************ok: [clickhouse-01]

TASK [clickhouse : Config | Generate remote_servers config] ************************************************************************skipping: [clickhouse-01]

TASK [clickhouse : Config | Generate macros config] ********************************************************************************skipping: [clickhouse-01]

TASK [clickhouse : Config | Generate zookeeper servers config] *********************************************************************skipping: [clickhouse-01]

TASK [clickhouse : Config | Fix interserver_http_port and intersever_https_port collision] *****************************************skipping: [clickhouse-01]

TASK [clickhouse : Notify Handlers Now] ********************************************************************************************
TASK [clickhouse : include_tasks] **************************************************************************************************included: /mnt/c/Users/Vova/hw-ansible-roles/playbook/roles/clickhouse/tasks/service.yml for clickhouse-01

TASK [clickhouse : Ensure clickhouse-server.service is enabled: True and state: started] *******************************************ok: [clickhouse-01]

TASK [clickhouse : Wait for Clickhouse Server to Become Ready] *********************************************************************ok: [clickhouse-01]

TASK [clickhouse : include_tasks] **************************************************************************************************included: /mnt/c/Users/Vova/hw-ansible-roles/playbook/roles/clickhouse/tasks/configure/db.yml for clickhouse-01

TASK [clickhouse : Set ClickHose Connection String] ********************************************************************************ok: [clickhouse-01]

TASK [clickhouse : Gather list of existing databases] ******************************************************************************ok: [clickhouse-01]

TASK [clickhouse : Config | Delete database config] ********************************************************************************skipping: [clickhouse-01]

TASK [clickhouse : Config | Create database config] ********************************************************************************skipping: [clickhouse-01]

TASK [clickhouse : include_tasks] **************************************************************************************************included: /mnt/c/Users/Vova/hw-ansible-roles/playbook/roles/clickhouse/tasks/configure/dict.yml for clickhouse-01

TASK [clickhouse : Config | Generate dictionary config] ****************************************************************************skipping: [clickhouse-01]

TASK [clickhouse : include_tasks] **************************************************************************************************skipping: [clickhouse-01]

PLAY [Install Vector] **************************************************************************************************************
TASK [Gathering Facts] *************************************************************************************************************ok: [vector-01]

TASK [vector-role : Download vector packages] **************************************************************************************ok: [vector-01]

TASK [vector-role : Install vector packages] ***************************************************************************************ok: [vector-01]

TASK [vector-role : Apply vector template] *****************************************************************************************ok: [vector-01]

TASK [vector-role : Change vector systemd unit] ************************************************************************************ok: [vector-01]

PLAY [Install lighthouse] **********************************************************************************************************
TASK [Gathering Facts] *************************************************************************************************************ok: [lighthouse-01]

TASK [lighthouse-role : Install EPEL repository] ***********************************************************************************ok: [lighthouse-01]

TASK [lighthouse-role : Create Nginx repo file] ************************************************************************************ok: [lighthouse-01]

TASK [lighthouse-role : Update YUM cache] ******************************************************************************************ok: [lighthouse-01]

TASK [lighthouse-role : Install Nginx] *********************************************************************************************ok: [lighthouse-01]

TASK [lighthouse-role : Install Git] ***********************************************************************************************ok: [lighthouse-01]

TASK [lighthouse-role : Configure Nginx] *******************************************************************************************ok: [lighthouse-01]

TASK [lighthouse-role : Clone Lighthouse repository] *******************************************************************************changed: [lighthouse-01]

TASK [lighthouse-role : Disable default Nginx site] ********************************************************************************ok: [lighthouse-01]

TASK [lighthouse-role : Set correct permissions for Lighthouse] ********************************************************************changed: [lighthouse-01]

TASK [lighthouse-role : Configure Lighthouse Nginx site] ***************************************************************************changed: [lighthouse-01]

RUNNING HANDLER [lighthouse-role : Restart Nginx] **********************************************************************************changed: [lighthouse-01]

PLAY RECAP *************************************************************************************************************************
clickhouse-01              : ok=23   changed=0    unreachable=0    failed=0    skipped=10   rescued=0    ignored=0   
lighthouse-01              : ok=12   changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
vector-01                  : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
</details>


**Выложите playbook в репозиторий.**

Готово

**В ответе дайте ссылки на оба репозитория с roles и одну ссылку на репозиторий с playbook.**

[Ссылка на Lighthouse-role](https://github.com/vladmgb/lighthouse-role)

[Ссылка на Vector-role](https://github.com/vladmgb/vector-role)

[Ссылка на Playbook](https://github.com/vladmgb/hw-ansible-roles)
