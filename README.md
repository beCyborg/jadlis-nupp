Русский · [English](README.en.md)

# Диагноз проекта по 6 универсальным принципам

Плагин `nupp` для Claude Code. Команда — `/nupp`.

## Было → стало

Раздел заполняется по контракту README 2026-09 (фаза 3 плана «GitHub beCyborg как витрина Jadlis»).

## Как это работает

Советник по проектам на мета-системе NUPP (Nearly Universal Principles of Projects): шесть универсальных принципов под PRINCE2, PMBOK, P3.express, DSDM, Scrum и XP — диагноз ситуации и что менять.

## Установка и первый запуск

```bash
claude plugin marketplace add https://github.com/beCyborg/jadlis-start.git
claude plugin install nupp@jadlis --config MEMORY_DIR=~/advisors-memory
```

## Границы, стоимость, обновление

Конспекты книг — производные работы, лицензии нет: см. [NOTICE.md](NOTICE.md). Правки принимаются только в источнике (`jadlis-advisors-source`), этот репо генерируется.

```bash
claude plugin marketplace update jadlis
claude plugin update nupp@jadlis
```
