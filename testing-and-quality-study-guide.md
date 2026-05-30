# Testing and Quality Study Guide

Source: https://houses-pay-526.craft.me/N0Y0koqTnNUNX3

## Core Premise

Software engineering should create an environment where teams can produce high-quality software that meets owner and user needs in a repeatable and efficient way.

Testing is the primary tool for checking whether software does what we think it should do. However, Agile's "release early and often" mindset can become reckless if teams use it as an excuse to push low-quality work and let users discover problems after release.

Key idea: testing is not a side activity. It is central to quality culture and engineering maturity.

## Quality and Testing Mindset

Testing starts with mindset. You need to think about what could go wrong, not only what should happen when everything goes right.

The marked idea from the notes:

- Some teams treat testing as too little of a priority.
- Other teams try to test every possible case and become paralyzed.
- The practical goal is proportional testing.
- Testing effort should match project risk.
- A life-critical system deserves far more testing than a small casual game feature.
- Risk should be clearly communicated between business owners and developers.

Rushed code without quality tends to create technical debt or failures eventually.

## More Software Means More Bugs

Simple Law of Bugs:

`E = MC^2`

Errors equal more code squared. This is a silly memory trick, but the point is serious: more code and more complexity usually mean more bugs.

"More" does not only mean lines of code. It can also mean:

- More dependencies
- More tools
- More services
- More configuration
- More integration points

Minimalism matters because every added piece increases the surface area for failure.

## Dependencies Require Caution

Using existing code is reasonable, especially in complex software. The danger is choosing dependencies mostly by weak signals like popularity, GitHub stars, or search results.

Important dependency principles:

- A dependency becomes part of your system.
- You are responsible for the risk it introduces.
- Dependencies have dependencies.
- External code can create fragility, conflicts, circular references, and instability.
- Wrap dependencies with an abstraction or insulation layer when possible so you can replace them later.

Do not confuse popularity with engineering quality.

## Software Perfection Is Fleeting

Software is rarely perfect unless it is trivial and conditions never change.

Software systems are organic. They live in changing environments with changing users, changing dependencies, changing infrastructure, and changing expectations.

Even if a system seems perfect now, that state probably will not last.

Engineering mindset: accept that software will degrade, break, and change. Plan for that reality instead of pretending perfection is permanent.

## Testing Mantras

Know these and be able to explain them:

- TETO: Test Early, Test Often
- ABT: Always Be Testing
- TFS: Test the Full Stack
- Eat your own dogfood: use your own software
- Production code is still under test
- Users are the ultimate test

## The Testing Pyramid and Testing Polygon

The testing pyramid says teams should have many small, fast tests at the base and fewer slow, broad tests near the top.

Typical interpretation:

- Many unit tests
- Fewer integration tests
- Fewer end-to-end or interface tests
- Some user acceptance tests

Why the pyramid shape exists:

- Small tests are faster.
- Small tests are cheaper.
- Small tests are easier to run often.
- Large tests are slower, more fragile, and harder to maintain.

Why the pyramid may become a "testing polygon":

The right mix depends on the software, risks, organization, and project goals. Some projects may need more security tests, browser tests, load tests, pixel tests, compatibility tests, or acceptance tests.

Do not use checkbox thinking. Pick tests based on risk.

## Test Throughout the Process

Testing should happen at every stage, not just at the end.

Software activities include defining, coding, testing, releasing, observing, and improving. Quality checks belong throughout the process.

## Quality Control Before Commit

Before adding code to the repository, review your own work.

Before commit, you should:

- Read your code
- Run local unit tests
- Use an IDE linter
- Use style checking
- Use formatting checks
- Consider pre-commit hooks

You may still need more checks after commit, but developer-local checking catches problems earlier.

## Quality Control Through Code Review

After code is committed to a branch, it should be evaluated before merging into the main trunk.

Review can be:

- Automated: Code Climate, complexity scoring, linters, metrics
- Manual: pull requests, human review, team review

Automated review is useful but can make people "code to the grade."

Manual review is valuable but socially hard. People may dislike criticism, and weak reviews often become empty "lgtm" approvals.

## Quality Control Before Release

Before release, run the complete test suite from fast tests to slower tests.

Good CI/CD test ordering:

1. Fast checks first
2. Slower checks later
3. Broad tests before release

Testing before release may include:

- Unit tests
- Integration tests
- End-to-end tests
- Interface-level tests
- Browser/device tests
- Beta or staging release checks

Beta releases, staging environments, feature flags, and limited rollouts reduce risk by exposing software to a smaller audience before full release.

## Quality Control After Release: Observability

Released software still has flaws. After release, quality depends on observability.

Observability includes:

- Exception handling
- Try/catch behavior
- Useful error messages
- Analytics
- Monitoring
- Logs
- Production feedback

Observability moves some quality work from pre-release testing into operational monitoring. This can be reasonable for some software and dangerous for others.

## TDD: Test Driven Development

TDD means writing tests before writing the code.

The three TDD phases:

1. Red: write tests that fail.
2. Green: write code that makes tests pass.
3. Refactor: improve the code while keeping tests green.

TDD is slow but can produce better code. It has startup costs and requires skill. It may become more important with LLM/AI code generation because generated code needs strong verification.

Alternative: test near code or test close to code. Write tests very quickly after the code and do not move forward until that step is verified.

## BDD: Behavior Driven Development

BDD tries to connect tests to user stories and user behavior.

TDD can become too code-focused. BDD addresses the missing question: does the software support the user behavior we actually care about?

BDD is less common than TDD, but the intention is valuable: keep user-centered thinking connected to testing.

## Security Testing

Golden Rule of Web Dev Security:

You cannot trust users or their intentions, so trust no data inputs or resulting outputs.

Watch all inputs:

- Expected 3 values but got more or fewer? Worry.
- Expected a number but got a string? Worry.
- Expired cookie appears again? Worry.
- Lots of 404s from one IP? Worry.
- Anything unexpected? Worry.

STRIDE security categories:

- Spoofed identity: authentication problems or stolen accounts
- Tampering input: malicious or unexpected data
- Repudiation: lack of audit trail or logs
- Information disclosure: leaking information unintentionally
- Denial of service: traffic or requests overwhelm the system
- Escalation of privilege: users gain abilities they should not have

## Project-Specific Testing

Testing depends on the project form and important "-ilities."

Examples:

- Browser testing: important for web projects because browser versions change.
- Load testing: checks when performance degrades or fails under traffic.
- Security testing: checks abuse and attack paths.
- Pixel/snapshot testing: catches visual regressions.
- Chaos testing: intentionally breaks things to test resilience.

TL;DR: different projects need different test mixes.

## Final Boss: Acceptance Testing

Acceptance testing asks whether users accept the delivered software.

This is the most important test because software can be technically correct and still fail if users reject it.

Marked idea:

To reduce acceptance risk, get software to users as early as possible. This supports "Interface First" thinking. If users do not accept the interface or workflow, the project carries major risk.

Acceptance can be explored through:

- Alpha testing
- Beta testing
- Feature flags
- Limited releases
- Analytics
- User feedback

Acceptance is subjective. UI style, brand, reputation, expectations, and social beliefs can affect it.

## Example Questions and Answer Frames

### 1. Explain the testing pyramid and why it may become a testing polygon.

The pyramid favors many fast, focused unit tests at the bottom and fewer slower broad tests near the top. It may become a polygon because different projects have different risks. A web app may need browser and E2E testing; a high-traffic app may need load testing; a security-sensitive app may need security testing.

### 2. What is code coverage, and why is it both useful and limited?

Code coverage measures how much code is executed by tests. It is useful because it reveals untested areas. It is limited because executed code is not necessarily well-tested code. A test can run a function without checking meaningful behavior or edge cases.

Counterexample: a test might call `validateEmail("x")` and increase coverage, but never check valid emails, empty input, malicious input, or expected error messages.

### 3. Improve an HTML form field and list 5 distinct tests.

Possible improvements:

- Use the correct input type.
- Add `required`.
- Add `maxlength`.
- Add `pattern` if appropriate.
- Add a label.
- Add useful error messages.

Five test types:

- Valid input
- Empty input
- Wrong type or format
- Boundary length
- Malicious or unexpected input

### 4. Define common testing types.

- Unit testing: tests one function/class/component in isolation.
- Integration testing: tests pieces working together.
- End-to-end testing: tests a full user workflow.
- Load testing: tests behavior under traffic or stress.
- Snapshot/pixel testing: tests visual output changes.
- Compatibility testing: tests across browsers/devices/environments.
- User acceptance testing: checks whether users accept the delivered software.

Hardest to automate: user acceptance testing, because it depends on human perception and subjective value.

### 5. Write the three steps of TDD and explain why TDD matters with LLM code generation.

Red, Green, Refactor.

TDD matters with LLM code generation because generated code can look correct while being wrong. Tests create a verification boundary before trusting generated implementation.

### 6. Define BDD and why it matters.

BDD connects tests to user behavior and user stories. It matters because code quality alone does not guarantee user success. BDD pushes teams to test outcomes users actually care about.

### 7. If user acceptance is the most important test, how can we reduce the risk of discovering failure too late?

Get interfaces and workflows in front of users early. Use prototypes, interface-first development, alpha/beta testing, feature flags, analytics, and feedback loops before full release.

## Quick Review

- Testing should be proportional to risk.
- More code and complexity usually mean more bugs.
- Dependencies become part of your system.
- Software perfection is temporary.
- Test early, often, and across the full stack.
- The right test mix depends on project risk.
- TDD is Red, Green, Refactor.
- BDD ties tests to user behavior.
- Security testing starts with distrust of all input.
- User acceptance is the final boss.

