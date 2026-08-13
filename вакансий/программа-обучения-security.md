# Программа: безопасность (фаза 7, минимум)

Компактный трек: применимый MVP + threat model «на салфетке», не курс по Zero Trust.

Связано: [`план-практики…`](./план-практики-инфраструктура-senior-devops.md), [`docs/security-baseline.md`](../../platform-service/docs/security-baseline.md), [`platform-infra/docs/secrets-policy.md`](../../platform-infra/docs/secrets-policy.md).

**Обновлено:** 2026-08-13  
**Статус:** ✅ S0–S3 закрыты (фаза 7 MVP)

---

## Журнал

### Урок S0 (закрыт, 2026-08-13)

Сделано: threat model + scope MVP + квиз.  
Артефакт: `docs/security-baseline.md`.  
Критерий: закрыт.

### Урок S1 (закрыт, 2026-08-13)

Сделано: NetworkPolicy + smoke (allow Traefik/Prom, deny default, Bugsink egress :8000).  
Артефакт: `helm/.../networkpolicy.yaml`.  
Критерий: закрыт.

### Урок S2 (закрыт, 2026-08-13)

Сделано: dedicated SA; CI `scan_image_trivy` (allow_failure).  
Артефакт: `serviceaccount.yaml`, `ci/includes/security.yml`.  
Критерий: закрыт (первый зелёный/жёлтый pipeline — после push).

### Урок S3 (закрыт, 2026-08-13)

Сделано: secrets policy §7 + буллет/компетенция в резюме.  
Артефакт: `резюме-черновик.md`, `platform-infra/docs/secrets-policy.md`.  
Критерий: закрыт.

---

## Треки

| ID | Содержание | Критерий |
| --- | --- | --- |
| **S0** | Threat model, trust boundaries, scope | документ + квиз |
| **S1** | NetworkPolicy для одного сервиса | apply + smoke |
| **S2** | Dedicated SA + Trivy в CI | pipeline + pod SA |
| **S3** | Secrets policy + резюме | политика + буллет |

## Чеклист

- [x] **S0** — threat model зафиксирован
- [x] **S1** — NetworkPolicy работает
- [x] **S2** — SA + Trivy
- [x] **S3** — резюме обновлено

---

## 3 вопроса на интервью (security)

1. **Зачем NetworkPolicy, если уже есть Ingress?**  
   Ingress — вход снаружи в кластер. NP — east-west: кто внутри кластера может говорить с подом.

2. **Почему DSN/kubeconfig не в values.yaml?**  
   Git = аудит и утечка в историю. Секреты — GitLab Variables / K8s Secret; в chart только `secretKeyRef`.

3. **Trivy в CI — gate или сигнал?**  
   В лабе: отчёт + fail на CRITICAL (или soft-fail). В проде: политика severity + exception process, иначе шум ломает поставку.
