# Building and Deving Part 1 Study Guide

Source: https://tpowell.craft.me/O43FoB5a4asCAa

## Core Premise

If iteration is the key to Agile success, then a solid build pipeline and strong development practices are required.

Agile assumes we cannot know everything about a project before starting. That does not mean "no design up front." The better idea is to do enough design engineering to explore the big ideas, identify obvious risks, and avoid walking blindly into preventable problems.

After that, process engineering helps deal with the uncertainty that remains. Agile handles uncertainty through experimentation by iteration: many small experiments, repeated quickly, with enough protection that a failed experiment does not roll the project backward too far.

## Highest-Priority Ideas

### Small, Safe Experimental Iteration

Agile development should grow software step by step. Each step should be small enough to test, understand, and reverse if needed.

The "rolling complexity uphill" metaphor is important:

- Software complexity grows as the project grows.
- Tests, checks, and automation act as backstops.
- Without backstops, the system can turn into a "big ball of mud."
- Teams should avoid pushing so far in one step that the project can roll back and crush them.

In exam language: Agile is not just "move fast." It is "move in small, protected steps with feedback."

### Build Pipeline

A build pipeline is the automated or semi-automated process that turns source work into a checked, usable build.

It may include:

- Unit testing
- Code metrics
- Style enforcement
- Linting
- Formatting
- Optimization
- Building and merging
- Documentation generation
- Deployment or delivery steps

A build pipeline supports Agile because it makes small experiments safer and faster. It gives the team feedback before changes become expensive.

The pipeline is not one-size-fits-all. It should be contextual and grow incrementally with the project.

## CI and CD

### CI: Continuous Integration

CI means constantly being able to integrate and test software into a workable build for testing and use.

Typical CI steps include:

- Unit tests
- Linting
- Formatting
- Optimization
- Building or merging
- Documentation generation

CI is mostly about validating that the system still works internally.

### CD: Continuous Delivery

CD means taking an automatically produced build and getting it out into production use quickly.

CD is higher risk than CI because it can affect real users. CI usually produces internal confidence; CD moves work toward users.

Important nuance: frequent release is not automatically correct. Release frequency depends on project context and risk tolerance.

## Small Experiments

Small experiments help teams:

- Learn quickly
- Reduce rollback cost
- Identify failures earlier
- Avoid "rocket launch" commits
- Keep the system understandable

Avoid large bursts of code that are hard to test, hard to review, and hard to reverse.

## Feature Flags

CI/CD is not the only way to experiment. Feature flags or feature toggles let teams introduce new functionality while hiding it behind a condition.

Feature flag idea:

- Add a feature to the system.
- Hide it behind a flag or if-then condition.
- Show it only to a small subset of users.
- Observe stability and acceptance.

Risk: feature flags can still hurt users if the feature is dangerous or exposed too broadly. A small experiment must still be safe.

## Incrementalism and Automation

"Feel the hate before you automate" means you should understand a manual pain point before automating it.

Do not build a complex pipeline too early just because it seems professional. That can become YAGNI: "You Ain't Gonna Need It."

Better approach:

- Start with a few useful steps.
- Notice repeated pain.
- Automate what clearly helps.
- Grow the pipeline as the project grows.

## Likely Exam Questions and Answer Frames

### 1. Why is a build pipeline central to Agile?

A build pipeline gives fast feedback. Agile depends on iteration, and iteration is only safe if the team can quickly test, verify, and recover from small changes.

### 2. Compare CI and CD.

CI focuses on integrating and testing code into a workable build. CD focuses on moving a build toward production or real users. CD is riskier because it affects end users more directly.

### 3. Why are small experiments better than "rocket launch" commits?

Small changes are easier to test, review, debug, and roll back. Large commits hide many risks at once and make failure more expensive.

### 4. Explain the rolling complexity uphill metaphor.

The growing codebase is like a heavy bundle being pushed uphill. Tests, automation, and quality checks are backstops that keep failures from rolling the whole project backward.

### 5. When should a team automate?

A team should automate after it understands the task and feels the repeated pain. Premature automation can create unnecessary complexity.

## Quick Review

- Agile requires fast, safe iteration.
- Safe iteration requires a build pipeline.
- CI validates integration and build quality.
- CD delivers builds outward and carries more user-facing risk.
- Feature flags are another form of controlled experimentation.
- Grow automation incrementally.
- Keep experiments small and reversible.

