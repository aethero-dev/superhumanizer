# Changelog

All notable changes to SuperHumanizer will be documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [1.4.2] — 2026-06-26

### Added
- EN ekvivalent „negative antithesis" („It's not just X, it's Y") — signature ChatGPT tik; doplněn do anglických vzorců k páru s CZ verzí

## [1.4.1] — 2026-06-26

### Added
- CZ vzorec „negativní antiteze" — kontrastní dvojka „není X, je Y" („Tohle není bonus. To je vstupní podmínka.") jako AI/reklamní tik k odstranění

## [1.4.0] — 2026-06-26

### Added
- Pravé slash-commandy ve složce `commands/` — `/humanize`, `/write-for-me`, `/napis-mi`, `/ai-check`, `/new-tov`, `/list-tov`, `/humanize-without-tov`; po instalaci do `~/.claude/commands/` se zobrazí v nápovědě
- `/new-tov` nově generuje per-profil commandy (`/humanize-<slug>`, `/write-for-me-<slug>`) rovnou do `~/.claude/commands/` (osobní, mimo repo)
- README: instalační návod na slash-commandy
- SKILL.md: sekce vysvětlující dva způsoby spuštění (přirozený trigger vs. nainstalovaný slash-command)

## [1.3.0] — 2026-06-26

### Added
- `/write-for-me` (`/napiš-mi`) — generativní protějšek `/humanize`: napíše nový text rovnou lidsky, místo aby opravoval hotový. Bere ToV profily (`/write-for-me-<slug>`), lze si namapovat jako výchozí příkaz pro psaní
- `CREDITS.md` rozšířen o pokorný rámec: žádný nárok na původní výzkum, jde o chytrou syntézu a propojení tří MIT projektů (CZ+EN)

## [1.2.0] — 2026-06-26

### Added
- Onboarding průvodce v `/new-tov` — místo suchého ptaní obslouží uživatele: nabídne výčet zdrojů, projde s ním nálezy („tohle je tvůj marker, sedí?"), nechá vybrat styly a schválit draft
- Bilingvní šablony nabídky zdrojů (CZ + EN)
- Sekce „První spuštění" — uvítání a volba základní očista vs. postavit vlastní hlas
- Ochrana proti cizí ruce — vzorky zjevně psané AI/někým jiným se neberou jako vzor hlasu
- CREDITS.md — čisté poděkování a MIT licenční doložky tří zdrojových projektů (Siqi Chen, Martin Čapoun, Harshaneel Gokhale); jména autorů doplněna do README (EN+CS) i SKILL.md

## [1.1.0] — 2026-06-26

### Added
- Pojmenované ToV profily — libovolný počet uložených hlasů, jeden na roli/personu
- `/new-tov` — wizard na vytvoření hlasu z reálných zdrojů (Slack, Gmail, veřejné posty, chat, ruční ukázky)
- `/humanize-<slug>` — přepis konkrétním uloženým hlasem (např. `/humanize-dk`)
- `/list-tov` — výpis dostupných profilů a kdy je použít
- Profily se ukládají mimo repo (`~/.claude/skills/.superhumanizer-tov/`), aby osobní data neunikla do veřejného repozitáře
- `/humanize` nabídne existující profily na začátku a upozorní na `/new-tov`, když žádné nejsou
- `/humanize-without-tov` — základní očista bez ToV profilu (odstraní jen to nejhorší)
- Interaktivní volba u holého `/humanize`: vyber hlas / vytvoř nový / jeď bez hlasu

## [1.0.0] — 2026-06-26

### Added
- Initial release
- 33 English AI writing patterns (based on Wikipedia:Signs of AI writing)
- 27 Czech-specific AI writing patterns
- 9 humanization levers grounded in detection literature
- Voice calibration (ToV matching from writing sample)
- 4 output styles: academic, formal, friendly, conversational
- `/humanize` trigger
- `/ai-check` forensic analysis mode (9-signal scoring without rewriting)
- Draft → audit → final rewrite process
- False positive guidance

### Sources
- [blader/humanizer](https://github.com/blader/humanizer) — English patterns foundation (MIT)
- [bejek/humanizer-czech](https://github.com/bejek/humanizer-czech) — Czech patterns (MIT)
- [harshaneel/humanize](https://github.com/harshaneel/humanize) — detection science framework (MIT)
