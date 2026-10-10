# День 6. Bash-скрипты: условия, циклы, функции

## Основы
- `$0` — имя скрипта
- `if` — выполняет действия, если условие истинно
- `$1` — первый аргумент скрипта
- `$#` — количество аргументов
- `$?` — код возврата последней команды
- `exit 0` / `exit 1` — явно задать код возврата
- `$$` — PID скрипта

## Как проверить сервисы
- `systemctl list-unit-files --type=service | grep -q "^ssh.service"` — проверить существование
- `systemctl is-active ssh` — проверить статус (код `0` — активен)

## Пример моего скрипта
```bash
#!/bin/bash
if [ $# -ne 1 ]; then
    echo "Usage: $0 <service_name>"
    exit 3
fi

SERVICE="$1"

systemctl list-unit-files --type=service | grep -q "^${SERVICE}.service"
if [ $? -ne 0 ]; then
    echo "not found"
    exit 2
fi

if systemctl is-active "$SERVICE" > /dev/null 2>&1; then
    echo "running"
    exit 0
else
    echo "stopped"
    exit 1
fi
```
## Важные моменты
   - `> /dev/null 2>&1` — скрывает весь вывод команды

   - `grep -q` — не выводит результат, только код возврата

   - `exit` завершает скрипт и возвращает код
