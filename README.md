# Michael's Personal Tutoring Harness

An agentic learning system that runs inside Claude Code. It teaches any topic through a closed feedback loop and refuses to move on until you actually understand — no fact-regurgitation, no jumping ahead.

## How it works

```
/learn <topic>
   │
   ▼
Intake ──► Diagnostic test ──► Roadmap ──► Teach loop ──► Final exam ──► Done
 (resources,  (adaptive, finds   (small units, (one concept    (cumulative,
  goals,       exactly what you   you approve   at a time +     weighted toward
  register)    know/don't)        the order)    mastery gates)  your weak spots)
                                                     ▲   │
                                                     └───┘
                                              fail a gate? reteach the
                                              exact gap a different way,
                                              re-quiz with fresh questions
```

The loop only ends when the roadmap is complete **and** you pass the final exam.

## Commands

| Command | What it does |
|---|---|
| `/learn <topic>` | Start a new topic, or resume one exactly where you left off (with a quick retention warm-up) |
| `/grill-gate <topic>` | Get grilled on something to prove you understand it — also runs automatically at the end of every unit |
| `/add-resources <topic>` | Add PDFs, notes, slides, or URLs to a topic's resource database; can web-search to fill gaps (asks first) |

You can also just talk: say **"eli5 that"**, **"eli15"**, or **"explain it like I'm an intern"** mid-lesson to change how explanations are pitched, instantly.

## What makes it different

- **Tests understanding, not memory.** Every quiz question is generative: explain it back with a *new* analogy, solve a problem you haven't seen, predict an edge case, find the flaw in a wrong claim. Never multiple choice, never fact recall.
- **Strict gates.** ~85% to pass a unit — a coherent teach-back AND a solved transfer problem. Fail, and the exact misconception gets named, logged, and retaught from a different angle (new analogy → concrete numbers → diagram → code) with fresh questions.
- **Learns how you learn.** [learner-profile.md](learner-profile.md) accumulates evidence about which explanations land for you, your recurring error patterns, and your interests (used as analogy anchors). Every lesson reads it first.
- **Topics build on each other.** Learning something that follows a previous topic (like consecutive units of a class)? It links them, spot-checks your retention of the old material, and opens with a bridge recap written from *your own words* in the old topic's notes.
- **Fully resumable.** All state lives in files. Close the laptop mid-roadmap, come back next week, run `/learn <topic>` — it warms you up on last session's material and continues at the exact unit.

## Layout

```
StopLosingBraincellsToAI/
├── README.md              ← you are here
├── CLAUDE.md              ← the Teaching Contract (rules every session follows)
├── learner-profile.md     ← how you learn, built up over time
├── .claude/skills/        ← learn.md, grill-gate.md, add-resources.md
└── topics/<topic>/        ← created per topic:
    ├── state.json         ← phase, current unit, register, prerequisite links
    ├── diagnostic.md      ← baseline: solid / shaky / missing / misconceptions
    ├── roadmap.md         ← ordered units with gate checkboxes
    ├── weak-spots.md      ← every misconception found, tracked to resolution
    ├── quiz-log.md        ← every gate attempt with per-question analysis
    ├── resources.md + resources/  ← your indexed study materials
    └── notes/             ← lesson notes in YOUR words — your study sheets
```

## Getting started

1. Open a Claude Code session in this folder (so `CLAUDE.md` and the skills load).
2. Run `/learn <something from one of your classes>`.
3. Answer the intake questions, take the short diagnostic (wrong answers are the point — they aim the teaching), approve the roadmap, and go.
