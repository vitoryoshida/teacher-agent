# teacher-agent

An English teacher agent for claude.ai. Holds natural conversations in English, corrects errors at the end of each response, tracks your progress across sessions, and warns you when you regress on any dimension.

---

## Installation

### 1. Create a Project on claude.ai

Go to [claude.ai](https://claude.ai) and create a new Project.

### 2. Add the System Prompt

Inside the project, open **Project Settings** and paste the full prompt from:

```
docs/superpowers/specs/2026-03-25-english-teacher-agent-v2-design.md
```

Copy the content inside the **"Final Prompt"** section and paste it into the **Custom Instructions** (or **System Prompt**) field. Save.

### 3. Enable Voice Input (optional)

Use the microphone button in the claude.ai chat interface to speak instead of type. The agent is designed to work with voice input — if your name is hard to understand via voice, it will ask you to type it.

### 4. Set Up History (first use)

No setup needed for the first session. After your first session ends, the agent will generate a **Session Report** and remind you to save it. Follow the instructions in [Per-User History](#per-user-history) below.

---

## How It Works

### Session Start

At the beginning of every conversation, the agent asks for your **full name** before anything else. It uses your name to load your history file from Project Knowledge and track your progress over time.

### During the Conversation

Talk about anything — daily life, work, travel, exams, whatever you want. The agent:

- Engages naturally with the topic
- Silently calibrates your English level based on what you write/say
- Adapts explanations and suggestions to your level
- **Warns you in real time** if it notices regression in any dimension compared to your last session (e.g., simpler vocabulary, shorter sentences, recurring errors)

### At the End of Each Response

After its conversational reply, the agent may add a feedback block:

```
---
📝 Corrections:
- "I go yesterday" → "I went yesterday" (past tense)

💡 Suggestion:
- "I want to know your opinion" works, but in a business context:
  "I'd love to hear your thoughts on this."
```

- **Corrections** appear only when there are actual errors — no filler praise
- **Suggestions** appear only when there is a genuinely useful formal/informal alternative
- For complex errors, the agent explains the rule and asks if you understood

### Session Report

When you say goodbye or ask for the report, the agent generates:

```
📊 Session Report — Maria Santos — 2026-03-25

Scores (0–100):
- Errors:      82 ▲ vs last session
- Vocabulary:  74 = vs last session
- Fluency:     68 ▼ vs last session
Overall:       75 = vs last session

Regressions flagged: Fluency
Summary: Maria maintained strong grammar accuracy today...
Topics covered: work meetings, weekend plans
Key corrections: conditional tense, article usage
Level estimate: B2

---
💾 Save reminder: Please save this report to your Project Knowledge
as "history_Maria Santos.md" before closing this session.
```

Scores are 0–100 where **higher is always better**:
- **Errors**: 100 = no errors observed (accuracy score, not error count)
- **Vocabulary**: 100 = rich and varied word choice
- **Fluency**: 100 = complex, varied sentence structures

---

## Per-User History

The agent stores one history file per person in **Project Knowledge**. This is how progress tracking and regression detection work across sessions.

### After Each Session

1. Copy the full **Session Report** generated at the end of the conversation
2. In your claude.ai Project, go to **Project Knowledge**
3. Upload or update the file named `history_[your full name].md`
   - Example: `history_Maria Santos.md`
4. On the next session, the agent will automatically load it

### Multiple Users

Each user gets their own file (`history_John Doe.md`, `history_Maria Santos.md`, etc.). All files live in the same Project Knowledge. The agent identifies the correct file by full name at session start.

### First Session

No history file needed. The agent starts fresh and the Session Report will not show deltas or regression flags — those appear from the second session onward.

---

## Specs

Design documents are in `docs/superpowers/specs/`:

- `2026-03-25-english-teacher-agent-design.md` — v1 base design
- `2026-03-25-english-teacher-agent-v2-design.md` — v2 with scoring, history, and regression detection
