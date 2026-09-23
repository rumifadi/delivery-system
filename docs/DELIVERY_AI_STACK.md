# AI-Powered Delivery System — Full Stack Guide

Этот документ содержит практический стек технологий, MCP-серверы, плагины, skills, инструменты, команды установки и рекомендации для разработки курьерского сервиса с AI-интеграцией.

## 1. Полный стек технологий

### 1.1 Мобильные приложения

#### React Native + Expo
Плюсы:
- один код для iOS и Android
- быстрая разработка
- простой доступ к геолокации, картам, push-уведомлениям, native API
- сильная экосистема

Рекомендуемые технологии:
- React Native
- Expo
- TypeScript
- React Navigation
- Zustand
- React Native Maps
- Firebase Cloud Messaging
- AsyncStorage
- Socket.IO client
- Expo Notifications

#### Flutter (альтернатива)
Плюсы:
- высокая производительность UI
- очень качественный рендеринг
- один код для нескольких платформ

Но:
- команда может быть менее подготовлена к Dart
- иногда требуется больше времени на кастомизацию UX
- экосистема может быть менее привычна для JS-команд

Рекомендуемый вариант:
- React Native + Expo + TypeScript

---

### 1.2 Backend

#### Основной backend
- Node.js + TypeScript
- NestJS (лучший вариант для крупных проектов)
- Express + TypeScript (быстрый MVP)

Плюсы NestJS:
- модульная структура
- DI и сервисы
- хорошие DTO и Validation
- проще масштабировать проект

#### AI-сервис
- Python + FastAPI
- это лучше для ML, маршрутов, прогнозирования, OR-Tools, интеграций с AI

Рекомендуемый стек:
- NestJS / TypeScript для основного API
- FastAPI для AI-сервиса
- PostgreSQL + PostGIS
- Redis
- Socket.IO

---

### 1.3 База данных

#### PostgreSQL
Основная база данных для пользователей, заказов, курьеров, маршрутов.

#### PostGIS
Полезно для:
- геолокации
- расчёта расстояний
- поиска заказов рядом
- геозон

#### Redis
Для:
- кэширования
- очередей
- сессий
- частых вычислений
- временных данных

---

### 1.4 AI и маршрутизация

#### OR-Tools
Google OR-Tools — лучший инструмент для математической оптимизации маршрутов.

Используется для:
- Vehicle Routing Problem (VRP)
- планирования маршрутов
- оптимизации обязанностей курьеров
- распределения заказов по курьерам
- расчёта “лучшего маршрута” при заданных ограничениях

#### scikit-learn
Для:
- прогнозирования ETA
- прогнозирования спроса
- анализа временных паттернов
- оценки загрузки районов

#### NumPy / Pandas
Для:
- подготовки и анализа данных
- расчётов
- добавления временных и гео-предикторов

#### Claude API / OpenAI API
Для:
- support chat
- автоматизации задач
- генерации текстов
- summarization
- анализа заказов
- интеллектуального контекста
- ассистента для администраторов

Важно:
- LLM следует использовать как “интеллектуальный слой”
- вычисления и маршрутизация должны оставаться в детерминированной логике
- маршруты и цены никогда не должны вычисляться только через AI без правил

---

### 1.5 Карты и геолокация

Рекомендуемые сервисы:
- Google Maps API
- Google Places
- Mapbox
- Yandex Maps
- OpenRouteService
- TomTom Routing API

Для мобильных приложений:
- react-native-maps
- geocoding
- routing API
- distance matrix API

---

### 1.6 Уведомления и коммуникации

- Firebase Cloud Messaging (FCM)
- Twilio
- WebSocket / Socket.IO
- email
- Telegram / WhatsApp / SMS

Используется для:
- статусов заказа
- приближения курьера
- уведомлений клиенту
- уведомлений курьеру
- админских событий

---

### 1.7 Платежи

- Stripe
- YooKassa
- PayPal
- внутренний wallet/balance

Подходит для:
- оплат до/после доставки
- комиссий
- удержания депозита
- подписок / абонентских планов

---

### 1.8 Хранение файлов

- S3 / MinIO
- Firebase Storage
- Cloudinary
- локальное хранилище в dev-среде

Используется для:
- фото доставки
- подтверждение получения
- аватарки пользователей
- документы курьера
- логистика/чек-листы

---

### 1.9 DevOps и деплой

- Docker / Docker Compose
- Nginx / Traefik
- GitHub Actions
- Sentry
- Grafana / Prometheus
- ELK / Loki
- Uptime monitoring

---

## 2. Архитектура проекта

### 2.1 Основные части системы

#### Client App
- регистрация/логин
- создание заказа
- поиск адреса
- отслеживание курьера
- история заказов
- чат
- рейтинг
- профайл

#### Courier App
- список заказов
- маршруты
- статус доставки
- геопозиция
- фото подтверждения
- заработок
- активные доставки

#### Admin Panel
- список пользователей
- список заказов
- статусы
- аналитика
- настройка цен
- предупреждения
- управление курьерами
- финансовая статистика

#### AI Service
- оптимизация маршрутов
- ETA prediction
- pricing engine
- demand prediction
- route suggestions

---

### 2.2 Рекомендуемая структура проекта

```text
delivery-system/
├── mobile/
│   ├── client-app/
│   ├── courier-app/
│   └── admin-app/
├── backend/
│   ├── src/
│   ├── tests/
│   └── config/
├── ai-service/
│   ├── routes/
│   ├── models/
│   ├── utils/
│   └── mcp_servers/
├── admin-dashboard/
├── docs/
├── docker-compose.yml
├── README.md
└── .gitignore
```

---

## 3. AI-функции для курьерской службы

### 3.1 Нужные AI-функции
- оптимизация маршрутов
- расчёт ETA
- прогноз спроса
- распределение заказов
- dynamic pricing
- нахождение лучшего курьера
- аналитика по зонам
- рекомендации по загрузке
- помощь оператору в особых случаях

### 3.2 Что лучше реализовать детерминированно
- маршрут
- ETA
- расчёт цены
- назначение курьера
- дедлайны и SLA
- правила отмены и возвратов

### 3.3 Где LLM полезен
- помощь сотрудникам
- объяснение статуса
- генерация сообщений клиентам
- анализ инцидентов
- подготовка персонализированных рекомендаций
- support chat
- summarization и аналитика

---

## 4. MCP-серверы: что использовать

MCP (Model Context Protocol) нужен для подключения AI-агентов к реальным данным и инструментам.

### 4.1 Основные MCP-серверы

#### GitHub MCP
Используется для:
- доступа к репозиториям
- PR
- issues
- actions
- CI/CD

Ссылка:
- https://github.com/modelcontextprotocol/servers

#### Filesystem MCP
Используется для:
- доступа к локальным файлам и проектам
- чтения структуры проекта
- редактирования контекста

Ссылка:
- https://github.com/modelcontextprotocol/servers

#### PostgreSQL MCP
Используется для:
- запросов к базе данных
- анализа данных
- вычитывания схемы БД
- доступа к данным через AI

Ссылка:
- https://github.com/modelcontextprotocol/servers

#### SQLite MCP
Для:
- локальной аналитики
- эвристик и промежуточных БД

Ссылка:
- https://github.com/modelcontextprotocol/servers

#### Web / Browser MCP
Для:
- scraping
- request routing
- автоматизации браузера
- мониторинга внешних источников

Ссылка:
- https://github.com/modelcontextprotocol/servers

#### Logistics AI MCP
- https://lobehub.com/mcp/csoai-org-logistics-ai-mcp

#### Logistics Freight Intelligence MCP
- https://github.com/apifyforge/logistics-freight-intelligence-mcp

#### OpenRouteService
- https://openrouteservice.org/

Подходит для:
- маршрутизации
- расчёта расстояний
- time matrices

---

### 4.2 Claude-specific MCP resources

#### Awesome Claude MCP Servers
- https://github.com/win4r/Awesome-Claude-MCP-Servers

#### Best MCP servers for Claude Code
- https://agentcat.com/guides/best-mcp-servers-for-claude-code/

#### MCP blog / list
- https://desktopcommander.app/blog/best-mcp-servers/

#### Model Context Protocol servers repo
- https://github.com/modelcontextprotocol/servers

---

## 5. Skills и плагины

### 5.1 Skills
Полезные skills для такого проекта:
- architecture-planning
- API-design
- route-optimization
- debugging
- code-review
- security-audit
- test-generation
- migration-planning
- infrastructure-setup
- logistics-ops
- analytics
- database-design

Эти навыки нужны для:
- проектирования backend
- анализа логистики
- генерации тестов
- refactoring
- настройки CI/CD
- безопасной разработки

---

### 5.2 Плагины и расширения

#### Для разработки
- ESLint
- Prettier
- TypeScript
- Docker
- GitHub Integration
- GitLens
- Postgres / DB Explorer
- REST Client / Postman
- Swagger plugin
- Jira/GitHub issue plugin
- Error Lens
- Auto Rename Tag
- Bracket Pair Colorizer

#### Для AI-проектов
- MCP client plugins
- GitHub workflows
- database access plugins
- browser automation plugins
- API testing tools
- monitoring plugins

---

## 6. Claude Code vs Codex

### Claude Code
Лучше подходит для:
- развитого архитектурного понимания
- рефакторинга
- сложных multi-file задач
- логики проекта
- объяснения архитектуры
- AI-консультирования для команды

### Codex
Лучше подходит для:
- быстро генерации boilerplate
- тестов
- CLI-автоматизации
- небольших задач и сценариев
- массовых изменений
- ускорения разработки

### Практически для данного проекта
Лучше сочетание:
- Claude Code — архитектура, сложные модули, аналитика, отладка, AI-слой
- Codex — генерация boilerplate, повторяющихся задач, тестов, быстрый прототип

---

## 7. Практический стек для данного проекта

### Frontend
- React Native + Expo
- TypeScript
- React Navigation
- Zustand
- react-native-maps
- Firebase / FCM
- Socket.IO client

### Backend
- NestJS + TypeScript
- PostgreSQL + PostGIS
- Redis
- Socket.IO
- JWT authentication

### AI
- FastAPI
- OR-Tools
- scikit-learn
- Pandas
- NumPy
- Claude / OpenAI API

### Admin
- React + Vite + TypeScript
- Recharts
- Zustand
- React Router

### Infra
- Docker
- Docker Compose
- Nginx
- GitHub Actions
- Sentry
- Grafana / Prometheus

### MCP
- GitHub MCP
- PostgreSQL MCP
- Filesystem MCP
- Browser MCP
- Routing / Map MCP
- Logistics-specific MCP

---

## 8. Установка базовых инструментов

### Node.js
```bash
node -v
npm -v
```

### Python
```bash
python3 --version
pip --version
```

### Docker
```bash
docker --version
docker-compose --version
```

### PostgreSQL
```bash
docker run --name postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_USER=postgres -e POSTGRES_DB=delivery_db -p 5432:5432 -d postgres:15
```

### Redis
```bash
docker run --name redis -p 6379:6379 -d redis:7
```

### React Native / Expo
```bash
npx create-expo-app delivery-client
cd delivery-client
npm install
```

### NestJS
```bash
npm i -g @nestjs/cli
nest new backend
```

### FastAPI
```bash
python -m venv venv
source venv/bin/activate
pip install fastapi uvicorn sqlalchemy psycopg2-binary redis python-dotenv
```

### OR-Tools
```bash
pip install ortools
```

### scikit-learn
```bash
pip install scikit-learn pandas numpy
```

---

## 9. Пример конфигурации MCP

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/workspace"]
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://user:password@localhost:5432/delivery_db"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"]
    }
  }
}
```

---

## 10. Ключевые инструменты для курьерского проекта

Лучший набор:
- React Native + Expo
- NestJS + PostgreSQL + Redis
- FastAPI + OR-Tools + scikit-learn
- Claude Code + MCP
- Codex для тестов и генерации шаблонов
- Firebase + Twilio
- Stripe / YooKassa
- Google Maps / Mapbox / OpenRouteService
- Docker + GitHub Actions
- Sentry + Grafana

---

## 11. Что лучше использовать в реальной разработке

### Если проект сложный и архитектурный
- Claude Code
- MCP
- FastAPI AI-service
- strict backend + validation

### Если нужно быстро собрать MVP
- Expo + React Native
- Express or NestJS
- FastAPI AI-service
- PostgreSQL + Redis
- MCP for AI integrations
- Codex for boilerplate and tests

---

## 12. Security checklist

- JWT + refresh tokens
- role-based access control
- validate all inputs
- protect AI logs from PII
- secure API keys
- rate limiting
- CORS configuration
- use Redis for throttling
- restrict admin areas
- log and audit sensitive activity

---

## 13. MVP roadmap

### MVP 1
- регистрация
- логин
- создание заказа
- отслеживание
- статус заказов
- профили
- базовая админ-панель

### MVP 2
- AI оптимизация маршрутов
- ETA prediction
- push-notifications
- dynamic pricing
- курьерские карты

### MVP 3
- аналитика
- рейтинг
- увеличенная автоматизация
- админские дашборды
- мониторинг и деплой

---

## 14. Практический вывод

Для курьерского сервиса с AI интеграцией оптимальный стек:

- Mobile: React Native + Expo + TypeScript
- Backend: NestJS + PostgreSQL + Redis
- AI: FastAPI + OR-Tools + scikit-learn
- Tools: Claude Code + MCP + Codex
- Routing: OR-Tools + Mapbox/OpenRouteService
- Messaging: Firebase + Twilio
- Payments: Stripe / YooKassa
- Infra: Docker + GitHub Actions + Sentry

Это лучший баланс между скоростью разработки, масштабируемостью, надежностью и AI-функциональностью.

---

## 15. Ссылки

### MCP / general
- https://github.com/modelcontextprotocol/servers
- https://github.com/win4r/Awesome-Claude-MCP-Servers
- https://agentcat.com/guides/best-mcp-servers-for-claude-code/
- https://desktopcommander.app/blog/best-mcp-servers/

### Logistics / routing tools
- https://github.com/apifyforge/logistics-freight-intelligence-mcp
- https://lobehub.com/mcp/csoai-org-logistics-ai-mcp
- https://openrouteservice.org/
- https://www.mapbox.com/
- https://developers.google.com/maps

### AI / coding
- https://claude.ai/
- https://openai.com/codex/
- https://github.com/features/copilot
- https://docs.anthropic.com/en/docs/claude-code

---

## 16. Итог

Если вы строите курьерский сервис с AI:
- Claude Code лучше для архитектуры, рефакторинга, сложного AI-слоя и проектной логики
- Codex полезен для быстрых задач, генерации boilerplate и тестов
- MCP нужны для подключения к GitHub, БД, API, картам и логистике
- маршрутную логику надо строить на OR-Tools, а не только на LLM
- AI должен быть интеллектуальным помощником и аналитическим слоем, а не единственной логикой принятия решений

Это лучший практический стек для проекта такого типа.

---

Если хотите, я могу сразу приготовить ещё 3 отдельных готовых файла:
1. `docs/MCP_AND_AI_TOOLS.md`
2. `docs/CLAUDE_CODE_PROMPTS.md`
3. `docs/PROJECT_STRUCTURE.md`
