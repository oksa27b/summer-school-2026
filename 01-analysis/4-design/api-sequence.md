# Sequence-диаграммы API

## 1. Создание брони (createBooking)

```mermaid
sequenceDiagram
    actor User as Клиент
    participant App as Приложение
    participant API as API (bookings)

    Note over App: SCR-004: Выбрано N мест и K проката
    User->>App: Тап «Записаться»
    App->>App: Генерирует Idempotency-Key (UUID)

    App->>API: POST /bookings {slot_id, N, K}
    
    alt Успех
        API-->>App: 201 Created {id, price_total}
        App-->>User: BS-002: Успех + Вибрация
    else Дефицит снаряжения (409 Conflict)
        API-->>App: 409 {code: gear_exhausted, available_gear: M}
        App-->>User: SCR-004: Измените выбор на "Своё"
    else Сбой сети (Retry Case)
        App->>API: Повторный POST (тот же Idempotency-Key)
        API-->>App: 201 Created (Исходный ответ)
        App-->>User: BS-002: Успех
    end

```

## 2. Отмена брони (cancelBooking)

```mermaid
sequenceDiagram
    actor User as Клиент
    participant App as Приложение
    participant API as API (bookings)

    User->>App: Тап «Отменить» (SCR-006)
    App-->>User: BS-003: Подтверждение
    User->>App: Подтверждает отмену
    
    App->>App: Генерирует Idempotency-Key (UUID)

    App->>API: POST /bookings/{id}/cancel
    Note over API: Re-validation: проверка времени (start_at - 2h)

    alt Ранняя отмена (>= 2ч)
        API-->>App: 200 OK {status: cancelled}
        App-->>User: SCR-006: Снек «Отменено» + Вибрация
    else Поздняя отмена (< 2ч)
        API-->>App: 200 OK {status: late_cancel}
        App-->>User: SCR-006: Снек «Место не освобождено» + Вибрация
    else Ошибка: Занятие началось
        API-->>App: 422 Unprocessable {code: slot_started}
        App-->>User: SCR-006: Снек «Отмена невозможна»
    end
