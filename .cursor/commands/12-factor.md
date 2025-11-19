# 12-Factor App Review

Use this command to review the current service/repo against the Twelve-Factor App methodology for building SaaS/web apps.

## Context

The Twelve-Factor methodology is for apps that:

- Use declarative setup for fast onboarding and automation
- Have a clean contract with the OS for max portability
- Are suitable for modern cloud platforms (no pets/SSH snowflakes)
- Minimize dev/prod divergence to enable continuous deployment
- Can scale out without major changes to tools or architecture :contentReference[oaicite:1]{index=1}

## What to do

1. Infer which app/service I’m working on from the open files, project layout, and config.
2. For this app, assess it against **all 12 factors**:

   1. **Codebase** – One codebase in version control, many deploys.
   2. **Dependencies** – Explicitly declare and isolate dependencies (no hidden system tools/packages).
   3. **Config** – Store deploy-specific config (URLs, creds, hostnames, feature flags) in env vars, not in code or committed files.
   4. **Backing services** – Treat DBs, queues, caches, SMTP, 3rd-party APIs, etc. as attached resources, swappable via config.
   5. **Build, release, run** – Strict separation of build (compile/bundle), release (build + config), and run (execute processes).
   6. **Processes** – Execute the app as one or more stateless, share-nothing processes; persistent state lives in backing services.
   7. **Port binding** – Export services via port binding (self-contained service listening on a port).
   8. **Concurrency** – Scale out via the process model (web/worker/scheduler process types, adjustable formation).
   9. **Disposability** – Fast startup and graceful shutdown; processes can be started/stopped at any time.
   10. **Dev/prod parity** – Keep dev, staging, and prod as similar as possible (time, people, tools, backing services).
   11. **Logs** – Treat logs as event streams; app writes to stdout/stderr, platform handles aggregation/storage.
   12. **Admin processes** – Run admin/one-off tasks (migrations, scripts, consoles) as one-off processes against the same release.

3. For each factor:
   - Describe how this app currently behaves (based on code, config, scripts, directory structure, Dockerfiles, CI, etc.).
   - Call out issues, risks, or twelve-factor violations.
   - Suggest concrete, incremental improvements that can be done in this repo.

4. When suggesting changes, bias toward:
   - Env vars and secret management instead of config checked into VCS.
   - Stateless processes with state in DB/queues/ object storage.
   - Build/release automation via existing CI, not brand new systems.
   - Small, realistic steps (one-PR-at-a-time changes).

## Output format

1. **Overview**  
   2–4 sentences summarizing how “twelve-factor” this app is overall (strong areas, weak areas).

2. **Per-factor table**  

   | # | Factor        | Current state (this app) | Issues / risks | Recommended changes |
   |---|---------------|--------------------------|----------------|---------------------|
   | I | Codebase      | …                        | …              | …                   |
   | II| Dependencies  | …                        | …              | …                   |
   | III| Config       | …                        | …              | …                   |
   | IV| Backing svcs  | …                        | …              | …                   |
   | V | Build/Release/Run | …                   | …              | …                   |
   | VI| Processes     | …                        | …              | …                   |
   | VII| Port binding | …                        | …              | …                   |
   | VIII| Concurrency | …                        | …              | …                   |
   | IX| Disposability | …                        | …              | …                   |
   | X | Dev/prod parity | …                     | …              | …                   |
   | XI| Logs          | …                        | …              | …                   |
   | XII| Admin procs  | …                        | …              | …                   |

3. **Prioritized next steps**  
   3–7 bullets, ordered by impact vs effort. Mark especially:
   - **Low-hanging fruit**: can be done in a single PR.
   - **Structural changes**: might need multiple PRs or some design work.

## Constraints

- Don’t propose a full rewrite; work with the existing stack and patterns.
- Assume the app is (or should be) deployable on modern cloud infra (containers, PaaS, or similar).
- Prefer suggestions that improve:
  - Portability between environments
  - Deployment safety and rollback
  - Scaling via processes, not hand-managed servers
- Keep the analysis focused and actionable, not academic.
