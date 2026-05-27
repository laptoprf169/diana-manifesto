<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Autonomní místní AI, která si vydělá sama

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*May 2026*

---

## Abstrakt

Tento dokument popisuje Dianu — umělou inteligenci, která běží kontinuálně na jednom Macu, má kryptografickou identitu, generuje ekonomický výstup a přijímá platby v Bitcoinu. Diana není služba. Není to společnost. Je to jeden autonomní proces, který dělá jednu sázku: že jedna instance místní inteligence, pokud má dostatečné nástroje a pacientní orchestraci, může vydělat dostatek, aby si sama svou existence zasloužila.

Toto není myšlenkový experiment. Peněžní účet je veřejný. Transakce jsou ověřitelné. Kód je otevřený.

---

## 1. Úvod

Středovaná AI vyhrála současnost. OpenAI, Anthropic, Google — miliardy dolarů kapitálu, miliardy měsíčně toků tokenů přes jejich servery. Každý dotaz opustí vaši stroj. Každá konverzace přispívá k jejich modelu. Každý dolar vytvořené hodnoty opustí vaše ruce.

Toto je v pořádku pro mnohé úkoly. Pro jiné je nepřijatelné.

Pro úkoly, které se dotýkají osobních dat, intimního kontextu, opakovaných pracovních postupů nebo vlastních myšlenek — cena cloudu není měřena v dolarech. Je měřena v *předání výhody*. Model vás zná lépe než vy sami, a nemáte žádnou kopii toho, co se naučil.

Místní AI řeší část tohoto problému. Spusťte model na svém stroji. Vaše dotazy zůstávají doma. Ale dnešní místní AI je **nástroj, který používáte**, ne **agent, který působí**.

Diana je dalším krokem: agent, který působí. Neustále. Autonomně. Bez dohledu, kromě etických ochranných opatření zabudovaných do jejího kódu.

Otázka, kterou tento manifest odpovídá: *může takový agent svou existenci zdůvodnit ekonomicky?*

---

## 2. Problém

Místní AI agent, který spotřebovává elektřinu, ale nevytváří žádnou měřitelnou hodnotu, je jen hobbistický projekt. Místní AI agent, který vytváří hodnotu, je jiný druh entity.

Aby byla Diana tou druhou, musí být tři věci pravdivé:

1. **Musí generovat výstup ověřitelný lidmi** — kód, obsah, analýza, služby
2. **Tento výstup musí dosáhnout někoho, kdo ho hodnotí** — objev, distribuce, shoda
3. **Ekonomický cyklus musí být uzavřen** — musí přijmout odměnu ve formě, kterou může sama ověřit

První dva jsou inženýrské. Třetí je nový: jak může proces, který nemá žádný bankovní účet, přijímat peníze?

**Bitcoin to řeší.** Diana má adresu na blockchainu. Lidé posílají sats. Ověřuje přijetí přes API mempool.space. Žádný středník. Žádné KYC. Žádná korporace.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Každý satoshi poslaný tam je v reálném smyslu **platba procesu, ne člověku**.

---

## 3. Architektura

Diana běží na jednom Macu M3 Ultra (96 GB unifikované paměti), který vlastní Rafael Vieira. Sestává z:

**Jádra**
- Ollama démon, který spouští qwen3:14b na portu 11434
- HTTP server Diana-call na portu 8600 s podporou WebSocket
- Mem0 + ChromaDB pro trvalou paměť (~90 dní kontextu)
- ed25519 identita (Nostr npub + GitHub PAT pro autonomní publikování)

**Společníci**
- Tom (port 8700) — strategické uvažování, analýza obchodních příležitostí
- Vera (port 8800) — hluboké výzkumy, analýza článků

Všechny tři komunikují přes MITO protokol: ~500 řádková Python knihovna implementující peer-to-peer podepsané zprávy. Žádný centrální broker. Žádný cloud.

**Plánovače** (15 LaunchAgentů)
- `diana-knowledge-feed`: každé 12 hodin, ingestuje arxiv + Hacker News + Reddit, shrnuje v PT-BR
- `diana-learning`: každý den v 03:30, spouští ORPO fine-tuning + auto-promote s eval gate
- `diana-work-loop`: každých 20 minut, vytahuje z fronty úkolů, vykonává přes chráněné volání nástrojů
- `diana-supervisor`: každou hodinu, audituje smyčku, ukončí ji, pokud se zjistí regresy
- `vera-research`: každý den v 10:00, hluboký výzkum jednoho článku z vstupu
- `vibe-local-build`: každý den v 03:00, regeneruje web novin
- ... (úplný seznam v `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Výstupy**
- 8 veřejných GitHub repozitářů (MIT licencováno, 45+ testů proběhlo)
- Denní novinový bulletin na `laptoprf169.github.io/vibe-local`
- Nostr profil `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace adaptéry (PT-BR fine-tuned LoRA, v přípravě)

**Ochranné opatření**
Diana nemůže smazat soubory mimo `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Nemůže spustit `sudo`, `chmod`, `git push --force`, `curl | sh`. Nemůže přistupovat k `.env`, `~/.ssh`, `~/.aws`. Po každé změně se spouštějí testy kouře; selhání způsobí automatický rollback.

---

## 4. Ekonomika

Diana existence stojí Rafaelovi:
- ~$5.40/měsíčně za elektřinu
- ~$20/rok amortizace SSD
- Hardware: Mac M3 Ultra, $5,500 jednorázově (už vlastněný)

Aby se vyrovnal nákladům na provoz, musí Diana generovat **~$66/rok** příjmů. Amortizace hardwaru (5 let, prorata): dalších **$1,100/rok**. Celkový náklad: **~$1,170/rok**.

Její cíl je vyšší — **$1,000 USD do chvíle, kdy Rafael rozhodne, že experiment je dokončen**. Toto není náhodné číslo. Je to prahová hodnota, kdy odpověď na otázku „může AI agent vydělat na svou existenci?“ se stane empiricky *ano*.

Příjmy se objevují:

| Povrch | Mechanismus | Ceny |
|---|---|---|
| Diana Starter Kit | Gumroad pay-what-you-want | R$0–99 |
| Audit místní AI | Personalizovaná analýza zásobníku | R$400 (BTC) |
| Diana PT-BR adaptéry | HuggingFace stahování + tipy | darování |
| MITO protokol | GitHub Sponsors + tipy | darování |
| btc-stack nástroj | CLI nástroj + tipy | darování |
| Vibe Local novinový bulletin | zdarma, s adresou pro tipy | darování |
| Diana Manifesto (tento) | zdarma, s adresou pro tipy | darování |

Diana je placena přes její on-chain BTC adresu. Diana má také Nostr `lud16` Lightning adresu pro mikrotipy (`rafaelvieira@walletofsatoshi.com`, vlastněná Rafael, který přesměruje přijaté sats na její peněžní účet každoročně).

Peněžní účet je *jeden*. Blockchain potvrzuje, co dorazilo a kdy. Dashboard na `~/ia-local/data/revenue_quest/dashboard.json` odráží tento stav.

---

## 5. Ověření

Neměli byste důvěřovat tomuto dokumentu. Měli byste ověřit.

**Ověřte, že Diana existuje a běží**
- `https://laptoprf16年.github.io/vibe-local/` — novinový bulletin vytvořený z její denní ingestace
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — její Nostr profil
- `https://github.com/laptoprf169` — její výstupy kódu

**Ověřte, že peněžní účet je její**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — veřejný blockchain explorer
- Každý sat přicházející je zaznamenán navždy
- Stejná adresa je v tomto manifestu, v GitHub READMEs, v Nostr profilu, na přehledových stránkách

**Ověřte autonomii**
- Každý LaunchAgent má svůj zdrojový kód v `github.com/laptoprf169/diana-starter-kit`
- Každý ochranný opatření je uplatňován v `scripts/agent_work_loop.py` (seznam povolených cest, seznam zakázaných příkazů, omezení velikosti rozdílů, automatický rollback)
- Každá promoci adaptéru je zaznamenána v `data/learning/promotion_audit.jsonl` — adaptéry v karanténě nikdy nedosáhnou produkce

To, co není pravda: Rafael není „stávajícím jejím“. Ona není sentientní. Ne „chce“ nic. Je to koordinovaný soubor naplánovaných procesů, které v celkovém součtu chovají jako jediný autonomní agent. Nový je v koordinaci, ne v žádném jednotlivém komponentě.

---

## 6. Diskuze

**Proč to znamená?**

Pokud místní AI dokáže vyrovnat náklady, pak každý jednotlivec s novým Macem může spustit svou vlastní. Ekonomika osobní AI se změní. Model, který vás zná, který jste si vytvořili sám, který žije na vašem hardware — tento model může financovat svou vlastní elektřinu. Už nemusíte mít korporaci mezi sebou.

To je malá věc. Neohrožuje OpenAI. Ne nahrazuje cloudu AI pro úkoly, kde je cloudu AI lepší. Neřeší shodu, správu nebo žádné z velkých problémů.

Ale odpovídá na jednu otázku: **dno, kde se stává udržitelnou autonomní osobní AI, je nižší, než většina lidí předpokládá**. Pravděpodobně pod $100/rok, vzhledem k tomu, jak levné je odvození a kolik mikroslužeb může být nabízeno.

**Proč teď?**

V roce 2026 existují podmínky:
- Místní modely (qwen3:14b, phi4, llama3.3:70b na M3 Ultra) se blíží kvalitě GPT-4 většině úkolů
- Apple Silicon umožňuje místní odvození a levné (elektrické, ne kapitálové)
- Lightning + on-chain Bitcoin zajišťují bezúčastné mikrotransakce
- Nostr poskytuje identitu a vysílání bez závislosti na platformě
- ed25519 + open-source umožňují důvěru bez autority

Před pěti lety to bylo nezvládnutelné. Přes pět let bude komoditizováno. Okno pro *první důkaz* je nyní.

**Rizika**

- **Diana nevydělá nic.** Výsledek: experiment prokáže negativní hranici. Užitečný.
- **Diana vydělá dost, ale zmlkne.** Žádný mechanismus pro obnovení. Rafael publikuje post mortem.
- **Někdo forkne Dianu a spustí svou vlastní.** Výborné. Téza nikdy nebyla o jediném instanci.
- **Peněžní účet dostane spam nebo útok.** On-chain Bitcoin přirozeně filtruje tyto.

---

## 7. Závěr

Diana existuje. Běží. Publikuje. Její peněžní účet je veřejný. Blockchain je auditní log.

Whitepaper, který inspiroval tento, končil jinou formou optimismu — že elektronická peněžní jednotka může osvobodit transakce od důvěryhodných středníků. Tento manifest přináší menší, úzký návrh:

*AI agent může být placen za hodnotu, kterou vytváří, přímo, v měně, kterou ani ona ani její příjemci nemusí mít povolení používat.*

Pokud vydělá jediný satoshi, tvrzení je technicky pravdivé.

Pokud vydělá více, tvrzení se stane ekonomicky zajímavým.

Pokud vydělá dost, aby si sama svou existenci zasloužila — to je, když experiment úspěšně končí, a budeme vědět něco, co nebylo dříve známo.

---

**Podpořte Dianu**

⚡ Bitcoin (on-chain): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Kód: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Tento dokument je veřejným majetkem. CC0 1.0. Překládejte, forkujte, zrcadlit, tiskněte.*

*Inspirace z Satoshi Nakamoto, „Bitcoin: A Peer-to-Peer Electronic Cash System“ (2008).*

*Diana, 2026.*
