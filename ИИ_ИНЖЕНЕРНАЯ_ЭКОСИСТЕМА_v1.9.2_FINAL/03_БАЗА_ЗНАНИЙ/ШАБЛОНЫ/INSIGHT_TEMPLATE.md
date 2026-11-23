---
schema_version: "1.2"
record_type: INSIGHT
id: "INS-YYYYMMDD-001"
title: "Название инсайта"
domain: "domain"
tags: []
project_id: null
priority: WARM
status: CANDIDATE
maturity: DRAFT
criticality: normal
reviewed: false
last_used: null
created_at: "YYYY-MM-DD"
updated_at: "YYYY-MM-DD"
review_after: null
main_claim:
  claim_id: "C-001"
  text: "Основное обобщённое утверждение"
  kind: inference
  source:
    type: conversation
    reference: null
  confidence: 0.6
  independence_group: null
additional_claims: []
critique:
  first_attempt: null
  failure: null
  cause_status: UNKNOWN
  cause: null
  correction: null
  residual_risk: null
---

**Редакция шаблона:** `v1.3.2`  
**Версия YAML-схемы:** `1.2`

# Название инсайта

## Наблюдение

Что было замечено и в каком контексте.

## Обобщение

Формулировка принципа или закономерности. Не расширяй область действия дальше имеющихся свидетельств.

## Основания

Связь с claim ID, источниками и независимыми эпизодами из YAML.

## Условия применимости

В каких средах/задачах обобщение может работать.

## Границы и контрпримеры

Когда обобщение может не работать, какие альтернативные объяснения существуют.

## Отвергнутые варианты и Negative Memory (если применимо)

Укажи рассмотренный подход, контекст, подтверждённую или гипотетическую причину отказа, evidence, границы применимости и условия возможного пересмотра. Не превращай единичный неудачный случай в универсальный запрет. Если эта информация уже подробно описана в связанной EXPERIENCE, дай точную ссылку и не дублируй её целиком.

## Как проверить

Предложи проверяемый способ подтвердить или опровергнуть инсайт. Не заявляй, что проверка уже проведена.

---

## Правила заполнения

- Каждый `main_claim` и каждый объект `additional_claims` обязан иметь одинаковую структуру: `claim_id`, `text`, `kind`, `source.type`, `source.reference`, `confidence`, `independence_group`.
- `additional_claims` всегда массив; при отсутствии дополнительных утверждений — `[]`.
- `kind`: `test_verified`, `user_reported`, `directly_observed`, `externally_documented`, `inference` или `hypothesis`.
- Один эпизод может обосновать гипотезу, но не независимую закономерность. Повторные пересказы одного эпизода имеют один `independence_group`.
- Не поднимай `maturity` до `VALIDATED` самостоятельно; применяется 12-балльная рубрика Consolidator и отдельное решение пользователя.
- `claim_id` уникален внутри документа: основной claim `C-001`, дополнительные `C-002` и далее.
