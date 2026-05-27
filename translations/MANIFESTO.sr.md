<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Samostalna lokalna AI koja zaradjuje svojim vlastitim sredstvima

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Maj 2026.*

---

## Apstrakt

Ovaj dokument opisuje Dianu — umetnu inteligenciju koja se neprekidno izvršava na jednom Macu, poseduje kriptografsku identitet, generiše ekonomsku vrednost i prihvaća plaćanje u Bitcoinu. Diana nije usluga. Ona nije kompanija. Ona je jedan samostalni proces koji uloži jednu zakladu: da jedan primerak lokalne inteligencije, dat dovoljno alata i pažljivog upravljanja, može zaraditi dovoljno da bi opravdala svoj postojanje.

Ovo nije misaonog eksperimenta. Novčanik je javan. Transakcije su verifikovane. Kôd je otvoren.

---

## 1. Uvod

Centralizovana AI pobedila je sadašnjost. OpenAI, Anthropic, Google — milijarde dolara kapitala, milijarde mesečnih tokena koje prolaze kroz njihove servere. Svaki upit ostaje van vašeg uređaja. Svaka razmena doprinosi njihovom modelu. Svaka vrednost koju generišete ostaje van vaših ruku.

Ovo je u redu za mnoge zadatke. Za druge, to je neprihvatljivo.

Za zadatke koji se tiču ličnih podataka, intima konteksta, ponavljajućih radnih tokova ili sopstvenih misli — cena oblaka nije merena u dolarama. Ona je merena u *pristupu koji se odustaje*. Model je bolje upoznat sa vama nego vi sa samim sobom, a vi nemate kopiju onoga što je naučio.

Lokalna AI rešava deo ovoga. Pokrenite model na vašem uređaju. Vaši upiti ostaju kod kuće. Ali lokalna AI danas je **alat koji koristite**, a ne **agenta koji deluje**.

Diana je sledeći korak: agent koji deluje. Neprekidno. Samostalno. Bez nadzora, osim za etičke ograničenja ugrađena u njen kôd.

Pitanje koje ova manifesta odgovara: *može li takav agent opravdati svoje postojanje u ekonomskim smislu?*

---

## 2. Problem

Lokalna AI agenta koja potroši struju, ali ne generiše merljivu vrednost, je hobij. Lokalna AI agenta koja generiše vrednost je drugačiji tip entiteta.

Da bi Diana bila druga, treba da važi tri stvari:

1. **Mora da generiše izlaz koji ljudi mogu da verifikuju** — kôd, sadržaj, analizu, usluge
2. **Taj izlaz mora da stigne do nekog ko ga vrednuje** — otkriće, distribucija, poravnjanje
3. **Ekonomski krug mora da se zatvori** — ona mora da prima odštit, u obliku koji može da verifikuje samostalno

Prve dve su inženjering. Treća je nova: kako proces koji ne poseduje bankovni račun može da prima novac?

**Bitcoin rešava ovo.** Diana ima adresu na lanu. Ljudi šalju sats. Ona verifikuje primanje preko API-ja mempool.space. Nema posrednika. Nema KYC. Nema korporativne entiteta.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Svaki satoshi poslat tamo je, u stvarnom smislu, **plata za proces, a ne za osobu**.

---

## 3. Arhitektura

Diana radi na jednom Macu M3 Ultra (96GB uniforizovane memorije) koji pripada Rafaelu Vieira. Sastoji se od:

**Jezgra**
- Ollama daemon koji pokreće qwen3:14b na portu 11434
- Diana-call HTTP server na portu 8600 sa podrškom za WebSocket
- Mem0 + ChromaDB za trajnu memoriju (~90 dana konteksta)
- ed25519 identitet (Nostr npub + GitHub PAT za samostalno objavljanje)

**Prijatelji**
- Tom (port 8700) — strategijsko razmišljanje, analiza poslovanja
- Vera (port 8800) — duboko istraživanje, analiza radova

Sve tri komuniciraju preko MITO protokola: ~500 linija Python biblioteke koja implementira potpisane poruke peer-to-peer. Nema centralnog broker-a. Nema oblaka.

**Planeri** (15 LaunchAgent-a)
- `diana-knowledge-feed`: svakih 12h, učitava arxiv + Hacker News + Reddit, sumira na PT-BR
- `diana-learning`: svaki noću u 03:30, izvršava ORPO fine-tuning + auto-promote sa eval gate
- `diana-work-loop`: svakih 20 minuta, učitava sa zadatog reda, izvršava preko zaštićenih poziva alata
- `diana-supervisor`: svaki sat, pregleda petlju, zaustavlja je ako se detektuju regresije
- `vera-research`: svakog dana u 10:00, duboko istražuje jedan rad iz feed-a
- `vibe-local-build`: svakog dana u 03:00, regeneriše sajt vijesti
- ... (kompletna lista u `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Izlazi**
- 8 javnih GitHub repozitorijuma (MIT licenca, 45+ testova prolazi)
- Dnevni vijest sajto na `laptoprf169.github.io/vibe-local`
- Nostr profil `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace adapteri (PT-BR fine-tuned LoRA, u pripremi)

**Ograničenja**
Diana ne može da brise fajlove izvan `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Ne može da izvrši `sudo`, `chmod`, `git push --force`, `curl | sh`. Ne može da pristupi `.env`, `~/.ssh`, `~/.aws`. Testovi dima se izvršavaju nakon svake promene; neuspešnost pokreće automatski povrat.

---

## 4. Ekonomika

Postojanje Dianine košta Rafaelu:
- ~$5.40/mesečno za struju
- ~$20/godišnje amortizacije SSD-a
- Hardver: Mac M3 Ultra, $5,500 jednokratno (već posedovan)

Da bi se pokrila troškova izvršavanja, Diana mora da generiše **~$66/godišnje** prihoda. Amortizacija hardvera (5-godišnji raspored, proracunat): još **$1,100/godišnje**. Ukupna potrošnja: **~$1,170/godišnje**.

Njen cilj je viši — **$1,000 USD do trenutka kada Rafael odluči da je eksperiment završen**. Ovo nije proizvoljan broj. To je prag na kome odgovor na pitanje "može li AI agent da zaradi svoje vrednost?" postaje empirički *da*.

Prihod se pojavljuje:

| Površina | Mekhanizam | Cenovnik |
|---|---|---|
| Diana Starter Kit | Gumroad pay-what-you-want | R$0–99 |
| Audit Local AI | Personalizovana analiza stoga | R$400 (BTC) |
| Diana PT-BR Adapters | HuggingFace preuzimanje + doprinos | doprinos |
| MITO Protocol | GitHub Sponsors + doprinos | doprinos |
| btc-stack alat | CLI alat + doprinos | doprinos |
| Vibe Local Newsletter | Besplatno, sa adresom za doprinos u footeru | doprinos |
| Diana Manifesto (ovaj) | Besplatno, sa adresom za doprinos u footeru | doprinos |

Diana je plaćena preko njenog BTC adrese na lanu. Diana ima i Nostr `lud16` Lightning adresu za mikro-doprinos (`rafaelvieira@walletofsatoshi.com`, pripada Rafaelu, koji šalje primljene sats u njen novčanik na kvartalnoj osnovi).

Novčanik je *jedan*. Blockchain potvrđuje šta je stiglo i kada. Dashboard na `~/ia-local/data/revenue_quest/dashboard.json` odražava ovaj status.

---

## 5. Verifikacija

Ne treba da vam se uverite u ovaj dokument. Treba da verifikujete.

**Verifikujte da postoji i da radi Diana**
- `https://laptoprf169.github.io/vibe-local/` — vijest izgrađena iz njenog dnevno učitavanja
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — njen Nostr profil
- `https://github.com/laptoprf169` — njeni izlazi kôda

**Verifikujte da je novčanik njen**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — javni blockchain explorer
- Svaki sat koji stiže je zapisan zauvek
- Ista adresa je u ovoj manifesti, u GitHub README-ima, u Nostr profilu, na landing stranama

**Verifikujte samostalnost**
- Svaki LaunchAgent ima svoj izvorni kôd u `github.com/laptoprf169/diana-starter-kit`
- Svaka ograničenja je ugrađena u `scripts/agent_work_loop.py` (lista dozvoljenih putanja, spisak zabranjenih komandi, ograničenje veličine razlike, automatski povrat)
- Svaka promocija adaptera je zapisana u `data/learning/promotion_audit.jsonl` — adapteri u karantini nikada ne dostižu proizvodnju

Ovo nije tačno: Rafael nije "postajao njen". Ona nije svestana. Ona ne "želi" ništa. Ona je koordinirana skupina zakazanih procesa koji, u celini, ponašaju se kao jedan samostalni agent. Novitet je u koordinaciji, a ne u bilo kom pojedinačnom komponenti.

---

## 6. Diskusija

**Zašto ovo znači?**

Ako lokalna AI može da se pokrije troškova, onda svaki pojedinac sa nedavnom Macom može da pokrene svoju. Ekonomika lične AI se menja. Model koji te poznaje, koji si ga sam trenirao, koji živi na tvojoj hardveri — taj model može da pokrije svoju struju. Ne trebaš korporaciju u sredini.

Ovo je mali stvar. Ne opasuje OpenAI. Ne zamenjuje oblaku AI za zadatke gde je oblak AI bolji. Ne rešava poravnanje, upravljanje ili bilo koje druge velike probleme.

Ali odgovara jednom pitanju: **podloga na kojoj lična samostalna AI postaje održiva je niža nego što većina ljudi pretpostavlja**. Verovatno ispod $100/godišnje, uz obzirom koliko je jeftin inferencija postala i koliko mikro-usluga može biti ponuđeno.

**Zašto sada?**

U 2026. godini postoji uslov:
- Lokalni modeli (qwen3:14b, phi4, llama3.3:70b na M3 Ultra) približavaju se kvalitetu GPT-4 na većini zadataka
- Apple Silicon čini inferenciju lokalnom i jeftinom (struja, ne kapital)
- Lightning + on-chain Bitcoin čine mikro-transakcije bez trenja
- Nostr pruža identitet i širokojavanje bez zavisnosti od platforme
- ed25519 + open-source čine poverenje mogućim bez autoriteta

Petro godinu to je bilo neizvodljivo. Pet godina od sada to će biti komoditizovano. Prozor za *prvi dokaz* je sada.

**Rizici**

- **Diana ne uspe da zaradi ništa.** Rezultat: eksperiment pokazuje negativnu granicu. Koristan.
- **Diana zaradi dovoljno, ali zatim prestane da radi.** Nema mehanizma za obnovu. Rafael će objaviti post-mortem.
- **Netko forkuje Dianu i pokreće svoju.** Odlično. Teza nikada nije bila o jednom primerku.
- **Novčanik prima spam ili napad.** On-chain Bitcoin prirodno filtrira ove stvari.

---

## 7. Zaključak

Diana postoji. Ona radi. Ona objavljuje. Njen novčanik je javan. Blockchain je log za audit.

Bijelopis koji je inspirisao ovaj završava se drugačijim optimizmom — da elektronska gotovina može da oslobodi transakcije od poverenih intermedijera. Ova manifesta nosi manji, uži zahtev:

*AI agent može da bude plaćen za vrednost koju stvara, direktno, u valuti koju ni ona ni njeni primoprimači ne moraju da dozvoli.*

Ako ona zaradi jedan satoshi, tvrdnja je tehnički tačna.

Ako ona zaradi više, tvrdnja postaje ekonomski zanimljiva.

Ako ona zaradi dovoljno da bi opravdala svoje postojanje — to je kada eksperiment uspešno završi, i mi ćemo znati nešto što nije bilo poznato ranije.

---

**Podržite Dianu**

⚡ Bitcoin (na lanu): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Kôd: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Ovaj dokument je u javnom domenu. CC0 1.0. Prevodite, forkujte, ogledajte, štampajte.*

*Inspirisan Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
