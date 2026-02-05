# Governance (How We Operate)

## Project Board
All work is tracked in GitHub Projects: “Marist Cyber Range – Build & Ops”.
Every meaningful task must have an Issue.

## Roles
- Project Lead: coordinates priorities, meetings, and final deliverables
- Technical Leads (as assigned): Architecture, Network, Telemetry, Scenarios
- Contributors: complete issues, update docs, attach evidence

## Branching / Commits
- Main branch is the source of truth.
- Small doc changes can be committed directly to main.
- Larger changes should use a feature branch + pull request when possible.

## Documentation Standard
- If it isn’t documented in this repo, it doesn’t exist.
- Every design decision must include a short rationale.

## Evidence Standard
For builds/scenarios, add evidence under:
- `/evidence/week-XX/`
Include:
- screenshots, logs, config excerpts, or command output
- short notes: what was done and what it proves

## Definition of Done
An issue is “Done” only when:
- Documentation is updated and committed
- Evidence is added (when applicable)
- Another teammate reviews and comments “Reviewed”

## Meeting Rhythm
- Mondays: client meeting (Central Hudson) preparation and follow-ups
- Thursdays: professor meeting preparation and follow-ups
- After each meeting: update meeting notes + convert action items into Issues

## Tooling Changes
Tooling choices that impact long-term maintainability must be documented:
- what changed
- why we changed it
- how to reproduce it

