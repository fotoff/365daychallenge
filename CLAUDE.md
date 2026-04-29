# 365daychallenge

Статический одностраничный SPA для трекинга 365-дневного фитнес-челленджа. Без бэкенда: данные хранятся в `localStorage` и синхронизируются через **Firebase Realtime Database**.

## Стек

- Чистый HTML/CSS/JS, без сборки и фреймворков
- Firebase Realtime DB (`compat` SDK 9.23.0)
- Шрифт Inter из Google Fonts

## Файлы

- `index.html` — всё приложение (UI, стили, логика, ~49 КБ, единый файл)
- `plan.html` — отдельная страница плана/правил (~24 КБ)

## Деплой

Сервер: `ssh -i ~/.ssh/bot_server_key root@91.201.114.128`
Путь: `/var/www/html/365daychallenge/`
URL: https://fuckfishing.ru/365daychallenge

Деплой = `scp index.html ...`. Никакого build-step нет.

## Идентификация пользователей

- Нет логина/пароля
- При создании генерится 6-символьный `userUID` (например `8CAWK5`) — он же «код входа»
- На другом устройстве: вводят этот код через `connectWithCode` → подтягиваются `cells` из Firebase
- Все данные пользователя в Firebase: `leaderboard/{uid}/{name, done, hours, typeList, cells, startDate, updated}`

## Ключевые состояния ячейки

- `done` — заполнена, ≥30 мин (зелёная)
- `done.short` — заполнена, <30 мин (оранжевая)
- `done.multi` — несколько типов активности (счётчик)
- `missed` — пропущена (красная), вычисляется как `cellDate < today` относительно `challengeStartDate`
- пустая будущая — нейтральная

## Известные баги/особенности

- `connectWithCode` не подгружает `startDate` с сервера → missed-дни не подсвечиваются красным до перезагрузки страницы
- В Firebase встречаются записи без `startDate` (старые миграции), для них missed не вычисляется

## Firebase config

Хардкод в `index.html`. Проект: `daychallenge-1572f`. Правила DB — в test-режиме (открытое чтение/запись).

## Тестирование

Открыть `index.html` напрямую в браузере (file://) или через `python3 -m http.server`. Firebase работает с любого origin.
