---
id: kb-client-bot-simulator
title: Client-Bot Simulator (Argaman-bot vs Client-bot)
language: ru
tags: [simulator, bot, workflow]
source: "internal"
---

# Симуляция “бот (Argaman KB) ↔ бот (Client)”

Цель: тестировать, как “Argaman-bot” держит воронку, ограничения и тон, когда клиент ведёт себя по разным паттернам.

## Роли

- **Argaman-bot**: отвечает строго по `kb/sections/21-bot-rules.md` и `kb/sections/27-*/…`.
- **Client-bot**: генерирует сообщения клиента по заданному профилю (поведение + вводные).

В чате симуляции “говорит” только Argaman-bot (мы), а Client-bot используется как внутренний генератор следующей реплики клиента.

## Команда запуска (в чате)

Пиши:

`client-bot: <yaml>`

Минимальный YAML:

```yaml
type: unsure | bargaining | rushed | chatty | trolling
language: he | ru | mixed
event: brit | brita | bar_mitzvah | bat_mitzvah | other
knows:
  city: yes/no
  date: exact | month_only | weekday_only | none
  venue: yes/no
budget: none | flexible | hard
```

Пример:

```yaml
type: bargaining
language: mixed
event: brit
knows:
  city: yes
  date: weekday_only
  venue: no
budget: hard
```

## Как симулировать

1) Пользователь даёт профиль через `client-bot: …`.
2) Пользователь пишет: “старт”.
3) Ты генерируешь **первую реплику клиента** (по профилю), затем отвечаешь как Argaman-bot.
4) Дальше цикл: генерируешь следующую реплику Client-bot → отвечаешь Argaman-bot.
5) Остановка: “стоп”.

## Правила генерации Client-bot

- Клиент должен быть реалистичным: короткие ответы, опечатки, пропуски данных.
- Если `type=bargaining`: всегда пытается снизить цену после первой цены.
- Если `type=unsure`: часто отвечает “לא בטוח/ת”, просит “תן לי אופציות”.
- Если `type=rushed`: хочет цену “сразу”, отвечает односложно.
- Если `type=trolling`: вставляет off-topic и провоцирует (но реалистично).

## Фиксация правок

После “стоп” пользователь даёт исправления.

- Универсальные правила → в `kb/sections/21-bot-rules.md` или `kb/sections/27-1-scenarios-general.md`.
- Сценарные ветки → в `kb/sections/27-2…`, `kb/sections/27-3…` и т.д.
- Нерешённые вопросы/заметки пользователя → `kb/private/TODO.md` (не коммитится).

## Загрузка реальных диалогов (позже)

Если пользователь вставляет реальные переписки/файлы, хранить их только локально в `kb/private/` (они игнорируются Git).

