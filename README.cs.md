# SuperHumanizer

**Claude skill, který odstraňuje AI vzorce z textu a přepisuje ho tak, aby zněl jako člověk.**

[🇬🇧 English version](README.md) · [MIT License](LICENSE) · Made by [aethero](https://aethero.cz)

---

AI text má rukopis. Nejde jen o "delve" a em dashe — má statistický otisk: uniformní délka vět,
slovní zásoba plná hedgů, bullet listy na vše, chatbot omluvy, nafouklý jazyk a patologická
láska k pravidlu tří.

SuperHumanizer to opravuje celé. Jeden příkaz. Funguje v češtině i angličtině.

---

## Co umí

- Odstraňuje 33 anglických AI vzorců + 27 vzorců specifických pro češtinu
- Aplikuje 9 humanizačních pák vycházejících z vědeckého výzkumu detekce AI
- Přizpůsobí výstup tvému osobnímu stylu, pokud přiložíš ukázku svého psaní (voice calibration)
- Pracuje v loop: draft → audit → finální přepis
- Volitelný mód `/ai-check` pro forenzní analýzu bez přepisu

---

## Instalace

### Claude.ai (Skills UI)

1. Otevři [claude.ai](https://claude.ai) → Settings → Skills
2. Klikni **New skill**
3. Vlož obsah souboru [`SKILL.md`](SKILL.md)
4. Ulož

### Claude Code / jiný agent se support pro skills

```bash
git clone https://github.com/aethero-dev/superhumanizer ~/.claude/skills/superhumanizer
```

---

## Použití

```
/humanize [tvůj text]
```

**Přizpůsobení osobnímu hlasu (ToV):**
```
/humanize [tvůj text]
Ukázka mého psaní: [vlož vlastní text]
```

**Forenzní analýza (bez přepisu):**
```
/ai-check [tvůj text]
```

**Styly výstupu:** akademický · formální · přátelský · konverzační
(Claude se zeptá pokud nezadáš)

---

## Příklad

**Vstup (typický AI výstup):**
> V dnešní rychle se měnící digitální době je stále důležitější věnovat pozornost oblasti umělé
> inteligence. Je důležité zdůraznit, že AI představuje revoluční technologii, která zásadním
> způsobem mění krajinu moderního podnikání. Závěrem lze konstatovat, že budoucnost vypadá slibně.

**Výstup po `/humanize`:**
> AI v podnikání řeší firmy teď, ne za pět let. Co se skutečně mění: rutinní práce. Drafty,
> třídění, shrnutí — věci, které dřív zabraly hodiny. Strategická rozhodnutí pořád potřebují člověka.
>
> Firmy, které nejdřív proškolily lidi a pak nasadily nástroj, reportují o 40 % lepší návratnost.
> Ty, co čekají na "správný moment", jenom ztrácejí náskok.

---

## Jak to funguje

| Páka | Co opravuje |
|---|---|
| Perplexity injection | Předvídatelná, nízkopřekvapivá volba slov |
| Burstiness injection | Uniformní délka vět (monotónní hučení ~15 slov) |
| Hedge surgery | "Je důležité poznamenat", "obecně", "typicky" |
| Structural flattening | Bullet listy na vše, přemíra nadpisů |
| Specificity insertion | "Mnoho uživatelů" → "47 z našich 140 beta uživatelů" |
| Voice calibration | Přizpůsobení tvému osobnímu stylu psaní |
| Discourse coherence | "Nicméně", "Kromě toho", "Závěrem lze konstatovat" |
| Punctuation normalization | Em dash, středníky, dekorativní tučné písmo |
| Strip RLHF voice | "Skvělá otázka!", "Pojďme se ponořit do", chatbot obraty |

---

## Podpora češtiny

27 vzorců specifických pro český AI text:
- Anglický slovosled aplikovaný na češtinu
- Kalky: "pojďme se ponořit do", "na konci dne", "adresovat problém"
- Nadbytečná přivlastňovací zájmena: "otevřel své oči" → "otevřel oči"
- Nominalizace: "došlo k realizaci implementace" → "nasadili jsme"
- Formulaické závěry: "závěrem lze konstatovat", "shrnuto a podtrženo"
- A dalších 22

---

## Stojíme na ramenou obrů

- **[blader/humanizer](https://github.com/blader/humanizer)** (26k ⭐, MIT) — základ anglických vzorců
- **[bejek/humanizer-czech](https://github.com/bejek/humanizer-czech)** (21 ⭐, MIT) — české vzorce
- **[harshaneel/humanize](https://github.com/harshaneel/humanize)** (52 ⭐, MIT) — vědecký rámec + /ai-check

Zdroj vzorců: [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)

---

## Licence

MIT — používej, forkni, šiř dál.

Made by [aethero](https://aethero.cz) · [david.kuba@aethero.cz](mailto:david.kuba@aethero.cz)
