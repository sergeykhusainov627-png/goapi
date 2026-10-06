# goapi — REST API на Go

Учебный проект команды из двух человек: переносим бизнес-логику Telegram-бота
[PyBot-ITAcadem](https://github.com/Cewerty/PyBot-ITAcadem) (Python + aiogram) в
**REST API на Go**. Telegram-интерфейс заменяется на HTTP-эндпоинты, бизнес-логика
(баллы, уровни, роли, компетенции, рассылки) сохраняется.

| | |
|---|---|
| Roadmap | [docs/ROADMAP.md](docs/ROADMAP.md) — версия 2.0: 12 фаз с целями и критериями приёмки |
| Канбан-доска | [Projects → goapi — Go REST API](https://github.com/users/sergeykhusainov627-png/projects/2) |
| Оригинал (Python) | [Cewerty/PyBot-ITAcadem](https://github.com/Cewerty/PyBot-ITAcadem) |
| Форк оригинала | [sergeykhusainov627-png/PyBot-ITAcadem](https://github.com/sergeykhusainov627-png/PyBot-ITAcadem) |

Мы делаем **не Telegram-бота**, а HTTP API с тем же бизнес-функционалом.

## Стек (roadmap §4.1)

| Задача | Решение |
|---|---|
| Язык | **Go 1.27** |
| HTTP | `net/http` + стандартный роутер (Go 1.22+). Финальный выбор и ADR-001 — в конце Фазы 1 (roadmap §4.1.1) |
| JWT | `github.com/golang-jwt/jwt/v5` |
| Пароли | `golang.org/x/crypto/bcrypt` |
| БД / доступ | PostgreSQL + `pgx` + чистый SQL (без ORM) |
| Миграции | `golang-migrate`, отдельным шагом (`cmd/migrate`), **не из API** (roadmap §8.3) |
| Redis | `redis/go-redis` — rate limiting и очереди. Refresh-токены живут в PostgreSQL (roadmap §4.2) |
| Логи | `log/slog`, JSON, `request_id` в каждом логе |
| Метрики | `prometheus/client_golang`, `/metrics` появляется уже в Фазе 1 (roadmap §9.3) |
| Тесты | `testing` + `testcontainers-go` (интеграционные с реальным PostgreSQL) |

## Правила работы (roadmap §6)

1. **`main` защищена** — только через Pull Request и ревью напарника.
2. Ветка на каждую задачу: `feat/auth`, `fix/points-bug`.
3. Один PR = одна задача; маленькие PR ревьюить легче.
4. **Conventional Commits:** `feat:`, `fix:`, `refactor:`, `test:`, `docs:`, `chore:`.
5. **`main` всегда зелёный** — сборка и тесты проходят.
6. Статус карточки на доске (Todo → In Progress → Done) меняет человек, а не бот.

## Как идёт работа

Фазы идут по порядку: Фаза 0 → Фаза 11. Каждая фаза — отдельный PR и отдельная
карточка на [доске](https://github.com/users/sergeykhusainov627-png/projects/2).
Фаза не закрывается без выполненного **критерия приёмки** из
[docs/ROADMAP.md](docs/ROADMAP.md#5-роадмап-реализации).

Первый шаг — Фаза 0: установить Go 1.27, пройти основы, договориться о процессе.

## Локальный запуск

Появится в Фазе 1 (`docker compose up`, `make run`) — см. roadmap §5.
