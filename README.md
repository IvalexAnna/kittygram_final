# 🐱 Kittygram

**Kittygram** — это веб-приложение для социальной сети, где пользователи могут делиться фотографиями своих кошек, создавать профили питомцев и отслеживать их достижения.

## 📋 Описание проекта

Kittygram представляет собой полнофункциональное веб-приложение, построенное по принципу микросервисной архитектуры. Проект состоит из:

- **Backend API** — Django REST API для управления данными
- **Frontend** — React приложение с современным UI
- **База данных** — PostgreSQL для хранения данных
- **Nginx** — веб-сервер и обратный прокси
- **Docker** — контейнеризация всех сервисов

## 🏗️ Архитектура

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Frontend  │    │   Backend   │    │     DB      │
│   (React)   │◄──►│   (Django)  │◄──►│ (PostgreSQL)│
└─────────────┘    └─────────────┘    └─────────────┘
       ▲                   ▲
       │                   │
       └─────── Nginx ─────┘
```

## 🚀 Технологии

### Backend
- **Django 3.2.3** — веб-фреймворк
- **Django REST Framework 3.12.4** — API фреймворк
- **Djoser 2.1.0** — аутентификация и авторизация
- **PostgreSQL** — база данных
- **Gunicorn** — WSGI сервер
- **Pillow** — обработка изображений

### Frontend
- **React 17.0.2** — JavaScript библиотека
- **React Router 5.3.0** — маршрутизация
- **CSS Modules** — стилизация компонентов

### DevOps
- **Docker & Docker Compose** — контейнеризация
- **GitHub Actions** — CI/CD пайплайн
- **Nginx** — веб-сервер и прокси
- **PostgreSQL 13** — база данных

## 📁 Структура проекта

```
kittygram_final/
├── backend/                 # Django backend
│   ├── cats/               # Основное приложение
│   │   ├── models.py       # Модели данных
│   │   ├── views.py        # API представления
│   │   ├── serializers.py  # Сериализаторы
│   │   └── admin.py        # Админ панель
│   ├── kittygram_backend/  # Основные настройки Django
│   ├── requirements.txt    # Python зависимости
│   └── Dockerfile         # Docker образ для backend
├── frontend/               # React frontend
│   ├── src/
│   │   ├── components/     # React компоненты
│   │   ├── utils/          # Утилиты и API
│   │   └── images/         # Статические изображения
│   ├── package.json        # Node.js зависимости
│   └── Dockerfile         # Docker образ для frontend
├── nginx/                  # Nginx конфигурация
├── docker-compose.yml      # Docker Compose для разработки
├── docker-compose.production.yml # Docker Compose для продакшена
└── kittygram_workflow.yml  # GitHub Actions CI/CD
```

## 🎯 Основной функционал

### Пользователи
- Регистрация и авторизация
- Профили пользователей
- Система токенов для API

### Кошки
- Создание профилей кошек
- Загрузка фотографий
- Указание цвета и года рождения
- Система достижений

### API Endpoints
- `POST /api/users/` — регистрация пользователя
- `POST /api/token/login/` — авторизация
- `GET /api/cats/` — список кошек
- `POST /api/cats/` — создание кошки
- `PUT /api/cats/{id}/` — редактирование кошки
- `DELETE /api/cats/{id}/` — удаление кошки

## 🚀 Быстрый старт

### Предварительные требования
- Docker и Docker Compose
- Git

### 1. Клонирование репозитория
```bash
git clone <your-repo-url>
cd kittygram_final
```

### 2. Создание .env файла
Создайте файл `.env` в корне проекта:
```env
POSTGRES_DB=django
POSTGRES_USER=django
POSTGRES_PASSWORD=your_password
DB_HOST=db
DB_PORT=5432
```

### 3. Запуск с Docker
```bash
docker-compose up -d
```

Приложение будет доступно по адресу: http://localhost:9000

## 🛠️ Разработка

### Backend (локально)
```bash
cd backend
python3 -m venv env
source env/bin/activate  # Linux/macOS
# или
env\Scripts\activate     # Windows

pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

### Frontend (локально)
```bash
cd frontend
npm install
npm start
```

## 🧪 Тестирование

### Backend тесты
```bash
cd backend
python manage.py test
```

### Frontend тесты
```bash
cd frontend
npm test
```

### Линтеры
```bash
# Backend
flake8 backend/

# Frontend
npm run lint
```

## 🚀 Деплой

Проект настроен для автоматического деплоя через GitHub Actions:

1. **Тестирование** — автоматические тесты backend и frontend
2. **Сборка Docker образов** — создание образов для всех сервисов
3. **Пуш в Docker Hub** — загрузка образов в реестр
4. **Деплой на сервер** — автоматическое развертывание
5. **Уведомления** — Telegram уведомления об успешном деплое

### Продакшен деплой
```bash
docker-compose -f docker-compose.production.yml up -d
```

## 📊 Модели данных

### User (Пользователь)
- Стандартная Django модель пользователя
- Связь один-ко-многим с кошками

### Cat (Кошка)
- `name` — имя кошки (макс. 16 символов)
- `color` — цвет кошки (макс. 16 символов)
- `birth_year` — год рождения
- `owner` — владелец (ForeignKey к User)
- `image` — фотография кошки
- `achievements` — достижения (ManyToMany через AchievementCat)

### Achievement (Достижение)
- `name` — название достижения (макс. 64 символа)

## 🔒 Безопасность

- JWT токены для аутентификации
- CORS настройки для API
- Валидация паролей Django
- Защищенные маршруты для авторизованных пользователей

## 📱 UI/UX особенности

- Адаптивный дизайн
- Модальные окна для форм
- Пагинация для списков
- Drag & Drop для загрузки изображений
- Современный минималистичный дизайн

## 🤝 Вклад в проект

1. Форкните репозиторий
2. Создайте ветку для новой функции
3. Внесите изменения
4. Создайте Pull Request


## 👥 Авторы

Ivanova Anna


---

**Kittygram** — место, где кошки становятся звездами! 🐾✨
