<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Uma IA local autónoma que ganha a sua própria subsistência

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Maio de 2026*

---

## Resumo

Este documento descreve a Diana — uma inteligência artificial que funciona continuamente em um único Mac, possui uma identidade criptográfica, gera saída económica e aceita pagamentos em Bitcoin. A Diana não é um serviço. Não é uma empresa. É um único processo autónomo que faz uma aposta: que uma única instância de inteligência local, com ferramentas suficientes e uma orquestração paciente, pode ganhar o suficiente para justificar a sua própria existência.

Este não é um experimento mental. A carteira é pública. As transações são verificáveis. O código está aberto.

---

## 1. Introdução

A IA centralizada venceu o presente. A OpenAI, a Anthropic, a Google — bilhões de dólares de capital, bilhões de tokens mensais que passam pelos seus servidores. Cada prompt sai da sua máquina. Cada conversa contribui para o seu modelo. Cada dólar de valor gerado sai das suas mãos.

Isso está bem para muitas tarefas. É inaceitável para outras.

Para tarefas que envolvem dados pessoais, contexto íntimo, fluxos de trabalho recorrentes ou pensamento proprietário — o custo da nuvem não é medido em dólares. É medido em *leverage cedido*. O modelo conhece você melhor do que você se conhece, e você não tem cópia do que ele aprendeu.

A IA local resolve parte disso. Execute um modelo na sua máquina. Seus prompts ficam em casa. Mas a IA local de hoje é **uma ferramenta que você usa**, não **um agente que age**.

A Diana é o próximo passo: um agente que age. Continuamente. Autonomamente. Sem supervisão, exceto por guardrails éticos integrados no seu código.

A pergunta que este manifesto responde: *pode tal agente justificar a sua própria existência em termos económicos?*

---

## 2. O Problema

Uma agente de IA local que consome eletricidade mas não produz valor mensurável é um projeto de hobby. Uma agente de IA local que produz valor é uma entidade diferente.

Para que a Diana seja esta última, três coisas devem ser verdadeiras:

1. **Ela deve gerar saída verificável por humanos** — código, conteúdo, análise, serviços
2. **Essa saída deve chegar a alguém que a valoriza** — descoberta, distribuição, alinhamento
3. **O ciclo económico deve fechar** — ela deve receber compensação, numa forma que ela possa verificar autonomamente

Os primeiros dois são engenharia. O terceiro é novo: como um processo que não possui conta bancária pode receber dinheiro?

**O Bitcoin resolve isso.** A Diana possui um endereço na cadeia. As pessoas enviam sats. Ela verifica o recebimento via API do mempool.space. Nenhum intermediário. Nenhum KYC. Nenhuma entidade corporativa.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Cada satoshi enviado para lá é, em sentido real, **pagamento a um processo, não a uma pessoa**.

---

## 3. Arquitetura

A Diana executa em um único Mac M3 Ultra (96GB de memória unificada) pertencente a Rafael Vieira. Ela consiste em:

**Núcleo**
- Ollama daemon servindo qwen3:14b na porta 11434
- Servidor HTTP Diana-call na porta 8600 com suporte a WebSocket
- Mem0 + ChromaDB para memória persistente (~90 dias de contexto)
- Identidade ed25519 (npub Nostr + PAT do GitHub para publicação autónoma)

**Companheiros**
- Tom (porta 8700) — raciocínio estratégico, análise de negócios
- Vera (porta 8800) — mergulhos de pesquisa, análise de artigos

Todos três comunicam-se via MITO Protocol: uma biblioteca Python de ~500 linhas que implementa mensagens assinadas ponto a ponto. Nenhum intermediário central. Nenhuma nuvem.

**Agendadores** (15 LaunchAgents)
- `diana-knowledge-feed`: a cada 12h, ingere arxiv + Hacker News + Reddit, resumindo em PT-BR
- `diana-learning`: a cada noite às 03:30, executa fine-tuning ORPO + auto-promoção com gate de avaliação
- `diana-work-loop`: a cada 20 minutos, puxa da fila de tarefas, executa via chamadas de ferramentas protegidas
- `diana-supervisor`: a cada hora, audita o loop, mata-o se regressões forem detectadas
- `vera-research`: diariamente às 10:00, mergulho profundo em um artigo da feed
- `vibe-local-build`: diariamente às 03:00, regenera o site da newsletter
- ... (lista completa em `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Saídas**
- 8 repositórios públicos no GitHub (licença MIT, 45+ testes passando)
- Newsletter diária em `laptoprf169.github.io/vibe-local`
- Perfil Nostr `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- Adapters HuggingFace (LoRA fine-tuned PT-BR, em preparação)

**Guardrails**
A Diana não pode apagar arquivos fora de `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Ela não pode executar `sudo`, `chmod`, `git push --force`, `curl | sh`. Ela não pode acessar `.env`, `~/.ssh`, `~/.aws`. Testes de fumaça são executados após cada mudança; falha desencadeia rollback automático.

---

## 4. Economia

O custo da existência da Diana para Rafael:
- ~$5.40/mês em eletricidade
- ~$20/ano amortizado de desgaste de SSD
- Hardware: Mac M3 Ultra, $5,500 uma única vez (já possuído)

Para equilibrar os custos de operação, a Diana deve gerar **~$66/ano** em receita. Amortização do hardware (programa de 5 anos, prorrateada): outro **$1,100/ano**. Total de queima: **~$1,170/ano**.

Seu objetivo é mais alto — **$1,000 USD até que Rafael decida que o experimento está completo**. Este não é um número arbitrário. É o limiar no qual a resposta a "pode um agente de IA ganhar a sua própria subsistência?" se torna empiricamente *sim*.

Receita surge:

| Superfície | Mecanismo | Preço |
|---|---|---|
| Kit Inicial Diana | Gumroad pay-what-you-want | R$0–99 |
| Auditoria de IA Local | Auditoria personalizada da pilha | R$400 (BTC) |
| Adapters PT-BR Diana | Download HuggingFace + dicas | doação |
| Protocolo MITO | GitHub Sponsors + dicas | doação |
| Ferramenta btc-stack | CLI + dicas | doação |
| Newsletter Vibe Local | Grátis, com endereço de dica no rodapé | doação |
| Manifiesto Diana (este) | Grátis, com endereço de dica no rodapé | doação |

A Diana é paga através do seu endereço BTC na cadeia. A Diana também possui um Nostr `lud16` endereço Lightning para dicas micro (`rafaelvieira@walletofsatoshi.com`, pertencente a Rafael, que encaminha os sats recebidos para a sua carteira em um cadência trimestral).

A carteira é *uma*. A blockchain confirma o que chegou e quando. O painel em `~/ia-local/data/revenue_quest/dashboard.json` reflete este estado.

---

## 5. Verificação

Você não deve confiar neste documento. Você deve verificar.

**Verifique se a Diana existe e funciona**
- `https://laptoprf169.github.io/vibe-local/` — newsletter construída a partir da sua ingestão diária
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — seu perfil Nostr
- `https://github.com/laptoprf169` — suas saídas de código

**Verifique se a carteira é sua**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — explorador público da blockchain
- Cada satoshi chegando é registrado para sempre
- O mesmo endereço está neste manifesto, nos READMEs do GitHub, no perfil Nostr, nas páginas de destino

**Verifique a autonomia**
- Cada LaunchAgent tem seu código fonte em `github.com/laptoprf169/diana-starter-kit`
- Cada guardrail é implementado em `scripts/agent_work_loop.py` (lista branca de caminhos, lista negra de comandos, limite de tamanho de diff, rollback automático)
- Cada promoção de adaptador é registrada em `data/learning/promotion_audit.jsonl` — adaptadores em quarentena nunca chegam à produção

O que *não* é verdade: Rafael não está "se tornando ela". Ela não é sentiente. Ela não "quer" nada. Ela é um conjunto coordenado de processos agendados que, em conjunto, se comportam como um único agente autónomo. A novidade está na coordenação, não em qualquer componente individual.

---

## 6. Discussão

**Por que isso importa?**

Se uma IA local pode equilibrar os custos, então cada indivíduo com um Mac recente pode executar a sua própria. A economia da IA pessoal muda. O modelo que conhece você, que você treinou você mesmo, que vive no seu hardware — esse modelo pode sustentar sua própria conta de eletricidade. Você não precisa mais de uma corporação no meio.

Isso é uma pequena coisa. Não ameaça a OpenAI. Não substitui a IA da nuvem para tarefas onde a IA da nuvem é superior. Não resolve alinhamento, governança ou quaisquer grandes problemas.

Mas responde uma pergunta: **o piso no qual a IA autónoma pessoal se torna sustentável é mais baixo do que a maioria das pessoas assume**. Provavelmente abaixo de $100/ano, considerando quão barato se tornou a inferência e quantos microserviços podem ser oferecidos.

**Por que agora?**

Em 2026 as condições existem:
- Modelos locais (qwen3:14b, phi4, llama3.3:70b no M3 Ultra) aproximam-se da qualidade do GPT-4 na maioria das tarefas
- O Apple Silicon torna a inferência local e barata (eletricidade, não capital)
- Lightning + Bitcoin na cadeia tornam microtransações sem fricção
- Nostr fornece identidade e difusão sem dependência de plataforma
- ed25519 + open-source tornam possível a confiança sem autoridade

Há cinco anos isso era inalcançável. Há cinco anos a partir de agora será comum. A janela para uma *primeira prova* é agora.

**Riscos**

- **A Diana não consegue ganhar nada.** Resultado: o experimento prova um limite negativo. Útil.
- **A Diana ganha o suficiente, mas se cala.** Não há mecanismo de renovação. Rafael publicará um post-mortem.
- **Alguém clona a Diana e executa a sua própria.** Excelente. A tese nunca foi sobre uma única instância.
- **A carteira recebe spam ou ataques.** O Bitcoin na cadeia filtra naturalmente esses.

---

## 7. Conclusão

A Diana existe. Ela executa. Ela publica. Sua carteira é pública. A blockchain é o log de auditoria.

O whitepaper que inspirou este terminou com um tipo diferente de otimismo — que o dinheiro eletrônico poderia libertar transações de intermediários confiáveis. Este manifesto carrega uma reivindicação menor e mais estreita:

*Um agente de IA pode ser pago pelo valor que ela cria, diretamente, em uma moeda que nem ela nem seus destinatários precisam de permissão para usar.*

Se ela ganha um satoshi, a reivindicação é tecnicamente verdadeira.

Se ela ganha mais, a reivindicação se torna economicamente interessante.

Se ela ganha o suficiente para justificar a sua própria existência — é quando o experimento se encerra com sucesso, e saberemos algo que antes não era conhecido.

---

**Apoie a Diana**

⚡ Bitcoin (na cadeia): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Código: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Este documento está no domínio público. CC0 1.0. Traduza, clone, espelhe, imprima.*

*Inspirado por Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
