# Building and Deving Part 2 Study Guide

Source: https://tpowell.craft.me/WJ7bDhvyPDO0T0

## Core Premise

Software is much greater than code, but code still needs care. Teams should keep workspaces clean, use consistent standards, and understand the intentions behind practices instead of treating them as dogma.

The most important distinction:

Working code is not automatically good code.

Good software also depends on team knowledge, documentation, organization, consistency, maintainability, and thoughtful tool use.

## Highest-Priority Ideas

### Software Is Greater Than Code

Software includes:

- Code
- Design documents
- Diagrams
- User stories
- Meeting notes
- Presentations
- Messages
- Tests
- Documentation
- Team knowledge

Code may be a large part of software, but the human product matters too. The team itself, and what the team knows, can be the real outcome of a software project.

Stable teams, retained knowledge, and disciplined habits strongly affect project success.

### Avoid Spreading

Project knowledge often spreads across issue trackers, diagramming tools, wikis, Google Drive, Slack, email, and people's heads.

This creates risk because important knowledge becomes hard to find, hard to update, and easy to lose.

Course emphasis: keep things in the repo when possible. This may not always work in larger organizations, but the intent is to reduce knowledge scattering.

### Work From Your Plans

Plans should drive the code. Do not treat plans as stale side documents.

Important marked idea:

Plans are often not kept near code, so keep them in the repo if possible.

Plans also go out of sync with code, so keep them updated or link/generate them from the code. JSDoc is a useful model: comments near code can generate documentation.

### Teams Should Code As One

The repo should look like team code, not a pile of individual styles.

This requires:

- Shared ownership
- Shared coding values
- Common style guidelines
- Consistent naming
- Consistent formatting
- Agreement on tool practices

There is no one true way. Consistency matters more than proving your personal preference is perfect.

## Code Craft Principles

### Be Cautious of "True Ways"

There are many paths to successful software. Be suspicious of anyone claiming one tool, design, style, or architecture is the only correct way.

The best way is the one your team can use to build solid systems effectively.

### Just Be Consistent

If your team chooses camelCase, keep using camelCase. Do not randomly switch to snake_case or kebab-case.

Consistency lowers mental load.

### Neatness Counts

Clean up:

- Commented-out code
- Junk files
- Dead branches
- Repo clutter
- Unused files
- Inconsistent formatting

FIX, HACK, and TODO comments can be useful, but they can also become clutter if ignored.

### Favor Reading Over Writing

Code is read more often than it is written.

Simple, slightly longer code may be better than clever, compact code. A plain function or loop can be easier to maintain than a short but confusing expression.

### Keep It Simple

KISS: keep it super simple.

Less code often means fewer bugs, but do not compress code so much that it becomes brittle. There is no such thing as fully self-documenting code.

More comments and more tests are often good.

### Plan for the Future, Focus on the Present

Use stubs and abstractions where they make change easier.

Example idea:

Use `save_entry(oUser)` rather than directly tying code to `save_LocalStorage("user", oUser)`.

This makes it easier to swap storage providers later, such as memory, localStorage, IndexedDB, filesystem, remote endpoints, and so on.

### Always Be Cleaning

Highlighted idea:

To keep velocity up and reduce chaos, clean as you go. If you do not, technical debt is guaranteed to grow.

Treat the repo, code, and docs like a garden that degrades without upkeep.

## Repo and Team Practices

### Keep the Repo Clean

Avoid cruft such as `.DS_Store`, unnecessary generated files, and accidental dependencies.

Use `.gitignore`.

Think carefully about whether dependencies like `node_modules` belong in the repo. Usually no, but understand dependency risks and package locking.

### Catch Problems Early

Use:

- Editor config files
- Linters
- Formatters
- Pre-commit hooks
- CI checks

It is easier to fix issues before they enter the repo.

### Prune Branches

Branches are useful, but dead branches should not pile up.

Possible branch strategy:

- main
- stage
- dev
- feature branches

Clean up work before the end.

### Do Not Let Issues Pile Up

Too many issues violates Agile's goal of limiting WIP: Work In Progress.

Huge backlogs can demotivate teams and users.

### Write Useful Commit Messages

Bad: `Small fixes`

Better: `[ Bug ] Added data sanitization to configuration screen #3455`

Good commit messages support changelog generation and project understanding.

### Actually Evaluate Pull Requests

Bad: `lgtm`

Better: Give specific review feedback about design, clarity, customer issues, complexity, or maintainability.

Large submissions often lead to weak review. Smaller submissions make better feedback possible.

## Web Technology Review

### HTML

Use consistent style:

- Lowercase elements and attributes
- Double quoted attributes
- Consistent empty element style

Validate markup:

- Use https://validator.w3.org
- Consider HTML validator GitHub Actions

Use semantic markup:

- Prefer `<nav>` over `<div class="nav">`
- Prefer real HTML elements before recreating behavior with JavaScript
- Semantic HTML improves accessibility by default

Explore HTML deeply:

- HTML has many useful elements.
- Avoid making everything a `<div>`.
- Elements like `<dialog>` and `<details>` can reduce unnecessary JavaScript.

Use custom elements and data attributes when appropriate:

- `<product-card>`
- `<li data-profile-id="3443cad4">`

Format for development, minify for deployment.

### Links

Remember URL case behavior:

- Protocol: case insensitive
- Domain: case insensitive
- Path: may be case sensitive
- File name: may be case sensitive
- Query string: may be case sensitive depending on implementation

Link guidance:

- Avoid "click here."
- Use meaningful link text.
- Keep URLs human-readable.
- Be cautious with shorteners.
- Keep URLs stable.
- Check links manually and automatically.

### Forms

Use the proper input type:

- `text`
- `email`
- `number`
- checkbox
- select/dropdown

Use validation and state attributes:

- `required`
- `maxlength`
- `pattern`
- `readonly`
- `disabled`

Support keyboard use:

- `tabindex`
- `autofocus`
- `autocomplete`
- `accesskey`

Validate client-side for UX and server-side for security. Client-side validation can be bypassed.

### Images

Ask whether the image is needed. Some images can be replaced by CSS.

Choose format by purpose:

- Logo or drawing: SVG
- Photo: JPEG, WebP, or AVIF

Optimize images:

- Use tools like TinyJPG
- Automate optimization in CI/CD

Use responsive delivery:

- `<picture>`
- `srcset`
- content negotiation

Accessibility:

- Use `alt` attributes.
- Watch color contrast, especially when the image contains content.

### CSS

Avoid class-itis. Use modern CSS features, especially in constrained environments.

Do not load a whole framework for a tiny task like centering something.

Use devtools coverage to see unused CSS.

Minify for deployment.

### JavaScript

Learn core language quirks:

- Types
- Closures
- OOP
- Async

Understand what the web platform gives you for free before simulating it with libraries.

Adopt third-party code carefully:

- Do not choose only by popularity.
- Understand dependencies of dependencies.
- Evaluate in proportion to risk.
- Go beyond Hello World.
- Once included, that code becomes your responsibility.

Use style guides thoughtfully. A common guide like Airbnb can be a starting point, but teams should understand and modify it as needed.

Consider TypeScript carefully:

- Try `// @ts-check` first.
- TypeScript has long-term cost.
- TypeScript does not replace runtime checks for user-supplied data.

Use linting:

- In the editor
- At check-in
- In CI

Use unit tests:

- Test functions and classes where appropriate.
- Cover common cases.
- Generate coverage reports.
- Write tests that can fail by exercising real edge cases.

Do not assume unit tests are enough. Add end-to-end tests, pixel capture tests, real browser tests, and real condition tests when appropriate.

Generate documentation from code using JSDoc-style comments.

## Project-Specific Advice

- Build the dev pipeline before significant coding.
- Avoid too much yak shaving.
- Do not over-engineer the pipeline early.
- Consider local-first or "worst that can happen" thinking.
- Account for unreliable, unavailable, or slow networks.
- Test offline behavior.
- Do not over-solve just because a pattern is common.
- Avoid excessive security for low-risk systems.
- Use your own application if possible.
- Ask for feedback from friends, other teams, TAs, the professor, and users.

## Example Questions and Answer Frames

### 1. Given that software is greater than code, name at least 3 important non-code parts of software.

Possible answers:

- Design documents
- Diagrams
- User stories
- Meeting notes
- Presentations
- Messages
- Documentation
- Tests
- Team knowledge

Strong answer: explain that these artifacts preserve intent, coordinate the team, and help future maintainers understand the system.

### 2. Argue for and against "best of breed" tools.

Argument for:

Best-of-breed tools may be excellent at one specific task. They can improve productivity, quality, and capability when chosen carefully.

Argument against:

Too many tools scatter project knowledge, increase onboarding cost, fragment team workflow, create integration problems, and make consistency harder.

Balanced answer:

Use tools when their value clearly exceeds their coordination cost. Prefer fewer tools when possible, especially for smaller teams.

### 3. Why do plans and diagrams go out of date, and how can the problem be reduced?

They go out of date because code changes faster than documentation. If plans live far away from code, teams forget to update them.

Solutions:

- Keep docs in the repo.
- Review docs during pull requests.
- Generate docs from code comments where possible.
- Use JSDoc-style comments to keep documentation near implementation.
- Link diagrams and plans to code or build outputs.

### 4. Why should a team stop arguing over perfect style decisions?

The perfect style is less important than a consistent shared style. Endless debate wastes time and prevents team alignment.

For non-conforming teammates:

- Use formatters.
- Use linters.
- Use editor config.
- Use pre-commit hooks.
- Add CI checks.
- Make the guideline automatic instead of personal.

## Quick Review

- Software is greater than code.
- Team knowledge matters.
- Keep plans near code.
- Make plans drive implementation.
- Code as one team.
- Consistency beats personal preference.
- Readability beats cleverness.
- Clean as you go or technical debt grows.
- Use tools wisely, not blindly.
- Working code is not automatically good code.

