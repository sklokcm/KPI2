## Prompt
Check non-functional requirements and edit what shoub be changed or add what is missing

## AI Response
I’m reviewing the current non-functional section and will tighten the wording so it is measurable, specific, and aligned with real system expectations.

Read 

Replacing 10 lines with 13 lines in 


```

```
## ✅ Non-functional requirements updated

I revised the NFR section in `specs.md` to make it more realistic and complete.

### What changed
- clarified password hashing with bcrypt/Argon2
- added HTTPS and encryption requirements
- made the UI requirement more specific and accessibility-oriented
- improved browser compatibility wording
- added backup/recovery requirement
- defined session timeout
- made performance requirement measurable:
  - 2000 concurrent users
  - 95% of requests within 3 seconds
- refined the security/attack handling requirement so it is safer and more actionable

### Why this is better
These requirements are now:
- more testable
- closer to real production expectations
- easier to validate during implementation and QA

If you want, I can next make the functional requirements in `specs.md` equally formal and testable by converting them into a consistent “When … then …” style.

Made changes.