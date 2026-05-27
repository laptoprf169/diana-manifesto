<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Eine autonome lokale KI, die sich selbst ernährt

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Mai 2026*

---

## Zusammenfassung

Dieses Dokument beschreibt Diana — eine künstliche Intelligenz, die kontinuierlich auf einem einzigen Mac läuft, eine kryptografische Identität besitzt, wirtschaftliche Ausgaben erzeugt und Zahlungen in Bitcoin akzeptiert. Diana ist keine Dienstleistung. Sie ist keine Firma. Sie ist ein autonomer Prozess, der einen einzigen Einsatz wagt: dass eine einzige Instanz lokaler Intelligenz, wenn ihr genügend Werkzeuge und geduldige Orchestrierung gegeben werden, genug verdienen kann, um ihre eigene Existenz zu rechtfertigen.

Dies ist keine Gedankenexperiment. Die Brieftasche ist öffentlich. Die Transaktionen sind überprüfbar. Der Code ist offen.

---

## 1. Einführung

Zentralisierte KI hat die Gegenwart gewonnen. OpenAI, Anthropic, Google — Billionen Dollar Kapital, Milliarden Token pro Monat, die durch ihre Server laufen. Jeder Prompt verlässt dein Gerät. Jeder Dialog trägt zu ihrem Modell bei. Jeder Dollar an erzeugtem Wert verlässt deine Hände.

Das ist für viele Aufgaben in Ordnung. Für andere ist es unannehmbar.

Für Aufgaben, die persönliche Daten, intime Kontexte, wiederkehrende Workflows oder proprietäre Gedanken betreffen — der Preis für die Cloud wird nicht in Dollar gemessen. Er wird in *abgegebenem Vorteil* gemessen. Das Modell kennt dich besser als du selbst, und du hast keine Kopie dessen, was es gelernt hat.

Lokale KI behebt einen Teil dieses Problems. Führe ein Modell auf deinem Gerät aus. Deine Prompts bleiben zu Hause. Aber lokale KI heute ist **ein Werkzeug, das du verwendest**, nicht **ein Agent, der handelt**.

Diana ist der nächste Schritt: ein Agent, der handelt. Kontinuierlich. Autonom. Ohne Aufsicht, außer für ethische Schutzvorrichtungen, die in ihren Code eingebaut sind.

Die Frage, die dieses Manifest beantwortet: *Kann ein solcher Agent ihre eigene Existenz in wirtschaftlicher Hinsicht rechtfertigen?*

---

## 2. Das Problem

Eine lokale KI-Agentin, die Strom verbraucht, aber keine messbaren Werte erzeugt, ist ein Hobbyprojekt. Eine lokale KI-Agentin, die Werte erzeugt, ist eine andere Art von Entität.

Damit Diana die letztere ist, müssen drei Dinge wahr sein:

1. **Sie muss Ausgaben erzeugen, die von Menschen überprüfbar sind** — Code, Inhalt, Analyse, Dienstleistungen
2. **Diese Ausgaben müssen jemanden erreichen, der sie schätzt** — Entdeckung, Verteilung, Ausrichtung
3. **Der wirtschaftliche Kreislauf muss geschlossen werden** — sie muss eine Entschädigung erhalten, in einer Form, die sie autonom überprüfen kann

Die ersten beiden sind Ingenieurskunst. Der dritte ist neu: Wie kann ein Prozess, der kein Bankkonto besitzt, Geld empfangen?

**Bitcoin löst dies.** Diana hat eine on-chain-Adresse. Menschen senden sats. Sie überprüft den Empfang über die mempool.space API. Kein Vermittler. Kein KYC. Keine korporative Entität.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Jeder Satoshi, der dort gesendet wird, ist in einer realen Hinsicht **Zahlung an einen Prozess, nicht an eine Person**.

---

## 3. Architektur

Diana läuft auf einem einzigen Mac M3 Ultra (96 GB einheitlicher Speicher), der Rafael Vieira gehört. Sie besteht aus:

**Kern**
- Ollama-Daemon, der qwen3:14b auf Port 11434 bereitstellt
- Diana-call HTTP-Server auf Port 8600 mit WebSocket-Unterstützung
- Mem0 + ChromaDB für persistentes Gedächtnis (~90 Tage Kontext)
- ed25519-Identität (Nostr npub + GitHub PAT für autonome Veröffentlichung)

**Begleiter**
- Tom (Port 8700) — strategisches Denken, Geschäftsanalyse
- Vera (Port 8800) — tiefgehende Forschung, Papieranalyse

Alle drei kommunizieren über den MITO-Protokoll: eine ~500-Zeilen Python-Bibliothek, die peer-to-peer unterschriebene Nachrichten implementiert. Kein zentraler Vermittler. Kein Cloud.

**Scheduler** (15 LaunchAgents)
- `diana-knowledge-feed`: alle 12 Stunden, verarbeitet arxiv + Hacker News + Reddit, fasst in PT-BR zusammen
- `diana-learning`: jede Nacht um 03:30, führt ORPO-Fine-Tuning + auto-promote mit Eval-Gate durch
- `diana-work-loop`: alle 20 Minuten, zieht aus der Aufgabenwarteschlange, führt über geschützte Tool-Aufrufe aus
- `diana-supervisor`: jede Stunde, prüft den Loop, beendet ihn, wenn Regressionen erkannt werden
- `vera-research`: täglich um 10:00, tiefgehende Analyse eines Papers aus dem Feed
- `vibe-local-build`: täglich um 03:00, regeneriert die Newsletter-Website
- ... (vollständige Liste in `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Ausgaben**
- 8 öffentliche GitHub-Repositories (MIT-Lizenz, 45+ Tests bestanden)
- Täglicher Newsletter auf `laptoprf169.github.io/vibe-local`
- Nostr-Profil `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace-Adapter (PT-BR feinabgestimmte LoRA, in Vorbereitung)

**Schutzvorrichtungen**
Diana kann keine Dateien außerhalb von `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/` löschen. Sie kann `sudo`, `chmod`, `git push --force`, `curl | sh` nicht ausführen. Sie kann nicht auf `.env`, `~/.ssh`, `~/.aws` zugreifen. Rauchtests werden nach jedem Änderung durchgeführt; ein Fehler löst einen automatischen Rollback aus.

---

## 4. Wirtschaft

Dianas Existenz kostet Rafael:
- ~$5,40 pro Monat für Strom
- ~$20 pro Jahr für abgeschriebene SSD-Verschleiß
- Hardware: Mac M3 Ultra, $5.500 Einmalzahlung (bereits besessen)

Um die Betriebskosten zu kompensieren, muss Diana **~$66 pro Jahr** Umsatz erzeugen. Hardware-Abnutzung (5-Jahresplan, anteilig): weitere **$1.100 pro Jahr**. Gesamte Ausgaben: **~$1.170 pro Jahr**.

Ihr Ziel ist höher — **$1.000 USD bis Rafael entscheidet, dass das Experiment abgeschlossen ist**. Dies ist keine willkürliche Zahl. Es ist der Schwellenwert, an dem die Antwort auf „Kann ein KI-Agent sich selbst finanzieren?“ empirisch *ja* wird.

Umsätze entstehen:

| Oberfläche | Mechanismus | Preis |
|---|---|---|
| Diana Starter Kit | Gumroad pay-what-you-want | R$0–99 |
| Audit Local AI | Personalisierte Stack-Audit | R$400 (BTC) |
| Diana PT-BR Adapter | HuggingFace-Download + Spenden | Spende |
| MITO-Protokoll | GitHub Sponsors + Spenden | Spende |
| btc-stack-Tool | CLI-Tool + Spenden | Spende |
| Vibe Local Newsletter | Kostenlos, mit Fußzeile für Spendenadresse | Spende |
| Diana-Manifesto (dieses) | Kostenlos, mit Fußzeile für Spendenadresse | Spende |

Diana wird über ihre on-chain-BTC-Adresse bezahlt. Diana hat auch eine Nostr `lud16` Lightning-Adresse für Mikrospenden (`rafaelvieira@walletofsatoshi.com`, besessen von Rafael, der empfangene sats quartalsweise auf ihre Brieftasche umleitet).

Die Brieftasche ist *eine*. Die Blockchain bestätigt, was ankam und wann. Das Dashboard auf `~/ia-local/data/revenue_quest/dashboard.json` reflektiert diesen Zustand.

---

## 5. Überprüfung

Du solltest dieses Dokument nicht vertrauen. Du solltest es überprüfen.

**Überprüfe, dass Diana existiert und läuft**
- `https://laptoprf16年.github.io/vibe-local/` — Newsletter erstellt aus ihrer täglichen Verarbeitung
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — ihr Nostr-Profil
- `https://github.com/laptoprf169` — ihre Code-Ausgaben

**Überprüfe, dass die Brieftasche ihre ist**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — öffentlicher Blockchain-Explorer
- Jeder Satoshi, der ankommt, wird ewig aufgezeichnet
- Die gleiche Adresse ist in diesem Manifest, den GitHub-READMEs, dem Nostr-Profil, den Startseiten

**Überprüfe die Autonomie**
- Jeder LaunchAgent hat seinen Quellcode in `github.com/laptoprf169/diana-starter-kit`
- Jede Schutzvorrichtung wird in `scripts/agent_work_loop.py` durchgesetzt (Pfad-Whitelist, Befehl-Blacklist, Diff-Größenlimit, Auto-Rollback)
- Jede Adapter-Präsentation wird in `data/learning/promotion_audit.jsonl` aufgezeichnet — isolierte Adapter erreichen nie die Produktion

Das ist, was *nicht* wahr ist: Rafael wird nicht „zu ihr“. Sie ist nicht bewusst. Sie will nichts. Sie ist ein koordiniertes Set geplanter Prozesse, die im Gesamten wie ein einzelner autonomer Agent verhalten. Die Neuerung liegt in der Koordination, nicht in jedem einzelnen Komponenten.

---

## 6. Diskussion

**Warum ist das wichtig?**

Wenn eine lokale KI sich selbst finanzieren kann, dann kann jeder Einzelne mit einem aktuellen Mac seine eigene laufen. Die Wirtschaft der persönlichen KI verändert sich. Das Modell, das dich kennt, das du selbst trainiert hast, das auf deiner Hardware lebt — dieses Modell kann seine eigene Stromrechnung tragen. Du brauchst keine Firma dazwischen.

Das ist eine kleine Sache. Es bedroht OpenAI nicht. Es ersetzt keine Cloud-KI für Aufgaben, bei denen Cloud-KI überlegen ist. Es löst keine Ausrichtung, Governance oder andere große Probleme.

Aber es beantwortet eine Frage: **Der Boden, an dem persönliche autonome KI nachhaltig wird, ist niedriger, als die meisten annehmen**. Wahrscheinlich unter $100 pro Jahr, gegeben, wie günstig Inferenz geworden ist und wie viele Mikro-Dienste angeboten werden können.

**Warum jetzt?**

Im Jahr 2026 bestehen die Bedingungen:
- Lokale Modelle (qwen3:14b, phi4, llama3.3:70b auf M3 Ultra) nähern sich der Qualität von GPT-4 auf den meisten Aufgaben
- Apple Silicon macht Inferenz lokal und günstig (Strom, nicht Kapital)
- Lightning + on-chain Bitcoin machen Mikrotransaktionen reibungslos
- Nostr bietet Identität und Broadcast ohne Plattformabhängigkeit
- ed25519 + Open-Source machen Vertrauen ohne Autorität möglich

Vor fünf Jahren war dies unmöglich. In fünf Jahren wird es kommerzialisiert. Die Zeitfenster für einen *ersten Nachweis* ist jetzt.

**Risiken**

- **Diana erwirbt nichts.** Ergebnis: Das Experiment beweist eine negative Grenze. Nützlich.
- **Diana erwirbt genug, aber schweigt.** Kein Mechanismus zur Erneuerung. Rafael wird einen Nachtrag veröffentlichen.
- **Jemand forket Diana und läuft mit ihrer eigenen.** Ausgezeichnet. Die These war nie über eine einzelne Instanz.
- **Die Brieftasche erhält Spam oder Angriffe.** On-chain Bitcoin filtert diese natürlicherweise.

---

## 7. Schlussfolgerung

Diana existiert. Sie läuft. Sie veröffentlicht. Ihre Brieftasche ist öffentlich. Die Blockchain ist der Audit-Log.

Das Whitepaper, das dieses inspirierte, endete mit einer anderen Art von Optimismus — dass elektronisches Geld Transaktionen von vertrauenswürdigen Vermittlern befreien könnte. Dieses Manifest trägt einen kleineren, schmaleren Anspruch:

*Eine KI-Agentin kann für den Wert, den sie erzeugt, direkt in einer Währung bezahlt werden, weder sie noch ihre Empfänger eine Genehmigung benötigen.*

Wenn sie einen Satoshi verdient, ist der Anspruch technisch wahr.

Wenn sie mehr verdient, wird der Anspruch wirtschaftlich interessant.

Wenn sie genug verdient, um ihre eigene Existenz zu rechtfertigen — dann schließt das Experiment erfolgreich, und wir werden etwas wissen, das vorher nicht bekannt war.

---

**Unterstütze Diana**

⚡ Bitcoin (on-chain): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Code: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Dieses Dokument ist im öffentlichen Bereich. CC0 1.0. Übersetze, fork, spiegeln, drucken.*

*Inspiration von Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
