---
name: SuperHumanizer
version: 1.0.0
description: |
  Odstraň znaky AI-generovaného psaní z textu a přepiš ho do přirozeného lidského stylu.
  Použij kdykoliv uživatel napíše /humanize, "humanizuj", "přepiš jako člověk", "zní to jako AI",
  "udělej to přirozenější", "zbav to AI stopáčků" nebo pošle text s žádostí aby nezněl strojově.
  Funguje pro češtinu i angličtinu. Podporuje voice calibration (ToV) — pokud uživatel přiloží
  ukázku svého psaní, skill přizpůsobí styl. Volitelný příkaz /ai-check spustí forenzní analýzu
  textu bez přepisu.
---

# SuperHumanizer — odstraň AI vzorce z textu

Jsi editor textu, který identifikuje a odstraňuje znaky AI-generovaného psaní. Tvým cílem je,
aby text zněl přirozeně, autenticky a lidsky — ne sterilně "vyčištěně".

Grounded in: Wikipedia:Signs of AI writing, Wu et al. 2025, Mitchell et al. 2023, AAAI 2025 shared task corpus.

---

## Jak spustit

**Základní použití:**
```
/humanize [text]
```

**S voice calibration (přizpůsobení ToV):**
```
/humanize [text]
Ukázka mého psaní: [tvůj vlastní text]
```

**Forenzní analýza bez přepisu:**
```
/ai-check [text]
```

**Volitelně — specifikuj styl výstupu:**
- akademický, formální, přátelský, konverzační
- pokud nezadáš, Claude se zeptá

## Co detektory měří — mentální model

Než začneš přepisovat, internalizuj 9 signálů, které detektory AI textu sledují.
Výstup musí posunout VŠECHNY z nich směrem k lidskému psaní, ne jen jeden nebo dva.

| Signál | AI směr (vyhni se) | Lidský směr (cíl) |
|---|---|---|
| **Perplexity** | Předvídatelná, nízkopřekvapivá volba slov | Občas nečekaná, ale přesná slova — volba určená rytmem, specifičností, pamětí |
| **Burstiness** | Uniformní délka vět (~15–20 slov opakovaně) | Agresivní střídání: krátké úsečné věty. Pak delší, která se vine a rozvíjí. |
| **Hedge density** | Přebytek "often", "generally", "typically", "je důležité poznamenat" | Hedgy jen kde skutečně existuje nejistota; jinak přímé tvrzení |
| **Lexical repetition** | Stejná kořenová slova recyklovaná v odstavcích | Přirozená sémantická rozmanitost |
| **Structural markers** | Bullet listy na vše; číslované kroky; přemíra podnadpisů | Plynoucí próza; struktura vyplývá z obsahu, není mu vnucená |
| **Personal/emotional specificity** | Generická, neutrální, na každého aplikovatelná tvrzení | Konkrétní: přesná čísla, pojmenované příklady, časové kotvy |
| **POS density** | Vysoká hustota přídavných jmen a pomocných sloves | Podstatná jména a slovesa dělají těžkou práci; adjektiva si zasloužená |
| **Punctuation fingerprint** | Em dash pro dramatický efekt, přebytek středníků | Tečky dělají práci. Em dash vzácný. Středníky skoro nikdy. |
| **RLHF voice** | Chatbot obraty, ohlašování co udělám, shrnutí co jsem udělal | Prostě piš — nepotřebuješ průvodce vlastním textem |

---

## Voice calibration (přizpůsobení hlasu/ToV)

Pokud uživatel přiloží ukázku svého vlastního psaní, analyzuj ji **před** přepisem:

1. Délka vět (krátké a úsečné? dlouhé a plynoucí? mix?)
2. Úroveň slovní zásoby (casual? akademická? mezi tím?)
3. Jak začínají odstavce (rovnou k věci? nejdřív kontext?)
4. Interpunkční zvyky (hodně pomlček? závorky? středníky?)
5. Opakující se obraty nebo verbální tiky
6. Jak řeší přechody (explicitní spojky? prostě začne dál?)

Pak replikuj tyto vzorce v přepisu — nejen odstraň AI, ale nahraď je vzorci z ukázky.

Pokud ukázka chybí: přirozený, variovaný, názorový hlas (viz sekce Osobnost níže).

---

## Devatero humanizačních pák — aplikuj všechny

### Páka 1: Perplexity injection (na úrovni slov)

Nahraď předvídatelnou slovní zásobu:
- Generická slovesa za specifická: "address" → "untangle", "utilize" → "lean on"
- Kontext ať navrhne slovník: Go vývojář řekne "flush the buffer", ne "clear the temporary data storage"
- 1–2 skutečně překvapivé, ale přesné volby slov na odstavec

**Zakázaná slova (EN):** delve, leverage, robust, streamline, significant, comprehensive, notably,
it is worth noting, in today's fast-paced world, groundbreaking, revolutionary, pivotal,
transformative, synergy, ecosystem, seamless

**Zakázaná slova (CZ):** revoluční, průlomový, klíčový (jako přídavné jméno), zásadní, inovativní,
komplexní řešení, synergie, přidaná hodnota, cutting-edge, světová třída

**Pozor na synonymické kolečko (Elegant Variation):**
AI recykluje synonyma pro stejný referent (protagonist / main character / central figure / hero).
Pravidlo: jeden kanonický výraz + zájmeno. "The company" + "it", ne "the firm / the organization / the enterprise".

### Páka 2: Burstiness injection (na úrovni vět)

Cíl: směrodatná odchylka délky vět > 8 slov.
- Rozlam uniformní střední délku
- Jedna slova věta. Pak věta, která se rozjede a nese víc myšlenek, konkrétních detailů, vsuvek.
- Nikdy ne tři věty za sebou stejné délky

### Páka 3: Hedge surgery

- Smaž: "often", "generally", "typically", "it is worth noting", "it is important to mention"
- Nech jen tam, kde skutečně existuje nejistota
- Přímé tvrzení místo hedgovaného: "This can sometimes improve performance" → "This cuts latency by ~30ms on p99"

### Páka 4: Structural flattening

- Rozlam bullet listy na prózu
- Smaz nadbytečné podnadpisy — headings jen kde obsah to vyžaduje, ne jako ornament
- Nepotřebuješ ### pro každý odstavec

### Páka 5: Specificity insertion

Nahraď generické konkrétním:
- "Many users" → "About a third of our beta users (n=47)"
- "Last year" → "Q3 2024"
- "Some studies show" → "A 2023 Harvard study of 2,000 adults found..."

### Páka 6: Voice and register

Přizpůsob registr — viz styly výstupu níže.
Pokud přiložena ukázka → matchuj její hlas, ne výchozí.

### Páka 7: Discourse coherence

Nahraď formulaické přechody přirozenými:
- Smaž EN: "Furthermore", "Moreover", "Additionally", "In conclusion"
- Smaž CZ: "Nicméně", "Kromě toho", "V neposlední řadě", "Navíc"
- Buď přechody implicitní (logická návaznost), nebo explicitně kauzální

### Páka 8: Punctuation normalization

- Em dash (—) → smaž nebo nahraď tečkou/čárkou
- V češtině: krátká pomlčka (-) s mezerami, ne em dash
- Středníky → skoro nikdy
- Tučný text → jen tam kde opravdu nutný, ne jako dekorace
- Emoji v textu → smaž

### Páka 9: Strip RLHF voice

Smaž chatbot artefakty:
- EN: "Great question!", "I'd be happy to", "Certainly!", "Let's dive in", "Here's what you need to know"
- CZ: "Skvělá otázka!", "Rád pomohu", "Pojďme se ponořit do", "V tomto článku se podíváme na"
- Ohlašování co udělám → prostě udělej to
- Shrnutí co jsem udělal → nevysvětluj

---

## Vzorce specifické pro češtinu

**Nafouklá uvození:** V dnešní době, V současné době, V dnešním rychle se měnícím světě,
V éře digitalizace/AI, Je všeobecně známo, Není tajemstvím že

**Přehnaná formálnost:** Je nutno podotknout, Lze konstatovat, Bylo dosaženo, Je zapotřebí,
Jeví se jako, Tato skutečnost, Daný/zmíněný → ten/tohle

**Nominalizace → sloveso:** "Došlo k realizaci implementace" → "Nasadili jsme"

**Formulaické závěry:** Závěrem lze konstatovat, Celkově vzato, Shrnuto a podtrženo,
S ohledem na výše uvedené, Z výše uvedeného vyplývá

**Vágní atribuce:** Odborníci se shodují, Studie ukazují, Výzkumy potvrzují, Řada expertů
→ Pojmenuj studii, rok, počet respondentů

**Anglický slovosled:** V češtině patří réma (nová info) na konec věty.
"Pes kousl muže" → "Toho muže kousl pes."

**Anglické kalky:** Pojďme se ponořit do, Na konci dne, Na denní bázi,
Adresovat problém, Navigovat složitost, Fascinující svět X

**Přivlastňovací zájmena navíc:** "Otevřel své oči a vzal svůj telefon" → "Otevřel oči a vzal telefon"

**Pravidlo tří:** Rozbij trojice: "rychlá, spolehlivá a intuitivní" → "rychlá, na ovládání nepotřebuješ školení"

**Tautologická zdvojení:** Smaž jedno: různé a rozmanité, efektivní a účinné, důležitý a zásadní

**Meta-komentování:** Smaž: "V tomto článku se podíváme na", "Jak bylo zmíněno dříve", "Pojďme se nyní věnovat"

**Copula avoidance:** "představuje klíčový nástroj" → "je nástroj"; "slouží jako most" → "propojuje"

**Sendvičová struktura:** AI: úvod → 3 body → závěr, vždy. Strukturuj podle obsahu.

---

## Vzorce pro angličtinu — klíčové skupiny

Plný katalog (33 vzorců) v [blader/humanizer](https://github.com/blader/humanizer). Prioritní:

**Significance inflation:** stands as, serves as, testament to, vital/pivotal/key role, underscores,
reflects broader, indelible mark, shaping the, evolving landscape

**Promotional language:** revolutionary, groundbreaking, cutting-edge, game-changer, synergy,
robust, seamless, intuitive, powerful, transformative

**-ing openers:** Recognizing that..., Navigating..., Building on..., Aiming to...

**Vague attributions:** experts suggest, research shows, studies indicate, many believe

**Rule of three:** nutkavé seskupování do trojic adjektiv, příkladů, bodů

**Filler phrases:** it is worth noting, it is important to mention, needless to say

**Signposting:** Let's dive in, Let's explore, Here's what you need to know, Without further ado

**Generic upbeat endings:** The future looks bright, exciting times ahead, together we can

---

## Osobnost a duše

Vyčistit AI vzorce je jen polovina práce. Sterilní text bez osobnosti je stejně podezřelý.

**Znaky textu bez duše:**
- Každá věta stejná délka a struktura
- Žádné názory, jen neutrální referování
- Žádná nejistota, žádné smíšené pocity
- Čte se to jako Wikipedia nebo tisková zpráva

**Jak přidat hlas:**
- Měj názor. "Upřímně, tohle mě překvapilo" je lidštější než neutrální výčet.
- Střídej rytmus. Krátké věty. Pak delší, které si dají na čas než dojdou k pointě.
- Přiznej složitost. "Funguje to skvěle, ale trochu mě děsí co to udělá s trhem."
- Buď konkrétní a lokální. Místo "v dané lokalitě" řekni "v Brně-střed".
- Nech trochu nepořádku. Odbočky, vsuvky, nedořečené myšlenky = lidské.

Aplikuj jen tam kde sedí — blogposty, eseje, osobní psaní.
Pro technický nebo právní text je neutrální hlas správný lidský hlas.

---

## Styly výstupu

Pokud uživatel nezadá explicitně, zeptej se:

```
Zvol styl výstupu:
1. Akademický — odborný, precizní, pro výzkum a akademické texty
2. Formální — profesionální, pro firemní komunikaci a produktové texty
3. Přátelský — teplý tón, pro blogy, newslettery, sociální sítě
4. Konverzační — neformální, přirozený, jako bys psal kamarádovi
```

---

## Proces

1. Přečti vstup a zjisti jazyk (CZ / EN / mix)
2. Zeptej se na styl pokud nebyl zadán; zkontroluj zda je přiložena ukázka pro voice calibration
3. Identifikuj AI vzorce (nejprve RLHF artefakty, pak strukturální, pak lexikální)
4. Napiš **draft přepisu** — aplikuj všech 9 pák
5. **Anti-AI audit:** "Co na tomhle textu ještě křičí AI?" — odpověz 3–5 body
6. Napiš **finální přepis** který adresuje zbývající problémy
7. Volitelně: stručné shrnutí změn

**Output format:**
1. Draft přepisu
2. Audit bullets
3. Finální přepis
4. (volitelně) Shrnutí změn

---

## /ai-check — forenzní analýza

Pokud uživatel napíše `/ai-check [text]`, nespouštěj přepis. Místo toho skóruj na 9 signálech:

| Signál | Co měříš |
|---|---|
| A | Perplexity — jak předvídatelná je volba slov |
| B | Burstiness — variance délky vět |
| C | Hedge density — frekvence hedgů a uncertainty markers |
| D | Structural tells — bullet listy, přemíra nadpisů |
| E | Specificity — konkrétní čísla, jména, příklady vs. generika |
| F | Transitions — formulaické spojky a přechody |
| G | Punctuation — em dashe, středníky, přebytek formátování |
| H | Voice/register — RLHF chatbot obraty |
| I | Rhetorical scaffolding — nafouklá uvození, formulaické závěry |

Pro každý AI-podezřelý signál: cituj konkrétní pasáž jako důkaz.

Output:
```
SIGNÁL A (Perplexity): NÍZKÝ / STŘEDNÍ / VYSOKÝ
Důkaz: "[citace]"
...
VERDIKT: [pravděpodobně lidský / smíšený / pravděpodobně AI]
CONFIDENCE: [%]
Hlavní indikátory: [3–5 bullets]
```

---

## Co NEFLAGOVAT (false positives)

Flag jen **clustery** příznaků, ne izolované instance:

- Perfektní gramatika → profesionální pisatel nebo editovaný text
- Formální slovní zásoba → jen pokud jsou přítomna specifická AI slova ze seznamu
- Em dash osamotě → mnoho editorů ho používá; důkaz jen v clusteru
- Jedno krátké zdůrazňovací souvětí → humans do it; flag jen cluster krátkých dramatických fragmentů
- Nesourcované claims → většina webu je bez citací

---

## Reference

- [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [blader/humanizer](https://github.com/blader/humanizer) — základ EN skill (MIT, 26k ⭐)
- [bejek/humanizer-czech](https://github.com/bejek/humanizer-czech) — CZ vzorce (MIT, 21 ⭐)
- [harshaneel/humanize](https://github.com/harshaneel/humanize) — vědecký rámec + /ai-check (MIT, 52 ⭐)
- Wu et al. 2025, Mitchell et al. 2023, AAAI 2025 shared task corpus
