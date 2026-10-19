---
id: infra-frameworks
title: Защита конкретного фреймворка
topic: supply
priority: high
applies_when:
  - django
  - laravel
  - rails
  - spring
  - dotnet
  - express
  - next
  - fastapi
  - symfony
  - php
owasp:
  - Django Security Cheat Sheet
  - Ruby on Rails Cheat Sheet
  - Nodejs Security Cheat Sheet
---

# Защита конкретного фреймворка

Общие промпты говорят, что закрыть. Фреймворк часто уже умеет это, пока защиту не выключили. Этот файл не заменяет вход, права и инъекции. Он запрещает обходить встроенные механизмы.

Защитный промпт: имена угроз здесь, чтобы их закрыть. Пошаговых атак нет.

## Уязвимости

| Угроза | Что происходит |
| --- | --- |
| Выключены CSRF, экранирование шаблонов или безопасные cookie «для API» | Общие дыры возвращаются |
| Отладка и список маршрутов включены в бою | Видно устройство |
| Сырой SQL, сырой HTML и сырой YAML включены рядом со штатным API | Штатная защита не покрывает этот вызов |
| Пример из старого руководства копирует слабый хеш и `debug=true` | Пример становится продом |

## Сделать

1. Включить рекомендуемые настройки безопасности фреймворка для прода: cookie, CSRF, заголовки, отладка выключена, хосты ограничены, если фреймворк это умеет.
2. Не выключать экранирование шаблонов и параметризацию запросов в отдельных вызовах.
3. Секреты фреймворка читать из окружения.
4. Если стек из списка ниже, сверяться с его шпаргалкой, а не с советом другого языка.
5. Языковые шпаргалки, которые не продублированы отдельным файлом этой базы:
   - https://cheatsheetseries.owasp.org/cheatsheets/Django_Security_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/Django_REST_Framework_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/DotNet_Security_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/FastAPI_Security_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/Java_Security_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/JavaScript_and_TypeScript_Security_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/Laravel_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/Nextjs_Security_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/Nodejs_Security_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/NPM_Security_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/PHP_Configuration_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/Ruby_on_Rails_Cheat_Sheet.html
   - https://cheatsheetseries.owasp.org/cheatsheets/Symfony_Cheat_Sheet.html

## Промпт

```text
Определи фреймворк и включи его штатную защиту для прода. Не выключай CSRF, экранирование, безопасные cookie и параметризацию запросов.
Отладку выключи. Секрет возьми из окружения.
Если нужно отличие от общего промпта этой базы, предпочитай более строгий серверный контроль и шпаргалку своего фреймворка по ссылкам в этом файле.
Не копируй устаревший пример с отладкой и слабым хешем.

Если фреймворка нет, закрой те же темы общими файлами и не добавляй фреймворк ради галочки.
```

## Готово, когда

- [ ] Штатные защиты фреймворка не выключены
- [ ] Отладка прода выключена
- [ ] Сырой обход шаблонов и запросов не добавлен
- [ ] Секрет фреймворка не в коде

## Источники

- https://cheatsheetseries.owasp.org/cheatsheets/Django_Security_Cheat_Sheet.html
- https://cheatsheetseries.owasp.org/cheatsheets/Nodejs_Security_Cheat_Sheet.html
- https://cheatsheetseries.owasp.org/cheatsheets/Ruby_on_Rails_Cheat_Sheet.html
