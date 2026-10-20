# SkillSwap — Part 1 Presentation Outline

**Team:** Dardanian Devs  
**Members:** Redon, Leanda, Rinor, Granit  
**Presentation date:** October 28, 2026  
**Duration:** 5 minutes  
**Report:** [SWEN383_P1_DardanianDevs.pdf](./docs/SWEN383_P1_DardanianDevs.pdf)

## 0:00–0:45 — Project purpose
**Show report page 1.**

SkillSwap is a campus web application where students offer skills and find peers who can help them learn.

Students can arrange free, one-to-one learning sessions. The same student can be both a learner and a tutor.

For example, Rinor could find Redon's Java listing and request a 45-minute session. Redon can accept the request if both students are available.

## 0:45–1:30 — Scope and features
**Show report page 2.**

Our planned application includes:
- Student accounts and profiles.
- Creating, editing, and archiving skill listings.
- Searching for skills and filtering by category.
- Requesting sessions with proposed times and meeting details.
- Accepting or declining requests.
- Viewing, cancelling, and completing sessions.

The first release serves one university community. Payments, ratings, real-time chat, built-in video calls, and group classes are outside its scope.

Keeping the scope focused makes the project manageable within the semester.

## 1:30–2:30 — Class diagram
**Show report page 4.**

Our main classes are Student, SkillListing, SkillCategory, and SessionRequest.

A student can own multiple skill listings. Each listing belongs to one category. A session request connects one learner to one listing, and the listing's owner is the tutor.

Learner and tutor are roles, not separate account types.

SessionStatus represents the request's current state: PENDING, ACCEPTED, DECLINED, CANCELLED, or COMPLETED.

The design uses guarded methods such as accept(), cancel(), and complete() to prevent invalid status changes.

## 2:30–3:30 — Request and acceptance walkthrough
**Show report pages 7–8.**

1. A learner selects an active skill listing and submits a proposed time and meeting details.
2. The application checks the listing, the time, and that the learner is not requesting their own listing.
3. A valid request is saved as PENDING. Pending requests do not reserve time.
4. The tutor chooses to accept the request.
5. The service locks both participant records in a consistent order and reloads the request.
6. It checks that the tutor is authorized, the request is still pending, the start is in the future, and neither participant has an overlapping accepted session.
7. If all checks pass, the request becomes ACCEPTED and the transaction commits. Otherwise, the operation is rejected without accepting the request.

These checks are part of our proposed design and have not yet been demonstrated by implementation tests.

## 3:30–4:30 — Design risks and planned patterns
**Show report page 10.**

### Risk 1: Business rules scattered across screens

If controllers repeat ownership and status checks, different screens could enforce different rules.

We plan to use a Service Layer and domain encapsulation. SessionService coordinates permissions and time checks, while SessionRequest methods guard valid state transitions.

The tradeoff is an additional application layer, but it gives business operations a clear location.

### Risk 2: Two overlapping bookings accepted concurrently

Two requests could both appear conflict-free before either acceptance finishes.

We plan to use Unit of Work with database transactions, participant locks, and a fresh overlap check after locking.

A transaction alone does not prevent this race. Every acceptance path must follow the same locking protocol.

The tradeoff is that simultaneous operations may wait for locks.

### Additional planned pattern: Repository

Repositories keep persistence operations separate from business logic. They provide focused methods for finding, locking, and saving records.

## 4:30–5:00 — Next steps and planned testing
**Show report page 11.**

Next, we plan to implement the proposed application and test its business rules.

Key checks include:
- Rejecting unauthorized actions and invalid status changes.
- Preventing overlapping accepted bookings.
- Allowing back-to-back sessions.
- Rolling back failed operations without leaving partial changes.

We will update the UML diagrams as the implementation develops.

## Speaking assignments

To be agreed by the team before rehearsal. These assignments describe presentation responsibilities, not authorship of the existing report.

| Section | Speaker |
|---|---|
| Project purpose and scope | To be agreed |
| Class diagram | To be agreed |
| Request and acceptance walkthrough | To be agreed |
| Risks, patterns, and next steps | To be agreed |

## Preparation checklist

- [ ] Each speaker reads the relevant report pages and checks these notes.
- [ ] The team agrees on speaking assignments.
- [ ] Everyone can explain the main classes and session lifecycle.
- [ ] Everyone can explain why transactions alone do not prevent double booking.
- [ ] The team rehearses with the report visible and a five-minute timer.
- [ ] The team adjusts the notes if rehearsal exceeds five minutes.
- [ ] The final PDF and repository link are submitted through myCourses.
- [ ] The team verifies that the submission was received.

