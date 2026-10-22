# Petzo web (admin portal)

Admin portal of Petzo (dog/cat adoption, Gran Caracas): moderation queue, foundations and plans, users, reports, Instagram imports, metrics (SPEC §4, HU-12 to HU-15, sprint F2). Source of truth: `docs/SPEC.md` (read only the section you need). Sibling repos: `petzo-backend` (Java API) and `petzo-frontend` (Expo app).

## Stack
- React + Vite + TypeScript. Auth with the Supabase Auth SDK (email/password + Google); data only through the REST API with `Authorization: Bearer <access token>`.
- API: `/api/admin/**` (requires `profiles.role = 'admin'`). Contract = the API's Swagger (`/swagger-ui.html`): camelCase JSON, ProblemDetail errors with `code`.

## Commands
- `npm run dev` · `npm run build`
- API locally: in `petzo-backend`, `./mvnw spring-boot:run` (port 8090).

## Rules
- Only the public Supabase key ships here; never the service_role key. The API is the only writer.
- Approve sends the `version` shown in the queue (`POST /api/admin/pets/{id}/approve?version=`) so stale content is never approved.
- UI text in Spanish; code, names and commits in English. Secrets only in `.env` (`.env.example` lists them).

## Workflow
- Sprint F2 (SPEC §16): short plan (≤10 lines), wait for OK, build, test, commit + push (Conventional Commits, subject only). Scan for secrets before pushing.
- Log skills in `docs/SKILLS_LOG.md` and subagents in `docs/AGENTS_LOG.md` (real uses only).
