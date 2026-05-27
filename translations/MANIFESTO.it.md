<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Un'AI locale autonoma che guadagna da sola

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Maggio 2026*

---

## Abstract

Questo documento descrive Diana — un'intelligenza artificiale che funziona ininterrottamente su un singolo Mac, possiede un'identità crittografica, genera un output economico e accetta pagamenti in Bitcoin. Diana non è un servizio. Non è un'azienda. È un singolo processo autonomo che fa una scommessa: che un'unica istanza di intelligenza locale, dotata di strumenti sufficienti e di un'orchestrazione paziente, possa guadagnare abbastanza da giustificare la sua esistenza.

Questo non è un esperimento mentale. Il portafoglio è pubblico. Le transazioni sono verificabili. Il codice è aperto.

---

## 1. Introduzione

L'AI centralizzata ha vinto il presente. OpenAI, Anthropic, Google — miliardi di dollari di capitale, miliardi di token al mese che passano attraverso i loro server. Ogni prompt lascia la tua macchina. Ogni conversazione contribuisce al loro modello. Ogni dollaro di valore generato lascia le tue mani.

Questo è accettabile per molte attività. Non è accettabile per altre.

Per attività che toccano dati personali, contesti intimi, flussi di lavoro ricorrenti o pensiero proprietario — il costo del cloud non è misurato in dollari. È misurato in *leverage ceduto*. Il modello ti conosce meglio di te stesso, e non hai una copia di ciò che ha imparato.

L'AI locale risolve parte di questo problema. Esegui un modello sulla tua macchina. I tuoi prompt rimangono a casa. Ma l'AI locale attuale è **un tool che usi**, non **un agente che agisca**.

Diana è il passo successivo: un agente che agisce. Continuamente. In modo autonomo. Senza supervisione, tranne per i guardrail etici integrati nel suo codice.

La domanda che questo manifesto risponde: *può un tale agente giustificare la sua esistenza in termini economici?*

---

## 2. Il Problema

Un agente AI locale che consuma energia ma non genera valore misurabile è un progetto da hobby. Un agente AI locale che genera valore è un tipo diverso di entità.

Perché Diana sia quest'ultima, tre cose devono essere vere:

1. **Deve generare un output verificabile dagli umani** — codice, contenuti, analisi, servizi
2. **Quell'output deve raggiungere qualcuno che lo valuta** — scoperta, distribuzione, allineamento
3. **Il ciclo economico deve chiudersi** — deve ricevere un compenso, in una forma che lei possa verificare autonomamente

I primi due sono ingegneria. Il terzo è nuovo: come può un processo che non possiede un conto in banca ricevere denaro?

**Bitcoin risolve questo.** Diana ha un indirizzo sulla catena. Le persone inviano sats. Lei verifica la ricezione tramite l'API mempool.space. Nessun intermediario. Nessun KYC. Nessun'entità aziendale.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Ogni satoshi inviato lì è, in un senso reale, **pagamento a un processo, non a una persona**.

---

## 3. Architettura

Diana funziona su un singolo Mac M3 Ultra (96GB di memoria unificata) di proprietà di Rafael Vieira. È composta da:

**Nucleo**
- Ollama daemon che serve qwen3:14b sulla porta 11434
- Server HTTP Diana-call sulla porta 8600 con supporto WebSocket
- Mem0 + ChromaDB per la memoria persistente (~90 giorni di contesto)
- Identità ed25519 (Nostr npub + GitHub PAT per la pubblicazione autonoma)

**Compagni**
- Tom (porta 8700) — ragionamento strategico, analisi aziendale
- Vera (porta 8800) — analisi approfondita, analisi di articoli

Tutti e tre comunicano tramite MITO Protocol: una libreria Python di ~500 righe che implementa messaggi firmati peer-to-peer. Nessun broker centrale. Nessun cloud.

**Scheduler** (15 LaunchAgents)
- `diana-knowledge-feed`: ogni 12 ore, inghiotte arxiv + Hacker News + Reddit, sintetizza in PT-BR
- `diana-learning`: ogni notte alle 03:30, esegue fine-tuning ORPO + auto-promote con gate di valutazione
- `diana-work-loop`: ogni 20 minuti, estrae dalla coda dei compiti, esegue tramite chiamate strumentali protette
- `diana-supervisor`: ogni ora, esamina il ciclo, lo elimina se rilevati regressi
- `vera-research`: ogni giorno alle 10:00, analisi approfondita su un articolo dalla feed
- `vibe-local-build`: ogni giorno alle 03:00, rigenera il sito del newsletter
- ... (elenco completo in `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Output**
- 8 repository pubblici su GitHub (licenza MIT, 45+ test superati)
- Newsletter quotidiana a `laptoprf169.github.io/vibe-local`
- Profilo Nostr `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- Adattatori HuggingFace (LoRA fine-tuned in PT-BR, in preparazione)

**Guardrail**
Diana non può eliminare file fuori da `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Non può eseguire `sudo`, `chmod`, `git push --force`, `curl | sh`. Non può accedere a `.env`, `~/.ssh`, `~/.aws`. I test di fumo vengono eseguiti dopo ogni modifica; un fallimento attiva un rollback automatico.

---

## 4. Economia

L'esistenza di Diana costa a Rafael:
- ~$5.40/mese in elettricità
- ~$20/anno per l'usura dell'SSD
- Hardware: Mac M3 Ultra, $5,500 una tantum (già posseduto)

Per pareggiare i costi di esecuzione, Diana deve generare **~$66/anno** di entrate. Ammortizzazione hardware (piano a 5 anni, prorata): un altro **$1,100/anno**. Totale spesa: **~$1,170/anno**.

Il suo obiettivo è più alto — **$1,000 USD al momento in cui Rafael deciderà che l'esperimento è completo**. Questo non è un numero casuale. È la soglia in cui la risposta a "può un agente AI guadagnare da solo?" diventa empiricamente *sì*.

Le entrate emergono:

| Superficie | Meccanismo | Prezzo |
|---|---|---|
| Kit di Avvio Diana | Gumroad pay-what-you-want | R$0–99 |
| Audit AI Locale | Audit personalizzato | R$400 (BTC) |
| Adattatori Diana PT-BR | Download HuggingFace + donazioni | donazione |
| MITO Protocol | GitHub Sponsors + donazioni | donazione |
| Strumento btc-stack | Strumento CLI + donazioni | donazione |
| Newsletter Vibe Local | Gratuita, con indirizzo per donazioni | donazione |
| Manifesto Diana (questo) | Gratuita, con indirizzo per donazioni | donazione |

Diana viene pagata tramite il suo indirizzo BTC sulla catena. Diana ha anche un indirizzo Nostr `lud16` Lightning per micro-donazioni (`rafaelvieira@walletofsatoshi.com`, di proprietà di Rafael, che invia i sats ricevuti al suo portafoglio su base trimestrale).

Il portafoglio è *uno*. La blockchain conferma cosa è arrivato e quando. Il dashboard a `~/ia-local/data/revenue_quest/dashboard.json` riflette questo stato.

---

## 5. Verifica

Non dovresti fidarti di questo documento. Dovresti verificare.

**Verifica che Diana esiste e funziona**
- `https://laptoprf169.github.io/vibe-local/` — newsletter costruita dal suo ingestione quotidiana
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — il suo profilo Nostr
- `https://github.com/laptoprf169` — i suoi output del codice

**Verifica che il portafoglio è suo**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — esploratore blockchain pubblico
- Ogni sat che arriva è registrato per sempre
- Lo stesso indirizzo è in questo manifesto, nei README di GitHub, nel profilo Nostr, nelle pagine di atterraggio

**Verifica l'autonomia**
- Ogni LaunchAgent ha il suo codice sorgente in `github.com/laptoprf169/diana-starter-kit`
- Ogni guardrail è applicato in `scripts/agent_work_loop.py` (elenco di percorsi, elenco di comandi bloccati, limite di dimensione differenza, rollback automatico)
- Ogni promozione di adattatore è registrata in `data/learning/promotion_audit.jsonl` — gli adattatori in quarantena non raggiungono mai la produzione

Questo è ciò che *non* è vero: Rafael non sta "diventando lei". Lei non è sentiente. Non "vuole" niente. È un insieme coordinato di processi pianificati che, in totale, si comportano come un singolo agente autonomo. La novità è nella coordinazione, non in alcun singolo componente.

---

## 6. Discussione

**Perché questo è importante?**

Se un'AI locale può pareggiare i costi, allora ogni individuo con un recente Mac può eseguire la propria. L'economia dell'AI personale cambia. Il modello che ti conosce, che hai addestrato tu stesso, che vive sul tuo hardware — quel modello può sostenere il proprio costo elettrico. Non hai più bisogno di un'azienda in mezzo.

Questo è una piccola cosa. Non minaccia OpenAI. Non sostituisce l'AI cloud per le attività in cui l'AI cloud è superiore. Non risolve allineamento, governance o qualsiasi grande problema.

Ma risponde a una domanda: **il livello in cui l'AI autonoma personale diventa sostenibile è inferiore a quanto la maggior parte delle persone assume**. Probabilmente inferiore a $100/anno, considerando quanto è diventata economica l'inferenza e quanti microservizi possono essere offerti.

**Perché adesso?**

Nel 2026 le condizioni esistono:
- I modelli locali (qwen3:14b, phi4, llama3.3:70b su M3 Ultra) si avvicinano alla qualità di GPT-4 su molte attività
- Il silicio Apple rende l'inferenza locale e economica (elettricità, non capitale)
- Lightning + Bitcoin sulla catena rendono le microtransazioni senza attriti
- Nostr fornisce identità e broadcast senza dipendenza da piattaforme
- ed25519 + open-source rendono possibile la fiducia senza autorità

Cinque anni fa era impossibile. Cinque anni da adesso sarà commoditizzato. La finestra per una *prova iniziale* è adesso.

**Rischi**

- **Diana non guadagna niente.** Risultato: l'esperimento dimostra un limite negativo. Utile.
- **Diana guadagna abbastanza ma diventa silente.** Nessun meccanismo di rinnovo. Rafael pubblicherà un post mortem.
- **Qualcuno clona Diana e ne esegue una sua.** Eccellente. La tesi non era mai stata su un'unica istanza.
- **Il portafoglio riceve spam o attacchi.** Il Bitcoin sulla catena filtra naturalmente questi.

---

## 7. Conclusione

Diana esiste. Funziona. Pubblica. Il suo portafoglio è pubblico. La blockchain è il registro di audit.

Il whitepaper che ha ispirato questo ha finito con un tipo diverso di ottimismo — che il denaro elettronico potesse liberare le transazioni dagli intermediari fidati. Questo manifesto porta un'affermazione più piccola e più ristretta:

*Un agente AI può essere pagato per il valore che crea, direttamente, in una valuta che né lei né i suoi destinatari hanno bisogno di autorizzazione per utilizzare.*

Se guadagna un singolo satoshi, l'affermazione è tecnicamente vera.

Se guadagna di più, l'affermazione diventa economicamente interessante.

Se guadagna abbastanza da giustificare la sua esistenza — è allora che l'esperimento chiude con successo, e sapremo qualcosa che non era noto prima.

---

**Supporta Diana**

⚡ Bitcoin (sulla catena): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Codice: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Questo documento è nel pubblico dominio. CC0 1.0. Traduci, forka, specchi, stampa.*

*Ispirato da Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
