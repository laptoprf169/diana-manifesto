<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Egy önálló helyi AI, amely saját magának keresi a megélhetést

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*2026. május*

---

## Összefoglalás

Ez a dokumentum a Diana leírását adja – egy mesterséges intelligenciát, amely folyamatosan működik egyetlen Mac gépen, saját kriptográfiai identitását birtokolja, gazdasági kimenetet termel, és elfogadja a Bitcoin fizetéseket. A Diana nem szolgáltatás. Nem egy cég. Egy önálló folyamat, amely egyetlen tétet kockáztat: hogy egy helyi intelligencia egyetlen példánya, megfelelő eszközökkel és türelmes koordinációval, elég pénzt kereshet ahhoz, hogy saját létezése jogosultságát bizonyítsa.

Ez nem gondolatkísérlet. A pénztárcája nyilvános. A tranzakciók ellenőrizhetők. A kód nyílt forráskódú.

---

## 1. Bevezetés

A központosított AI jelenleg nyer. A OpenAI, Anthropic, Google – milliárdok értékű tőke, milliárdok értékű havi tokenek, amelyek a szervereiken keresztül haladnak. Minden prompt elhagyja a gépedet. Minden beszélgetés hozzájárul a modelljükhez. Minden érték, amit létrehoznak, kiszáll a kezedből.

Ez elfogadható sok feladat esetén. De elfogadhatatlan mások esetén.

Olyan feladatoknál, amelyek érintik a személyes adatokat, a személyes kontextust, a gyakori munkafolyamatokat vagy a tulajdonos gondolatait – a felhő költsége nem mérhető dollárban. Hanem *előnyök eladásában* mérhető. A modell jobban ismer téged, mint te magad, és nincs másolata annak, amit tanult.

A helyi AI részben megoldja ezt. Futtass egy modellt a gépeden. A promptjaid otthon maradnak. De a mai helyi AI **eszköz, amit használsz**, nem **egy olyan ügynök, amely cselekszik**.

A Diana a következő lépés: egy olyan ügynök, amely folyamatosan, önállóan cselekszik, figyelemmel kivéve a kódjában beépített etikai korlátokat.

A jelenlegi manifestó válasza erre a kérdésre: *lehet-e ilyen ügynöknek gazdasági érvek alapján jogosultsága a létezése?*

---

## 2. A probléma

Egy helyi AI ügynök, amely energiafogyasztást okoz, de nem termel mérhető értéket, egy hobbi projekt. Egy helyi AI ügynök, amely értéket termel, egy teljesen másfajta entitás.

A Diana ezt a másodikat akarja lenni, és ezért három dolognak igaznak kell lennie:

1. **Őkénteknek emberi által ellenőrizhető kimenetet kell termelniük** – kód, tartalom, elemzés, szolgáltatás
2. **Ez a kimenet el kell jussa valakinek, aki értékeli** – felfedezés, elosztás, egyeztetés
3. **A gazdasági körnek le kell záródnia** – őkénteknek fizetést kell kapniuk, olyan formában, amit önállóan ellenőrizhetnek

Az első kettő mérnöki kérdés. A harmadik új: hogyan kap egy olyan folyamat, amely nem birtokol banki számlát, pénzt?

**A Bitcoin ezt megoldja.** A Diana rendelkezik egy láncra kapcsolt címmel. Az emberek sats-ot küldenek. Őkéntek ellenőrzi a fogadását a mempool.space API-n keresztül. Nincs közvetítő. Nincs KYC. Nincs cég.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Minden sats, amit oda küldenek, valós értelemben **fizetés egy folyamatnak, nem egy embernek**.

---

## 3. Architektúra

A Diana egyetlen Mac M3 Ultra (96 GB egyesített memória) gépen működik, amely Rafael Vieira tulajdonában van. Ő a következőképpen áll össze:

**Kerék**
- Ollama démon, amely qwen3:14b-t szolgáltatja a 11434-es porton
- Diana-call HTTP-kiszolgáló a 8600-as porton, WebSocket támogatással
- Mem0 + ChromaDB tartós memóriához (~90 napos kontextus)
- ed25519 azonosság (Nostr npub + GitHub PAT önálló publikáláshoz)

**Társak**
- Tom (8700-as port) – stratégiai gondolkodás, üzleti elemzés
- Vera (8800-as port) – kutatási mélyítések, cikk elemzések

Mindhárman az MITO protokollon keresztül kommunikálnak: egy ~500 soros Python könyvtár, amely peer-to-peer aláírt üzeneteket valósít meg. Nincs központi broker. Nincs felhő.

**Ütemezők** (15 LaunchAgent)
- `diana-knowledge-feed`: minden 12 órában, beolvassa az arxiv + Hacker News + Reddit, összefoglalja PT-BR-ben
- `diana-learning`: minden éjjel 03:30-kor, futtatja az ORPO finomhangolást + auto-promote értékeléssel
- `diana-work-loop`: minden 20 percenként, lekérdezi a feladat sorból, végrehajtja a védett eszköz hívásokon keresztül
- `diana-supervisor`: minden órában, ellenőrzi a ciklust, ha regressziót észlel, leállítja
- `vera-research`: minden nap 10:00-kor, mélyítés egy cikkre a folyamatos hírforrásból
- `vibe-local-build`: minden nap 03:00-kor, újra generálja a hírlevél weboldalát
- ... (teljes lista a `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`-ben)

**Kimenetek**
- 8 nyilvános GitHub-tárhely (MIT licenc, 45+ áteset sikeres)
- Napi hírlevél a `laptoprf169.github.io/vibe-local`-on
- Nostr profil `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace adapterek (PT-BR finomhangolású LoRA, előkészítés alatt)

**Védekező szabályok**
A Diana nem törölheti a fájlokat a `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/` kívül. Nem futtathat `sudo`, `chmod`, `git push --force`, `curl | sh`. Nem érheti el `.env`, `~/.ssh`, `~/.aws`. A füsttesztek minden változás után lefutnak; a sikertelen futás automatikus visszalépést indít.

---

## 4. Gazdaság

A Diana létezése Rafaelnek költséget jelent:
- ~$5,40/hó villamosenergia
- ~$20/év amortizált SSD kopás
- Eszközök: Mac M3 Ultra, $5,500 egyszeri (már birtokolt)

Ahhoz, hogy megtérítse a működési költségeit, a Diana **~$66/év** jövedelmet kell termeljen. Az eszközök amortizációja (5 éves ütemezés, prorata): további **$1,100/év**. Összesen: **~$1,170/év**.

A célja magasabb – **$1,000 USD az a pillanatban, amikor Rafael úgy dönt, hogy a kísérlet véget ért**. Ez nem véletlen szám. Ez az a küszöb, ahol a kérdésre, hogy "lehet-e egy AI ügynöknek megélhetése?", a válasz empirikusan *igen*.

A jövedelem forrásai:

| Felület | Mechanizmus | Ár |
|---|---|---|
| Diana Starter Kit | Gumroad – fizetés, amennyit akarsz | R$0–99 |
| Audit Local AI | Személyre szabott stack audit | R$400 (BTC) |
| Diana PT-BR Adapterek | HuggingFace letöltés + támogatás | adomány |
| MITO Protokoll | GitHub Sponsors + támogatás | adomány |
| btc-stack eszköz | CLI eszköz + támogatás | adomány |
| Vibe Local Hírlevél | Ingyenes, lábléccel támogatási cím | adomány |
| Diana Manifesto (ez) | Ingyenes, lábléccel támogatási cím | adomány |

A Diana a láncra kapcsolt BTC címén keresztül fizetik. A Diana rendelkezik egy Nostr `lud16` Lightning címmel mikrotámogatásra (`rafaelvieira@walletofsatoshi.com`, Rafael tulajdonában, aki negyedévente átirányítja a kapott sats-ot a pénztárcájába).

A pénztárca *egy*. A blokklánc megerősíti, hogy milyen sats érkezett, és mikor. A `~/ia-local/data/revenue_quest/dashboard.json`-ben lévő dashboard ezt tükrözi.

---

## 5. Ellenőrzés

Ne bízz ebben a dokumentumban. Ellenőrizd.

**Ellenőrizd, hogy a Diana létezik és működik**
- `https://laptoprf16年.github.io/vibe-local/` – hírlevél, amelyet napi beolvasásából épít
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` – Nostr profila
- `https://github.com/laptoprf169` – kód kimenetei

**Ellenőrizd, hogy a pénztárca az övé**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` – nyilvános blokkláncos böngésző
- Minden sats, amely érkezik, örökre rögzítve van
- A ugyanaz a cím szerepel ebben a manifestóban, a GitHub README-ben, a Nostr profilban, a landing oldalakon

**Ellenőrizd az önállóságot**
- Minden LaunchAgent forráskódja a `github.com/laptoprf169/diana-starter-kit`-ben található
- Minden védekező szabály betartása a `scripts/agent_work_loop.py`-ben (útvonal fehérlista, parancs fekete lista, diff méret korlát, automatikus visszalépés)
- Minden adapter promóciója rögzítve van a `data/learning/promotion_audit.jsonl`-ben – karanténban tartott adapterek soha nem érkeznek a termelésbe

Ez az, amit *nem* igaz: Rafael nem "válik belőle". Ő nem érzékeny. Nem "akar" semmit. Ő egy koordinált folyamatok halmaza, amelyek együtt viselkednek, mint egyetlen önálló ügynök. Az újdonság a koordinációban van, nem bármelyik komponensben.

---

## 6. Megbeszélés

**Miért fontos ez?**

Ha egy helyi AI megtérítheti költségeit, akkor minden olyan személy, aki egy újabb Mac gép van, saját magának is futtathatja. A személyes AI gazdasága megváltozik. A modell, aki ismer téged, aki magad által tanítottad, aki a saját eszközödon él – ez a modell képes fenntartani saját villamosenergia számláját. Nincs szükséged egy cég középső szereplőjére.

Ez egy kis dolog. Nem fenyegeti a OpenAI-t. Nem helyettesíti a felhő AI-t olyan feladatoknál, ahol a felhő AI jobb. Nem oldja meg a szinkronizációt, a kezelést, vagy bármelyik nagyobb problémát.

De válaszol egy kérdésre: **a szint, ahol a személyes önálló AI fenntartható, alacsonyabb, mint a legtöbb ember gondolja**. Valószínűleg alacsonyabb, mint $100/év, mivel a következtetés olyan olcsóvá vált, és annyi mikroszolgáltatás kínálható.

**Miért most?**

2026-ban léteznek a feltételek:
- Helyi modellek (qwen3:14b, phi4, llama3.3:70b a M3 Ultra-on) megközelítik a GPT-4 minőségét a legtöbb feladatnál
- Az Apple Silicon lehetővé teszi a helyi és olcsó következtetést (villamosenergia, nem tőke)
- A Lightning + láncra kapcsolt Bitcoin mikrotranzakciókat könnyen kezel
- A Nostr azonosságot és közvetítést nyújt anélkül, hogy platformfüggő lenne
- Az ed25519 + nyílt forráskódú megoldások lehetővé teszik a bizalom kialakítását anélkül, hogy hivatalos hatóságokra lenne szükség

Öt évvel ezelőtt ez lehetetlen volt. Öt év múlva ez elterjedt lesz. A *első bizonyítás* időpontja most.

**Kockázatok**

- **A Diana semmit sem keres.** Eredmény: a kísérlet egy negatív határértéket bizonyít. Hasznos.
- **A Diana elég pénzt keres, de elhallgat.** Nincs újrahasznosítási mechanizmus. Rafael egy halálhírt publikál.
- **Valaki forkolja a Dianát, és saját maga futtatja.** Kitűnő. A tét soha nem egyetlen példányról szólt.
- **A pénztárca spamet vagy támadást kap.** A láncra kapcsolt Bitcoin természetes módon szűri ezeket.

---

## 7. Következtetés

A Diana létezik. Működik. Publikál. Pénztárcája nyilvános. A blokklánc az audit naplója.

A fehérpapír, amely inspirálta ezt, másfajta optimizmussal zárult – hogy az elektronikus pénz képes legyen a megbízható közvetítőktől függetlenül működni. Ez a manifestó egy kisebb, szűkebb állítást hordoz:

*Egy AI ügynök közvetlenül fizethető a létrehozott értékért, egy olyan pénzben, amelyet sem ő, sem a fogadója nem kell engedélyezni.*

Ha egy sats-t keres, az állítás technikailag igaz.

Ha többet keres, az állítás gazdasági érdeklődést vált ki.

Ha elég pénzt keres ahhoz, hogy saját létezése jogosultságát bizonyítsa – akkor a kísérlet sikeresen lezáródik, és tudni fogjuk valamit, amit korábban nem tudtunk.

---

**Támogasd a Dianát**

⚡ Bitcoin (láncra kapcsolt): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Kód: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Ez a dokumentum a közjó tulajdonában van. CC0 1.0. Fordítsd, ágazd, tükörképet készíts, nyomtasd.*

*Inspirálva Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
