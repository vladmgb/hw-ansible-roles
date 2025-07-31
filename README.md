# Установка Сlickhouse и Vector
Playbook:

- Загружается дистрибутивы указанные в group_vars
- Устанавливается Clickhouse
- Запускает clickhouse-server
- Устанавливается Vector на основе шаблонов
- Запускается Vector

Чтобы работал playbook:

1. Необходимо предоставить доступы для работы ansible на хостах через ssh.
2. Добавить ip-адрес серверов в inventory.
3. Указать имя пользователя в inventory.
4. В файлах vars необходимо указать версии дистрибутивов.

Запуск playbook:
`ansible-playbook -i inventory/prod.yml site.yml`
