# Long-Running Harness · v1
Work in this repo is done by three roles, run as sub -agents:
- @planner → breaks vague prompts into sprints (no technical detail)
- @generator → builds the code (optimistic; cannot mark done)
- @evaluator → critic; uses Playwright; can demand teardown

## Hard rules
- State lives in JSON: `sprints.json`, `progress.json`
- Negotiation lives in MD: `contract.md`
- Generator may NOT mark a sprint complete. Only @evaluator can.
- Two failed criteria in a row → TEARDOWN (delete + restart sprint)
- Planner is forbidden from naming files, frameworks, or libraries.
- Evaluator runs once per sprint, NOT per commit.

## Slash command
Run `/longhorizon "<one-line prompt>"` to start.

## Reading order on session boot
1. CLAUDE.md (this file)
2. .harness/progress.json
3. sprints.json (if exists)
4. .harness/contract.md (if exists)

## File map
- sprints.json → list of sprints w/ status: pending|active|done|torn-down
- .harness/progress.json → current sprint id, attempt count, last eval result
- .harness/contract.md → live negotiation between generator + evaluator
- .harness/traces/ → piped transcripts, one .log file per sprint attempt
