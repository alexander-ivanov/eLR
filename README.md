# eLR (electronic Lab Reporing)

## Цель документа

Сформировать план действий по созданию руководства разработчика по обмену лабораторными отчетами. Мы хотим получить единый документ и для выгрузки в РЭМД и для обмена между частными организациями и на его основе сформировать первый базовый профиль ресурсов FHIR для использования в РФ (FHIR_RU Core).

## Ссылки

* [Запись встречи FHIR Ru посвященная обмену лабораторными исследованиями](https://www.youtube.com/watch?v=uZv4l2iIHrE&feature=youtu.be)
* [НСИ Минздрава](https://nsi.rosminzdrav.ru/#!/refbook)
* [Руководство по реализации СЭМД «Протокол лабораторного исследования» в формате CDA R2-2009](http://portal.egisz.rosminzdrav.ru/materials/2939)

## Решения первой встречи

* Использовать [FHIR R4](https://www.hl7.org/fhir/index.html)
* Использовать JSON как базовый формат
* Создать новое руководство для использования FHIR, а не автоматически конвертировать правила CDA

## Задачи

### Основные

* Сформулировать сценарии на которые нацелено данное руководство (базовые сценарии, профили (панели тестов) НСИ, микробиология)
* Сформировать список ресурсов FHIR для передачи результатов лаб исследований (база руководство CDA)
* Для ресурсов сформировать профили (ограничения, привязки к справочникам)
* Разработать примеры документов FHIR R4 для передачи результатов лаб исследований
* Опубликовать IG
* Написать руководство разработчика для FHIR R4
* Разработать ограничения (в т.ч. и логические) на сформированный документ
* Разработать или описать механизм проверки валидности на стороне клиента
* Разработать или описать средства визуализации документа для пациентов
* Разработать или описать механизм подписания документа (разные части могут подписывать разные лаборатории и в конце финальное подписание)

### Желаемые

* Перевести страницу про варианты [валидации](https://www.hl7.org/fhir/validation.html) которые предоставляет FHIR
* Описать, как можно в отчете указывать услуги в т.ч. иерархичные (важно для ФОМС)
* Опубликовать справочники Минздрава, как терминологию FHIR
* Сделать конвертер DSTU2 to R4 (важно, т.к. МИАЦ и Нетрика накопили много данных)
* Сделать конвертер CDA <-> FHIR (хотя бы в одну сторону) (интеграция с РЭМД)

### Коннектатоны

Коннектатоны - живые встречи участников сообщества HL7 FHIR, в рамках которого они тестируют спецификации и дают обратную связь.

Мы предлагаем сделать коннектатоны регулярным событием в рамках формирования руководства и национального профиля. Обычно на коннектатон выносятся два три сценария, сложность реализации которых возрастает. Заинтересованные участники стараются реализовать все сценарии и сформулировать пожелания, возражения, рекомендации на доработку.

Потенциальные темы коннектатонов:

* Кодирование/декодирование результатов лаб исследований
* Проверка валидации документов
* Проверка подписи документа

### План

Предлагаю использовать итеративный подход и выполнить первую итерацию по выбранным сценариям, для этого создать полный список сценариев для кодирования. Предлагаю использовать сценарии двух видов:

* Сценарии для кодирования сложных вариантов лабораторных исследований
* Сценарии бизнес-процессов (см. 4.1. Сценарий использования в "Руководство по реализации СЭМД «Протокол лабораторного исследования» в формате CDA R2-2009")

1. Выбор базовых сценариев для первой итерации
1. Выбрать механизм распределения задач (Предлагаю issues в github)
1. Конвертация заголовка CDA в ресурс Composition
Заголовок CDA не может быть конвертирован один в один, часть текущих полей заголовка должны быть перенесены в отдельные ресурсы, на которые Composition будет ссылаться внутренними ссылками:

    * Перенос базовых полей
    * Перенос полей в ресурсы (см. [CDA Header в Ресурсы](#cda))
    * Перенос ограничений

1. Конвертация заголовка CDA в ресурсы FHIR и создание профилей (задача будет декомпозирована по разделу CDA Header в Ресурсы)
1. Конвертация тела CDA в ресурсы
1. Создание конвертеров CDA<->FHIR для валидации, что кодирование не теряет данные (хотя бы на (см. 4.1. Сценарий использования в "Руководство по реализации СЭМД «Протокол лабораторного исследования» в формате CDA R2-2009"))
1. Валидация, что все базовые сценарии, выбранные на первую итерацию могут быть закодированы

#### Предложение по ответственностям первого этапа

| **Задачи** | **Участники** | **Конкретные исполнители** |
| ------ | ------ | ------ |
| Сценарии для кодирования сложных вариантов лабораторных исследований | Лаборатории, Разработчики ЛИС, HL7 Russia |  |
| Выбрать механизм распределения задач | FHIR-RU Core, HL7 Russia |  |
| Конвертация заголовка CDA | FHIR-RU Core, HL7 Russia |  |
| Создание базовых профилей | FHIR-RU Core, HL7 Russia |  |
| Конвертация тела CDA в ресурсы | FHIR-RU Core, HL7 Russia |  |
| Создание конвертеров CDA<->FHIR для валидации | FHIR-RU Core |  |
| Валидация, что все базовые сценарии, выбранные на первую итерацию могут быть закодированы | HL7 Russia, FHIR-RU Core, Лаборатории, Разработчики ЛИС |  |

## Информация для первой итерации

### Сценарии кодирования сложных вариантов лабораторных исследований

TBD

### CDA Header в Ресурсы

| **Название CDA Header** | **Поле CDA Header** | **Вложенность** | **Ресурс FHIR** | **Комментарий** |
| ------ | ------ | ------ | ------ | ------ |
| Информация о пациенте | ```<recordTarget>``` | ```<patientRole>``` | Patient |  |
| Информация о пациенте | ```<recordTarget>``` | ```<patientRole>.<providerOrganization>``` | Organization | |
| Автор | ```<author>``` | ```<assignedAuthor>``` | Practitioner(+extension) / Practitioner, PractitionerRole | Зависит от того как кодировать, где работает врач |
| Автор | ```<author>``` | ```<assignedAuthor>.<representedOrganization>``` | Organization | |
| Владелец оригинала документа | ```<custodian>``` | ```<assignedCustodian>``` | Organization | |
| Получатель документа | ```<informationRecipient>``` | ```<intendedRecipient>``` | Organization | |
| Лицо, придавшее юридическую значимость документу | ```<legalAuthenticator>``` | ```<assignedEntity>``` | Practitioner(+extension) / Practitioner, PractitionerRole | см. ```<author>``` |
| Лицо, придавшее юридическую значимость документу | ```<legalAuthenticator>``` | ```<assignedEntity>.<representedOrganization>``` | Organization | |
| Страховой полис ОМС | ```<participant>[@typeCode=”HLD”]``` | ```<associatedEntity>``` | Coverage | |
| Страховой полис ОМС | ```<participant>[@typeCode=”HLD”]``` | ```<associatedEntity>.<scopingOrganization>``` | Organization | |
| Направивший врач | ```<participant>[@typeCode="REF"]``` | ```<associatedEntity>``` | Practitioner(+extension) / Practitioner, PractitionerRole | см. ```<author>``` |
| Направивший врач | ```<participant>[@typeCode="REF"]``` | ```<associatedEntity>.<scopingOrganization>``` | Organization | |
| Сведения о направлении | ```<inFulfillmentOf>``` | ```<order>``` | ServiceRequest | |
| Документируемое событие | ```<documentationOf>``` | ```<serviceEvent>``` | Encounter | |
| Случай оказания медицинской помощи | ```<componentOf>``` | ```<encompassingEncounter>``` | Encounter | |

### CDA Body в Ресурсы

TBD