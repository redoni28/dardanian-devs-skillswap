# SkillSwap

**Dardanian Devs · SWEN383 · Professor Valon Raca**

SkillSwap is a campus web application where students offer skills, find peers who can help them learn, and arrange free one-to-one learning sessions.

**Team:** Redon, Rinor, Granit, and Leanda.

**Project stage:** Part 1 design and documentation. Application implementation is the next phase.

## Project documents

- [Part 1 report (PDF)](docs/SWEN383_P1_DardanianDevs.pdf)
- [UML diagrams, editable sources, and design notes](docs/uml/README.md)

The report covers the project description, scope, requirements, proposed architecture, one class diagram, four sequence diagrams, and three design risks with planned patterns.

## Core features

- Student accounts and profiles with learning interests.
- Skill offers that students can create, edit, and archive.
- Search by skill and filter by category.
- Session requests with a proposed time and meeting details.
- Tutor acceptance or rejection of requests, with checks for overlapping bookings.
- Personal dashboards, cancellation, and session completion.

A student can act as a learner and a tutor using the same account. Teaching is voluntary and does not require payment or credits.

## Proposed technology stack

| Area | Planned tools |
| --- | --- |
| Application | Java and Spring Boot |
| Web interface | Spring MVC, Thymeleaf, HTML, CSS, and small amounts of JavaScript |
| Authentication | Spring Security |
| Persistence | Spring Data JPA and PostgreSQL |
| Build and tests | Maven, JUnit, and database integration tests |

The design uses a Service Layer, repositories, and a Unit of Work with database locking for booking changes.

## Scope boundaries

The first release serves one university community and supports individual sessions. Payments, time credits, ratings, real-time chat, built-in video calls, AI matching, group classes, recurring bookings, calendar/email integrations, university SSO, and native mobile apps are outside the planned release.

## Repository structure

```text
.
├── README.md
├── CONTRIBUTING.md
├── .gitignore
└── docs/
    ├── SWEN383_P1_DardanianDevs.pdf
    └── uml/
        ├── README.md
        ├── 01-domain-class.puml
        ├── 01-domain-class.svg
        ├── 02-publish-skill.puml
        ├── 02-publish-skill.svg
        ├── 03-request-session.puml
        ├── 03-request-session.svg
        ├── 04-accept-session.puml
        ├── 04-accept-session.svg
        ├── 05-cancel-or-complete.puml
        └── 05-cancel-or-complete.svg
```

## Team workflow

Each team member should commit their own work from their own account, with messages explaining the change. Keep diagrams and documentation aligned with the implementation. See [contribution guidance](CONTRIBUTING.md).
