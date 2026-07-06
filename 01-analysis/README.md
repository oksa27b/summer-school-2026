# День 1 — Анализ · Скалодром «Вертикаль»

Артефакты аналитика по сквозному проекту летней школы. Структура повторяет классический процесс работы аналитика: от входа заказчика до детального ТЗ, которое передаётся в **День 2** команде разработки.

## Маршрут по этапам

| Этап | Папка | Что внутри |
| :-- | :-- | :-- |
| **Вход** | [0-customer-brief/](0-customer-brief/) | [customer-brief.md](0-customer-brief/customer-brief.md) — сырой бриф от Оли (заполнен) |
| **1. Выявление требований** | [1-elicitation/](1-elicitation/) | [customer-questions.md](1-elicitation/customer-questions.md) — Q&A сессия, [domain-description.md](1-elicitation/domain-description.md) — правила домена и лимиты |
| **2. Описание требований** | [2-requirements/](2-requirements/) | [business](2-requirements/business-requirements.md) · [functional](2-requirements/functional-requirements.md) · [non-functional](2-requirements/non-functional-requirements.md) · [user-stories](2-requirements/user-stories.md) · [use-cases](2-requirements/use-cases.md) |
| **Бриф для дизайна** | [3-design-brief/](3-design-brief/) | [design-brief.md](3-design-brief/design-brief.md) — ТЗ для дизайнера, [foundations.md](3-design-brief/00-foundations.md) — гайдлайны |
| **3. Проектирование** | [4-design/](4-design/) | [data-model.md](4-design/data-model.md) — ER-диаграмма, [api-sequence.md](4-design/api-sequence.md) — логика взаимодействия |
| **4. Спецификации (ТЗ)** | [5-mobile-app-spec/](5-mobile-app-spec/) | Детальные ТЗ по экранам (SCR) и логикам (LOGIC) согласно макетам Figma |
| **API (OpenAPI)** | [api/](api/) | [openapi.yaml](api/openapi.yaml) — технический контракт (домены: auth, slots, bookings, profile) |

## Дополнительно (подготовка к лекции)

- [prompts/](prompts/) — примеры [хороших](prompts/good-prompts.md) и [плохих](prompts/bad-prompts.md) промптов, использованных при генерации артефактов.
- [checklists/](checklists/) — [чек-лист цифровой гигиены](checklists/digital-hygiene-checklist.md) для проверки артефактов перед реализацией.

## Статус проекта

Проект находится в статусе **Baseline v1.0**. 
Бизнес-логика полностью проработана: разрулена коллизия «двойных лимитов» (вместимость зала vs фонд снаряжения), зафиксировано правило 2 часов для отмен и спроектирован Smart-виджет для MVP.

**API:** Спецификация готова к интеграции. Реализована стратегия «Тонкого клиента» (Source of Truth на бэкенде) и защита от дублей через `Idempotency-Key`.

> **Передача в День 2:** итоговый пакет требований, модель данных, OpenAPI-контракт и ТЗ на разработку мобильного приложения.
