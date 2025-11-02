# Структура документации

**Цель:** лёгкая, минималистичная, но уже «рабочая» документация, которая не перегружает проект на раннем этапе и при этом сразу покрывает нужные области:

- обзор системы и карта проекта и компонентов
- быстрый старт
- подробные deep-dive’ы для критичных частей системы

## Почему такая структура — кратко

* **Ясный вход** (карта + обзор): новый разработчик/архитектор быстро получает картину системы и ключевые зависимости.
* **Минимум бюрократии**: только нужные разделы — не перегружаем проект на старте.
* **Карточки → Deep dive**: карточки дают быстрый контекст; при необходимости — переход на глубокое описание компонента.
* **Docs-as-code**: markdown-репо легко версионировать и потом плавно перевести в `Docusaurus` статичный сайт документации.
* **Ops-ready**: с самого начала закладываем `ADR`, `changelog` и `runbook`-пояснения — это экономит время при принятии архитектурных решений.


# Cтруктура папки `docs/`

```
docs/
├─ README.md                        # (эта страница) структура и rationale
├─ 01-overview.md                   # Карта + краткий обзор (mermaid + TL;DR)
├─ 02-getting-started.md            # Get it started & FAQs (локальный запуск, основные команды)
├─ 03-architecture.md               # Архитектура & design (концепты, sequence diagrams)
├─ 04-adr/                          # Architecture Decision Records
│   ├─ README.md
│   └─ 0001-use-faiss-vs-remote.md
├─ 05-changelog.md                  # Хронология изменений (high-level)
├─ 06-ideas/                        # Сохраняем все наши идеи =)
│   ├─ idea1.md
│   └─ idea2.md
├─ diagrams_src                     # Храним исходники для PluntUML-диаграмм
│   ├─ 01-overview/
│   │   ├─ system-diagram.puml      # Исходник диаграммы
│   │   └─ system-diagram.svg       # Результат рендеринга диаграммы PNG/SVG
│   └─ other_docs_part
├─ components/
│   ├─ index.md                     # Список компонентных карточек (карточки — ссылки)
│   ├─ cards/
│   │   ├─ orchestrator.md          # Component Card (короткая)
│   │   └─ retriever.md
│   └─ deep/
│       ├─ orchestrator-deep.md
│       └─ retriever-deep.md
├─ dev-tools/                       # Документация по инструментам полезным для разработки
│   └─ pluntuml_diagram_renderer.md # Рендеринг PluntUML-диаграмм из исходников
├─ testing-ci.md                    # Testing & CI (как запускать, что покрывать)
├─ diagrams/
│   └─ system.mmd                   # mermaid-диаграмма (использовать в overview)
└─ templates/
    ├─ component-card-template.md
    └─ deep-doc-template.md
```

# Описание ключевых разделов

## 01-overview.md — Карта + краткий обзор

* Описание системы и `mermaid`-диаграмма (файл `diagrams/system.mmd`), текст описывающий потоки данных: пользователь → UI → API → Orchestrator → Retriever/LLM → storages.
* Цель: дать «высокоуровневое» понимание системы.

## 02-getting-started.md — Быстрый старт & FAQs

* Как запустить проект локально (docker-compose / dev scripts).
* Как запустить тесты, как создать dev-данные.
* Частые вопросы (краткие ответы).
* Контакты: владельцы/команды (owner fields в карточках).

## 03-architecture.md — Архитектура & design

* Ключевые концепты (Orchestrator, Retriever, Embedding pipeline, MQ, Workers).
* 3–5 sequence diagrams для типовых сценариев:
  * Generate quiz (UI → API → Orchestrator → Retriever → LLM → MQ → Workers → DB)
  * Web snapshot processing (Tavily → FS → MQ → Workers → VDB/ES)
* Схемы data-flow и краткие упоминания о масштабировании и отказоустойчивости.

## 04-adr/ — Architecture Decision Records

* Каждое серьёзное решение (выбор FAISS vs managed, RabbitMQ vs Redis Streams, локальная LLM vs облачная) — отдельный ADR в виде markdown (формат: контекст → опции → решение → последствия).

## 05-changelog.md

* Короткие записи по релизам/важным изменениям архитектуры. 
* Формат: дата — краткое описание — ссылки на PR/ADR.

## 06-ideas/ - Идеи и предложения по проекту

* записываем все наши идеи!
* потом будет обсуждать их
* добавлять в задачи
* и реализовывать!

## components/ — Component Cards + Deep Dive

* **cards/** — компактные карточки компонентов (описание + интерфейсы + owner + метрики + зависимости).
* **deep/** — подробные страницы (API, sequence, schema сообщений для MQ, runbook, observability, scaling).
* **index.md** — оглавление компонентных карточек.

## testing-ci.md (не сейчас)

* Что должен покрывать CI (unit, integration for retriever, end-to-end for quiz generation).
* Минимум: линтинг markdown/mermaid + тесты, которые запускаются в PR.
* Примеры команд и чеклист перед merge.

## diagrams/

* Хранить исходники mermaid, ссылки на export (svg/png) — Docusaurus позже вставит их в docs.

## templates/

* Шаблоны для карточки и deep-doc, чтобы все радилось в едином стиле.

# Шаблоны

Папка с `templates` содержит шаблоны для заметок в формате `mermaid`.
- `template_for_any-thing.md` - шаблон для такой то цели.


# Правила и конвенции (коротко)

* **Язык:** русский (нам проще и можно локализовать позже на другие языки).
* **Формат:** markdown, `mermaid`/`pluntuml` для диаграмм, OpenAPI для endpoint’ов (в `apis/` когда появятся).
* **Naming:** файлы `kebab-case.md`, заголовки H1. Компонентная карточка — в `components/cards/`, deep — в `components/deep/`.
* **Owner:** каждый компонент будет иметь `Owner` (GitHub handle / команда).
* **PR workflow:** docs PR — review by owner. CI линтит markdown + проверяет mermaid-ошибки.
* **ADR:** номерованная нотация `0001-*.md`, каждая ADR содержит дату, контекст и последствия.

# Что добавить (опционально, если потребуется)

* **Runbooks/ops/** — отдельная папка с конкретными playbook’ами по restore/rollback.
* **Security.md** — политика секретов, хранения PII, шифрования.
* **API Reference (OpenAPI)** — когда появятся реальные API, положить в `apis/` + auto-generated docs.
* **Glossary** — если проект растёт и появляются специфичные термины.

# Первые практические шаги (микро-план)

1. Создать `docs/README.md` (эту страницу) и `01-overview.md` с mermaid-диаграммой (копировать ваш уже готовый flowchart).
2. Добавить `components/index.md` и **3–5 карточек** (Orchestrator, Retriever, LLM Service, MQ/Workers, Storage).
3. Наполнить `02-getting-started.md` минимальными командами для локального запуска (docker-compose/dev script).
4. Создать папку `04-adr/` и добавить первый ADR (например: выбор FAISS).
5. Подключить линтер markdown в CI и шаблон PR для docs (owner required).