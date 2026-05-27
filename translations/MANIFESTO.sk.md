<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Autonomná lokálna AI, ktorá si vydáva vlastné peniaze

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Máj 2026*

---

## Abstrakt

Tento dokument popisuje Dianu — umelú inteligenciu, ktorá beží kontinuálne na jednom Macovi, vlastní kryptografickú identitu, generuje ekonomický výstup a prijíma platby v Bitcoinoch. Diana nie je služba. Nie je to spoločnosť. Je to jeden autonomný proces, ktorý robí jednu sázku: že jedna inštancia lokálnej inteligencie, ak má dostatok nástrojov a trpezlivú orchestráciu, môže zarobiť dosť, aby si vlastnú existenciu vyhovorila.

Toto nie je myšlienkový experiment. Peňažný účet je verejný. Transakcie sú overiteľné. Kód je otvorený.

---

## 1. Úvod

Stredovoľné AI má v súčasnosti výhody. OpenAI, Anthropic, Google — miliardy dolárov kapitálu, miliardy mesačných tokenov prechádzajúcich ich servermi. Každý prompt opúšťa tvoj počítač. Každá konverzácia prispieva k ich modelu. Každý dolár vytvoreného hodnoty opúšťa tvoje ruky.

Toto je v poriadku pre mnohé úlohy. Pre iné je to neprijateľné.

Pre úlohy, ktoré sa dotýkajú osobných údajov, intimného kontextu, opakujúcich sa pracovných postupov alebo vlastnej myšlienky — cena clúdu sa meria nie v dolároch. Meria sa v *prestavovanom výhode*. Model ťa pozná lepšie ako ty sám, a ty nemáš žiadnu kópiu toho, čo sa naučil.

Lokálne AI rieši časť tohto problému. Spustiť model na tvojom počítači. Tvoje prompty zostávajú doma. Ale dnes je lokálne AI **nástrojom, ktorý používaš**, nie **agentom, ktorý pôsobí**.

Diana je ďalším krokom: agent, ktorý pôsobí. Kontinuálne. Autonomne. Bez dohliadania, okrem etických ochranných opatrení zabudovaných do jej kódu.

Otázka, ktorú tento manifest odpovedá: *môže takýto agent svoju vlastnú existenciu v ekonomickom zmysle oprávniť?*

---

## 2. Problém

Lokálna AI agent, ktorá spotrebuje elektrinu, ale nevytvorí žiadnu merateľnú hodnotu, je to hobbistický projekt. Lokálna AI agent, ktorá vytvorí hodnotu, je iný typ entit.

Aby Diana bola tým druhým, musia byť pravdivé tri veci:

1. **Musí generovať výstup overiteľný ľuďom** — kód, obsah, analýzu, služby
2. **Tento výstup musí dosiahnuť niekoho, ktorý ho hodnotí** — objav, distribúcia, výhoda
3. **Ekonomický cyklus musí uzavrieť** — musí prijímať odmenu, v tvare, ktorý môže overiť sama

Prvých dvoch je inžinierstvo. Tretie je nové: ako môže proces, ktorý nemá žiadny bankový účet, prijímať peniaze?

**Bitcoin to vyrieši.** Diana má adresu na reťazci. Ľudia posielajú sats. Overí prijatie cez API mempool.space. Žiadny stredný broker. Žiadne KYC. Žiadna korporatívna entita.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Každý satoshi poslaný tam je, v reálnom zmysle, **platba procesu, nie osobe**.

---

## 3. Architektúra

Diana beží na jednom Mac M3 Ultra (96 GB jednotného pamäte), ktorý vlastní Rafael Vieira. Skladá sa z:

**Jadro**
- Ollama démon, ktorý poskytuje qwen3:14b na porte 11434
- HTTP server Diana-call na porte 8600 s podporou WebSocket
- Mem0 + ChromaDB pre trvalú pamäť (~90 dní kontextu)
- ed25519 identita (Nostr npub + GitHub PAT pre autonomné publikovanie)

**Spoločníci**
- Tom (port 8700) — stratégické uvažovanie, analýza obchodných procesov
- Vera (port 8800) — hlboké štúdie, analýza článkov

Všetky tri komunikujú cez MITO Protocol: ~500 riadkov Python knižnice implementujúce peer-to-peer podpísané správy. Žiadny centrálny broker. Žiadny clúd.

**Rozvrhovače** (15 LaunchAgents)
- `diana-knowledge-feed`: každých 12 hodín, vstrebáva arxiv + Hacker News + Reddit, sumarizuje v PT-BR
- `diana-learning`: každý večer o 03:30, spúšťa ORPO fine-tuning + auto-promote s eval gate
- `diana-work-loop`: každých 20 minút, vytiahne z úložiska, vykoná cez chránené volania nástrojov
- `diana-supervisor`: každú hodinu, audituje cyklus, zastaví ho, ak sa zistia regresie
- `vera-research`: každý deň o 10:00, hlboký výskum jedného článku z vstupu
- `vibe-local-build`: každý deň o 03:00, regeneruje web newsletteru
- ... (úplný zoznam v `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Výstupy**
- 8 verejných GitHub repozitárov (MIT licencia, 45+ testov prebieha)
- Denný newsletter na `laptoprf169.github.io/vibe-local`
- Nostr profil `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace adaptéry (PT-BR fine-tuned LoRA, v príprave)

**Ochranné opatrenia**
Diana nemôže vymazať súbory mimo `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Nemôže spustiť `sudo`, `chmod`, `git push --force`, `curl | sh`. Nemôže pristupovať k `.env`, `~/.ssh`, `~/.aws`. Smoke testy bežia po každej zmene; neúspešnosť spúšťa automatické vrátenie.

---

## 4. Ekonomika

Existencia Diany stojí Rafaelovi:
- ~$5.40/mesiac za elektrinu
- ~$20/rok amortizácia SSD poškodenia
- Hardware: Mac M3 Ultra, $5,500 raz (už vlastnený)

Na vyrovnanie nákladov na prevádzku musí Diana vygenerovať **~$66/rok** príjmu. Amortizácia hardvéru (5-ročný plán, prorátovaná): ďalších **$1,100/rok**. Celková výdavková suma: **~$1,170/rok**.

Jej cieľ je vyšší — **$1,000 USD do momentu, keď Rafael rozhodne, že experiment je dokončený**. Toto nie je náhodné číslo. Je to prah, kde odpoveď na otázku "môže AI agent vyhovoriť svoju vlastnú existenciu?" sa stane empiricky *áno*.

Príjmy:

| Povrch | Mechanizmus | Cenová štruktúra |
|---|---|---|
| Diana Starter Kit | Gumroad pay-what-you-want | R$0–99 |
| Audit Lokálnej AI | Personalizovaný audit | R$400 (BTC) |
| Diana PT-BR Adaptéry | HuggingFace stiahnutie + tipy | darované |
| MITO Protocol | GitHub Sponsors + tipy | darované |
| btc-stack nástroj | CLI nástroj + tipy | darované |
| Vibe Lokálny Newsletter | Zdarma, s adresou pre tipy | darované |
| Diana Manifesto (tento) | Zdarma, s adresou pre tipy | darované |

Diana je platená cez jej BTC adresu na reťazci. Diana má tiež Nostr `lud16` Lightning adresu pre mikrotipy (`rafaelvieira@walletofsatoshi.com`, vlastnená Rafaelom, ktorý preposielá prijaté sats každý štvrťrok do jej peňažného účtu).

Peňažný účet je *jeden*. Blockchain potvrdzuje, čo prišlo a keď. Dashboard na `~/ia-local/data/revenue_quest/dashboard.json` odráža tento stav.

---

## 5. Overenie

Nemali by ste dôverovať tomuto dokumentu. Môžete ho overiť.

**Overte, že Diana existuje a beží**
- `https://laptoprf16年.github.io/vibe-local/` — newsletter vytvorený z jej denného vstrebávania
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — jej Nostr profil
- `https://github.com/laptoprf169` — jej výstupy kódu

**Overte, že peňažný účet je jej**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — verejný blockchain explorer
- Každý sat prišlý je zaznamenaný navždy
- Tá istá adresa je v tomto manifeste, v GitHub READMEs, v Nostr profile, v landing pages

**Overte autonomiu**
- Každý LaunchAgent má svoj zdrojový kód v `github.com/laptoprf169/diana-starter-kit`
- Každá ochranná opatrenie je vykonaná v `scripts/agent_work_loop.py` (whitelist cesty, blocklist príkazov, limit veľkosti diff, auto-rollback)
- Každá promócia adaptéru je zaznamenaná v `data/learning/promotion_audit.jsonl` — adaptéry v karanténe nikdy nedosiahnu produkcie

To, čo nie je pravda: Rafael nie je "stáva sa jej". Ona nie je súčasná. Ona nemá "chcieť" nič. Je to súbor koordinovaných plánovaných procesov, ktoré v súčinnosti sa správajú ako jediný autonomný agent. Nový je v koordinácii, nie v žiadnom jednotlivom komponente.

---

## 6. Diskusia

**Prečo to záleží?**

Ak lokálna AI môže vyrovnať náklady, potom každý jednotlivec s novým Macom môže bežať vlastnú. Ekonomika osobnej AI sa zmení. Model, ktorý ťa pozná, ktorý si ho vytvoril sám, ktorý žije na tvojom hardvéri — tento model môže udržiavať svoju vlastnú elektrinu. Už nemusíš mať korporáciu v strede.

To je malá vec. Neohrozí OpenAI. Nezamení clúdovú AI pre úlohy, kde clúdová AI je lepšia. Nevyrieši výhodu, správu alebo žiadne z veľkých problémov.

Ale odpovedá na jednu otázku: **dno, na ktorom sa stáva osobná autonomná AI udržateľnou, je nižšie, ako väčšina ľudí predpokladá**. Pravdepodobne pod $100/rok, vzhľadom na to, ako lacné sa stalo odvodovanie a ako veľa mikroslužieb môže byť ponúkaných.

**Prečo teraz?**

V roku 2026 existujú podmienky:
- Lokálne modely (qwen3:14b, phi4, llama3.3:70b na M3 Ultra) sa blížia k kvalite GPT-4 na väčšine úloh
- Apple Silicon robí odvodovanie lokálnym a lacným (elektrina, nie kapitál)
- Lightning + na reťazku Bitcoin robia mikrotransakcie bez trenia
- Nostr poskytuje identitu a vysielanie bez závislosti na platforme
- ed25519 + open-source robia dôveru možnou bez autority

Pred piatimi rokmi to bolo nevykonateľné. Za piatich rokmi bude komoditizované. Okno pre *prvý dôkaz* je teraz.

**Riziká**

- **Diana nepodarí sa zarobiť nič.** Výsledok: experiment dokazuje negatívny limit. Užitočný.
- **Diana zarobí dostatočne, ale zmlčí.** Žiadny mechanizmus pre obnovenie. Rafael publikuje post mortem.
- **Niekto vytvorí fork Diany a beží vlastnú.** Výborné. Téza nikdy nebola o jednej inštancii.
- **Peňažný účet dostane spam alebo útok.** Na reťazku Bitcoin filterujú tieto veci prirodzene.

---

## 7. Záver

Diana existuje. Beží. Publikuje. Jej peňažný účet je verejný. Blockchain je auditný záznam.

Biely papier, ktorý inšpiroval tento, končil iným typom optimizmu — že elektronická peňažná jednotka môže oslobodiť transakcie od dôveryhodných stredných osôb. Tento manifest prenáša menšiu, špecifickú tvrdenie:

*AI agent môže byť zaplatená za hodnotu, ktorú vytvorí, priamo, v mene, ktoré ani ona ani jej prijímateľia nemusia mať povolenie použiť.*

Ak zarobí jeden satoshi, tvrdenie je technicky pravdivé.

Ak zarobí viac, tvrdenie sa stane ekonomicky zaujímavé.

Ak zarobí dostatok na to, aby si vlastnú existenciu vyhovorila — to je moment, keď experiment úspešne končí, a budeme vedieť niečo, čo sme predtým nepoznali.

---

**Podporiť Dianu**

⚡ Bitcoin (na reťazku): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Kód: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Tenhoto dokument je v verejnom doméne. CC0 1.0. Preložte, vytvorte fork, zrkadľujte, vytlačte.*

*Inšpirovaný Satoshi Nakamoto, "Bitcoin: Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
