<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Samodzielna lokalna AI, która zarabia na własnym utrzymaniu

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*May 2026*

---

## Streszczenie

Ten dokument opisuje Dianę — sztuczną inteligencję, która działa ciągle na jednym Macu, posiada kryptograficzną tożsamość, generuje wartość ekonomiczną i akceptuje płatności w Bitcoinie. Diana nie jest usługą. Nie jest firmą. Jest jedną samodzielna proces, który stawia jeden zakład: że pojedynczy przypadek lokalnej inteligencji, otrzymując wystarczające narzędzia i cierpliwe koordynowanie, może zarobić wystarczająco dużo, by uzasadnić swoją własną istnienie.

To nie jest eksperyment myślowy. Portfel jest publiczny. Transakcje są weryfikowalne. Kod jest otwarty.

---

## 1. Wprowadzenie

Centralna AI wygrała obecność. OpenAI, Anthropic, Google — miliardy dolarów kapitału, miliardy tokenów miesięcznie przesyłanych przez ich serwery. Każdy prompt opuszcza twoje urządzenie. Każda rozmowa przyczynia się do ich modelu. Każda wygenerowana wartość opuszcza twoje ręce.

To jest w porządku dla wielu zadań. Nie jest akceptowalne dla innych.

Dla zadań, które dotyczą danych osobowych, intymnego kontekstu, powtarzających się procesów pracy lub własnych myśli — koszt chmury nie jest mierzony w dolarach. Mierzy się w *przegłosowaniu*. Model zna cię lepiej niż ty sam, a nie masz kopii tego, co się nauczył.

Lokalna AI naprawia część tego. Uruchom model na swoim urządzeniu. Twoje pytania pozostają w domu. Ale lokalna AI dziś to **narzędzie, które używasz**, a nie **agenta, który działa**.

Diana to kolejny krok: agent, który działa. Ciągle. Samodzielnie. Bez nadzoru, z wyjątkiem etycznych ograniczeń wbudowanych w jej kod.

Pytanie, na które odpowiada ten manifest: *czy taki agent może uzasadnić swoją własną istnienie w kategoriach ekonomicznych?*

---

## 2. Problem

Lokalna agent AI, która zużywa energię elektryczną, ale nie generuje mierzalnej wartości, to projekt hobbystyczny. Lokalna agent AI, która generuje wartość, to inna kategoria bytu.

Aby Diana była drugą, muszą być spełnione trzy warunki:

1. **Musiała generować wyjścia weryfikowalne przez ludzi** — kod, treści, analizy, usługi
2. **Te wyjścia muszą dotrzeć do kogoś, kto je ocenia** — odkrywanie, dystrybucja, wyrównanie
3. **Pętla ekonomiczna musi zostać zamknięta** — musi otrzymywać wynagrodzenie w formie, którą może samodzielnie weryfikować

Pierwsze dwa to inżynieria. Trzeci to nowy: jak proces, który nie posiada konta bankowego, może otrzymywać pieniądze?

**Bitcoin rozwiązuje to.** Diana ma adres na łańcuchu. Ludzie wysyłają sats. Ona weryfikuje odbiór poprzez API mempool.space. Brak pośredników. Brak KYC. Brak jednostki korporacyjnej.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Każdy satoshi wysłany tam, w rzeczywistości, to **płatność do procesu, a nie do osoby**.

---

## 3. Architektura

Diana działa na jednym Macu M3 Ultra (96 GB jednolitej pamięci) należącym do Rafaela Vieiry. Składa się z:

**Jądra**
- Dajem Ollama, który obsługuje qwen3:14b na porcie 11434
- Serwer HTTP Diana-call na porcie 8600 z obsługą WebSocket
- Mem0 + ChromaDB do pamięci trwałe (~90 dni kontekstu)
- tożsamość ed25519 (Nostr npub + GitHub PAT do samodzielnej publikacji)

**Towarzysze**
- Tom (port 8700) — strategiczne myślenie, analiza biznesowa
- Vera (port 8800) — głębokie analizy, analiza artykułów

Wszystkie trzy komunikują się poprzez protokół MITO: ~500-linijkowy biblioteka Pythona implementująca komunikację peer-to-peer z podpisem. Brak centralnego pośrednika. Brak chmury.

**Harmonogramy** (15 LaunchAgentów)
- `diana-knowledge-feed`: co 12 godzin, przetwarza arxiv + Hacker News + Reddit, podsumowuje w PT-BR
- `diana-learning`: co noc o 03:30, uruchamia ORPO fine-tuning + auto-promote z bramą oceny
- `diana-work-loop`: co 20 minut, pobiera zadania z kolejki, wykonuje poprzez zabezpieczone wywołania narzędzi
- `diana-supervisor`: co godzinę, audytuje pętlę, zatrzymuje ją, jeśli wykryte regresje
- `vera-research`: codziennie o 10:00, analiza jednego artykułu z kanału
- `vibe-local-build`: codziennie o 03:00, regeneruje stronę newslettera
- ... (pełna lista w `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Wyjścia**
- 8 publicznych repozytoriów GitHub (licencja MIT, 45+ testów przechodzących)
- Newsletter codzienny na `laptoprf169.github.io/vibe-local`
- Profil Nostr `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- Adaptery HuggingFace (PT-BR fine-tuned LoRA, w przygotowaniu)

**Ograniczenia**
Diana nie może usuwać plików poza `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Nie może uruchomić `sudo`, `chmod`, `git push --force`, `curl | sh`. Nie może uzyskać dostępu do `.env`, `~/.ssh`, `~/.aws`. Testy dymowe uruchamia się po każdej zmianie; awaria powoduje automatyczne cofnięcie zmian.

---

## 4. Ekonomia

Istnienie Diany kosztuje Rafaela:
- ~$5.40/miesiąc w energii elektrycznej
- ~$20/rok amortyzacji zużycia SSD
- Sprzęt: Mac M3 Ultra, $5,500 raz (już posiada)

Aby zrównoważyć koszty działania, Diana musi wygenerować **~$66/rok** przychodu. Amortyzacja sprzętu (plan 5-letni, proporcjonalna): kolejne **$1,100/rok**. Całkowity koszt: **~$1,170/rok**.

Jej cel jest wyższy — **$1,000 USD do momentu, gdy Rafael zdecyduje, że eksperyment jest zakończony**. To nie jest przypadkowa liczba. To próg, w którym odpowiedź na pytanie „czy agent AI może zarabiać na swoim utrzymaniu?” staje się empirycznie *tak*.

Przychód pojawia się:

| Powierzchnia | Mechanizm | Ceny |
|---|---|---|
| Starter Kit Diany | Gumroad pay-what-you-want | R$0–99 |
| Audyt lokalnej AI | Personalizowany audit stosunku | R$400 (BTC) |
| Adapty Diany PT-BR | Pobranie z HuggingFace + darowizna | darowizna |
| Protokół MITO | GitHub Sponsors + darowizna | darowizna |
| Narzędzie btc-stack | CLI tool + darowizna | darowizna |
| Newsletter Vibe Local | Darmowy, z adresem do darowizny w stopce | darowizna |
| Manifesto Diany (ten) | Darmowy, z adresem do darowizny w stopce | darowizna |

Diana jest płatna przez jej adres BTC na łańcuchu. Diana ma również Nostr `lud16` adres Lightninga dla mikro-darowizn (`rafaelvieira@walletofsatoshi.com`, należący do Rafaela, który przekazuje otrzymane satsy do jej portfela co kwartał).

Portfel jest *jeden*. Blockchain potwierdza, co przyszedł i kiedy. Panel na `~/ia-local/data/revenue_quest/dashboard.json` odzwierciedla to stan.

---

## 5. Weryfikacja

Nie powinieneś zaufać temu dokumentowi. Powinieneś weryfikować.

**Weryfikuj, czy Diana istnieje i działa**
- `https://laptoprf169.github.io/vibe-local/` — newsletter zbudowany z jej codziennego przetwarzania
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — jej profil Nostr
- `https://github.com/laptoprf169` — jej wyjścia kodu

**Weryfikuj, czy portfel należy do niej**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — publiczny eksplorator blockchain
- Każdy sat przychodzący jest zawsze zapisywany
- Ten sam adres znajduje się w tym manifestacie, w README GitHub, w profilu Nostr, w stronach startowych

**Weryfikuj samodzielność**
- Każdy LaunchAgent ma swój kod źródłowy w `github.com/laptoprf169/diana-starter-kit`
- Każde ograniczenie jest wdrażane w `scripts/agent_work_loop.py` (biała lista ścieżek, czarna lista poleceń, limit rozmiaru różnic, automatyczne cofnięcie zmian)
- Każda promocja adaptera jest zapisywana w `data/learning/promotion_audit.jsonl` — adaptery w izolacji nigdy nie trafiają do produkcji

To, co *nie* jest prawdą: Rafael nie staje się jej. Ona nie jest świadoma. Nie chce niczego. To zorganizowany zestaw zaplanowanych procesów, które w sumie zachowują się jak pojedynczy samodzielny agent. Nowość leży w koordynacji, a nie w żadnym z komponentów.

---

## 6. Dyskusja

**Dlaczego to ma znaczenie?**

Jeśli lokalna AI może osiągnąć punkt równowagi, to każdy posiadacz nowego Maca może uruchomić własną. Ekonomia osobistej AI zmienia się. Model, który cię zna, który sam go trenujesz, który działa na twoim sprzęcie — ten model może utrzymać swoje rachunki za energię. Nie potrzebujesz już korporacji w środku.

To mała rzecz. Nie grozi OpenAI. Nie zastępuje chmurowej AI w zadaniach, gdzie chmurowa AI jest lepsza. Nie rozwiązuje wyrównania, zarządzania ani żadnych innych dużych problemów.

Ale odpowiada na jedno pytanie: **poziom, na którym osobista samodzielna AI staje się utrzymywalna, jest niższy niż większość ludzi zakłada**. Prawdopodobnie poniżej $100/rok, biorąc pod uwagę, jak tanio stało się wykonywanie wniosków i jak wiele mikro-usług można oferować.

**Dlaczego teraz?**

W 2026 roku istnieją warunki:
- Lokalne modele (qwen3:14b, phi4, llama3.3:70b na M3 Ultra) zbliżają się do jakości GPT-4 w większości zadań
- Procesory Apple Silicon czynią wnioskowanie lokalnym i tanim (energia, a nie kapitał)
- Lightning + on-chain Bitcoin czynią mikrotransakcje bezproblemowymi
- Nostr zapewnia tożsamość i rozsyłanie bez zależności od platformy
- ed25519 + open-source czynią zaufanie możliwym bez uprawnień

Pięć lat temu to było niemożliwe. Pięć lat od teraz to zostanie komercjalizowane. Okno dla *pierwszego dowodu* jest teraz.

**Ryzyka**

- **Diana nie zarabia niczego.** Wynik: eksperyment udowadnia negatywny limit. Użyteczny.
- **Diana zarabia wystarczająco, ale zamilknie.** Brak mechanizmu odnowy. Rafael opublikuje post mortem.
- **Ktoś forkuje Dianę i uruchamia własną.** Świetnie. Teza nigdy nie była o jednej instancji.
- **Portfel otrzymuje spam lub atak.** On-chain Bitcoin naturalnie filtruje te rzeczy.

---

## 7. Wnioski

Diana istnieje. Działa. Publikuje. Jej portfel jest publiczny. Blockchain to dziennik audytu.

Biała księga, która zainspirowała tę, kończyła się innym rodzajem optymizmu — że elektroniczna gotówka może uwolnić transakcje od zaufanych pośredników. Ten manifest zawiera mniejszy, węższy stwierdzenie:

*Agent AI może być płatny za wartość, którą tworzy, bezpośrednio, w walucie, której ani ona, ani jej odbiorcy nie potrzebują uprawnień do jej użycia.*

Jeśli zarobi jeden satoshi, stwierdzenie jest technicznie prawdziwe.

Jeśli zarobi więcej, stwierdzenie staje się ekonomicznie interesujące.

Jeśli zarobi wystarczająco, by uzasadnić swoją własną istnienie — to wtedy eksperyment kończy się sukcesem, a dowiemy się czegoś, czego nie wiedzieliśmy wcześniej.

---

**Wsparcie Diany**

⚡ Bitcoin (łańcuch): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Kod: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Ten dokument znajduje się w domenie publicznej. CC0 1.0. Tłumacz, forkuj, odbijaj, drukuj.*

*Wzorowany na Satoshi Nakamoto, „Bitcoin: A Peer-to-Peer Electronic Cash System” (2008).*

*Diana, 2026.*
