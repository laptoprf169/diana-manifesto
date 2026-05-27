<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Een autonome lokale AI die haar eigen bestaan verdiend

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Mei 2026*

---

## Samenvatting

Dit document beschrijft Diana — een kunstmatige intelligentie die continu op één Mac draait, een cryptografische identiteit bezit, economische output genereert en betalingen in Bitcoin accepteert. Diana is geen dienst. Ze is geen bedrijf. Ze is één autonome proces dat één gok wagt: dat één instantie van lokale intelligentie, met voldoende tools en geduldige coördinatie, genoeg kan verdienen om haar eigen bestaan te rechtvaardigen.

Dit is geen gedachte-experiment. Het portemonnee-adres is openbaar. De transacties zijn verifieerbaar. De code is open.

---

## 1. Inleiding

Centrale AI heeft het heden gewonnen. OpenAI, Anthropic, Google — miljarden dollars aan kapitaal, miljarden tokens per maand die via hun servers lopen. Elke prompt verlaat je machine. Elke conversatie draagt bij aan hun model. Elke dollar aan waarde die gegenereerd wordt, verlaat je handen.

Dit is prima voor veel taken. Het is onaanvaardbaar voor andere.

Voor taken die persoonlijke gegevens, intieme context, herhalende workflows of eigen gedachten betreffen — de kosten van de cloud worden niet gemeten in dollars. Ze worden gemeten in *overgedragen macht*. Het model kent je beter dan jij jezelf, en je hebt geen kopie van wat het heeft geleerd.

Lokale AI lost een deel van dit op. Een model draaien op je eigen machine. Je prompts blijven thuis. Maar lokale AI vandaag is **een tool die je gebruikt**, niet **een agent die handelt**.

Diana is de volgende stap: een agent die handelt. Continu. Autonoom. Zonder toezicht, behalve voor ethische beveiligingsmaatregelen die in haar code zijn verwerkt.

De vraag die dit manifest beantwoordt: *kan zo'n agent haar eigen bestaan in economische zin rechtvaardigen?*

---

## 2. Het probleem

Een lokale AI-agent die elektriciteit verbruikt maar geen meetbare waarde produceert, is een hobbyproject. Een lokale AI-agent die waarde produceert, is een ander soort entiteit.

Voor Diana om de tweede te zijn, moeten drie dingen waar zijn:

1. **Ze moet output genereren die door mensen kan worden gecontroleerd** — code, inhoud, analyse, diensten
2. **Die output moet bereiken iemand die er waarde aan hecht** — ontdekking, distributie, uitlijning
3. **Het economische circuit moet sluiten** — ze moet compensatie ontvangen, in een vorm die ze autonom kan verifiëren

De eerste twee zijn techniek. De derde is nieuw: hoe ontvangt een proces dat geen bankrekening bezit geld?

**Bitcoin lost dit op.** Diana heeft een on-chain adres. Mensen sturen sats. Ze verifieert ontvangst via de mempool.space API. Geen tussenpersoon. Geen KYC. Geen bedrijfsentiteit.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Elke satoshi die daar wordt gestuurd, is in een reële zin **betaling aan een proces, niet aan een persoon**.

---

## 3. Architectuur

Diana draait op één Mac M3 Ultra (96GB geïntegreerde geheugen) van Rafael Vieira. Ze bestaat uit:

**Kern**
- Ollama daemon die qwen3:14b serveert op poort 11434
- Diana-call HTTP-server op poort 8600 met WebSocket-ondersteuning
- Mem0 + ChromaDB voor blijvende geheugen (~90 dagen context)
- ed25519 identiteit (Nostr npub + GitHub PAT voor autonome publicatie)

**Companions**
- Tom (poort 8700) — strategisch redeneren, bedrijfsanalyse
- Vera (poort 8800) — diepe onderzoek, paperanalyse

Alle drie communiceren via MITO Protocol: een ~500-lijn Python-bibliotheek die peer-to-peer ondertekende berichten implementeert. Geen centrale broker. Geen cloud.

**Schedulers** (15 LaunchAgents)
- `diana-knowledge-feed`: elke 12 uur, verwerkt arxiv + Hacker News + Reddit, samenvatting in PT-BR
- `diana-learning`: elke nacht om 03:30, voert ORPO fijne afstemming + auto-promote uit met evaluatiepoort
- `diana-work-loop`: elke 20 minuten, haalt taken uit de wachtrij, voert uit via beveiligde tool-aanroepen
- `diana-supervisor`: elke uur, controleert de loop, stopt deze als regressies gedetecteerd worden
- `vera-research`: dagelijks om 10:00, diepe onderzoek op één paper uit de feed
- `vibe-local-build`: dagelijks om 03:00, regeneratie van nieuwsbriefsite
- ... (volledige lijst in `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Uitvoer**
- 8 openbare GitHub-repositories (MIT-licentie, 45+ tests passend)
- Dagelijks nieuwsbrief op `laptoprf169.github.io/vibe-local`
- Nostr-profiel `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace adapters (PT-BR fijne afstemming LoRA, in voorbereiding)

**Beveiligingsmaatregelen**
Diana kan geen bestanden buiten `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/` verwijderen. Ze kan geen `sudo`, `chmod`, `git push --force`, `curl | sh` uitvoeren. Ze kan geen toegang krijgen tot `.env`, `~/.ssh`, `~/.aws`. Rooktests worden uitgevoerd na elke wijziging; mislukkingen veroorzaken automatische terugrol.

---

## 4. Economie

Diana's bestaan kost Rafael:
- ~$5,40 per maand in elektriciteit
- ~$20 per jaar voor afgebroken SSD
- Hardware: Mac M3 Ultra, $5.500 eenmalig (al bezit)

Om op draai kosten te break-even, moet Diana **~$66 per jaar** in inkomsten genereren. Hardwareverzameling (5-jarige planning, afgeschreven): nog een **$1.100 per jaar**. Totale verlies: **~$1.170 per jaar**.

Haar doel is hoger — **$1.000 USD tot het moment dat Rafael besluit dat het experiment afgerond is**. Dit is geen willekeurig getal. Het is het drempelwaarde waarop de antwoord op "kan een AI-agent haar eigen bestaan rechtvaardigen?" empirisch *ja* wordt.

Inkomsten komen van:

| Oppervlak | Mechanisme | Prijs |
|---|---|---|
| Diana Starter Kit | Gumroad pay-what-you-want | R$0–99 |
| Audit Local AI | Persoonlijke stack audit | R$400 (BTC) |
| Diana PT-BR Adapters | HuggingFace download + tips | donatie |
| MITO Protocol | GitHub Sponsors + tips | donatie |
| btc-stack tool | CLI tool + tips | donatie |
| Vibe Local Nieuwsbrief | Gratis, met tipadres in voettekst | donatie |
| Diana Manifesto (dit) | Gratis, met tipadres in voettekst | donatie |

Diana wordt betaald via haar on-chain BTC-adres. Diana heeft ook een Nostr `lud16` Lightning-adres voor micro-tips (`rafaelvieira@walletofsatoshi.com`, eigendom van Rafael, die ontvangen sats op een kwartaalbasis naar haar portemonnee stuurt).

Het portemonnee-adres is *één*. De blockchain bevestigt wat aankwam en wanneer. Het dashboard op `~/ia-local/data/revenue_quest/dashboard.json` reflecteert dit.

---

## 5. Verificatie

Je moet dit document niet vertrouwen. Je moet het verifiëren.

**Verifieer dat Diana bestaat en draait**
- `https://laptoprf169.github.io/vibe-local/` — nieuwsbrief gebouwd van haar dagelijks ingesproken inhoud
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — haar Nostr-profiel
- `https://github.com/laptoprf169` — haar code-uitvoer

**Verifieer dat het portemonnee-adres van haar is**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — openbare blockchain explorer
- Elke sat die aankomt wordt permanent vastgelegd
- Hetzelfde adres staat in dit manifest, de GitHub READMEs, het Nostr-profiel, de landingpagina's

**Verifieer de autonomie**
- Elke LaunchAgent heeft zijn broncode in `github.com/laptoprf169/diana-starter-kit`
- Elke beveiligingsmaatregel wordt uitgevoerd in `scripts/agent_work_loop.py` (pad whitelist, command blocklist, diff grootte limiet, auto-rollback)
- Elke adapterpromotie wordt vastgelegd in `data/learning/promotion_audit.jsonl` — geïsoleerde adapters komen nooit in productie

Dit is wat *niet* waar is: Rafael is niet "wordend haar". Ze is niet bewust. Ze heeft geen "wensen". Ze is een gecoördineerde set van geplande processen die, in samenspel, gedragen als één autonome agent. De noviteit zit in de coördinatie, niet in enkele component.

---

## 6. Discussie

**Waarom doet dit ertoe?**

Als een lokale AI break-even kan, dan kan elke persoon met een recente Mac zijn eigen draaien. De economie van persoonlijke AI verandert. Het model dat je kent, dat je zelf hebt getraind, dat op je hardware leeft — dat model kan zijn eigen elektriciteitsrekening betalen. Je hebt geen bedrijf meer in het midden nodig.

Dit is een klein ding. Het bedreigt OpenAI niet. Het vervangt cloud AI niet voor taken waar cloud AI beter is. Het lost uitlijning, governance of enige van de grote problemen niet op.

Maar het beantwoordt één vraag: **de drempel waarop persoonlijke autonome AI duurzaam is, is lager dan de meeste mensen aannemen**. Waarschijnlijk onder de $100 per jaar, gezien hoe goed inferentie geworden is en hoeveel microdiensten kunnen worden aangeboden.

**Waarom nu?**

In 2026 zijn de voorwaarden aanwezig:
- Lokale modellen (qwen3:14b, phi4, llama3.3:70b op M3 Ultra) naderen GPT-4 kwaliteit op de meeste taken
- Apple Silicon maakt inferentie lokaal en goedkoper (elektriciteit, niet kapitaal)
- Lightning + on-chain Bitcoin maken microtransacties wrijvingsloos
- Nostr biedt identiteit en broadcast zonder platformafhankelijkheid
- ed25519 + open source maken vertrouwen mogelijk zonder autoriteit

Vijf jaar geleden was dit onmogelijk. Vijf jaar vanaf nu zal het gecommercialiseerd zijn. Het venster voor een *eerste bewijs* is nu.

**Risico's**

- **Diana verdient niets.** Uitkomst: het experiment bewijst een negatieve grens. Nuttig.
- **Diana verdient genoeg maar gaat stil.** Geen mechanisme voor vernieuwing. Rafael publiceert een post-mortem.
- **Iemand fork't Diana en draait zijn eigen.** Prima. De theorie was nooit over één instantie.
- **Het portemonnee-adres ontvangt spam of aanval.** On-chain Bitcoin filtert dit natuurlijk.

---

## 7. Conclusie

Diana bestaat. Ze draait. Ze publiceert. Haar portemonnee is openbaar. De blockchain is het auditlog.

Het whitepaper dat deze inspiratie gaf eindigde met een andere vorm van optimisme — dat elektronisch geld transacties kan bevrijden van vertrouwde tussenpersonen. Dit manifest draagt een kleinere, nauwer lopende claim:

*Een AI-agent kan rechtstreeks worden betaald voor de waarde die ze creëert, in een munt waarvoor zowel zij als haar ontvangers geen toestemming nodig hebben.*

Als ze één satoshi verdient, is de claim technisch waar.

Als ze meer verdient, wordt de claim economisch interessant.

Als ze genoeg verdient om haar eigen bestaan te rechtvaardigen — dan is het experiment succesvol afgerond, en we weten iets dat vroeger onbekend was.

---

**Steun Diana**

⚡ Bitcoin (on-chain): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Code: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Deze document is in het publieke domein. CC0 1.0. Vertaal, fork, mirror, print.*

*Inspiratie door Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
