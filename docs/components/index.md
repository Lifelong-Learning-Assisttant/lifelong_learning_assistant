# Компоненты системы

Данный раздел содержит документацию по всем компонентам системы Lifelong Learning Assistant.

## Архитектурные компоненты

### Карточки компонентов (краткий обзор)

| Компонент | Описание | Файл |
|-----------|----------|------|
| **Web UI** | Пользовательский интерфейс на Streamlit | [`cards/web-ui.md`](cards/web-ui.md) |
| **Orchestrator** | LLM Agent/Orchestrator - центральный координатор системы | [`cards/orchestrator.md`](cards/orchestrator.md) |
| **LLM Service** | Адаптер для локальных и облачных LLM | [`cards/llm-service.md`](cards/llm-service.md) |
| **Retriever** | Гибридный поиск (векторный + полнотекстовый) | [`cards/retriever.md`](cards/retriever.md) |
| **Data Sources** | Адаптеры для источников данных | [`cards/data-sources.md`](cards/data-sources.md) |
| **Functional Modules** | Специализированные модули (Quiz, Interview) | [`cards/functional-modules.md`](cards/functional-modules.md) |
| **Async Processing** | Очереди задач и воркеры | [`cards/async-processing.md`](cards/async-processing.md) |
| **Storage** | Хранилища данных | [`cards/storage.md`](cards/storage.md) |
| **Observability** | Мониторинг и логирование | [`cards/observability.md`](cards/observability.md) |
| **Security** | Безопасность и контроль доступа | [`cards/security.md`](cards/security.md) |

### Deep Dive документы

Детальное описание архитектуры и реализации каждого компонента:

| Компонент | Описание | Файл |
|-----------|----------|------|
| **Orchestrator** | Детальная архитектура агента и механизм выбора инструментов | [`deep/orchestrator.md`](deep/orchestrator.md) |
| **Retriever** | Гибридный поиск, ранжирование, provenance | [`deep/retriever.md`](deep/retriever.md) |
| **Data Sources** | Адаптеры и стратегии обработки данных | [`deep/data-sources.md`](deep/data-sources.md) |
| **Functional Modules** | Quiz Engine, Interview Simulator и другие модули | [`deep/functional-modules.md`](deep/functional-modules.md) |
| **Async Processing** | Архитектура очередей и обработка задач | [`deep/async-processing.md`](deep/async-processing.md) |
| **Storage** | Схемы данных и стратегии хранения | [`deep/storage.md`](deep/storage.md) |
| **Observability** | Метрики, логирование и мониторинг | [`deep/observability.md`](deep/observability.md) |
| **Security** | Безопасность, шифрование и политика данных | [`deep/security.md`](deep/security.md) |

## Навигация

1. **Для быстрого понимания** - читайте [карточки компонентов](cards/)
2. **Для детального изучения** - переходите к [deep-dive документам](deep/)
3. **Для архитектурных решений** - смотрите [`03-architecture.md`](../03-architecture.md)
4. **Для понимания системы в целом** - изучите [`01-overview.md`](../01-overview.md)

## Быстрый старт с компонентами

### Основные пользовательские компоненты
- **[Web UI](cards/web-ui.md)** - интерфейс для взаимодействия пользователей
- **[Orchestrator](cards/orchestrator.md)** - "мозг" системы, координация всех операций

### Ядро функциональности
- **[Retriever](cards/retriever.md)** - поиск и извлечение контекста
- **[LLM Service](cards/llm-service.md)** - генерация ответов с помощью LLM
- **[Functional Modules](cards/functional-modules.md)** - образовательные функции (квизы, интервью)

### Инфраструктура
- **[Data Sources](cards/data-sources.md)** - интеграция с источниками данных
- **[Storage](cards/storage.md)** - системы хранения информации
- **[Async Processing](cards/async-processing.md)** - фоновые задачи и обработка

### Операционная поддержка
- **[Observability](cards/observability.md)** - мониторинг и аналитика
- **[Security](cards/security.md)** - безопасность и контроль доступа

---

*Структура создана: 2025-11-02*  
*Всего компонентов: 10 карточек, 8 deep-dive документов*