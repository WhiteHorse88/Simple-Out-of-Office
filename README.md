# Slack Autoresponder Bot 🤖

Автоматичний відповідач для Slack, який реагує на смайлики в статусі.

## 🚀 Швидкий старт

### 1. Створи Slack App

1. Йди на https://api.slack.com/apps
2. Натисни **"Create New App"** → **"From scratch"**
3. Назва: `Autoresponder` (або будь-яка інша)
4. Вибери свій workspace
5. Натисни **"Create App"**

### 2. Налаштуй дозволи (Scopes)

**OAuth & Permissions** → **Scopes** → додай:

**Bot Token Scopes:**
- `chat:write` - відправляти повідомлення
- `im:history` - читати DM
- `im:write` - писати в DM
- `users:read` - читати інфо про користувачів
- `users.profile:read` - читати статуси користувачів

### 3. Увімкни Events

**Event Subscriptions:**
1. Увімкни Events
2. Request URL: `https://твій-домен.railway.app/slack/events` (поки не заповнюй, повернешся після деплою)
3. Subscribe to bot events:
   - `message.im` - отримувати DM повідомлення

### 4. Додай App Home

**App Home:**
1. Увімкни **Home Tab**
2. Увімкни **Messages Tab**

### 5. Встанови App у workspace

**Install App** → **Install to Workspace** → Дозволь

Скопіюй **Bot User OAuth Token** (починається з `xoxb-`)

### 6. Отримай Signing Secret

**Basic Information** → **App Credentials** → скопіюй **Signing Secret**

---

## 💻 Локальний запуск

### Передумови
- Docker встановлений
- Git встановлений

### Кроки:

1. **Клонуй репо:**
```bash
git clone https://github.com/твій-username/slack-autoresponder.git
cd slack-autoresponder
```

2. **Створи .env файл:**
```bash
cp .env.example .env
```

3. **Відредагуй .env:**
```env
SLACK_BOT_TOKEN=xoxb-твій-токен
SLACK_SIGNING_SECRET=твій-signing-secret
PORT=3000
```

4. **Запусти Docker:**
```bash
docker-compose up --build
```

5. **Для локального тестування (ngrok):**
```bash
# В іншому терміналі
npx ngrok http 3000
```

Скопіюй ngrok URL і додай `/slack/events` в Event Subscriptions

---

## 🚂 Деплой на Railway

### 1. Створи новий проєкт
1. Йди на https://railway.app
2. **New Project** → **Deploy from GitHub repo**
3. Вибери свій репо `slack-autoresponder`

### 2. Додай змінні оточення

**Variables:**
```
SLACK_BOT_TOKEN=xoxb-твій-токен
SLACK_SIGNING_SECRET=твій-signing-secret
PORT=3000
```

### 3. Отримай URL

Railway автоматично створить URL типу: `https://slack-autoresponder-production-xxxx.up.railway.app`

### 4. Онови Request URL в Slack

Повернись в **Event Subscriptions** і встав:
```
https://твій-railway-url.railway.app/slack/events
```

Натисни **Save Changes**

---

## 📖 Як користуватися

### 1. Відкрий App Home
- Знайди апку в Slack
- Перейди на вкладку **Home**

### 2. Додай правило
- Натисни **➕ Додати правило**
- Вибери емодзі (наприклад 🏖️)
- Напиши повідомлення для автовідповіді
- Натисни **Зберегти**

### 3. Використовуй
- Встанови статус з емодзі 🏖️
- Коли хтось напише тобі в DM
- Бот автоматично відповість

---

## 🛠 Розробка

### Структура проєкту:
```
slack-autoresponder/
├── src/
│   ├── app.js           # Основна логіка
│   ├── database.js      # SQLite база
│   ├── views/           # UI компоненти
│   └── utils/           # Допоміжні функції
├── Dockerfile
├── docker-compose.yml
├── package.json
└── .env.example
```

### Команди:
```bash
# Локальний запуск
docker-compose up

# Перебудувати
docker-compose up --build

# Зупинити
docker-compose down

# Логи
docker-compose logs -f
```

---

## 🐛 Troubleshooting

**Бот не відповідає:**
- Перевір чи правильний Request URL
- Перевір чи додані всі scopes
- Подивись логи в Railway

**Request URL не верифікується:**
- Почекай 1-2 хвилини після деплою
- Перевір чи правильний SLACK_SIGNING_SECRET

**База даних не зберігається:**
- Railway автоматично створює volume для `/data`

---

## 📝 Ліцензія

MIT
