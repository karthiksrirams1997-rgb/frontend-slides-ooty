---
name: frontend-slides-ooty
description: Create distinctive, animation-rich, zero-dependency HTML presentations for hackathon pitches, demo-day judging, technical product demos, and other short presentations; also convert PPT/PPTX files into fixed-stage web decks. Use when a presentation needs strong visual storytelling, 16:9 fidelity, live-demo resilience, inline editing, and browser delivery.
---

# Frontend Slides Ooty

Create polished, self-contained HTML presentations that run directly in a browser. This is a remix of `zarazhangrui/frontend-slides`, adapted for Manus and optimized for short, persuasive hackathon pitches. It retains general presentation and PPT/PPTX conversion support, with an optional Ooty-inspired visual vocabulary—mist, tea, botanical greens, warm paper, and measured editorial typography—used only when it fits the project.

## When to use this skill

Use this skill whenever the user asks to create, remix, convert, improve, or present:

- A **hackathon presentation**, hackathon pitch, demo-day deck, judging deck, project showcase, or prototype pitch.
- A **live product demo deck**, technical demo, engineering showcase, or startup-style prototype presentation.
- A presentation for a **time-boxed competition**, where judges need to understand the problem, solution, evidence, technology, and impact quickly.
- A PPT/PPTX conversion or HTML presentation that needs a fixed 16:9 stage, visual style options, browser navigation, inline editing, or PDF/live sharing.

Treat phrases such as “hackathon slides,” “demo day,” “pitch my project,” “present our prototype,” “judge our build,” “technical showcase,” “product demo,” and “make a deck for the competition” as strong signals to activate the hackathon workflow below. Do not wait for the user to say the exact word “hackathon” if the request clearly describes a judged prototype or short demo pitch.

### Typical requests this skill should handle

- “Make an 8-slide deck for our 5-minute AI hackathon demo.”
- “Turn this prototype into a compelling demo-day presentation.”
- “Create slides that explain our architecture and live product flow to judges.”
- “Convert our pitch PPTX into an editable HTML deck with a fallback for the live demo.”
- “Improve this presentation so judges understand the problem and impact in three minutes.”

For these requests, default to the hackathon intake, speaker-led density, one takeaway per slide, a concise technical proof point, and a resilient demo path. Ask only for missing details that materially affect the narrative, timing, rubric, or output.

## Non-negotiable invariants

1. **Use a single HTML file** with inline CSS and JavaScript. Avoid npm, build tools, and runtime dependencies.
2. **Author every slide on a fixed 1920×1080 stage.** Scale the entire stage uniformly to fit the viewport; never reflow slide content for phones.
3. **Include the complete `references/viewport-base.css` contents** inside every generated presentation. Read it before authoring.
4. **Control slide visibility with `.active`/`.visible`**, `visibility`, `opacity`, and `pointer-events`. Never switch slides with `display: none`/`display: block`.
5. **Prevent overflow and overlap.** Split content into more slides instead of shrinking type until it becomes unreadable.
6. **Use distinctive fonts from Google Fonts, Fontshare, or another explicit web-font URL.** Do not use Arial, Roboto, Inter, or system fonts as display typography.
7. **Support `prefers-reduced-motion`, keyboard navigation, touch/swipe navigation, and accessible semantic HTML.**
8. **Never negate CSS functions directly.** Use `calc(-1 * clamp(...))`, `calc(-1 * min(...))`, or `calc(-1 * max(...))`.

## Workflow decision tree

### 1. Detect the task mode

- **Hackathon pitch:** follow the hackathon workflow below; default to speaker-led density and demo resilience.
- **Other new presentation:** continue through content discovery, style discovery, generation, and verification.
- **PPT/PPTX conversion:** run `scripts/extract-pptx.py`, summarize the extracted deck, then use the relevant style workflow while preserving order, text, images, and speaker notes as HTML comments.
- **Existing HTML enhancement:** inspect the current deck first. Count existing elements and check density before adding anything. If content would overflow, split slides proactively.

### 2. Hackathon intake and narrative

Ask missing questions together in one concise structured prompt:

1. What is the hackathon theme, judging rubric, or event context?
2. What is the time limit, including or excluding the demo?
3. Is there a working prototype, screenshots, recording, or only a concept?
4. Who is the target user, and what problem is being solved?
5. Which technologies, APIs, models, or integrations should be highlighted?
6. What evidence exists—users, benchmark results, pilot feedback, metrics, or demo outcomes?
7. What should judges remember, approve, fund, try, or do at the end?

Use reasonable defaults when unanswered: a 3–5 minute speaker-led pitch, 8–10 slides, one demo flow, a concise architecture slide, and a closing ask. Let the supplied judging rubric override the default.

Build the story around one clear takeaway per slide:

1. Title, one-line promise, team, and event context.
2. Problem in one vivid user-centered statement.
3. Why now, target user, and stakes.
4. Solution overview and product promise.
5. Product flow or live-demo setup.
6. Technical architecture or implementation choices.
7. Differentiation and why the approach is credible.
8. Evidence, traction, benchmark, or demo result.
9. Impact and next steps.
10. Closing takeaway, ask, QR/link, or demo continuation.

Collapse or expand this outline to match the time limit. Omit architecture or evidence when they do not strengthen the judging case; move extra technical detail to appendix slides.

For non-hackathon decks, ask the normal purpose, length, content status, and density questions. Do not ask about inline editing; include it by default unless the user explicitly requests a locked/export-only deck.

If images are supplied, scan them, inspect each one, record what it depicts and its dominant colors, and design the outline around usable images before choosing layouts. Do not repeat an image across slides except a logo on the title and closing slides.

### 3. Run visual style discovery

Always generate three distinct, self-contained title-slide previews in `.frontend-slides/slide-previews/` as `style-a.html`, `style-b.html`, and `style-c.html`. Open all three and ask which style the user prefers or whether to mix elements.

For a hackathon, make the three options different but readable under stage lighting and quick judging conditions:

- One high-contrast, presentation-safe option with large type.
- One expressive product/demo option with a strong accent color and screenshot or UI framing.
- One custom option aligned to the hackathon theme or project domain.

Each preview must look like a genuine first slide from the user’s deck. Never show internal labels such as “preview,” “option A,” “template,” file paths, or design-process notes on the slide itself.

Read `references/STYLE_PRESETS.md` first. If bold templates are candidates, read only their `preview.md` files from `references/bold-template-pack/`. Read a selected template’s full `design.md` only after the user picks it. Do not load every template design document.

For an Ooty-inspired direction, prefer deep Nilgiri green, fog gray, tea-leaf olive, terracotta, warm cream, and a serif/sans pairing. Use botanical or terrain references as abstract CSS shapes, not generic illustrations. Keep the direction appropriate to the project and audience.

### 4. Generate the deck

Before generation, read:

- `references/html-template.md` for the required architecture and controller behavior.
- `references/viewport-base.css` for mandatory fixed-stage CSS.
- `references/animation-patterns.md` for motion choices.
- `references/hackathon-playbook.md` for timing, demo, and judging heuristics.
- The selected preset or selected bold template’s design recipe.

Apply density consistently:

- **Speaker-led:** use more slides, fewer words, oversized headings, visual metaphors, section beats, quotes, and generous negative space.
- **Reading-first:** use structured grids, comparison tables, annotated diagrams, captions, and concise explanatory copy without creating document-like clutter.

Preserve the chosen style’s typography, palette, spacing rhythm, decorative vocabulary, and component grammar across the entire deck. Do not copy demo content from a template. Keep all CSS and JS inline and add clear `/* === SECTION NAME === */` comments.

### 5. Make live demos resilient

- Keep the demo setup slide explicit and short: state what the audience should watch for.
- Use screenshots or a lightweight fallback sequence for every critical demo step.
- Do not rely on animation timing, an external network request, or a live API response to communicate the core story.
- Include a demo-fallback slide or visual sequence when failure would materially weaken the pitch.
- Keep technical detail in optional appendix slides rather than crowding the main narrative.
- Verify that every QR code, URL, repository link, or product access path is readable and visually correct.
- Treat product screenshots as evidence, not decorative filler; label the user action and outcome.

### 6. Include presentation controls and editing

Implement a `SlidePresentation` controller with:

- Arrow keys, Space, Page Up/Down, and Home/End navigation.
- Touch/swipe and mouse-wheel navigation with sensible throttling.
- Optional progress/page count outside the slide stage.
- Whole-stage scaling based on `Math.min(window.innerWidth / 1920, window.innerHeight / 1080)`.

Include inline editing by default:

- Hide the edit control until the user hovers a top-left hotzone or presses `E`.
- Use JavaScript hover handling with a 400 ms grace timeout; do not use a CSS `~` sibling selector because `pointer-events: none` can break the hover path.
- Allow text editing, localStorage auto-save, and Ctrl/Cmd+S export/save behavior.
- Do not toggle edit mode when `E` is typed into an editable text target.

### 7. Verify before delivery

Check all of the following:

- The first slide communicates the project and value proposition within a few seconds.
- Every main slide has one clear takeaway.
- The deck fits the stated time limit using an approximate speaking-time budget.
- Text is legible from presentation distance and does not depend on tiny body copy.
- The demo path is understandable even if the live product is unavailable.
- Architecture labels remain readable at 1920×1080 and in rendered previews.
- The closing slide contains the intended takeaway, ask, URL, QR code, or contact information.
- The stage remains exactly 16:9 at desktop and phone viewport sizes.
- Only the intended slide is visible and interactive.
- No text, images, panels, or controls overflow the stage.
- No grid or card panels visually overlap.
- Fonts load or have a deliberate fallback.
- Keyboard, touch, reduced-motion, and edit-mode behavior work.
- Preview slides contain no internal workflow metadata.

For modifications, verify before and after the change. If a new image or text block would exceed the slide’s density limit, split the slide rather than compressing it.

## Image handling

If images are provided, keep them as relative file paths beside the HTML rather than embedding base64 unless there is a compelling portability reason. Use `Pillow` when needed to create `_processed` copies for circular crops, resizing, or aspect-ratio corrections; never overwrite originals. Keep screenshots inside authored bounds with `object-fit: contain` and style borders/shadows to match the chosen palette.

## Delivery and optional sharing

After generating a deck:

1. Delete `.frontend-slides/slide-previews/` if previews should not ship.
2. Open the HTML file in a browser.
3. Tell the user the file location, style name, slide count, navigation controls, CSS customization points, and inline editing shortcut.
4. Offer deployment to a live URL or PDF export only as a follow-up choice. Use `scripts/deploy.sh` for Vercel deployment and `scripts/export-pdf.sh` for PDF export. Explain that PDF export captures static visual states and does not preserve animation or editing.

## Supporting files

| File | Read when | Purpose |
|---|---|---|
| `references/STYLE_PRESETS.md` | Style discovery | Curated palettes, fonts, layouts, and anti-patterns |
| `references/bold-template-pack/selection-index.json` | Style discovery | Compact metadata for candidate bold templates |
| `references/bold-template-pack/templates/*/preview.md` | After shortlisting | Lightweight preview guidance |
| `references/bold-template-pack/templates/*/design.md` | After selection | Full recipe for the selected template only |
| `references/viewport-base.css` | Every deck generation | Mandatory fixed-stage CSS |
| `references/html-template.md` | Every deck generation | HTML/controller/editing architecture |
| `references/animation-patterns.md` | Every deck generation | Motion and background-effect reference |
| `references/hackathon-playbook.md` | Hackathon pitches | Timing, narrative, demo, and judging heuristics |
| `scripts/extract-pptx.py` | PPT/PPTX conversion | Extract slide text, images, and notes |
| `scripts/deploy.sh` | User requests live sharing | Vercel deployment |
| `scripts/export-pdf.sh` | User requests PDF | Browser screenshot-to-PDF export |

## Quality bar

Favor authored visual systems over generic dashboards, evenly distributed palettes, purple-gradient clichés, and repetitive card grids. Make each deck feel designed for its audience. Use one strong visual thesis per deck, then vary slide layouts within that system so the presentation has rhythm without losing coherence. For hackathons, optimize for fast comprehension, credible proof, memorable demos, and a clear closing ask.
