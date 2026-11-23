---
schema_version: "1.2"
record_type: EXPERIENCE
id: "EXP-YYYYMMDD-001"
title: "Название опыта"
domain: "domain"
tags: []
project_id: null
priority: WARM
status: CANDIDATE
maturity: DRAFT
lifecycle: PROVISIONAL
criticality: normal
reviewed: false
last_used: null
created_at: "YYYY-MM-DD"
updated_at: "YYYY-MM-DD"
review_after: null
main_claim:
  claim_id: "C-001"
  text: "Основное утверждение об исходе эпизода"
  kind: user_reported
  source:
    type: conversation
    reference: null
  confidence: 0.7
  independence_group: null
additional_claims: []
critique:
  first_attempt: null
  failure: null
  cause_status: UNKNOWN
  cause: null
  correction: null
  residual_risk: null
outcome:
  requested_result: null
  observed_result: null
  test_status: NOT_RUN
  user_confirmed: false
  code_review: false
  evidence_reference: null
---

**Редакция шаблона:** `v1.3.2`  
**Версия YAML-схемы:** `1.2`

# Название опыта

## Контекст

Опиши исходную задачу и условия без приватных деталей и секретов.

## Цель и критерии

Какая цель была поставлена и по каким признакам оценивался результат.

## Ход работы

Фактические действия, важные решения и отклонённые варианты. Не приписывай эпизоду действия, которых нет в источниках.

## Архитектурные и инженерные решения (если применимо)

Для существенного решения зафиксируй исходную проблему, выбранный вариант, рассмотренные альтернативы, критерии выбора, последствия, компромиссы, ограничения и условия пересмотра. Не оформляй это как отдельный YAML `record_type: ADR`: решение остаётся частью EXPERIENCE. Если материал имеет самостоятельную переносимую ценность, Extractor может отдельно предложить INSIGHT с теми же исходными `independence_group`.

## Результат

Разделяй требуемый, наблюдаемый, протестированный и подтверждённый результат.

## Что сработало

Факты и условия, при которых подход оказался полезен.

## Что не сработало

Ошибки, неудачные попытки и ограничения. Если неудач не было в предоставленных данных, укажи «не зафиксировано», а не «не было».

## Negative Memory — отвергнутые варианты

Для каждого варианта укажи контекст, причину отказа, evidence, статус причины (`CONFIRMED` / `HYPOTHESIS` / `UNKNOWN`), границы применимости и условия возможного пересмотра. Не формулируй глобальный запрет из единичного случая. Если таких вариантов нет в источнике, укажи «не зафиксировано».

## Уроки и переносимость

Что может пригодиться в будущих задачах и какие условия ограничивают перенос.

## Остаточные риски

Неизвестные, непроверенные и потенциально опасные моменты.

---

## Правила заполнения

- `lifecycle: PROVISIONAL` — результат или существенные детали ещё не получили достаточного подтверждения. `CONFIRMED` — только при явном пользовательском подтверждении или соответствующих проверяемых свидетельствах. `SUPERSEDED` — только если запись действительно заменена и это подтверждено.
- Каждый `main_claim` и каждый объект `additional_claims` обязан содержать `claim_id`, `text`, `kind`, `source.type`, `source.reference`, `confidence`, `independence_group`.
- `additional_claims` всегда массив; при отсутствии дополнительных claims — `[]`.
- `kind`: `test_verified`, `user_reported`, `directly_observed`, `externally_documented`, `inference` или `hypothesis`.
- `test_status: PASS` в отчёте Worker без доступного свидетельства остаётся сообщённым результатом, а не автоматически `test_verified`.
- Один PASS без user confirmation и без code review остаётся `lifecycle: PROVISIONAL`; такой результат не разрешает SKILL.
- Создание EXPERIENCE не означает применение знания. `last_used` остаётся `null`, пока пользователь не зафиксировал фактическое применение.
- `claim_id` уникален внутри документа: основной claim `C-001`, дополнительные `C-002` и далее.
