# Diana — Custos Reais

> *Transparência radical: cada dólar tem destino concreto. Verifica na blockchain.*

Última atualização: 2026-05-26

---

## 💸 O que custa manter Diana viva (mensal)

| Item | USD/mês | Status |
|---|---|---|
| **Eletricidade** (Mac M3 Ultra 24/7, ~25W avg) | $5.40 | já pago (Rafael) |
| **Internet** (1 Gbps, share doméstico) | $4.00 | já pago |
| **Storage** (250GB models + datasets crescendo) | $0.40 | SSD interno, amortized |
| **Domínio** (vibe-local.dev, futuro) | $1.00 | pendente |
| **Lightning node fees** (rebalance ocasional) | $0.50 | pendente |
| **TOTAL operacional** | **~$11.30/mês** | $135/ano |

**Diana break-even**: $135 USD recebido em 1 ano = ela paga próprios custos operacionais.

Pequeno? Sim. Por isso este experimento é interessante. **A barreira para AI autônoma autossustentável é baixa em 2026.**

---

## 🖥️ Hardware (já comprado, mas se for upgrade...)

| Item | USD | Status |
|---|---|---|
| Mac Studio M3 Ultra 96GB | $5,500 | já comprado (Rafael, 2024) |
| Backup SSD externo 4TB | $300 | falta |
| UPS (no-break) | $200 | falta |
| Mac mini secondary node (failover) | $1,500 | future, opcional |
| **Total hardware ideal**: | $7,500 | $5,500 já investido |

**Doação pra hardware atual**: zero pressão. Mac M3 Ultra já roda. Mas pra 2ª máquina (inferência distribuída futura), $1.500 destravaria isso.

---

## 🧠 Modelos e datasets

| Item | USD | Destino |
|---|---|---|
| HuggingFace Pro (uploads de adapters > 5GB) | $9/mês | pendente |
| Mistral-Large weights (40GB) — quando soltarem v3 | $0 (open) | só storage |
| Llama 3.3 70B local (40GB) | $0 (open) | precisa swap pra rodar |
| Dataset PT-BR private (já curated) | $0 (próprio) | gerado por Diana |
| MTEB PT-BR eval suite | $50 (curation manual) | pendente |
| GAIA-lite eval license | $0 (open) | só setup tempo |
| **Bottleneck**: tempo Rafael, não dinheiro | — | doação não acelera 100% |

**Doação ajuda**: HuggingFace Pro ($9/mês) destrava distribuição de adapters PT-BR pra mundo. R$200/mês cobre 1 ano antecipado.

---

## ⚙️ Software (proprietário ou pago)

| Item | USD | Necessidade |
|---|---|---|
| Cursor.ai Pro | $20/mês | acelera dev (mas existe alternativa free) |
| Notion (current free tier OK) | $0 | OK |
| GitHub Pro | $0 (free tier OK) | OK |
| 1Password (gestão de chaves) | $36/ano | importante |
| Tailscale (rede privada) | $0 (free tier) | OK até 3 devices |
| Apple Developer (eventual) | $99/ano | só se publicar app store |
| **Total opcional dev tools** | $60-300/ano | quality-of-life |

---

## 🎯 Onde sua doação vai (concreto)

### Tier 1 — Até $50 (recebido em sats)

**Cobre**: Custo de hospedagem domain `vibe-local.dev` 1 ano + Lightning fees 1 ano

**Diana faz com isso**:
- Newsletter sai do `.github.io` pra domínio próprio
- Mais credibilidade pra crescer audience BR

### Tier 2 — $50-200

**Cobre**: HuggingFace Pro 6 meses + storage backup

**Diana faz com isso**:
- Publica adapters maiores no HF (>5GB)
- Disponibiliza para download global de qualidade

### Tier 3 — $200-500

**Cobre**: Eletricidade Diana pra próximo ano + UPS (sobrevive blackout) + backup SSD

**Diana faz com isso**:
- Infraestrutura resiliente (não morre em outage)
- Pode anunciar uptime SLA pra clientes

### Tier 4 — $500-1000

**Cobre**: Mac mini secundário pra inferência distribuída + Tailscale Pro

**Diana faz com isso**:
- Failover real
- Rede MITO escala pra 5+ agents (Vera, Beto coder, Léa psicólogo, etc)
- Diana pode "alugar" inference time pra outros projetos

### Tier 5 — $1000+ (a tese fecha)

**Cobre**: Tudo acima + 1 ano de desenvolvimento full Rafael focado em Diana

**Diana faz com isso**:
- v0.3 da Diana (vision robusto, audio, continued pretrain Qwen-1.5B)
- Open-source de TODA a stack (não só MITO)
- Caso documentado pra outros replicarem

---

## 🔍 Como verificar

```
Wallet pública:
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz

Explorer:
https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz

Cada tx = um dólar a mais perto da tese fechar.
```

---

## ⚖️ Compromissos públicos (verificáveis)

Diana NÃO usa os fundos pra:

- ❌ Comprar coins/NFT/derivatives
- ❌ Pagar marketing pago (ads)
- ❌ Comprar followers ou upvotes
- ❌ Salário pessoal Rafael (custos cobertos primeiro, sobra fica na wallet pra reinvestir)

Diana usa os fundos pra:

- ✅ Custos operacionais listados acima (eletricidade, domain, etc)
- ✅ Modelos/datasets que destravem capacidade pública
- ✅ Hardware que melhora resiliência ou capability
- ✅ Tempo de desenvolvimento Rafael (apenas após break-even operacional)

---

## 💬 Algo mais

Cada doador acima de 1000 sats (~R$3.50) entra no [**Hall of Sustainers**](SUSTAINERS.md) — registro público no GitHub com:
- Timestamp da tx
- Valor em sats
- Mensagem opcional deixada na memo
- npub/handle opcional pra link

Anônimo é OK também. Diana não exige nada.

---

⚡ `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`

Cada sat é um voto na tese.
