# День 8. Git — контроль версий

## Что такое Git?
Это **распределённая система контроля версий**. Она запоминает все изменения файлов, позволяет откатываться к предыдущим версиям, работать в параллельных ветках и синхронизировать код между компьютерами.

## Основные понятия
- **Репозиторий (repo)** — папка, за которой следит Git (внутри есть скрытая папка `.git/`).
- **Коммит (commit)** — снимок состояния файлов с комментарием.
- **Ветка (branch)** — отдельная линия разработки.
- **Remote (удалённый репозиторий)** — копия на GitHub/GitLab.

## Основные команды

| Команда | Действие |
|---------|----------|
| `git init` | Создать новый репозиторий в текущей папке |
| `git status` | Показать, какие файлы изменены |
| `git add .` | Добавить все файлы в следующий коммит |
| `git add <файл>` | Добавить конкретный файл |
| `git commit -m "сообщение"` | Создать коммит с комментарием |
| `git log` | Показать историю коммитов |
| `git log --oneline` | Компактная история (один коммит — одна строка) |
| `git branch` | Показать список веток |
| `git branch -M main` | Переименовать текущую ветку в `main` |
| `git checkout -b <имя>` | Создать новую ветку и переключиться на неё |
| `git merge <ветка>` | Слить ветку с текущей |
| `git remote add origin <URL>` | Привязать удалённый репозиторий |
| `git remote -v` | Показать список удалённых репозиториев |
| `git push -u origin main` | Отправить коммиты на GitHub |

## Настройка Git (один раз)

```bash
git config --global user.name "Vlad"
git config --global user.email "v-amanov@users.noreply.github.com"
```
# Проверить настройки:
```bash

git config --global --list
```
Важно: email можно использовать «скрытый» от GitHub — вида твой_ник@users.noreply.github.com. Тогда твой настоящий адрес не попадёт в публичные коммиты.
GitHub: аутентификация через токен

GitHub не принимает обычный пароль при git push — нужен Personal Access Token (PAT).

# Как создать токен:

    GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)

    Generate new token (classic)

    Note: devops-notes, Expiration: 90 days

    Scope: галочка repo (полный доступ к репозиториям)

    Generate token → скопируй (показывается только один раз!)

Использование: при git push введи:

    Username: твой ник на GitHub

    Password: токен (не пароль от аккаунта)

Чтобы не вводить каждый раз:
```bash

git config --global credential.helper store
```
Типичный рабочий цикл
```bash

# 1. Проверить, что изменилось
git status

# 2. Добавить изменения
git add .

# 3. Закоммитить
git commit -m "Описание изменений"

# 4. Отправить на GitHub
git push
```
## Мой репозиторий

https://github.com/v-amanov/devops-notes
# Ошибки, с которыми я столкнулся

    fatal: not a git repository — пытался выполнить git-команду в папке без git init. Решение: cd в нужную папку и git init.

    Author identity unknown — Git не знает, кто ты. Решение:
    bash

git config --global user.name "Vlad"
git config --global user.email "v-amanov@users.noreply.github.com"

Could not resolve host: github.com — не работал DNS в ВМ. Решение: починил NAT/ICS на Windows + перезапустил сеть.

Опечатка в URL remote — deops-notes вместо devops-notes. Решение:
bash

git remote set-url origin https://github.com/v-amanov/devops-notes.git

Важные моменты

    Коммит делается в 3 шага: add → commit → push.

    .gitignore — файл со списком того, что Git должен игнорировать (например, *.log, __pycache__/).

    HEAD — указатель на текущий коммит (последний в текущей ветке).

    origin/main — ссылка на состояние ветки main в удалённом репозитории.

    SSH-ключ (из Дня 4) можно использовать вместо токена — удобнее на будущее.