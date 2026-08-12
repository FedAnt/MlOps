# Программа: Terraform / OpenTofu (минимум под оффер)

> Компактный трек **фазы 5b** — рынок Senior remote 400k часто требует IaC (Terraform).  
> Не растягивать в отдельный «курс на месяцы»: цель — **применяемый MVP + буллет в резюме**.

Связано: [`карта-курса-лаборатории.md`](./карта-курса-лаборатории.md), [`резюме-черновик.md`](./резюме-черновик.md), сигнал рынка в command `career/data/market/`.

**Обновлено:** 2026-08-04  
**Статус:** ⏳ не начато (старт после Prometheus baseline трека F)

---

## Зачем (рынок)

В срезе `@devops_jobs_feed` (2026-08-04) Terraform ~⅓ вакансий и часто в remote с верхом ≥400k.  
Ansible у вас уже есть в проде — на интервью нужна связка: **Ansible = config/CM, Terraform = provisioning / cloud-like IaC**.

---

## Ограничения лабы

- VirtualBox / on-prem: провайдер **не AWS обязателен**.
- Допустимые MVP (выбрать **один**):
  1. **OpenTofu/Terraform + null/local/kubernetes/helm provider** — описать namespace, configmap или helm release data-platform; state в Git-игнорируемом backend (local) или HTTP/S3-compatible MinIO.
  2. Позже stretch: **Yandex Cloud** provider (если появится облачный аккаунт) — VPC/SA/Managed K8s — не блокер оффера.

Рекомендация: вариант 1 сейчас; YC — отдельный stretch после фазы 5b ✅.

---

## Порядок треков

| Трек | Содержание | Критерий «готово» | Оценка |
|------|------------|-------------------|--------|
| **T0** | Зачем TF vs Ansible; state; plan/apply/destroy | Устно 2 мин на интервью | 1 сессия |
| **T1** | OpenTofu или Terraform CLI в lab; первый `*.tf` | `tofu plan` без ошибок | 1–2 сессии |
| **T2** | Ресурс(ы) под k3s: namespace + один helm_release **или** kubernetes_manifest | `apply` → объект есть в кластере | 2–3 сессии |
| **T3** | Модуль + variables/outputs; два env через tfvars (dev/staging-имена) | Повторный apply идемпотентен | 1–2 сессии |
| **T4** | CI: job `tofu validate` / `plan` (без apply в main без manual) | Pipeline зелёный | 1–2 сессии |
| **T5** | Буллет в резюме + 5 вопросов интервью | Запись в `резюме-черновик.md` | 1 сессия |

**Не делать в 5b:** полный multi-cloud, Terragrunt monorepo, Atlantis — это post-offer / фаза 7+.

---

## Чеклист

- [ ] **T0** — различия TF / Ansible сформулированы
- [ ] **T1** — CLI установлен; провайдер выбран
- [ ] **T2** — apply создаёт ресурс в k3s
- [ ] **T3** — модуль + tfvars
- [ ] **T4** — validate/plan в GitLab CI
- [ ] **T5** — буллет + дата в таблице компетенций

---

## Артефакт для резюме (шаблон)

> Описал инфраструктуру lab data-platform как IaC (OpenTofu/Terraform): …; `plan`/`apply` идемпотентны; проверка `validate`/`plan` в GitLab CI.

---

## Когда стартовать

1. Закрыть в фазе 5 минимум: **§0 + трек F (Prometheus scrape UP + один дашборд/PromQL)**.  
2. Затем **5b T0–T5**.  
3. Параллельно/после: StatsD, Sentry, сквозной H — не блокировать офферный трек бесконечным observability.
