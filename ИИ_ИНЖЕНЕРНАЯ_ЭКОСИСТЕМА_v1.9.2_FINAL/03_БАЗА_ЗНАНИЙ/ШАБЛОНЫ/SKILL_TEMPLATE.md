---
schema_version: "1.2"
record_type: SKILL
id: "SKILL-YYYYMMDD-001"
title: "Название навыка"
skill_type: CHECKLIST
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
  text: "Основное проверяемое утверждение навыка"
  kind: hypothesis
  source:
    type: conversation
    reference: null
  confidence: 0.5
  independence_group: null
additional_claims: []
critique:
  first_attempt: null
  failure: null
  cause_status: UNKNOWN
  cause: null
  correction: null
  residual_risk: null
outcome_gate:
  user_confirmed: false
  test_status: NOT_RUN
  code_review: false
  evidence_reference: null
---

**Редакция шаблона:** `v1.3.1`  
**Версия YAML-схемы:** `1.2`

# Название навыка

## Назначение

Какую задачу решает навык и в каких условиях он полезен.

## Предварительные условия

- Необходимые инструменты и доступы без указания секретов.
- Предположения и ограничения.

## Процедура

1. Шаг 1.
2. Шаг 2.
3. Шаг 3.

## Проверка результата

Опиши наблюдаемый критерий успеха и доступный способ проверки. Не утверждай, что проверка выполнена, если результат проверки не зафиксирован.

## Ограничения и нецелевые случаи

Опиши сценарии, когда навык не подходит или требует дополнительного согласования.

## Безопасность

Укажи риски, потенциально опасные операции и точки обязательного подтверждения.

## История и evidence

Кратко опиши, на каком исходном эпизоде/проверке основан навык, ссылаясь на `claim_id` из YAML. Не дублируй секреты или приватные детали.

---

## Правила заполнения

- `skill_type`: строго одно из `CHECKLIST`, `PROCEDURE`, `RUNBOOK`, `DECISION_TREE`, `PLAYBOOK`.
- Каждый `main_claim` и каждый объект `additional_claims` обязан иметь одинаковые поля: `claim_id`, `text`, `kind`, `source.type`, `source.reference`, `confidence`, `independence_group`.
- `kind`: `test_verified`, `user_reported`, `directly_observed`, `externally_documented`, `inference` или `hypothesis`.
- `additional_claims` всегда массив; при отсутствии дополнительных утверждений — `[]`.
- `outcome_gate.user_confirmed: true` допустим только при явном подтверждении пользователя; `evidence_reference` должен указывать на соответствующее сообщение/эпизод.
- Альтернативный путь: `test_status: PASS` и `code_review: true`; `evidence_reference` должен позволять найти оба свидетельства. Один PASS без пользовательского подтверждения и code review не допускает SKILL.
- Прохождение Outcome Gate разрешает тип записи SKILL, но не `maturity: VALIDATED`. Новая запись остаётся `status: CANDIDATE`, `maturity: DRAFT`, `reviewed: false` до отдельной проверки и решения.
- `claim_id` уникален внутри документа. Для основного claim начни с `C-001`, дополнительные — `C-002` и далее.
- Не переиспользуй `kind` как название типа навыка: тип задаётся исключительно через `skill_type`.

**Примечание Outcome Gate:** шаблон сам по себе не является доказательством прохождения Gate. Значения `user_confirmed`, `test_status`, `code_review` должны соответствовать реальным источникам, а не выводам модели.
