# Operating and Evolving Software Study Guide

Source: https://tpowell.craft.me/xoCX6L2EDAq7kN

## Core Premise

After software is created and released, it evolves until eventual retirement. Operating software is different from building software because it happens in contact with real users, real infrastructure, real failures, and real organizational limits.

Traditional software operations were often handled by specialized operations teams. Modern DevOps puts more operational responsibility into the development team's world.

Operational work includes:

- Observability
- Remediation
- Testing
- Iteration
- Logs
- Analytics
- Monitoring
- Incident response

Mature software becomes a living system that grows and changes over time.

## DevOps

### Ops Is Not Separate Anymore

Historically, administrators wanted stability and developers wanted or needed change. This created a divide:

- Admins wanted stable systems with little change.
- Developers wanted to evolve the system.

DevOps grew to close this gap. Developers understand the software they built, so they need a heavier hand in running and observing it.

### DevOps Is Not CI/CD

DevOps is cultural. It joins the creation and operation of software and breaks down organizational silos.

CI/CD is technical. It focuses on building, integrating, and delivering software reliably and quickly.

Important warning: some organizations misuse DevOps as a way to make developers do more work with fewer resources.

## The Engineering Insanity of Perfect Availability

Availability is often used to measure reliability for network-delivered software.

Many organizations talk about "five nines" or even 100% uptime. The key idea is that 100% uptime is not a stable state. It is only a passing moment.

Things eventually break:

- Hardware fails.
- Networks fail.
- Routers get misconfigured.
- Connections are severed.
- Software bugs surface.
- Strange rare events happen.

Engineering mindset: aspire to reliability, but accept that some problems are inevitable.

### Availability Numbers

- 99% availability = 3.65 days downtime per year, about 7 hours per month.
- 99.9% availability = 8.76 hours downtime per year, about 43 minutes per month.
- 99.99% availability = 52.6 minutes downtime per year, about 4 minutes per month.
- 99.999% availability = 5.26 minutes downtime per year, about 25 seconds per month.

Each extra nine requires much more investment.

High availability requires:

- Redundancy at every layer
- Sophisticated monitoring and alerting
- Automated recovery systems
- Chaos engineering
- On-call rotations
- Incident response

Marked idea: chaos engineering deliberately breaks things in production to test resilience.

Big analysis point:

The question is not "How do we achieve perfect uptime?" The better question is "What level of availability serves user needs while remaining economically sustainable?"

That answer requires realistic risk assessment and reveals organizational values.

## Logging

Logs are necessary for running software, even though teams often dislike dealing with them.

Logs should contain enough information to understand what happened during a time period or incident.

Challenges:

- Logs can create cognitive load.
- Logs can become huge.
- Logs may need rotation, offloading, rollups, or deletion.
- Logs can contain sensitive information.
- Intruders may try to delete logs.
- PII in logs creates privacy and security risk.

Log format has two dimensions:

- Data format: standard or custom structure.
- Tech format: TSV, CSV, JSON, and so on.

Tactical logging questions:

- What should be logged?
- At what granularity?
- Where will logs be stored?
- How long will logs be kept?
- How will logs be searched or displayed?
- How will the logging system itself be monitored?

## Monitoring and Verification

Monitoring is like continuous verification. It happens after release and is usually less complete than testing, but it runs continuously.

Monitoring should come from requirements and project risks.

Possible monitoring targets:

- Availability: is the app reachable and functioning?
- Performance: is it fast enough?
- Accessibility: contrast, keyboard support, and related checks
- Compatibility: browsers, devices, JS errors, environments
- Functionality: lightweight E2E execution of core tasks
- Usability: rage clicks, time on page, confusing flows
- User acceptance: outcomes, feedback forms, analytics
- Security: project-specific checks

There is no universal monitoring solution. Monitoring should reflect user and organizational needs.

## Monitoring Practices

### Simple Access Checks

Synthetic access checks ask whether a site or app is reachable.

Warning: surface checks can give false comfort.

A site may return `200 OK` and still be broken. Error pages can sometimes return successful HTTP status codes.

Better checks:

- Fetch pages and look for expected strings or assets.
- Fetch a diagnostic route.
- Monitor the diagnostic route too.

Open questions:

- How often should checks run?
- Should checks run from multiple locations?
- Where should checks run from based on users?

Fast checks catch downtime sooner but can create false positives and cost more.

### Scripted Scenario Checks

Scripted scenario checks are synthetic monitoring similar to E2E testing.

They perform real workflows:

- Click through pages
- Fill out forms
- Submit tasks
- Complete core user actions

Use real browsers where possible because fake browsers are not what real users use.

Tradeoff: these checks are useful but can be fragile and slow.

### Real User Monitoring

RUM means real user monitoring.

Instead of observing a test bot, RUM observes actual users under actual conditions.

Common RUM signals:

- Performance data
- Navigation timing
- JavaScript errors
- Console output
- Crash dumps
- Full session/event replay

Danger: detailed user monitoring can become invasive. Balance observability with privacy.

### Monitor the Full Stack

Monitor both frontend and backend holistically.

A frontend symptom may actually be caused by a backend problem. Over-architected systems can make monitoring harder because failure sources multiply.

## Analytics and Software Improvement

Analytics help teams move toward data-driven decision-making.

Operational data can include:

- Availability
- Performance
- Usage patterns
- User behaviors
- User satisfaction
- Software value
- Feedback

Analytics can reveal skipped or weak user-centered design work. If KPIs feel slapped onto the software after the fact, the team may not have designed around user value properly.

Analytics types:

- Basic usage: trends, Google Analytics, log files
- Advanced usage: flows, heatmaps, replay analytics
- Simple feedback: thumbs up/down
- Surveys and free-form feedback
- Solicited and unsolicited user feedback

## Analytics-Driven Iteration

Analytics can suggest changes, but the team must:

1. Formulate a change.
2. Implement it.
3. Track the result.

Common methods:

- A/B testing
- Feature flags
- Beta or pre-release mechanisms
- Dogfooding
- Trusted partner testing

Warning: mind the testing effect. Users may behave differently when they know they are being tested.

## Danger of Analytics-Driven Design

Analytics do not always reveal user intention.

Numeric simplifications can mislead teams.

Example: more clicking may look like engagement, but it may really mean the UI is confusing or manipulative.

Do not blindly chase metrics.

## Users Not Complaining Does Not Mean Software Is Correct

Highlighted idea:

Just because users do not complain does not mean the software is correct.

Reasons:

- Users may not have time to complain.
- Users may not care enough to report the problem.
- Users may silently leave.
- One complaint might be unreasonable.
- One complaint might also be the tip of the iceberg.

Engineering judgment is required. Do not satisfy every complaint blindly, but do not dismiss complaints automatically.

## Incidents, Remediation, and Iteration

Once monitoring reveals a problem, teams need to respond. Not everything can have the same priority.

Priority examples:

- Availability or major functionality break: big emergency.
- Performance degradation: mid-level emergency.
- Accessibility, usability, or acceptance issue: variable emergency depending on impact and organizational priorities.

High priority response may include:

- On-call scheduling
- ChatOps
- Status pages
- Social media updates
- Incident communication

Important: status pages should not be hosted on the same infrastructure that is failing.

Lower priority issues may go into a sprint or backlog.

Bold closing idea:

Operating software correctly turns software into a garden, not a building. You tend it over time: observe, prune, plant, adjust, and improve.

## Analysis Questions and Answer Frames

No explicit "Example Questions" section appeared in this chapter, so these are study questions built from the bold and marked concepts.

### 1. Explain why DevOps is not the same thing as CI/CD.

DevOps is a cultural approach that connects development and operations and breaks down silos. CI/CD is a technical practice focused on building, integrating, and delivering software reliably and quickly.

### 2. Why is perfect uptime an unrealistic engineering goal?

Complex systems eventually fail because hardware, networks, software, configuration, and human processes all have failure modes. Perfect uptime is a passing moment, not a permanent state.

### 3. What does each extra "nine" of availability cost?

Each extra nine reduces allowed downtime but requires far more investment in redundancy, monitoring, alerting, automated recovery, incident response, and operational discipline. The cost grows non-linearly.

### 4. Why are logs important, and why are they dangerous?

Logs help teams understand incidents and system behavior. They are dangerous because they can grow huge, create cognitive load, expose PII, and become targets for attackers who want to hide evidence.

### 5. Why can a simple `200 OK` access check be misleading?

A site can respond successfully while the actual app is broken. For example, an error page might still return `200 OK`. Better checks should inspect expected content, assets, diagnostics, or user workflows.

### 6. Compare synthetic monitoring and real user monitoring.

Synthetic monitoring uses scripted checks or bots. It is controlled and repeatable but may miss real user conditions. Real user monitoring observes actual user sessions and environments, but it can raise privacy concerns.

### 7. Why can analytics-driven design go wrong?

Metrics can hide intention. More clicks may mean engagement, but they may also mean confusion. Analytics need interpretation and user-centered judgment.

### 8. Why does "no complaints" not prove software is good?

Users may silently leave, lack time to complain, or not know how to report problems. Complaints have friction, so silence is not strong evidence of correctness.

### 9. Explain the garden metaphor for operating software.

A building is constructed and left alone, but software is more like a garden. It grows, changes, breaks, accumulates problems, and needs ongoing care through monitoring, remediation, and iteration.

## Quick Review

- Operating software is ongoing work after release.
- DevOps is cultural; CI/CD is technical.
- Perfect uptime is not permanent.
- Each availability nine costs much more.
- Logs are essential but risky.
- Monitoring should come from requirements and risk.
- Synthetic checks and RUM answer different questions.
- Analytics help, but can mislead.
- No complaints does not mean no problems.
- Software should be tended like a garden.

