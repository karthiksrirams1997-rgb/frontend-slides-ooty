# Frontend Slides Ooty

**Frontend Slides Ooty** is an agent skill for creating distinctive, animation-rich, zero-dependency HTML presentations. It is optimized for **hackathon pitches, demo-day judging, technical product demos, prototype showcases, and short time-boxed presentations**, while also supporting general talks, reports, and PPT/PPTX conversion.

The skill is designed for coding agents and agentic development environments, including **Claude Code, Claude-based coding agents, Manus, OpenAI Codex-style agents, Cursor agents, and other assistants that load `SKILL.md` or repository instructions**.

> The repository packages the skill instructions and reusable references. It does not include a generated presentation; agents use the skill to produce one for a specific project.

## What agents can do with this skill

- Create a complete single-file HTML presentation from a brief, notes, screenshots, or a prototype.
- Turn a working application into a persuasive hackathon demo-day deck.
- Convert a `.pptx` into a fixed-stage HTML deck while preserving slide order, text, images, and speaker notes.
- Generate three visual style previews before committing to a design direction.
- Build decks with a fixed 1920×1080 stage that scales uniformly on desktop and mobile.
- Include keyboard, touch, wheel, reduced-motion, inline-editing, local-save, and export behavior.
- Add demo fallback visuals so the pitch remains understandable when a live API, network, or product fails.
- Deploy a presentation to a live URL or export it to a static PDF using the bundled scripts.

## Installation and use

### For Manus

Add the skill through the skill attachment flow using [`SKILL.md`](SKILL.md). Once installed, requests mentioning hackathon slides, demo day, prototype pitches, judged builds, technical showcases, or product demos should activate the hackathon workflow automatically.

### For Claude Code or coding agents

Clone or copy this repository into the agent’s skills directory, or point the agent’s project instructions at the skill file:

```bash
git clone https://github.com/karthiksrirams1997-rgb/frontend-slides-ooty.git
```

Then instruct the agent to read `SKILL.md` before creating or modifying a presentation. A project-level instruction can say:

```text
For presentation tasks, read frontend-slides-ooty/SKILL.md first and follow its fixed-stage, style-discovery, hackathon, and verification workflows. Read supporting references only when the skill directs you to.
```

The skill is intentionally tool-agnostic. An agent may use its available browser, filesystem, image, rendering, or project tools, but it must preserve the output invariants in `SKILL.md`.

### Typical prompts

```text
Create an 8-slide, 5-minute hackathon pitch for our working AI prototype. Read the frontend-slides-ooty skill, ask only the missing intake questions, create three style previews, and include a screenshot fallback for the live demo.
```

```text
Turn this app into a demo-day deck for technical judges. Explain the user problem, product flow, architecture, differentiation, evidence, and next step. Keep it speaker-led and verify it at desktop and phone viewports.
```

```text
Convert pitch.pptx into an editable HTML presentation using frontend-slides-ooty. Preserve slide order, images, and notes, then redesign it for a three-minute judged prototype demo.
```

## Hackathon mode

The skill treats the following as strong activation signals: **hackathon presentation, hackathon pitch, demo day, judging deck, project showcase, prototype pitch, live product demo, technical showcase, time-boxed competition, pitch my project, present our prototype, judge our build, and make a deck for the competition**.

When the request is clearly a judged prototype or short demo pitch, the agent should activate hackathon mode even if the user does not use the word “hackathon.” The default is a **3–5 minute speaker-led pitch with 8–10 slides**, one complete demo flow, one concise architecture proof point, and a clear closing ask. Event rules and the supplied judging rubric always override these defaults.

## Detailed slide-planning method

Slide planning comes before visual polish. Agents should create a narrative and a time budget before generating HTML.

### 1. Collect the planning inputs

Ask for the smallest set of missing facts that can materially change the deck:

| Input | Why it matters |
|---|---|
| Event theme and judging rubric | Determines which proof and vocabulary deserve time |
| Pitch time, including or excluding demo | Sets the maximum story length and demo budget |
| Prototype status | Determines whether to use live interaction, screenshots, recording, or concept visuals |
| Target user and painful workflow | Keeps the problem concrete and user-centered |
| Technologies, APIs, models, and integrations | Identifies the one or two technical choices worth explaining |
| Evidence | Prevents unsupported claims and determines the proof slide |
| Desired final action | Shapes the closing slide and call to action |

If the user cannot provide all inputs, proceed with explicit assumptions instead of blocking. Never invent traction, benchmark results, customer counts, or impact metrics.

### 2. Translate the rubric into a story map

Create a private planning table or presenter-note map before writing slides:

| Judging criterion | Claim the deck should make | Proof or visual | Slide / speaking beat |
|---|---|---|---|
| Problem relevance | A real user is blocked by this workflow | User scenario, consequence, quote | Problem |
| Novelty | The approach is meaningfully different | Before/after or comparison | Differentiation |
| Technical execution | The team built a credible path | Architecture or implementation choice | Technical proof |
| Feasibility | The prototype can become a real product | Working flow, constraints, next step | Evidence / roadmap |
| Impact | The outcome matters | Verified metric, pilot, or intended benefit | Impact |

Every important criterion should map to at least one visible slide or speaking beat. Keep internal rubric labels in presenter notes or HTML comments unless the user explicitly wants them rendered.

### 3. Budget the speaking time

Use the event limit as a hard constraint. A practical five-minute starting budget is:

| Segment | Approximate share | Typical slides |
|---|---:|---|
| Hook and problem | 15% | Title, problem, why now |
| Solution and product flow | 25% | Solution, demo setup |
| Live demo | 30% | One complete user journey |
| Technical credibility | 15% | Architecture, key implementation choice |
| Evidence and close | 15% | Results, impact, ask |

For a pitch shorter than three minutes, use five core beats: hook/problem, solution, demo result, technical differentiator, and closing ask. For a longer pitch, add evidence, differentiation, impact, and appendix slides rather than making the main slides denser.

Estimate speaking time from the actual script or presenter notes. If a slide requires more explanation than the time budget allows, split the idea or remove it. A slide that is beautiful but cannot be explained clearly within the slot is not finished.

### 4. Choose the slide architecture

Use this as a flexible default, not a mandatory template:

1. **Title and promise:** project name, one-line value proposition, team, and event context.
2. **Problem:** one vivid user, workflow, or consequence.
3. **Why now / stakes:** urgency, affected audience, or cost of inaction.
4. **Solution:** what was built and how it changes the workflow.
5. **Demo setup:** what judges should watch for.
6. **Product flow:** input → key action → visible outcome.
7. **Technical proof:** the differentiating architecture or implementation choice.
8. **Evidence:** benchmark, pilot feedback, usage, demo result, or honest current status.
9. **Impact and roadmap:** who benefits and what comes next.
10. **Closing ask:** memorable takeaway, QR code, URL, repository, or requested next step.

Collapse the outline when the time limit is short. Expand it with appendix material when judges need deeper architecture, security, evaluation, or implementation detail.

### 5. Plan the demo and its fallback

The demo should show the shortest complete path, not every feature. Define:

- **Starting state:** what is already prepared before the presenter clicks.
- **User action:** the one interaction that demonstrates the product’s value.
- **Visible outcome:** the result judges must notice.
- **Proof point:** the metric, speed, quality, or behavior that makes the result credible.
- **Return point:** where the presenter returns to the deck after the demo.
- **Fallback:** screenshot sequence or static state for every mission-critical step.

Do not make the core story depend on a network request, an animation completing on time, an unavailable API, or a fragile external login. Label screenshots honestly; do not present a static fallback as live evidence.

### 6. Plan visual evidence, not decoration

For every slide, specify the dominant visual and its job:

- Product screenshot: prove the workflow or outcome.
- Architecture diagram: explain the differentiating path.
- Number or chart: show verified evidence.
- Comparison: establish differentiation.
- Quote or user scenario: make the problem memorable.
- Abstract CSS motif: establish atmosphere without pretending to be product proof.

Prefer one dominant visual with a clear caption over a collage of small cards. Keep technical labels readable at presentation distance.

### 7. Plan the closing before styling

Decide what judges should remember in one sentence. Then choose one closing action: try the product, scan a QR code, visit a URL, approve a pilot, support the next milestone, or remember the team. The closing slide should not introduce a new complex idea.

## Output invariants

Every generated presentation must:

- Use a single self-contained HTML file with inline CSS and JavaScript.
- Use a fixed 1920×1080 stage scaled uniformly to the viewport.
- Include the full contents of `references/viewport-base.css`.
- Use `.active` / `.visible` visibility states instead of display-based slide switching.
- Support reduced motion, keyboard navigation, touch/swipe navigation, and accessible semantics.
- Avoid overflow, overlap, unreadably small text, generic AI styling, and unsupported claims.
- Include inline editing by default unless the user explicitly requests a locked or export-only file.

## Repository layout

```text
frontend-slides-ooty/
├── SKILL.md
├── README.md
├── LICENSE
├── references/
│   ├── STYLE_PRESETS.md
│   ├── animation-patterns.md
│   ├── hackathon-playbook.md
│   ├── html-template.md
│   ├── viewport-base.css
│   └── bold-template-pack/
└── scripts/
    ├── deploy.sh
    ├── export-pdf.sh
    └── extract-pptx.py
```

Read `SKILL.md` for the operational workflow. Read `references/hackathon-playbook.md` for compact timing, narrative, demo-resilience, and judging guidance. Read `references/html-template.md`, `references/viewport-base.css`, and `references/animation-patterns.md` before generating a deck.

## Utilities

### Convert PPTX content

```bash
python scripts/extract-pptx.py input.pptx extracted/
```

### Deploy a deck

```bash
bash scripts/deploy.sh path/to/deck.html
```

### Export a deck to PDF

```bash
bash scripts/export-pdf.sh path/to/deck.html output.pdf
```

PDF export is static: animations and inline editing are not preserved.

## Attribution and contributor

This repository is a remix of [`zarazhangrui/frontend-slides`](https://github.com/zarazhangrui/frontend-slides), retaining its MIT license and acknowledging the original author, Zara Zhang. The hackathon configuration, agent-facing documentation, and repository packaging are maintained with **`thebhoopesh-commits` credited as contributor**.

## License

The repository is distributed under the MIT License. See [LICENSE](LICENSE).
