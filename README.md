# 🏋️ 365-Дневный Челлендж

Веб-приложение для отслеживания 365-дневного фитнес-челленджа с общим лидербордом.

**Живой сайт:** [fuckfishing.ru/365daychallenge](https://fuckfishing.ru/365daychallenge)

---

## Возможности

- **Сетка 365 дней** — отмечай каждый день тренировки
- **17 типов активности** — бег, силовые, бокс, плавание, рыбалка и др.
- **Длительность и ощущение** — фиксируй время и самочувствие
- **Достижения** — разблокируются по мере прогресса
- **Лидерборд** — общий рейтинг через Firebase Realtime Database
- **Синхронизация между устройствами** — по уникальному коду
- **Лимит** — не более 1 ячейки в день (редактирование без ограничений)
- **Экспорт / Импорт** — сохранение данных в JSON

---

## Технологии

- Чистый HTML/CSS/JS — без фреймворков
- [Firebase Realtime Database](https://firebase.google.com) — лидерборд и синхронизация

---

## Установка и запуск

### 1. Клонируй репозиторий

```bash
git clone https://github.com/fotoff/365daychallenge.git
cd 365daychallenge
```

### 2. Создай Firebase проект

1. Открой [console.firebase.google.com](https://console.firebase.google.com)
2. Создай новый проект
3. Перейди в **Realtime Database** → создать в режиме **test**
4. В настройках проекта добавь веб-приложение (`</>`) и скопируй конфиг

### 3. Вставь Firebase конфиг

В `index.html` найди и замени:

```js
const FIREBASE_CONFIG = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT-default-rtdb.firebaseio.com",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "000000000000",
  appId: "YOUR_APP_ID"
};
```

### 4. Разверни на сервере

```bash
scp index.html user@yourserver:/var/www/html/365daychallenge/index.html
```

Или просто открой `index.html` в браузере — без сервера тоже работает (лидерборд требует Firebase).

---

## Синхронизация между устройствами

1. На первом устройстве зайди в **Лидерборд** → введи имя → появится **код** (например `K7X2PQ`)
2. На втором устройстве зайди в **Лидерборд** → введи код в поле "Уже участвую с другого устройства"
3. Данные подтянутся автоматически

---

## Структура Firebase

```
leaderboard/
  {uid}/
    name: "wardarc"
    done: 42
    hours: 38.5
    typeList: ["Бег", "Бокс", "Ходьба"]
    cells: { 1: {...}, 2: {...}, ... }
    updated: 1234567890
```

