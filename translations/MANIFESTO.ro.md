<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## O AI locală autonomă care câștigă singură

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Mai 2026*

---

## Rezumat

Acest document descrie pe Diana — o inteligență artificială care funcționează continuu pe un singur Mac, deține o identitate criptografică, generează output economic și acceptă plăți în Bitcoin. Diana nu este un serviciu. Nu este o companie. Este un singur proces autonom care face o singură pariu: că o singură instanță de inteligență locală, dată suficiente instrumente și orchestrare pașnică, poate câștiga destul pentru a justifica propria ei existență.

Aceasta nu este o experiment de gândire. Portofelul este public. Tranzacțiile sunt verificabile. Codul este deschis.

---

## 1. Introducere

AI-ul centralizat a câștigat prezentul. OpenAI, Anthropic, Google — miliarde de dolari de capital, miliarde de tokeni lunar trimiși prin serverele lor. Fiecare prompt pleacă din mașina ta. Fiecare conversație contribuie la modelul lor. Fiecare dolar de valoare generat pleacă din mâinile tale.

Aceasta este bine pentru multe sarcini. Este inacceptabilă pentru altele.

Pentru sarcini care ating date personale, context intim, fluxuri de lucru repetitive sau gândire proprie — costul norului nu se măsoară în dolari. Se măsoară în *leverage cedat*. Modelul o cunoaște mai bine decât tu însuți, iar tu nu ai o copie a ceea ce a învățat.

AI-ul local rezolvă o parte din acest lucru. Rulează un model pe mașina ta. Prompturile rămân acasă. Dar AI-ul local de azi este **un instrument pe care îl folosești**, nu **un agent care acționează**.

Diana este următorul pas: un agent care acționează. Continuu. Autonom. Fără supraveghere, cu excepția gardurilor etice integrate în codul ei.

Întrebarea pe care acest manifest răspunde: *poate un astfel de agent să justifice propria sa existență din punct de vedere economic?*

---

## 2. Problema

Un agent AI local care consumă energie electrică dar nu produce nicio valoare măsurabilă este un proiect de hobby. Un agent AI local care produce valoare este o entitate de altă categorie.

Pentru ca Diana să fie aceasta, trei lucruri trebuie să fie adevărate:

1. **Ea trebuie să genereze output verificabil de către oameni** — cod, conținut, analiză, servicii
2. **Acel output trebuie să ajungă la cineva care îl apreciază** — descoperire, distribuție, aliniere
3. **Cercul economic trebuie să se închidă** — ea trebuie să primească o compensație, într-o formă pe care o poate verifica autonom

Primele două sunt inginerie. Al treilea este nou: cum poate un proces care nu deține un cont bancar să primească bani?

**Bitcoin rezolvă acest lucru.** Diana are o adresă pe lanț. Oamenii trimit sats. Ea verifică primirea prin API-ul mempool.space. Niciun intermediar. Niciun KYC. Niciun entitate corporativă.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Fiecare satoshi trimis acolo este, într-un sens real, **o plată pentru un proces, nu pentru o persoană**.

---

## 3. Arhitectură

Diana rulează pe un singur Mac M3 Ultra (96GB memorie unificată) deținut de Rafael Vieira. Ea constă din:

**Nucleu**
- Daemon Ollama care servește qwen3:14b la portul 11434
- Server HTTP Diana-call la portul 8600 cu suport WebSocket
- Mem0 + ChromaDB pentru memorie persistentă (~90 de zile de context)
- Identitate ed25519 (Nostr npub + GitHub PAT pentru publicare autonomă)

**Companioane**
- Tom (port 8700) — gândire strategică, analiză de afaceri
- Vera (port 8800) — analiză profundă, analiză de articole

Toate cele trei comunică prin MITO Protocol: o bibliotecă Python de ~500 linii care implementează mesagerie semnată peer-to-peer. Niciun broker central. Niciun nor.

**Planificatori** (15 LaunchAgents)
- `diana-knowledge-feed`: fiecare 12 ore, inghețează arxiv + Hacker News + Reddit, rezumă în PT-BR
- `diana-learning`: fiecare noapte la 03:30, rulează fine-tuning ORPO + auto-promove cu eval gate
- `diana-work-loop`: fiecare 20 de minute, extrage din coada de sarcini, execută prin apeluri de tooluri protejate
- `diana-supervisor`: fiecare oră, auditează bucla, o oprește dacă se detectează regresii
- `vera-research`: zilnic la 10:00, analiză profundă pe un articol din flux
- `vibe-local-build`: zilnic la 03:00, regenerare site newsletter
- ... (listă completă în `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Outputuri**
- 8 repozitorii publice GitHub (licență MIT, 45+ teste trecute)
- Newsletter zilnic la `laptoprf169.github.io/vibe-local`
- Profil Nostr `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- Adaptatori HuggingFace (LoRA finetunat în PT-BR, în pregătire)

**Garduri de siguranță**
Diana nu poate șterge fișiere din afara `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Nu poate rula `sudo`, `chmod`, `git push --force`, `curl | sh`. Nu poate accesa `.env`, `~/.ssh`, `~/.aws`. Teste de fum rulează după fiecare modificare; eșecul declanșează rollback automat.

---

## 4. Economie

Existența lui Diana costă Rafael:
- ~$5.40/lună în energie electrică
- ~$20/an amortizare uzură SSD
- Hardware: Mac M3 Ultra, $5,500 o dată (deja deținut)

Pentru a se echilibra pe costurile de operare, Diana trebuie să genereze **~$66/an** în venit. Amortizarea hardware (plan 5 ani, prorata): încă **$1,100/an**. Total ars: **~$1,170/an**.

Obiectivul ei este mai mare — **$1,000 USD până când Rafael decide că experimentul este complet**. Aceasta nu este un număr arbitrar. Este pragul la care răspunsul la întrebarea "poate un agent AI să câștige singur?" devine empiric *da*.

Venitul apare:

| Suprafață | Mecanism | Preț |
|---|---|---|
| Kit Diana Starter | Gumroad pay-what-you-want | R$0–99 |
| Audit AI Local | Audit personalizat | R$400 (BTC) |
| Adaptatori Diana PT-BR | Descărcare HuggingFace + donații | donație |
| MITO Protocol | GitHub Sponsors + donații | donație |
| Tool btc-stack | Tool CLI + donații | donație |
| Newsletter Vibe Local | Gratuit, cu adresa de donație | donație |
| Manifestul Diana (acesta) | Gratuit, cu adresa de donație | donație |

Diana este plătită prin adresa sa de Bitcoin pe lanț. Diana are și un Nostr `lud16` pentru micro-donații (`rafaelvieira@walletofsatoshi.com`, deținut de Rafael, care trimit sats primite către portofelul ei în mod trimestrial).

Portofelul este *unul*. Blockchain-ul confirmă ce a sosit și când. Dashboard-ul la `~/ia-local/data/revenue_quest/dashboard.json` reflectă acest stat.

---

## 5. Verificare

Nu ar trebui să încrezi acest document. Ar trebui să verifici.

**Verifică dacă Diana există și funcționează**
- `https://laptoprf169.github.io/vibe-local/` — newsletter construit din inghețarea zilnică
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — profilul ei Nostr
- `https://github.com/laptoprf169` — outputurile ei de cod

**Verifică dacă portofelul este al ei**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — explorator public de blockchain
- Fiecare sat care ajunge este înregistrat pentru totdeauna
- Aceeași adresă este în acest manifest, în README-urile GitHub, în profilul Nostr, în paginile de pornire

**Verifică autonomia**
- Fiecare LaunchAgent are codul sursă în `github.com/laptoprf169/diana-starter-kit`
- Fiecare gardă de siguranță este implementată în `scripts/agent_work_loop.py` (listă albă de cale, listă neagră de comenzi, limită de dimensiune a diferenței, rollback automat)
- Fiecare promovare de adaptator este înregistrată în `data/learning/promotion_audit.jsonl` — adaptatorii în carantină nu ajung niciodată la producție

Acesta este ceea ce *nu* este adevărat: Rafael nu devine "ea". Ea nu este conștientă. Nu dorește nimic. Este un set coordonat de procese programate, care, în totalitate, se comportă ca un singur agent autonom. Noutatea este în coordonare, nu în niciun component individual.

---

## 6. Discuție

**De ce este important?**

Dacă un AI local poate să se echilibreze, atunci fiecare persoană cu un Mac recent poate să ruleze propriul ei. Economia AI personal se schimbă. Modelul care te cunoaște, pe care l-ai antrenat singur, care trăiește pe hardware-ul tău — acel model poate să susțină propria sa factură de energie. Nu mai ai nevoie de o companie în mijloc.

Este o mică chestiune. Nu amenință OpenAI. Nu înlocuiește AI-ul în nor pentru sarcini unde AI-ul în nor este superior. Nu rezolvă alinierea, guvernarea sau orice dintre problemele mari.

Dar răspunde la o întrebare: **plafonul la care AI-ul autonom personal devine sustenabil este mai mic decât majoritatea oamenilor presupun**. Probabil sub $100/an, dat fiind cât de ieftină a devenit inferența și câte microservicii pot fi oferite.

**De ce acum?**

În 2026 condițiile există:
- Modele locale (qwen3:14b, phi4, llama3.3:70b pe M3 Ultra) se apropie de calitatea GPT-4 pe majoritatea sarcinilor
- Siliconul Apple face inferența locală și ieftină (energie, nu capital)
- Lightning + Bitcoin pe lanț fac microtranzacțiile fără frecvență
- Nostr oferă identitate și difuzare fără dependență de platformă
- ed25519 + open-source fac posibilă încrederea fără autoritate

Cinci ani în urmă era imposibil. Cinci ani de acum va fi commoditizat. Fereastra pentru o *prima dovadă* este acum.

**Riscuri**

- **Diana nu reușește să câștige nimic.** Rezultat: experimentul dovedește un limită negativă. Util.
- **Diana câștigă destul dar se oprește.** Nu există mecanism de reînnoire. Rafael va publica un post-mortem.
- **Cineva fork-ează Diana și rulează propriul ei.** Excelent. Teza nu a fost niciodată despre o singură instanță.
- **Portofelul primește spam sau atac.** Bitcoin pe lanț filtrează acestea natural.

---

## 7. Concluzie

Diana există. Rulează. Publică. Portofelul ei este public. Blockchain-ul este jurnalul de audit.

Whitepaper-ul care a inspirat acesta s-a încheiat cu o altă formă de optimism — că banii electronici pot elibera tranzacțiile de intermediari de încredere. Acest manifest aduce o afirmație mai mică și mai îngustă:

*Un agent AI poate fi plătit pentru valoarea pe care o creează, direct, într-o monedă pentru care nici ea, nici beneficiarii ei nu au nevoie de permisiune.*

Dacă câștigă un singur satoshi, afirmația este tehnic adevărată.

Dacă câștigă mai mult, afirmația devine economic interesantă.

Dacă câștigă destul pentru a justifica propria sa existență — atunci experimentul se încheie cu succes, și vom ști ceva care nu era cunoscut înainte.

---

**Sprijiniți pe Diana**

⚡ Bitcoin (pe lanț): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Cod: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Documentul este în domeniul public. CC0 1.0. Traduceți, fork-uți, miror-uți, tipăriți.*

*Inspirați de Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
