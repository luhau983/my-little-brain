---
title: pd-management
type: entity
entity_type: project
tags: [project, doltech, teacher, penalty, bonus, hr]
created: 2026-06-22
updated: 2026-06-22
status: active
source_count: 1
sources: ["[[src-2026-06-22-spring-monorepo-survey]]"]
---

# pd-management

## English

**One-liner.** Teacher Performance & Discipline management: penalties (late/unmarked/incomplete),
performance bonuses, and workload tracking — with Kafka sync, internal-event side-effects, and CQRS-lite.

**Stack.** Baseline + Kafka inbound listeners, internal application-event pattern, cron batch jobs.

**Features.**
- **Teacher penalty management** — `/api/penalty/*`: paged penalty notes/records, `PenaltyAnalysis` detail, teacher search.
  Polymorphic `PenaltyRecord` (Assignment/FinalTest/StudentNote) → monthly `PenaltyAnalysis` → `PenaltySummary`. Kafka inbound
  `penalty-record-sync`, `pd.penalty.kill-record`.
- **Penalty discount** — `/api/penalty/discount` (POST/PATCH/DELETE): manual reductions w/ reason; `DiscountRecord(+History)`;
  recalculates parent analysis/summary.
- **Teacher bonus management** — `/api/bonus/*`: create-full / by-subclass, update/complete, precalculate, recalculate-stats/rank,
  sync-appsheet. Entity `CourseTeacherBonus` (feedback scores, `DolRank` NONE/GOOD/VERY_GOOD/LINEAR_GOOD/JUNIOR, temp/final amounts, AM review).
- **Workload management** — `/api/workload/*`: paged teacher workload (pending/overdue counts), workload detail, named `WorkloadView` configs.
- **Cron/batch** — `PenaltyCronJobServiceCommandHandler`, history archiving; manual triggers via `CronjobController`.

**Data model.** `penalty_record` (polymorphic), `penalty_analysis`, `penalty_summary`, `penalty_settlement`, `discount_record`,
`course_teacher_bonus(+history)`, `course_student_feedback_matching`, `workload_management`, `workload_view`.

**Integrations.** [[assignment-service]] (late/approval events), course-app-sheet (course/feedback + bonus sync target),
mid-final-test (unmarked tests), Directus; Kafka inbound topics above; Redis. Internal event listeners trigger recalcs.

**Gotchas.** Complex bonus rank logic (JUNIOR vs standard; feedback ≥3.5 + keyword match ≥25% → rank; skill multiplier 0.5-1.5×,
student-count multiplier). Polymorphic penalty records need matching `mainType` for Jackson. `internalEvent` (transient) field
signals downstream recalcs via listeners. Settlement vs external-sync timestamps can lag (`lastSyncSettleStatusAt`).

## Tiếng Việt

**Một dòng.** Quản lý Hiệu suất & Kỷ luật giáo viên: phạt (trễ/chưa chấm/thiếu note), thưởng hiệu suất, và theo dõi
khối lượng công việc — với Kafka sync, side-effect qua internal-event, và CQRS-lite.

**Stack.** Baseline + listener Kafka inbound, pattern internal application-event, cron batch.

**Chức năng.**
- **Quản lý phạt giáo viên** — `/api/penalty/*`: phân trang note/record phạt, chi tiết `PenaltyAnalysis`, search giáo viên.
  `PenaltyRecord` đa hình (Assignment/FinalTest/StudentNote) → `PenaltyAnalysis` tháng → `PenaltySummary`. Kafka inbound
  `penalty-record-sync`, `pd.penalty.kill-record`.
- **Giảm trừ phạt** — `/api/penalty/discount` (POST/PATCH/DELETE): giảm thủ công kèm lý do; `DiscountRecord(+History)`; tính lại analysis/summary.
- **Quản lý thưởng** — `/api/bonus/*`: create-full / theo subclass, update/complete, precalculate, recalculate-stats/rank,
  sync-appsheet. Entity `CourseTeacherBonus` (điểm feedback, `DolRank`, số tiền tạm/cuối, AM review).
- **Quản lý workload** — `/api/workload/*`: phân trang khối lượng giáo viên (pending/overdue), chi tiết, cấu hình `WorkloadView`.
- **Cron/batch** — xử lý phạt theo tháng, archive history; trigger tay qua `CronjobController`.

**Data model.** `penalty_record` (đa hình), `penalty_analysis`, `penalty_summary`, `penalty_settlement`, `discount_record`,
`course_teacher_bonus(+history)`, `course_student_feedback_matching`, `workload_management`, `workload_view`.

**Tích hợp.** [[assignment-service]] (event trễ/duyệt), course-app-sheet (feedback + đích sync bonus), mid-final-test, Directus;
Kafka inbound; Redis. Internal event listener kích hoạt recalc.

**Lưu ý.** Logic rank thưởng phức tạp (JUNIOR vs thường; feedback ≥3.5 + keyword match ≥25% → rank; nhân hệ số skill 0.5-1.5×,
hệ số sĩ số). `PenaltyRecord` đa hình cần `mainType` khớp cho Jackson. Field `internalEvent` (transient) báo hiệu recalc qua listener.
Mốc settlement vs sync ngoài có thể lệch (`lastSyncSettleStatusAt`).

## Sources
- [[src-2026-06-22-spring-monorepo-survey]]
