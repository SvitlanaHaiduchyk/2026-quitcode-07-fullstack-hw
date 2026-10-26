# Здача WS7

## Дані

- Роль: dev
- Команда: leave-portal
- GitHub-логін: SvitlanaHaiduchyk
- Ваше репо: https://github.com/SvitlanaHaiduchyk/course-staff-management
- SHA: cf2ba4bbf585dec2c805136c224a38c814a7820d
- Репо вимог PM: https://github.com/mkozlovskyi-ops/course-staff-management-spec
- Прод-URL: https://course-staff-management.vercel.app

## PM

—

### Приймання на проді (трек D)

—

## Розробник

- Рядок «Вимоги:» з `docs/conformance.md` на SHA: Вимоги: https://github.com/mkozlovskyi-ops/course-staff-management-spec · джерело: docs · знімок 2026-10-26
- PR «Оновлення вимог» зі зрізом 2 (A): https://github.com/SvitlanaHaiduchyk/course-staff-management/pull/19 — знімок 2026-10-26 (коміт PM `cddaf8f` від 24.10)
- PR «Оновлення вимог» після уточнень PM (A): той самий https://github.com/SvitlanaHaiduchyk/course-staff-management/pull/19 — `/requirements-sync` запущено 26.10 вже після відповідей PM. Коміт PM `cddaf8f` додав п'ять припущень за відповідями на питання #13–#17 і уточнив причини в «Out of scope»; **жодного AC не додано, не змінено й не прибрано** (67 до і після), тож зміни специфікації з ADDED / MODIFIED цей сync не потребував.
- Питання в репо PM (A; щонайменше 2, з них щонайменше 1 — власне issue): https://github.com/mkozlovskyi-ops/course-staff-management-spec/issues/13, https://github.com/mkozlovskyi-ops/course-staff-management-spec/issues/14, https://github.com/mkozlovskyi-ops/course-staff-management-spec/issues/15 — три власні issues через вебформу «Питання до вимог» (23.10). Раніші: …/issues/5, …/issues/6, …/issues/7, …/issues/12. Журнал — https://github.com/SvitlanaHaiduchyk/course-staff-management/blob/cf2ba4bbf585dec2c805136c224a38c814a7820d/docs/spec-reading.md
- PR «Специфікація» з `add-<зріз2>` (A): https://github.com/SvitlanaHaiduchyk/course-staff-management/pull/23 — план `impl-leave-decision`.

  **Чому не `add-leave-decision`:** PM опублікував усі три вимоги (`01-leave-request.md`, `02-leave-decision.md`, `03-leave-balance.md`) разом ще 19.10, і я переклала їх усі в WS6 однією зміною. Тому всі 24 AC зрізу 2 (`AC-DECIDE-01` … `AC-DECIDE-24`) уже лежать в `openspec/specs/` із **тими самими ID PM** — архів зміни: https://github.com/SvitlanaHaiduchyk/course-staff-management/tree/cf2ba4bbf585dec2c805136c224a38c814a7820d/openspec/changes/archive/2026-10-20-add-leave · уточнення після відповідей PM: …/archive/2026-10-20-align-leave і …/archive/2026-10-21-align-leave-2. Специфікація зрізу 2: https://github.com/SvitlanaHaiduchyk/course-staff-management/blob/cf2ba4bbf585dec2c805136c224a38c814a7820d/openspec/specs/leave-decision/spec.md. `npm run ac:coverage` зелений, без «вимогу PM ще не перекладено».
- Дизайн-система — PR (B): https://github.com/SvitlanaHaiduchyk/course-staff-management/pull/20
- Дизайн-система — `DESIGN.md` і джерело (B): https://github.com/SvitlanaHaiduchyk/course-staff-management/blob/cf2ba4bbf585dec2c805136c224a38c814a7820d/DESIGN.md · джерело: AI-чат: Claude Code (промпт — в описі PR #20)
- Дизайн-система — прогін `architecture` на `main` (B): https://github.com/SvitlanaHaiduchyk/course-staff-management/actions/runs/40404070688
- Знімки «до/після» (B): https://github.com/SvitlanaHaiduchyk/course-staff-management/blob/cf2ba4bbf585dec2c805136c224a38c814a7820d/docs/img/ws7-before-login-light.jpg, …/ws7-before-login-dark.jpg, …/ws7-after-login-light.jpg, …/ws7-after-login-dark.jpg
- Зміна `impl-<зріз2>` (C): https://github.com/SvitlanaHaiduchyk/course-staff-management/tree/cf2ba4bbf585dec2c805136c224a38c814a7820d/openspec/changes/impl-leave-decision
- PR-и задач «Реалізація» (C; щонайменше 2): https://github.com/SvitlanaHaiduchyk/course-staff-management/pull/25 (рішення менеджера: база, дія, сторінка `/decisions`), https://github.com/SvitlanaHaiduchyk/course-staff-management/pull/27 (працівник після рішення: години, скасування, повторне подання). Плюс https://github.com/SvitlanaHaiduchyk/course-staff-management/pull/26 — виправлення за рев'ю CodeRabbit на #25.
- Мутаційна перевірка — червоні прогони (C; щонайменше 2): **червоних прогонів CI немає.** Усі шість мутацій я проганяла локально, а вивід кожної вклала в опис відповідного PR — таблиця «AC → що прибрали → який тест упав»:
  - #25: `private.decides_record → select true` валить `AC-DECIDE-09` і `AC-DECIDE-18`; прибрати `status = 'awaiting'` з `using` — валить `AC-DECIDE-07`; прибрати constraint trigger — валить `AC-DECIDE-15`;
  - #27: прибрати `status in ('awaiting','returned')` з `using` — валить `AC-DECIDE-12` і `AC-DECIDE-17`; прибрати `rec.id <> p_record_id` — валить `AC-DECIDE-16` і `AC-DECIDE-06`.

  В описі #27 я також чесно зазначила **одну мутацію, яку жоден тест не впіймав** (ослаблення `with check`): той самий випадок уже перекривають дві інші лінії, тож цей фрагмент політики лишаю як захист углиб і **не** приписую йому жодного AC.
- ADR (D): https://github.com/SvitlanaHaiduchyk/course-staff-management/blob/cf2ba4bbf585dec2c805136c224a38c814a7820d/docs/decisions/0002-permission-depends-on-owner-not-only-role.md — рішення зрізу 2: право вирішувати залежить від власника запису, а не лише від ролі (п'ять розглянутих варіантів із «чому ні»). Другий: …/docs/decisions/0001-atomic-request-via-db-function.md
- Архітектурне правило, крім `check:design` (D): job **«Секретний ключ лише на сервері»** у `.github/workflows/architecture.yml` (`npm run check:boundary`). Зелений на `main`: https://github.com/SvitlanaHaiduchyk/course-staff-management/actions/runs/40404070688. Доказ, що ловить порушення, — вивід скрипта на навмисному порушенні в описі https://github.com/SvitlanaHaiduchyk/course-staff-management/pull/24 (admin-клієнт у `page.tsx` і `NEXT_PUBLIC_…SECRET…`: 4 порушення, exit 1; на чистому дереві — OK, exit 0). ADR 0001 і ADR 0002 посилаються на це правило.
- Акаунти для PM (E): admin@example.test (адміністратор), manager1@example.test (відповідальний менеджер), teacher1@example.test (працівник). Паролі — PM особистим повідомленням у чаті команди.
- Скріни за ролями (E): **ще не додано** — буде окремим PR до кінця 27.10.
- AC зрізу 2 (E): усі 24 AC вимоги `02-leave-decision.md` — **реалізовано**: AC-DECIDE-01, -02, -03, -04, -05, -06, -07, -08, -09, -10, -11, -12, -13, -14, -15, -16, -17, -18, -19, -20, -21, -22, -23, -24. Матриця: https://github.com/SvitlanaHaiduchyk/course-staff-management/blob/cf2ba4bbf585dec2c805136c224a38c814a7820d/docs/conformance.md (45 із 67 AC реалізовано; решта 22 — зрізи WS8–WS11)
- Відхилення від PM (E): не надходило

## Бонус

—
