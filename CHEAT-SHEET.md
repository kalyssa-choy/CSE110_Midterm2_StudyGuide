# CSE 110 Midterm 2 — One-Page Cheat Sheet

*Last-night rapid review. Every pattern → what it decouples → the smell it kills → the
one "gotcha" the lesson plants.*

---

## The 14 Patterns

| # | Pattern | Decouples / what can change independently | Smell it kills | ⚠️ Lesson gotcha |
|---|---|---|---|---|
| 01 | **Pub/Sub** | Publisher ↔ subscriber (no direct refs; events) | A directly calling B's methods | `composed: true` to **escape shadow DOM**; `bubbles: true` to go up; **remove listener** in `disconnectedCallback` |
| 02 | **Event Delegation** | Parent handles many children's events | A listener on every child; re-bind on render | One listener on **parent**; `event.target.closest()`; works for **dynamically added** children |
| 03 | **Notifications Hub** | Hub ↔ each publisher (routes by `detail.source`) | Parent querying child internals | Hub reads **only `event.detail`**, never child DOM; `.bind(this)` for a stable ref |
| 04 | **Components / Decomposition** | logic / template / styles / i18n in separate files | One giant mixed component file | Over-decomposition = more files; **clean up observers/listeners** in `disconnectedCallback` |
| 05/06 | **MVC** | Model (data) ↔ View (UI) ↔ Controller (bridge) | UI mutating state; logic in DOM handlers | **Model extends `EventTarget`**, never touches DOM; View fires `intent`, knows nothing of Model; **Controller** knows both |
| 07 | **Strategy** | Behavior swapped at runtime | Giant `if/else`/`switch` per mode | Shared signature **`(a,b)=>number`** = swappable; lookup `strategies[key] ?? default` |
| 08 | **Dependency Injection** | Component ↔ concrete backend (inject interface) | Hardcoded `localStorage` everywhere | Depend on interface (`save/load/getName`); factory `options={}` = **elastic/"trap door"**; **bug**: don't re-add listeners every `render()` |
| 09 | **Sortable-Storable** | sort axis ⟂ storage axis (independent) | Sort & storage tangled together | Two `observedAttributes`; swap storage = **no migration** (documented choice) |
| 10 | **State Machine** | State transitions explicit in a table | Boolean soup (`isLoading && isSuccess`) | **One** state at a time; invalid transition = **no-op + warn**; gate async on accepted transition |
| 11 | **Robustness** | Failure handling isolated | Unhandled rejections; "something broke" | Check **`res.ok`** (fetch only rejects on network); **`AbortController`** > `Promise.race`; typed errors; `isConnected` guard; `window.error` + `unhandledrejection` = last line |
| 12 | **Stateful Form** | UI state ↔ async submit | State scattered in conditionals | **Persistent `aria-live`** (don't recreate it); `_submit` owns its `try/catch` → no unhandled rejection |
| 13 | **CRUD facade** | Component ↔ backend (service layer) | `fetch` scattered through UI | All methods **async** (memory↔REST same interface); **optimistic update → reconcile w/ `serverTask` → revert on error**; `_pendingIds` blocks races |
| 14 | **Routing** | URL ↔ active view (hash = source of truth) | Nav state hidden from URL | Back/forward **free**; router **owns the hash** → in-page `#anchor` links collide; guard double-start |

---

## Architecture principles (one-liners)

- **High cohesion** (related stuff together) + **loose coupling** (few dependencies between parts).
- **SRP** = one responsibility per part. **Separation of Concerns** = logic/markup/style/data split.
- **DRY** = one source of truth (kills duplication). **Orthogonality** = parts don't interfere (kills *interdependence*).
- **Encapsulation / data hiding** = `#private` fields; hand out **copies** (`[...arr]`), not internals.
- **Abstraction** = hide details so code changes without breaking unrelated code. Don't over-generalize.
- **DI / IoC** = receive dependencies / framework calls *your* code. Risk: "loss of control" if you don't understand it.
- **Minimalism / KISS / YAGNI** = less code = fewer bugs; don't build it before you need it.
- **"Appropriate," not "correct."** **"It depends."** Fight **solution-first thinking**.

---

## Web platform gotchas

- **`composed: true`** = event escapes shadow DOM; **`bubbles: true`** = travels up. Light DOM (`innerHTML`, no `attachShadow`) needs only `bubbles`.
- **Shadow DOM** for *widgets* (scoped styles); **light DOM** for *page views* (inherit global CSS).
- **`bind()` trap:** `addEventListener('x', fn.bind(this))` then `removeEventListener('x', fn)` removes **nothing** (different ref) → leak. Save one bound ref.
- **Full re-render** (`innerHTML = …`) = simple + correct but **loses keyboard focus** → usability/a11y.
- **`escapeAttr` / never trust input** → XSS golden rule: distrust all inputs *and* outputs.
- **Optimistic UI:** apply locally → await → reconcile with server response → revert on failure.
- **`||` vs `??`:** `||` falls through on `""`/0 (good for defaults); `??` only on `null`/`undefined`.
- Clean up in **`disconnectedCallback`**: listeners, timers (`clearTimeout`/`clearInterval`), `MutationObserver.disconnect()`.

## REST / CRUD
- **C**reate→`POST`, **R**ead→`GET`, **U**pdate→`PUT`/`PATCH`, **D**elete→`DELETE`. **URLs = nouns, methods = verbs.**
- **Client-server**: client (browser, untrusted, variable) · server (controlled, securable) · **network** (variable!).
- **Localhost Effect** = local dev hides real network latency/failure → build defensively.
- **MPA** = full page loads; **SPA** = one page, JS swaps views (fast, but fails w/o JS). **Graceful degradation** (fail usefully) vs **progressive enhancement** (baseline works, layer JS on top).

---

## Agile ↔ tooling
- **CI** = integrate/test into a working build (internal). **CD** = deliver to users (riskier). Big deal for Agile because **small safe reversible steps** need fast feedback (avoid the "big ball of mud").
- **Pull requests** = quality gate before `main`; catch design/bugs/missing tests; **large PRs → weak "lgtm" reviews**.
- **Build pipeline** (fast→slow): lint/format → unit tests → build/merge → integration/E2E → docs → optimize → deploy.
- **Feature flags/toggles** = ship work hidden behind a condition → trunk-based, A/B testing; failed experiment = flag flip.
- **A/B testing** = compare variants; risk: more clicks ≠ love (metrics hide intent).
- **Merge conflict** = two branches edit same lines; the merging PR resolves it; small frequent merges hurt less.
- Docs: **ADR** = *why* we chose this (hard-to-reverse decisions). **JSDoc** = generate docs from code → fights staleness.

## Testing & quality
- **Pyramid**: many fast **unit** → fewer **integration** → few slow **E2E** → **acceptance** (final boss). Becomes a **"polygon"**: mix by **risk**, not checkbox.
- **TDD** = **Red** (failing test) → **Green** (pass) → **Refactor**. Slow to start; matters more vs LLM code (verification boundary).
- **BDD** = Given/When/Then tied to user behavior.
- **Coverage**: executed ≠ well-tested (can run a line without asserting).
- **STRIDE**: Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Escalation of privilege.
- **Pure functions** (`strategies.byNameAsc`, `next(state,event)`) = easiest to unit-test; DOM = slow/fragile.

## Operating & evolving
- **DevOps = culture** (joins dev+ops, breaks silos). **CI/CD = tech**. Not the same thing.
- **100% uptime is a passing moment, not a state.** Each "nine" costs non-linearly. 99.9% ≈ 8.76 hr/yr down.
- **`200 OK` ≠ healthy** (error pages return 200) → check content / diagnostic route.
- **Synthetic checks** (bots, repeatable) vs **RUM** (real users, real conditions, privacy risk).
- **Logs**: essential but risky (huge, PII, attackers delete them). **Status page off the failing infra.**
- **"No complaints ≠ correct"** (users silently leave). Software is a **garden, not a building**.

---

## The 8 ISO "-ilities"
**Functional suitability · Performance efficiency · Compatibility · Usability · Reliability · Security · Maintainability · Portability.**
(Pick the one(s) a code/design choice affects, name the risk, give a verification + a fix.)

## GenAI angles (likely reasoning Qs)
- AI **relocates/preserves** difficulty — hardcoding `localStorage` or omitting `disconnectedCallback` *looks* fine in a demo but is **tech debt**; the difficulty moved to **reviewers + future maintainers + users**.
- AI shifts effort from **writing** code → **reviewing/verifying/owning** it. "More code = more bugs" (E=MC²), so favor **readable** code; critical reasoning + trade-off awareness is the human edge.
- TDD/BDD become *more* valuable: tests are the boundary you trust instead of plausible-looking generated code.

## Quick smell list
magic numbers · `var`/`==` · `http://` · no `res.ok` · `innerHTML` w/ user data (XSS) · object into `localStorage` w/o `JSON.stringify` · `setInterval` never cleared · `parseInt` no radix · `<div onclick>` (use `<button>`) · `<div class="nav">` (use `<nav>`) · missing `alt`/`<label>` · placeholder-as-label · `!important` · table-for-layout · `<font>` · "click here" links · listeners re-added every render · bind-reference leak.
