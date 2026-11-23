# Between the Shelves

**Game Design Document / Agent Handoff**  
**Version:** 0.1 — November 23, 2026  
**Status:** Working product vision; decisions marked *proposed* require validation.

> A cozy literary game about finding the right book for the right person, building relationships with readers, and bringing a magical, timeless storybook library to life.

## 1. North star

**Working title:** Between the Shelves. Check trademark, domain, and app-store availability before release.

**Audience:** Book lovers first, casual cozy-game players second. A niche but enthusiastic audience is acceptable.

**Core promise:** Help distinctive patrons identify forgotten books and discover their next favorite read, using *real* literary works. Between shifts, tend a living storybook library, organize events, and gradually uncover its secrets.

**Design pillars**
1. **Real books are the heroes.** Accurate metadata, recognizable literary knowledge, and carefully verified quotations where rights permit.
2. **Thoughtful, fair challenges.** Exact identification is deterministic; subjective recommendations recognize multiple defensible choices.
3. **A place worth inhabiting.** Rich 2.5D hand-painted environments, tactile paper and wood, warm light, expressive illustrated characters, subtle magical flourishes.
4. **Cozy without manipulation.** No forced ads, punitive streaks, energy gates, or pay-to-win hints.
5. **Handcrafted quality.** Curated scenarios, editorial review, consistent art direction, and satisfying audio/tactile details.

**Non-goals:** 3D free-roaming world, generic match-three minigames, live AI required for gameplay, competitive multiplayer, sprawling simulation systems at MVP.

## 2. World and tone

The player becomes the librarian of an old neighborhood library that seems to exist just outside ordinary time. Its tall shelves bend into warm shadows, brass labels gleam, rain taps leaded windows, and the building reveals small wonders as its community grows. **The books are real; the library and patrons are fictional.** Magic is atmospheric, not a substitute for book knowledge: a lamp glows when a reader finds their book; a forgotten shelf appears after a story milestone; a pressed flower drifts from a returned volume.

**Tone:** Gentle, curious, witty, wistful, never saccharine. A light overarching mystery (missing manuscript, anonymous donor, secret archive) supports progression but must not eclipse book gameplay.

## 3. Visual design bible

### Chosen direction
**First visual direction from the concept discussion:** cozy, richly illustrated storybook library interior with warm amber lighting, wooden bookshelves, painterly textures, and restrained isometric/2.5D depth. Prefer a scene-based 2D presentation over flat vector characters or photorealistic 3D.

**Palette (starting tokens; test accessibility):**
- Forest green `#263B32` — primary surfaces, navigation, identity
- Parchment `#E8D9B9` — reading panels and dialog
- Terracotta `#A85D43` — interactions and accents
- Antique gold `#B79654` — rewards, embellishment
- Ink `#263B32`, ivory `#FAF5E9`, muted brown `#766957`

**Materials:** Embossed leather, clothbound spines, deckle-edge paper, wood grain, engraved brass, catalog cards, fountain-pen ink, pressed botanicals. Use layered lighting and shadows rather than a uniformly sepia filter.

**Environments:** Full-bleed illustrated library scene, parallax layers, interactive front desk, shelves, catalog drawer, event board, reading nook, rain-streaked windows. Daylight/weather/season changes should be visual treatments on reusable base art.

**Characters:** 12 recurring patrons eventually; begin with one. Painterly portraits with consistent silhouettes, costume, palette, and proportions. Use limited expressive states (neutral, curious, pleased, disappointed), subtle blinking and breathing, and reusable animation rigs. Avoid generic geometric/block figures.

**Paper and passage UI:** A quotation appears as a tactile fragment of a real book: off-white textured page, carefully chosen readable serif, uneven but not illegible edge, realistic drop shadow, optional edition/source label. Never imply a fabricated passage is an authentic quote. Provide plain-text accessible presentation.

**Animation:** Book slides into shelf, drawer opens, card lifts, page turns, lamp flickers, patron expression changes. Prefer 150–400 ms purposeful motion; honor reduced-motion setting.

**Audio:** Soft footsteps, bell at entrance, pages, book thunks, drawer slides, rain, fireplace, gentle ambient score. Adjustable sound/music independently.

**Visual reference handoff:** See `VISUAL_REFERENCES.md` and `visual_reference_board.html`. These are *search/reference prompts*, not cleared production art or copies of the earlier displayed images.

## 4. Mobile information architecture

Four persistent destinations:
1. **Home:** Library scene, today's shift, waiting patron, current weather, shift progress, shortcuts via objects.
2. **Patrons:** Recurring characters, taste profiles, relationship milestones, story chapters.
3. **Collection:** Searchable catalog, discovered books, genres, reading list.
4. **Profile:** Achievements, cosmetics, settings, accessibility, purchases.

**Home screen layout:** Top header with fictional date/season, reputation/bookmarks; hero illustration of library with animated visitor; contextual parchment dialog card with primary `Help this reader` CTA; object hotspots for Catalog, Events, and Library customization; bottom navigation. Do not clutter scene with generic dashboard cards.

**Core screens:** Library Home; Patron Conversation; Clue/Passage Detail; Book Catalog/Search; Book Detail; Selection/Scoring Feedback; Reshelving; Event Planner; End-of-Shift Summary; Patron Journal; Collection; Settings/Store.

**UX standards:** Thumb-reachable primary actions, iPhone/Android safe areas, dynamic type where practical, VoiceOver/TalkBack, large touch targets, accessible contrast, no gesture-only critical action, reduced motion, offline play, graceful interruptions and save/resume.

## 5. Core challenge modes

### A. The Forgotten Book — exact identification
A patron vaguely remembers plot, characters, author, setting, or vibes. Search catalog or choose among candidates; optional clarifying question/hints. Score exactness, difficulty, hints. Example: a detective on a snowbound train -> *Murder on the Orient Express*.

### B. The Lost Passage — exact identification
A torn-page presentation contains a verified, rights-cleared authentic excerpt. Identify book/author. Public-domain excerpts first; modern excerpts only with rights review or license. Do not generate invented quotes and label them authentic.

### C. Read My Mind — subjective recommendation
Patron describes mood, preferences, aversions, reading history. Player selects a book. Score against a human-reviewed rubric with multiple excellent matches and explanations. Example dimensions: genre, mood, theme, pacing, complexity, novelty, content sensitivities.

### D. The Perfect Follow-Up — subjective recommendation
After finishing a known title, patron wants a thematically, stylistically, or emotionally related read. Judge compatibility, not only genre overlap.

**Scoring:**
- Identification: deterministic correct IDs, difficulty, optional hint penalty.
- Recommendation: curated `bookScores` per scenario (0–100) with rationales and a tolerance for multiple good answers. Do not rely on a live LLM judge.
- Feedback: explain *why* the match works or fails; avoid humiliating players for a defensible interpretation.
- Difficulty: genre preferences and tiered challenges; introduce unfamiliar books gradually.

## 6. Catalog and content

**Full launch target (not MVP):** ~150 real books, ~120 editorially reviewed scenarios, ~12 recurring patrons. Proposed initial mix: ~40 verified public-domain classics, ~60 modern popular books, ~50 other genre titles.

**MVP:** 25–50 books, 30 curated scenarios, two modes (Forgotten Book and Read My Mind), one recurring patron, searchable catalog.

Catalog fields: stable ID, title, author, year, genres, themes, moods, pacing, complexity, content warnings, rights status, cover rights/asset, bibliographic provenance, excerpt source and permission status if used. Allow filters by title, author, genre; show readable book cards and discoveries.

**Reading list:** Want to Read / Reading / Read; valuable to book lovers even outside the game. Optional later export, subject to integration rights and privacy review.

### Rights and factual quality
- Titles, authors, and basic bibliographic facts are generally usable, but validate factual accuracy.
- **Fair use is not automatic** for short copyrighted excerpts, especially when systematically embedded in a commercial product. Seek qualified legal review for intended uses.
- Prefer verified public-domain texts (verify jurisdiction, edition, translation, and source conditions), licensed modern excerpts, or *original paraphrased clues*.
- Cover artwork, edition design, illustrations, translations, and photographs may have separate rights. Do not assume database availability grants commercial reuse.
- Suggested discovery sources: Open Library, Project Gutenberg, Standard Ebooks; review their data and distribution terms.
- Every published passage requires source edition, attribution, rights determination, exact text verification, and approval record.

## 7. Secondary gameplay

**Launch priority 1 — Reshelving:** Drag books into simplified genre/author order; progress to more complex classification. Snappy tactile book-placement feedback. Accessibility alternative to drag/drop.

**Launch priority 2 / post-MVP — Event planning:** Choose theme, featured books, date, and intended audience. Patron interests influence attendance and relationship outcomes. Avoid complex calendar simulations.

**Later — Book restoration:** Clean, repair, and rebind worn volumes in a tactile, low-pressure minigame.

**Later — Decoration:** Unlock and place lamps, rugs, chairs, plants, shelf details, seasonal skins. Start with fixed slots; no full room editor at MVP.

**Target session composition (directional):** ~60% book challenges, 15% reshelving, 15% events, 10% story/progression/customization. Tune through playtesting.

## 8. Session loop

A 5–10 minute shift:
1. Open library; see weather, day, visitors, event notices.
2. Help 3–5 patrons through mixed challenges.
3. Complete one short library task.
4. Review shift summary: satisfaction, discoveries, reputation, bookmarks.
5. Spend rewards, unlock story/collection, optionally continue.

Untimed by default. Optional timed challenge mode only after the core experience is proven. No forced wait timers or punitive streak resets.

## 9. Narrative and progression

**Patron seeds:**
- Mrs. Whitmore — retired teacher, mystery devotee, investigating an old local secret.
- Elliot — skeptical student who discovers genres he likes.
- Nora — aspiring novelist whose reading influences her manuscript.

Each patron has preferences, relationship milestones, a few expression states, branching-but-manageable dialogue, and episodic requests. Relationships unlock letters, new requests, event attendance, and narrative scenes, not generic romance mechanics.

**Currencies / tracks:** Reputation (community trust and story/library unlocks), Bookmarks (earned cosmetic currency), Discoveries (catalog and literary achievements). Avoid multiple confusing premium currencies.

**Retention:** Optional daily literary puzzle, weekly theme, monthly narrative/content update if sustainable. Never promise a cadence the content team cannot deliver.

## 10. Monetization

**Recommended:** Free first chapter + **proposed $6.99 one-time full-game unlock**, with testing range $5.99–$7.99. Free sample: 30–40 challenges and basic library. Full unlock: main story, core catalog, progression, patrons.

Optional later offerings: cosmetic seasonal themes ($1.99–$3.99), narrative/book challenge expansions ($3.99–$4.99), supporter cosmetics (~$4.99). No forced ads, energy gates, paid score advantages, or paid correct answers. Test pricing with beta audience; these are hypotheses, not forecasts.

**Illustrative unit economics:** 10,000 downloads × 5% purchase conversion × $6.99 = $3,495 gross, before store fees, taxes, refunds, art, marketing, and operations. Store fees depend on platform and eligibility.

## 11. Technical approach

**Recommended:** React Native + Expo + TypeScript for a scene-based 2D/2.5D experience. Reanimated/Skia/Rive where needed for polished effects; SQLite for local content/progress; Supabase/PostgreSQL for optional accounts/cloud sync/content distribution; RevenueCat for cross-platform purchases; PostHog for opt-in/privacy-conscious analytics; Python/Pydantic for content authoring and validation.

**Why not a full engine initially:** Most gameplay is scenes, dialogue, catalogs, cards, and lightweight minigames. Reconsider Godot/Unity only if complex real-time world navigation or character simulation becomes essential.

**Offline-first:** Bundle enough content for complete shifts. No runtime AI dependency. Persist progress locally; cloud sync later with conflict policy. Version content bundles and support save migrations.

**Example types:**
```ts
type Book = {
  id: string;
  title: string;
  author: string;
  publicationYear: number;
  genres: string[];
  themes: string[];
  moods: string[];
  pacing: 'slow' | 'medium' | 'fast';
  complexity: 1 | 2 | 3 | 4 | 5;
  contentWarnings: string[];
  rightsStatus: 'public_domain' | 'licensed' | 'metadata_only';
  coverAssetId?: string;
};

type RecommendationScenario = {
  id: string;
  patronId: string;
  mode: 'recommendation';
  dialogue: string;
  preferences: {
    preferredGenres: string[];
    desiredMoods: string[];
    preferredThemes: string[];
    dislikedThemes: string[];
    preferredPacing?: 'slow' | 'medium' | 'fast';
  };
  bookScores: Record<string, { score: number; explanation: string }>;
  difficulty: 1 | 2 | 3 | 4 | 5;
};
```

**Content pipeline:** Verified book records -> Sonnet-assisted draft scenarios -> Pydantic/schema validation -> duplicate/factual/rights checks -> human editorial review -> versioned signed-off JSON bundles. AI helps author but does not unilaterally determine literary truth or licensing.

## 12. Agent-ready repository layout

```text
between-the-shelves/
  apps/mobile/src/
    screens/ scenes/ components/ animations/
    game/scoring/ game/shifts/ game/progression/
    data/ storage/
  apps/mobile/assets/
    backgrounds/ characters/ books/ textures/ audio/
  content/books/ content/patrons/ content/scenarios/ content/events/
  tools/content_pipeline/
  docs/GAME_DESIGN.md
  docs/ART_DIRECTION.md
  docs/UI_SPEC.md
  docs/CONTENT_GUIDELINES.md
  docs/ARCHITECTURE.md
  AGENTS.md
```

### Rules for coding agents
1. Read this document and existing architecture/art specs before edits.
2. Build a vertical slice before adding systems; one scoped feature per task.
3. Follow shared design tokens and reusable UI components; never invent a separate art style per screen.
4. Separate rendering, gameplay rules, storage, and content.
5. Never fabricate a quote or infer copyright permission.
6. Validate all external/content data with typed schemas.
7. Test scoring, unlocks, saves, migration, and catalog searches.
8. Respect small screens, safe areas, screen readers, reduced motion, and offline behavior.
9. Use real-device visual QA; no placeholder UI in a feature marked done.
10. Report changed files, tests run, limitations, and follow-up tasks.

### Suggested agent ticket format
**Goal / Context / Files in scope / Inputs / Acceptance criteria / Non-goals / Tests / Visual QA / Rights considerations.** Keep tickets small enough for one model implementation/review cycle.

## 13. Milestones and exit criteria

**M0 — Visual/interaction proof (1–2 weeks, aggressive):** One scene, one patron with three expressions, 10 authored challenges in two modes, 25 books, catalog, result feedback, complete 5-minute shift, local save. Must run on a real phone. No backend/store.

**M1 — Core systems (weeks 3–4):** Four challenge modes (or defer two if polish suffers), deterministic scoring, 30 curated scenarios, shift progression, content validation and tests.

**M2 — Variety (weeks 5–6):** Reshelving, simple event planning, reputation, initial unlocks.

**M3 — Narrative and polish (weeks 7–9):** Recurring patrons, chapter one, layered art, sound, accessible motion, refined feedback.

**M4 — Beta/release (weeks 10–12+):** Purchases, privacy, cloud sync if needed, analytics, legal review, content expansion, TestFlight/Android beta, store assets.

**Schedule caveat:** These are ambitious solo-developer/AI-assisted targets. Custom art, editorial work, legal review, and device polish can push the timeline to 4–6+ months.

### MVP acceptance gates
- A new player completes a shift without explanation.
- The catalog feels like a usable library, not a multiple-choice screen.
- Scoring is understandable and reproducible.
- 30 scenarios are verified, varied, and enjoyable.
- One animated character and environment feel cohesive and premium.
- Saves survive app restarts and offline use.
- No uncleared text or cover art ships.
- Testers voluntarily play more than one shift.

## 14. Playtesting and analytics

Recruit 20–30 early readers for qualitative tests, then 100–200 beta participants. Ask: Was the challenge fair? Did you learn about a book? Did the catalog feel intuitive? Would you return tomorrow? What was tedious? Did the atmosphere feel distinctive?

Track with privacy care: tutorial completion, shift completion, catalog search friction, hints per challenge, score distribution, second-shift rate, D1/D7 retention, free-to-paid conversion, and qualitative feedback. Do not collect sensitive reading preferences unnecessarily.

## 15. Key risks

- **Repetitive trivia:** Mix identification, subjective recommendations, stories, and short library tasks.
- **Wrong AI content:** Provenance, review, deterministic scoring, automated tests.
- **Copyright:** Public domain/permission-first, legal review, rights ledger.
- **Inconsistent generated art:** One art bible, approved asset sheets, reusable rigs.
- **Runaway scope:** M0 vertical slice gates all further investment.
- **Niche economics:** Low operational costs, modest upfront unlock, optional expansions.
- **Unfair difficulty:** Genres, tiers, hint choices, multiple valid recommendations.

## 16. Decisions locked vs open

**Locked:** Title *Between the Shelves* (working); magical timeless storybook library; warm richly illustrated first visual direction; real books; book-lover-first niche; polished tactile presentation; fair scoring; no predatory monetization; Sonnet-friendly modular implementation.

**Open:** Final title rights check; final art vendor/workflow; precise narrative mystery; launch book list and rights ledger; target iOS minimum; exact price; whether event planning ships in v1; how much catalog is unlocked initially; long-term content cadence.

## 17. Immediate next actions

1. Create `ART_DIRECTION.md` with 1 approved environment composition, palette, character sheet, texture examples, and animation principles.
2. Create `UI_SPEC.md` with screen-by-screen wireframes, interaction states, and responsive dimensions.
3. Implement M0 with only one room, one patron, 10 challenges, catalog, scoring, shift summary, and local save.
4. Validate the fun of the core interaction with readers before building the rest.
5. Start a rights/provenance ledger from the first book record.

**Agent kickoff prompt:** "Read `BETWEEN_THE_SHELVES_GAME_PLAN.md` and `VISUAL_REFERENCES.md`. Propose a minimal Expo/React Native architecture and a sequence of independently testable M0 tickets. Do not implement M1+ systems. Preserve the approved art direction, offline-first design, rights rules, and deterministic scoring. State assumptions and request approval before significant scope or dependency changes."
