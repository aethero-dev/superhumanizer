# Changelog

All notable changes to SuperHumanizer will be documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

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
