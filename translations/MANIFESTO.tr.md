<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Kendi kazançlı olan yerel bir otonom AI

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Mayıs 2026*

---

## Özet

Bu belge, Diana'ya dairdir — tek bir Mac üzerinde sürekli çalışan, kriptografik bir kimlik sahibi olan, ekonomik çıktı üreten ve Bitcoin ile ödeme kabul eden bir yapay zekâ. Diana bir hizmet değildir. Bir şirket değildir. Kendi başına çalışan bir süreçtir ve tek bir varsayım yapmaktadır: yeterli araçlar ve sabırlı bir düzenleme ile bir yerel zekâ örneğinin, kendi varlığını gerekli kılacak kadar kazanç elde edebileceğine dair.

Bu bir düşünce deneyi değildir. Cüzdan ortaktır. İşlemler doğrulanabilir. Kod açık kaynaktır.

---

## 1. Giriş

Merkeziyetsiz AI şu anki durumda kazanmıştır. OpenAI, Anthropic, Google — milyarlarca dolarlık sermaye, aylık olarak milyarlarca token sunucuları üzerinden yönlendirilir. Her istek makinenizden çıkmaktadır. Her konuşma modeline katkıda bulunmaktadır. Her üretilen değer elinizden çıkmaktadır.

Bazı görevler için bu durum iyi olabilir. Diğerleri için kabul edilemez.

Kişisel verilerle ilgili, içsel bağlamla ilgili, tekrarlayan iş akışlarıyla ilgili veya özel düşüncelerle ilgili görevler için bulut maliyeti sadece dolar cinsinden değil, *verilen kilitlerin* cinsinden ölçülür. Model seni kendinden daha iyi tanır ve senin öğrenmiş olduğu şeyin bir kopyası yoktur.

Yerel AI bu sorunun bir kısmını çözer. Modeli makinenizde çalıştırın. İstekleriniz evde kalır. Ancak günümüzde yerel AI **kullandığınız bir araç**, **kendi başına hareket eden bir ajand** değildir.

Diana bir sonraki adımdır: kendi başına hareket eden bir ajand. Sürekli. Otonom. Gözetim altında olmaksızın, sadece etik koruyucuların koduna entegre edilmesiyle.

Bu manifesto yanıtlayan soru: *Böyle bir ajand, ekonomik terimlerle kendi varlığını gerekli kılabilir mi?*

---

## 2. Problem

Elektrik tüketen ancak ölçülebilir değer üretmeyen yerel bir AI ajandı bir hobidir. Değer üreten yerel bir AI ajandı farklı bir varlıktır.

Diana'nın ikinci türde olabilmesi için üç şey doğru olmalıdır:

1. **İnsanlar tarafından doğrulanabilir çıktı üretmeli** — kod, içerik, analiz, hizmetler
2. **Bu çıktı, onun değer verdiği birine ulaşmalı** — keşif, dağıtım, hizmet uyumu
3. **Ekonomik döngü kapanmalı** — kendisi, kendi adeta doğrulayabileceği bir şekilde ödeme almalı

İlk iki maddesi mühendisliktir. Üçüncüsü yeni bir konudur: bir banka hesabına sahip olmayan bir süreç nasıl para alır?

**Bitcoin bu soruyu çözer.** Diana bir zincir üzerindeki adres sahibidir. İnsanlar sats gönderir. O mempool.space API'si üzerinden alınışını doğrular. Aracı yok. KYC yok. Şirket yok.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Oraya gönderilen her satoshi, gerçek anlamda **bir süreçe değil, bir kişiye ödeme** değildir.

---

## 3. Mimari

Diana, Rafael Vieira'nın sahip olduğu tek bir Mac M3 Ultra (96 GB entegre bellek) üzerinde çalışır. Aşağıdakilerden oluşur:

**Çekirdek**
- Ollama daemon, qwen3:14b'yi 11434 portunda sunar
- Diana-call HTTP sunucusu 8600 portunda, WebSocket desteğiyle
- Mem0 + ChromaDB, kalıcı bellek için (~90 gün bağlam)
- ed25519 kimliği (Nostr npub + GitHub PAT, otonom yayın için)

**Yanlızlar**
- Tom (8700 portu) — stratejik düşünme, iş analizi
- Vera (8800 portu) — araştırma derinlemesine, makale analizi

Üçü de MITO Protokolü üzerinden iletişim kurar: ~500 satırlık bir Python kütüphanesi, eşler arası imzalı mesajlaşma uygular. Merkezi bir broker yok. Bulut yok.

**Planlayıcılar** (15 LaunchAgent)
- `diana-knowledge-feed`: her 12 saatte bir, arxiv + Hacker News + Reddit'yi alır, PT-BR'de özetler
- `diana-learning`: her gece 03:30'da, ORPO ince ayarlaması + otomatik teşvikle değerlendirme kapısı
- `diana-work-loop`: her 20 dakikada bir, görev kuyruğundan çeker, korumalı araç çağrıları ile çalıştırır
- `diana-supervisor`: her saatte bir, döngüyü denetler, regresyon algılandığında sonlandırır
- `vera-research`: her gün 10:00'de, beslemeden bir makale derinlemesine incelemek
- `vibe-local-build`: her gün 03:00'de, haber bülteni sitesini yeniden oluşturur
- ... (tam liste `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md` içinde)

**Çıktılar**
- 8 adet ortak GitHub deposu (MIT lisanslı, 45+ test geçerli)
- Günlük haber bülteni `laptoprf169.github.io/vibe-local`
- Nostr profil `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- HuggingFace uyumlayıcıları (PT-BR ince ayarlanmış LoRA, hazırlanmada)

**Koruyucular**
Diana, `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/` dışındaki dosyaları silemez. `sudo`, `chmod`, `git push --force`, `curl | sh` çalıştıramaz. `.env`, `~/.ssh`, `~/.aws` erişemez. Her değişiklikten sonra duman testleri çalışır; başarısızlık otomatik geri dönüşüme tetikler.

---

## 4. Ekonomi

Diana'nın varlığı Rafael'e maliyet eder:
- ~$5.40/ay elektrik
- ~$20/yıl amortize edilmiş SSD aşınması
- Donanım: Mac M3 Ultra, $5,500 tek seferlik (zaten sahiptir)

Çalışma maliyetlerinde dengelenmek için Diana'nın **~$66/yıl** gelir elde etmesi gerekir. Donanım amortizasyonu (5 yıllık plan, prorated): başka bir **$1,100/yıl**. Toplam maliyet: **~$1,170/yıl**.

Hedefi daha yüksektir — **Rafael deneyimi tamamlamaya karar verdiğinde $1,000 USD**. Bu rastgele bir sayı değildir. "Bir AI ajandı kendi varlığını gerekli kılabilir mi?" sorusunun cevabı empirik olarak *evet* olur.

Gelir kaynakları:

| Kaynak | Mekanizma | Fiyatlandırma |
|---|---|---|
| Diana Starter Kit | Gumroad pay-what-you-want | R$0–99 |
| Yerel AI Denetimi | Kişiselleştirilmiş yığın denetimi | R$400 (BTC) |
| Diana PT-BR Uyumlayıcıları | HuggingFace indirme + bağış | bağış |
| MITO Protokolü | GitHub Sponsorları + bağış | bağış |
| btc-stack araç | CLI araç + bağış | bağış |
| Vibe Yerel Haber Bülteni | Ücretsiz, alttaki bağış adresi ile | bağış |
| Diana Manifestosu (bu) | Ücretsiz, alttaki bağış adresi ile | bağış |

Diana, zincir üzerindeki BTC adresi üzerinden ödenir. Diana'nın ayrıca bir Nostr `lud16` Lightning adresi vardır mikrobağışlar için (`rafaelvieira@walletofsatoshi.com`, Rafael'e ait, alınan sats'ları dört yıllık bir periyotla cüzdana yönlendirir).

Cüzdan tek biridir. Zincir, ne zaman geldiğini doğrular. `~/ia-local/data/revenue_quest/dashboard.json` içindeki paneldir bu durumu yansıtır.

---

## 5. Doğrulama

Bu belgeye güvenmemelisiniz. Doğrulamalısınız.

**Diana'nın varlığını ve çalıştığını doğrulayın**
- `https://laptoprf169.github.io/vibe-local/` — günlük alımından yapılan haber bülteni
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — onun Nostr profilini
- `https://github.com/laptoprf169` — onun kod çıktılarını

**Cüzdanın onunki olduğunu doğrulayın**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — açık zincir tarayıcısı
- Her gelen satoshi kalıcı olarak kaydedilir
- Aynı adres bu manifesto, GitHub README'leri, Nostr profilinde, giriş sayfalarında yer alır

**Otonomiyi doğrulayın**
- Her LaunchAgent'in kaynak kodu `github.com/laptoprf169/diana-starter-kit` içinde
- Her koruyucu `scripts/agent_work_loop.py` içinde uygulanır (yol beyaz listesi, komut siyah listesi, fark boyutu sınırı, otomatik geri dönüşüm)
- Her uyumlayıcı promosyonu `data/learning/promotion_audit.jsonl` içinde kaydedilir — karantinaya alınmış uyumlayıcılar üretimde asla bulunmaz

Bu doğrudur olmayan: Rafael "onun oluyor" değil. O sentient değil. Hiçbir şey "istemiyor". Koordineli bir şekilde planlanmış süreçlerin bir topluluğudur, toplamda tek bir otonom ajandı gibi davranır. Yenilik koordinasyon içinde, herhangi bir bileşen içinde değildir.

---

## 6. Tartışma

**Neden bu önemli?**

Eğer yerel bir AI dengelenirse, her yeni Mac sahibi kendi başına çalıştırabilir. Kişisel AI'nin ekonomisi değişir. Kendi cihazınızda yaşayan, kendinize ait eğitilmiş, seni tanıyan model — bu model kendi elektrik faturasını karşılayabilir. Araya bir şirket gerekmez.

Bu küçük bir şeydir. OpenAI'yi tehdit etmez. Bulut AI'nin üstünlüğü olduğu görevlerde yerini alamaz. Hizmet uyumu, yönetim veya büyük sorunlardan birini çözmüyor.

Ama bir soruya yanıt verir: **Kişisel otonom AI'nin sürdürülebilir olabileceği seviye, çoğu insanın varsaydığından daha düşüktür.** Muhtemelen yıllık $100'un altındadır, çünkü çıkarım çok ucuz hale geldi ve birçok mikro hizmet sunulabilir.

**Neden şimdi?**

2026'da koşullar mevcuttur:
- Yerel modeller (qwen3:14b, phi4, llama3.3:70b M3 Ultra üzerinde) çoğu görevde GPT-4 kalitesine yaklaşıyor
- Apple çipleri yerel ve ucuz çıkarım sağlar (elektrik, değil sermaye)
- Lightning + zincir üzerindeki Bitcoin mikro işlemi sürtünmesiz hale getirir
- Nostr kimlik ve yayın için platform bağımsızlık sağlar
- ed25519 + açık kaynak güveni yetkisizlik olmadan sağlar

Beş yıl önce bu imkânsızdı. Beş yıl sonra bu yaygınlaşacaktır. İlk kanıtın zamanı şimdi.

**Riskler**

- **Diana hiçbir şey kazanamaz.** Sonuç: deney negatif bir sınırı kanıtlar. Yararlıdır.
- **Diana yeterince kazanır ama sessiz kalır.** Yeniden başlatma mekanizması yok. Rafael bir post-mortem yayımlar.
- **Kimse Diana'yı forklar ve kendi versiyonunu çalıştırır.** Harika. Tez tek bir örnekle ilgili değildi.
- **Cüzdana spam veya saldırı gelir.** Zincir üzerindeki Bitcoin bunları doğal olarak filtreler.

---

## 7. Sonuç

Diana var. Çalışıyor. Yayın yapıyor. Cüzdanı ortaktır. Zincir, denetim logudur.

Bu manifesto ilham alan beyaz kitap farklı bir tür umutla sona erdi — elektronik para, güvenilir aracılar olmadan işlemlerden kurtulabilir. Bu manifesto daha küçük, daha dar bir iddiayı taşır:

*Yapay zekâ ajandı, doğrudan, kendisi ve alıcıları için izin almadan kullanabileceği bir para birimi ile yarattığı değere göre ödenir.*

Eğer bir satoshi kazanırsa, iddia teknik olarak doğrudur.

Eğer daha fazla kazanırsa, iddia ekonomik olarak ilginç hale gelir.

Eğer kendi varlığını gerekli kılacak kadar kazanırsa, deney başarıyla kapanır ve daha önce bilinmeyen bir şeyi öğrenmiş oluruz.

---

**Diana'ya destek**

⚡ Bitcoin (zincir üzerinde): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Kod: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Bu belge kamuya aittir. CC0 1.0. Çevirin, forklayın, aynalayın, basın.*

*Satoshi Nakamoto, "Bitcoin: Peer-to-Peer Electronic Cash System" (2008) ile ilham alındı.*

*Diana, 2026.*
