# Data Model and Security — Supabase/PostgreSQL

## 1. Scope

This schema supports one authenticated user without introducing organizations, team roles, invitations, subscriptions, or public profiles. Tables still include `user_id` so Row Level Security can enforce ownership.

Use UUID primary keys, `timestamptz` for event timestamps, `date` for date-only values, and `Europe/Warsaw` only at the presentation and scheduling boundary. Store timestamps in UTC.

Every mutable table should normally include `created_at` and `updated_at`.

## 2. Core entities

### `profiles`

- `user_id uuid primary key references auth.users`
- `display_name text`
- `timezone text default 'Europe/Warsaw'`
- `locale text default 'pl-PL'`
- `primary_google_email text`
- `onboarding_completed_at timestamptz null`

No public profile access.

### `app_settings`

- `id uuid primary key`
- `user_id uuid unique`
- `sidebar_collapsed boolean`
- `daily_source_check_enabled boolean`
- `push_enabled boolean`
- `default_focus_minutes integer`
- `default_break_minutes integer`
- `training_template jsonb`
- `notification_preferences jsonb`

### `courses`

- `id uuid primary key`
- `user_id uuid`
- `name text`
- `short_name text null`
- `term text`
- `lecturer text null`
- `language_code text null`
- `course_kind text`
- `measurement_mode text check in ('none','skill_level','cefr')`
- `measurement_value text null`
- `source_id uuid null`
- `archived_at timestamptz null`

### `class_series`

- `id uuid primary key`
- `user_id uuid`
- `course_id uuid`
- `weekday smallint`
- `start_time time`
- `end_time time`
- `valid_from date`
- `valid_until date null`
- `recurrence_rule text null`
- `building text null`
- `room text null`
- `status text check in ('confirmed','tentative','cancelled')`
- `source_id uuid null`

### `class_occurrences`

- `id uuid primary key`
- `user_id uuid`
- `series_id uuid null`
- `course_id uuid`
- `starts_at timestamptz`
- `ends_at timestamptz`
- `building text null`
- `room text null`
- `status text check in ('scheduled','moved','cancelled','completed')`
- `supersedes_occurrence_id uuid null`
- `source_id uuid null`

Occurrences support exceptions without destroying the original series.

### `tasks`

- `id uuid primary key`
- `user_id uuid`
- `course_id uuid null`
- `title text`
- `description text null`
- `status text check in ('inbox','planned','in_progress','done','missed','cancelled')`
- `priority text check in ('low','medium','high','urgent')`
- `due_at timestamptz null`
- `due_precision text check in ('exact','date_only','unknown')`
- `estimated_minutes integer null`
- `completed_at timestamptz null`
- `source_id uuid null`

### `assessments`

- `id uuid primary key`
- `user_id uuid`
- `course_id uuid`
- `title text`
- `kind text check in ('quiz','colloquium','exam','project','presentation','activity','other')`
- `scheduled_at timestamptz null`
- `deadline_at timestamptz null`
- `weight numeric null`
- `max_score numeric null`
- `status text check in ('planned','completed','cancelled','unknown_date')`
- `source_id uuid null`

### `grade_entries`

- `id uuid primary key`
- `user_id uuid`
- `course_id uuid`
- `assessment_id uuid null`
- `label text`
- `score numeric`
- `max_score numeric null`
- `weight numeric null`
- `recorded_at timestamptz`
- `source_id uuid null`

Forecasts should be calculated from entries and assessment rules. Avoid storing a forecast as an authoritative grade unless also storing calculation inputs and timestamp.

### `study_sessions`

- `id uuid primary key`
- `user_id uuid`
- `course_id uuid null`
- `task_id uuid null`
- `title text`
- `starts_at timestamptz`
- `planned_minutes integer`
- `actual_minutes integer default 0`
- `status text check in ('planned','active','completed','partial','missed','cancelled')`
- `focus_mode text null`
- `rescheduled_from_id uuid null`
- `source_id uuid null`

### `focus_intervals`

- `id uuid primary key`
- `user_id uuid`
- `study_session_id uuid`
- `started_at timestamptz`
- `ended_at timestamptz null`
- `duration_seconds integer null`
- `interruption_count integer default 0`

### `materials`

- `id uuid primary key`
- `user_id uuid`
- `course_id uuid null`
- `title text`
- `material_kind text check in ('pdf','presentation','note','link','image','other')`
- `storage_bucket text null`
- `storage_path text null`
- `external_url text null`
- `mime_type text null`
- `size_bytes bigint null`
- `source_id uuid null`

Require exactly one of app-managed storage or external URL where practical.

### `study_session_materials`

- `study_session_id uuid`
- `material_id uuid`
- composite primary key

### `opportunities`

- `id uuid primary key`
- `user_id uuid`
- `title text`
- `category text`
- `pipeline_status text check in ('detected','review','watching','applying_registered','completed','rejected')`
- `starts_at timestamptz null`
- `ends_at timestamptz null`
- `application_deadline timestamptz null`
- `location text null`
- `format text null`
- `cost_text text null`
- `eligibility text null`
- `prizes text null`
- `official_url text null`
- `relevance_reason text null`
- `is_priority boolean default false`
- `last_verified_at timestamptz null`
- `source_id uuid null`

### `formalities`

- `id uuid primary key`
- `user_id uuid`
- `title text`
- `authority text null`
- `status text check in ('unknown','todo','waiting','done','not_applicable')`
- `deadline_at timestamptz null`
- `urgency text`
- `official_url text null`
- `source_id uuid null`

### `source_records`

Provenance table for user statements, screenshots, files, calendar imports, emails, and portal checks.

- `id uuid primary key`
- `user_id uuid`
- `source_type text check in ('user_text','image','screenshot','pdf','presentation','email_paste','gmail','google_calendar','ics','portal_check','seed')`
- `display_name text`
- `external_reference text null`
- `captured_at timestamptz`
- `confidence numeric null check between 0 and 1`
- `confirmed_at timestamptz null`
- `storage_path text null`
- `metadata jsonb`

### `ingestion_items`

- `id uuid primary key`
- `user_id uuid`
- `source_id uuid`
- `status text check in ('received','parsed','needs_clarification','proposed','accepted','rejected','failed')`
- `raw_text text null`
- `extracted_data jsonb`
- `missing_fields jsonb`
- `error_message text null`

### `change_proposals`

- `id uuid primary key`
- `user_id uuid`
- `ingestion_item_id uuid null`
- `target_type text`
- `target_id uuid null`
- `operation text check in ('create','update','delete','reschedule','link')`
- `before_data jsonb null`
- `after_data jsonb`
- `status text check in ('pending','accepted','rejected','expired')`
- `requires_external_write boolean default false`
- `confirmed_at timestamptz null`

### `external_actions`

- `id uuid primary key`
- `user_id uuid`
- `proposal_id uuid`
- `provider text check in ('google_calendar','gmail','google_drive','push')`
- `action_type text`
- `preview_payload jsonb`
- `status text check in ('preview','confirmed','executing','succeeded','failed','cancelled')`
- `idempotency_key text unique`
- `provider_reference text null`
- `executed_at timestamptz null`
- `error_message text null`

### `notifications`

- `id uuid primary key`
- `user_id uuid`
- `title text`
- `body text`
- `severity text check in ('info','action_required','urgent','critical')`
- `destination_url text null`
- `read_at timestamptz null`
- `resolved_at timestamptz null`
- `source_id uuid null`

### `source_check_status`

- `id uuid primary key`
- `user_id uuid`
- `source_name text`
- `last_checked_at timestamptz null`
- `last_result text null`
- `freshness_state text check in ('current','check_recommended','stale')`
- unique `(user_id, source_name)`

### `briefs`

- `id uuid primary key`
- `user_id uuid`
- `brief_date date`
- `brief_kind text check in ('daily','evening')`
- `snapshot jsonb`
- `generated_at timestamptz`
- unique `(user_id, brief_date, brief_kind)`

### `daily_reviews`

- `id uuid primary key`
- `user_id uuid`
- `review_date date`
- `rating smallint check between 1 and 10`
- `note text null`
- unique `(user_id, review_date)`

### `audit_log`

- `id uuid primary key`
- `user_id uuid`
- `actor_type text check in ('user','agent','system','integration')`
- `action text`
- `entity_type text`
- `entity_id uuid null`
- `before_data jsonb null`
- `after_data jsonb null`
- `source_id uuid null`
- `created_at timestamptz`

Audit records are append-only from the normal application path.

## 3. Suggested indexes

- `(user_id, due_at)` on tasks.
- `(user_id, starts_at)` on class occurrences and study sessions.
- `(user_id, pipeline_status, application_deadline)` on opportunities.
- `(user_id, read_at, created_at desc)` on notifications.
- `(user_id, status, created_at desc)` on ingestion items and change proposals.
- `(user_id, source_name)` unique on source checks.
- Full-text or trigram search only after real search needs are observed.

## 4. RLS policy pattern

Enable RLS for every exposed table. For an owned table:

```sql
create policy "read own rows"
on public.example
for select
to authenticated
using ((select auth.uid()) = user_id);

create policy "insert own rows"
on public.example
for insert
to authenticated
with check ((select auth.uid()) = user_id);

create policy "update own rows"
on public.example
for update
to authenticated
using ((select auth.uid()) = user_id)
with check ((select auth.uid()) = user_id);

create policy "delete own rows"
on public.example
for delete
to authenticated
using ((select auth.uid()) = user_id);
```

Do not rely on `TO authenticated` without ownership. Do not use `user_metadata` for authorization.

## 5. Storage

Suggested private bucket: `materials`.

Path convention:

`{auth.uid()}/{course_id-or-general}/{uuid}/{sanitized-filename}`

Rules:

- private bucket;
- signed download URLs created server-side when needed;
- MIME allowlist;
- configurable size cap;
- ownership check from the first path segment;
- INSERT + SELECT + UPDATE for allowed upserts;
- delete requires explicit app confirmation and audit entry.

## 6. Integration boundaries

Define typed provider interfaces:

- `CalendarProvider`
- `MailProvider`
- `FileProvider`
- `NotificationProvider`
- `DocumentExtractor`
- `AgentInterpreter`

Provide fixture implementations before live integrations. External calls should use idempotency keys and record result state.

## 7. Migrations and verification

1. Iterate against a development environment.
2. Review schema and RLS together.
3. Test each policy as authorized user, different user, and anonymous client.
4. Run Supabase database and security advisors.
5. Generate a clean migration only after behavior is verified.
6. Commit migration files and generated TypeScript types.

No production schema change is complete without policy tests and advisor review.

