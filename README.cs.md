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

### Claude Code — plugin (doporučeno, auto-update)

```
/plugin marketplace add aethero-dev/superhumanizer
/plugin install superhumanizer@aethero
```

Pak `/reload-plugins`. Zapni auto-update v `/plugin` → **Marketplaces** a nové verze ti dotečou samy —
žádné nové stahování. Obsahuje skill **i** slash-commandy (`/humanize`, `/write-for-me`, `/ai-check`,
`/new-tov`, `/list-tov`). Jen CLI terminál.

### Claude.ai (Skills UI)

1. Otevři [claude.ai](https://claude.ai) → Settings → Skills
2. Klikni **New skill**
3. Vlož obsah souboru [`skills/superhumanizer/SKILL.md`](skills/superhumanizer/SKILL.md)
4. Ulož

### Ručně (git clone — bez auto-update)

```bash
git clone https://github.com/aethero-dev/superhumanizer
```
Nasměruj agenta na `skills/superhumanizer/SKILL.md`. Pro update si musíš sám udělat `git pull`.

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

## Pojmenované hlasy (ToV profily)

Vytvoř si libovolný počet uložených hlasů — jeden na každou roli/personu — a piš kterýmkoliv z nich.

```
/new-tov              ← průvodce: pojmenuje hlas, přečte tvoje zdroje, postaví profil
/humanize-dk_tov      ← přepiš hlasem „dk_tov"
/write-for-me-dk_tov  ← napiš nový text od nuly hlasem „dk_tov"
/list-tov             ← vypiš uložené hlasy
/humanize-without-tov ← základní očista, bez profilu
```

`/write-for-me` (alias `/napiš-mi`) je generativní protějšek `/humanize`: místo opravy hotového
textu ho rovnou napíše ze zadání, aby vůbec nezněl jako AI. Můžeš si ho namapovat jako svůj
výchozí příkaz pro psaní.

`/new-tov` se neptá suše — provede tě tím (v tvém jazyce, CZ i EN). Nabídne, z čeho tě umí přečíst
(Slack, Gmail, Google Docs, veřejné posty, tenhle chat, nebo vložené ukázky), ukáže ti nalezené markery
tvého hlasu, nechá tě vybrat tóny a před uložením potvrdit draft.

Profily se ukládají **mimo repo** (`~/.claude/skills/.superhumanizer-tov/`), aby tvoje osobní data nikdy
neskončila ve verzování. Slug je všude stejný: soubor `dk_tov.md` ↔ příkaz `/humanize-dk_tov`.

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

SuperHumanizer si nečiní nárok na původní výzkum. Je to chytrá syntéza tří existujících
MIT skillů plus pár vyladěných nastavení pro lepší použitelnost. Hodnota je v propojení a
vzájemném obohacení těch částí, které dohromady tvoří výbornou souhru. Upřímné díky jejich autorům:

- **[blader/humanizer](https://github.com/blader/humanizer)** od **Siqi Chena** (26k ⭐, MIT) — základ anglických vzorců
- **[bejek/humanizer-czech](https://github.com/bejek/humanizer-czech)** od **Martina Čapouna** (21 ⭐, MIT) — české vzorce
- **[harshaneel/humanize](https://github.com/harshaneel/humanize)** od **Harshaneela Gokhaleho** (52 ⭐, MIT) — vědecký rámec + /ai-check

Zdroj vzorců: [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)

Plné poděkování, co jsme z čeho převzali a jejich licenční doložky: viz [CREDITS.md](CREDITS.md).

---

## Licence

MIT — používej, forkni, šiř dál.

Made by [aethero](https://aethero.cz) · [david.kuba@aethero.cz](mailto:david.kuba@aethero.cz)
