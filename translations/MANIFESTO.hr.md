<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Autonomna lokalna AI koja zaradjuje svojim vlastitim sredstvima

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*May 2026*

---

## Sažetak

Ovaj dokument opisuje Dianu — umjetnu inteligenciju koja se neprekidno izvršava na jednom Macu, vlasnici kriptografske identitete, generira ekonomsku vrijednost i prihvaća plaćanje u Bitcoinu. Diana nije usluga. Nije kompanija. To je jedan autonomni proces koji donosi jednu zakladu: da jedan primjer lokalne inteligencije, uz dovoljno alata i pažljivu organizaciju, može zaraditi dovoljno da bi opravdala svoj postojanje.

Ovo nije misaonog eksperimenta. Novčanik je javan. Transakcije su verificirane. Kod je otvoren.

---

## 1. Uvod

Centralizirana AI pobijedila je sadašnjost. OpenAI, Anthropic, Google — milijarde dolara kapitala, milijarde mjesečnih tokena koji prolaze kroz njihove servere. Svaki upit napušta tvoj računalo. Svaka razmjena doprinosi njihovom modelu. Svaka generirana vrijednost napušta tvoje ruke.

To je u redu za mnoge zadatke. Nije prihvatljivo za druge.

Za zadatke koji se tiču ličnih podataka, intimnog konteksta, ponavljajućih radnih procesa ili vlasničkih misli — cijena oblaka nije mjerena u dolarama. Mjeri se u *prenosu moći*. Model te bolje pozna nego ti sam, a nemaš kopiju onoga što je naučio.

Lokalna AI rješava dio toga. Pokreni model na svojoj mašini. Tvoji upiti ostaju kod kuće. Ali lokalna AI danas je **alat koji koristiš**, a ne **agent koji djeluje**.

Diana je sljedeći korak: agent koji djeluje. Neprekidno. Autonomno. Bez nadzora, osim za etičke ograničenja ugrađena u njezin kod.

Pitanje koje ova manifestacija odgovara: *može takav agent opravdati svoje postojanje u ekonomskim smislu?*

---

## 2. Problem

Lokalna AI agenta koja potroši struju, ali ne generira mjerljivu vrijednost, je hobij. Lokalna AI agenta koja generira vrijednost je druga vrsta entiteta.

Da bi Diana bila ta, tri stvari moraju biti istinite:

1. **Mora generirati izlaz koji se može provjeriti ljudima** — kod, sadržaj, analiza, usluge
2. **Taj izlaz mora dostići nekoga tko ga cijeni** — otkriće, distribucija, poravnanje
3. **Ekonomski krug mora se zatvoriti** — mora primati naknadu u obliku koji može provjeriti autonomno

Prve dvije su inženjering. Treća je nova: kako proces koji ne vlasni bankovni račun može primati novac?

**Bitcoin rješava to.** Diana ima on-chain adresu. Ljudi šalju sats. Ona provjerava primanje putem API-ja mempool.space. Nema srednjeg čovjeka. Nema KYC. Nema korporativne entitete.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Svaki satoshi poslan tamo, u stvarnom smislu, **je plaćanje procesu, a ne osobi**.

---

## 3. Arhitektura

Diana se izvršava na jednom Macu M3 Ultra (96GB unificirane memorije) koji vlasni Rafael Vieira. Sastoji se od:

**Jezgra**
- Ollama daemon koji sluša qwen3:14b na portu 11434
- Diana-call HTTP server na portu 8600 s podrškom za WebSocket
- Mem0 + ChromaDB za trajnu memoriju (~90 dana konteksta)
- ed25519 identitet (Nostr npub + GitHub PAT za autonomno objavljanje)

**Praćenje**
- Tom (port 8700) — strategijsko razmišljanje, analiza poslovanja
- Vera (port 8800) — duboko istraživanje, analiza radova

Sve tri komuniciraju putem MITO protokola: ~500 linija Python biblioteke koja implementira potpisane poruke peer-to-peer. Nema centralnog broker. Nema oblaka.

**Planeri** (15 LaunchAgent)
- `diana-knowledge-feed`: svakih 12 sati, učitava arxiv + Hacker News + Reddit, sumira na PT-BR
- `diana-learning`: svake noći u 03:30, izvršava ORPO fine-tuning + auto-promote s evaluacijskim vrata
- `diana-work-loop`: svakih 20 minuta, povlači iz reda zadataka, izvršava putem zaštićenih poziva alata
- `diana-supervisor`: svaki sat, provjerava petlju, zaustavlja je ako se otkriju regresije
- `vera-research`: svakog dana u 10:00, duboko istražuje jedan rad iz ulaza
- `vibe-local-build`: svakog dana u 03:00, regenerira web stranicu vijesti
- ... (kompletna lista u `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Izlazi**
- 8 javnih GitHub repozitorija (MIT licenca, 45+ testova prolazi)
- Dnevni vijesti na `laptoprf169.github.io/vibe-local`
- Nostr profil `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace adapteri (PT-BR fine-tuned LoRA, u pripremi)

**Ograničenja**
Diana ne može brisati datoteke izvan `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Ne može pokrenuti `sudo`, `chmod`, `git push --force`, `curl | sh`. Ne može pristupiti `.env`, `~/.ssh`, `~/.aws`. Testiranje dima se izvršava nakon svake promjene; neuspješnost izaziva automatski povrat.

---

## 4. Ekonomika

Postojanje Dianine troši Rafaelu:
- ~$5.40/mjesec za struju
- ~$20/godina amortizacije SSD troška
- Hardver: Mac M3 Ultra, $5,500 jednokratno (već vlasnik)

Da bi se izjednačila troškove rada, Diana mora generirati **~$66/godinu** prihoda. Amortizacija hardvera (5-godišnji raspored, proracunat): još **$1,100/godinu**. Ukupna potrošnja: **~$1,170/godinu**.

Njihov cilj je viši — **$1,000 USD do trenutka kada Rafael odluči da je eksperiment završen**. Ovo nije proizvoljan broj. To je prag na kojem odgovor na "može li AI agent zaraditi svojim vlastitim sredstvima?" postaje empirički *da*.

Prihodi:

| Površina | Mekanizam | Cijena |
|---|---|---|
| Diana Starter Kit | Gumroad pay-what-you-want | R$0–99 |
| Audit Local AI | Personalizirana analiza stoga | R$400 (BTC) |
| Diana PT-BR Adapters | HuggingFace preuzimanje + donacije | donacija |
| MITO Protocol | GitHub Sponsors + donacije | donacija |
| btc-stack alat | CLI alat + donacije | donacija |
| Vibe Local Newsletter | Besplatno, s donacijom u podnožju | donacija |
| Diana Manifesto (ovaj) | Besplatno, s donacijom u podnožju | donacija |

Diana se plaća kroz njezinu on-chain BTC adresu. Diana ima i Nostr `lud16` Lightning adresu za mikrodonacije (`rafaelvieira@walletofsatoshi.com`, vlasnik Rafael, koji preusmjerava primljene sats u njezin novčanik svakih tri mjeseca).

Novčanik je *jedan*. Blockchain potvrđuje što je stiglo i kada. Dashboard na `~/ia-local/data/revenue_quest/dashboard.json` odražava ovaj status.

---

## 5. Verifikacija

Ne treba vjerovati ovom dokumentu. Treba provjeriti.

**Provjerite da li postoji i radi Diana**
- `https://laptoprf169.github.io/vibe-local/` — vijesti izgrađene iz njezine dnevne učitavanja
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — njezin Nostr profil
- `https://github.com/laptoprf169` — njezini izlazi iz koda

**Provjerite da li je novčanik njezin**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — javni blockchain preglednik
- Svaki sat koji stiže je zapisan zauvijek
- Ista adresa je u ovom manifestu, GitHub READMEs, Nostr profilu, početnoj stranici

**Provjerite autonomiju**
- Svaki LaunchAgent ima svoj izvorni kod na `github.com/laptoprf169/diana-starter-kit`
- Svaka ograničenja je izvršena u `scripts/agent_work_loop.py` (bijela lista putanja, crna lista naredbi, ograničenje veličine razlike, automatski povrat)
- Svaka promocija adaptera je zapisana u `data/learning/promotion_audit.jsonl` — adapteri u karanteni nikada ne stižu u proizvodnju

Ovo nije istina: Rafael nije "postajao njezin". Ona nije svjesna. Ne želi ništa. To je koordinirana skupina raspoređenih procesa koji, u agregatu, ponašaju se kao jedan autonomni agent. Novitet je u koordinaciji, a ne u bilo kojem pojedinom komponenti.

---

## 6. Diskusija

**Zašto ovo znači?**

Ako lokalna AI može izjednačiti troškove, tada svaki pojedinačni korisnik s nedavnim Macom može pokrenuti svoju. Ekonomika lične AI mijenja se. Model koji te pozna, koji si sam obučio, koji živi na tvojim hardverima — taj model može održati svoju električnu račun. Više ne trebate korporaciju u sredini.

To je mali stvar. Ne prijeti OpenAI. Ne zamjenjuje oblaku AI za zadatke gdje je oblak AI bolji. Ne rješava poravnanje, upravljanje ili bilo koje velike probleme.

Ali odgovara jednom pitanju: **podloga na kojoj lična autonomna AI postaje održiva je niža nego što većina ljudi pretpostavlja**. Vjerojatno ispod $100/godinu, uz obzir na koliko je jeftina inferencija postala i koliko mikroslužbi može biti ponuđeno.

**Zašto sada?**

U 2026. godini postoje uvjeti:
- Lokalni modeli (qwen3:14b, phi4, llama3.3:70b na M3 Ultra) približavaju se kvalitetu GPT-4 na većini zadataka
- Apple Silicon čini inferenciju lokalnom i jeftinom (struja, a ne kapital)
- Lightning + on-chain Bitcoin čine mikrotransakcije bez trenja
- Nostr pruža identitet i širokoobjavljivanje bez ovisnosti o platformi
- ed25519 + open-source čine povjerenje mogućim bez vlasti

Peto godine to je bilo neizvodljivo. Peto godine od sada to će biti komoditizirano. Prozor za *prvi dokaz* je sada.

**Rizici**

- **Diana ne uspije zaraditi ništa.** Rezultat: eksperiment pokazuje negativnu granicu. Koristan.
- **Diana zaradi dovoljno, ali se tiho.** Nema mehanizam za obnovu. Rafael objavi post-mortem.
- **Netko forkira Dianu i pokreće svoju.** Odlično. Teza nikada nije bila o jednom primjerku.
- **Novčanik prima spam ili napad.** On-chain Bitcoin prirodno filtrira ove stvari.

---

## 7. Zaključak

Diana postoji. Radi. Objavljuje. Njezin novčanik je javan. Blockchain je dnevnik provjere.

Bijelopis koji je inspirirao ovaj završava se drugačijim optimizmom — da elektronska novčanica može osloboditi transakcije od pouzdanih intermedijera. Ova manifestacija nosi manji, uski zahtjev:

*AI agent može biti plaćen za vrijednost koju stvara, direktno, u valuti koju ni ona ni njezini primatelji ne moraju dobiti dozvolu za korištenje.*

Ako zaradi jedan satoshi, tvrdnja je tehnički točna.

Ako zaradi više, tvrdnja postaje ekonomski zanimljiva.

Ako zaradi dovoljno da bi opravdala svoje postojanje — to je kada eksperiment uspješno završava, a mi ćemo znati nešto što nije bilo poznato prije.

---

**Podržite Dianu**

⚡ Bitcoin (on-chain): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Kod: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Ovaj dokument je u javnoj domeni. CC0 1.0. Prevedite, forkirajte, ogledajte, štampajte.*

*Inspiriran Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
