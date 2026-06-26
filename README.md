# SuperHumanizer

**A Claude skill that strips AI writing patterns from text and rewrites it to sound genuinely human.**

[🇨🇿 Česká verze](README.cs.md) · [MIT License](LICENSE) · Made by [aethero](https://aethero.cz)

---

AI-generated text has tells. Not just "delve" and em dashes — it has a statistical fingerprint:
uniform sentence length, hedge-packed vocabulary, bullet lists for everything, chatbot preamble,
significance inflation, and a pathological love of the rule of three.

SuperHumanizer fixes all of it. One command. Works in English and Czech.

---

## What it does

- Strips 33 English AI writing patterns + 27 Czech-specific patterns
- Applies 9 humanization levers grounded in detection research (Wu et al. 2025, Mitchell et al. 2023)
- Matches your personal voice if you supply a writing sample (ToV calibration)
- Runs a draft → audit → final rewrite loop
- Optional `/ai-check` mode for forensic scoring without rewriting

---

## Install

### Claude.ai (Skills UI)

1. Open [claude.ai](https://claude.ai) → Settings → Skills
2. Click **New skill**
3. Paste the contents of [`SKILL.md`](SKILL.md)
4. Save

### Claude Code / any agent with skills support

```bash
git clone https://github.com/aethero-dev/superhumanizer ~/.claude/skills/superhumanizer
```

---

## Usage

```
/humanize [your text here]
```

**Match your personal voice:**
```
/humanize [your text here]
Writing sample: [paste your own writing here]
```

**Forensic analysis (no rewrite):**
```
/ai-check [your text here]
```

**Output styles:** academic · formal · friendly · conversational
(Claude will ask if you don't specify)

---

## Example

**Input (typical AI output):**
> In today's rapidly evolving technological landscape, artificial intelligence serves as a testament
> to human ingenuity. Organizations across industries — from agile startups to established enterprises
> — are increasingly leveraging cutting-edge solutions to streamline workflows and unlock transformative
> value. The future looks bright.

**Output after `/humanize`:**
> AI is moving fast, and most companies know it. What's actually changing: the boring work. Drafting,
> sorting, summarizing — things that used to take hours. The strategic stuff still needs a person.
>
> Teams that trained before deploying got 40% better ROI than those that didn't. The companies still
> waiting for "the right moment" are just falling behind.

---

## How it works

| Lever | What it fixes |
|---|---|
| Perplexity injection | Predictable, low-surprise word choices |
| Burstiness injection | Uniform sentence length (the ~15-word drone) |
| Hedge surgery | "It is worth noting", "generally", "typically" |
| Structural flattening | Bullet lists for everything, excessive headers |
| Specificity insertion | "Many users" → "47 of our 140 beta users" |
| Voice calibration | Matches your personal writing sample |
| Discourse coherence | "Furthermore", "Moreover", "In conclusion" |
| Punctuation normalization | Em dash overuse, semicolons, decorative bold |
| Strip RLHF voice | "Great question!", "Let's dive in", announcements |

---

## Czech support

SuperHumanizer includes 27 patterns specific to Czech AI writing:
- English word order imposed on Czech sentences
- Calques: "pojďme se ponořit do", "na konci dne", "adresovat problém"
- Excessive possessive pronouns: "otevřel své oči" → "otevřel oči"
- Nominalization: "došlo k realizaci implementace" → "nasadili jsme"
- Formulaic conclusions: "závěrem lze konstatovat", "shrnuto a podtrženo"
- And 22 more

---

## Standing on the shoulders of giants

- **[blader/humanizer](https://github.com/blader/humanizer)** (26k ⭐, MIT) — English pattern foundation
- **[bejek/humanizer-czech](https://github.com/bejek/humanizer-czech)** (21 ⭐, MIT) — Czech-specific patterns
- **[harshaneel/humanize](https://github.com/harshaneel/humanize)** (52 ⭐, MIT) — detection science + /ai-check

Pattern source: [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)

---

## License

MIT — use it, fork it, ship it.

Made by [aethero](https://aethero.cz) · [david.kuba@aethero.cz](mailto:david.kuba@aethero.cz)
