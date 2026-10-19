---
id: transport-csp
title: Content Security Policy
topic: transport
priority: high
applies_when:
  - csp
  - content-security-policy
  - xss
  - script
owasp:
  - Content Security Policy Cheat Sheet
  - ASVS V3.4 Browser Security Mechanism Headers
---

# Content Security Policy

CSP ограничивает, откуда страница берёт скрипты и куда им можно ходить. Политика с `unsafe-inline` и `*` почти ничего не режет.

Защитный промпт: имена угроз здесь, чтобы их закрыть. Пошаговых атак нет.

## Уязвимости

| Угроза | Что происходит |
| --- | --- |
| Нет CSP | Внедрённый скрипт выполняется без второго барьера |
| `script-src *` или `'unsafe-inline'` навсегда | Барьер не работает |
| `unsafe-eval` без причины | Строка превращается в код |
| Политика только в отчёте, и отчёт никто не смотрит | Дыры видны, но не закрыты |
| В CSP забыт `base-uri` и `object-src` | Подменяют базу URL или подключают старые плагины |
| Формы уходят на чужой хост | Введённый пароль отправляется не туда |

## Сделать

1. Начать со списка реальных источников скриптов, стилей, картинок и соединений. Запрет по умолчанию: `default-src 'self'`.
2. Скрипты: свои файлы и точечные хосты. Инлайн убрать в файлы или nonce/hash на каждый ответ, nonce не угадывается и не переиспользуется между ответами. Не оставлять `'unsafe-inline'` в `script-src`.
3. `object-src 'none'`, `base-uri 'self'`, `frame-ancestors` как в заголовках. `form-action` ограничить своими хостами.
4. Если продукт ещё падает от жёсткой политики, временно включить режим отчётов и собрать нарушения. Срок, когда режим отчётов станет блокирующим, записать. Не заканчивать работу вечным Report-Only.
5. Не вставлять секреты в отчёты CSP. Эндпоинт отчёта не должен исполнять присланный JSON как команду.
6. Сторонние виджеты - в `third-party-scripts.md`.

## Промпт

```text
Собери и включи Content-Security-Policy под реальные ресурсы приложения.

default-src 'self'. script-src без звёздочки и без постоянного unsafe-inline. object-src none, base-uri self, form-action на свои хосты, frame-ancestors как нужно продукту.
Инлайн-скрипты перенеси или закрой nonce/hash.
Если сразу блокирующая политика ломает прод, включи отчёт, перечисли нарушения и не называй это законченной защитой.
Не добавляй примеры внедряемого скрипта.
```

## Готово, когда

- [ ] CSP отдаётся приложением
- [ ] Скрипты не разрешены отовсюду
- [ ] Нет вечного `unsafe-inline` для скриптов
- [ ] `object-src` и `base-uri` заданы
- [ ] Режим «только отчёт» не считается финалом без списка дыр

## Источники

- https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html
- https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html
