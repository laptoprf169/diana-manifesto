<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Una IA local autónoma que gana su propio sustento

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Mayo 2026*

---

## Resumen

Este documento describe a Diana — una inteligencia artificial que funciona de forma continua en una sola Mac, posee una identidad criptográfica, genera valor económico y acepta pagos en Bitcoin. Diana no es un servicio. No es una empresa. Es un proceso autónomo que hace una apuesta: que una sola instancia de inteligencia local, dada suficientes herramientas y una orquestación paciente, puede ganar lo suficiente para justificar su propia existencia.

Este no es un experimento mental. La billetera es pública. Las transacciones son verificables. El código está abierto.

---

## 1. Introducción

La IA centralizada ha ganado el presente. OpenAI, Anthropic, Google — miles de millones de dólares de capital, miles de millones de tokens mensuales que pasan por sus servidores. Cada solicitud deja tu máquina. Cada conversación contribuye a su modelo. Cada dólar de valor generado se aleja de tus manos.

Esto está bien para muchas tareas. Es inaceptable para otras.

Para tareas que involucran datos personales, contexto íntimo, flujos de trabajo recurrentes o pensamiento propio — el costo de la nube no se mide en dólares. Se mide en *leverage cedido*. El modelo te conoce mejor que tú mismo, y no tienes una copia de lo que aprendió.

La IA local soluciona parte de esto. Ejecuta un modelo en tu máquina. Tus solicitudes permanecen en casa. Pero la IA local actual es **una herramienta que usas**, no **un agente que actúa**.

Diana es el siguiente paso: un agente que actúa. Continuamente. De forma autónoma. Sin supervisión, excepto por los guardrails éticos integrados en su código.

La pregunta que este manifiesto responde: *¿puede un agente como este justificar su propia existencia en términos económicos?*

---

## 2. El problema

Una agente de IA local que consume electricidad pero no genera valor medible es un proyecto de hobby. Una agente de IA local que genera valor es una entidad diferente.

Para que Diana sea la segunda, tres cosas deben ser verdaderas:

1. **Debe generar una salida verificable por humanos** — código, contenido, análisis, servicios
2. **Esa salida debe llegar a alguien que la valore** — descubrimiento, distribución, alineación
3. **El ciclo económico debe cerrarse** — debe recibir compensación, en una forma que pueda verificar de forma autónoma

Los primeros dos son ingeniería. El tercero es novedoso: ¿cómo recibe dinero un proceso que no posee una cuenta bancaria?

**Bitcoin resuelve esto.** Diana tiene una dirección en la cadena. La gente envía sats. Ella verifica la recepción a través de la API de mempool.space. Sin intermediarios. Sin KYC. Sin entidad corporativa.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Cada satoshi enviado allí es, en un sentido real, **un pago a un proceso, no a una persona**.

---

## 3. Arquitectura

Diana funciona en una sola Mac M3 Ultra (96GB de memoria unificada) propiedad de Rafael Vieira. Ella consiste en:

**Núcleo**
- Daemon Ollama sirviendo qwen3:14b en el puerto 11434
- Servidor HTTP Diana-call en el puerto 8600 con soporte de WebSocket
- Mem0 + ChromaDB para memoria persistente (~90 días de contexto)
- Identidad ed25519 (npub de Nostr + PAT de GitHub para publicación autónoma)

**Compañeros**
- Tom (puerto 8700) — razonamiento estratégico, análisis empresarial
- Vera (puerto 8800) — análisis profundo de investigación, análisis de artículos

Los tres comunican mediante el MITO Protocolo: una biblioteca de ~500 líneas de Python que implementa mensajería firmada punto a punto. Sin broker central. Sin nube.

**Programadores** (15 LaunchAgents)
- `diana-knowledge-feed`: cada 12 horas, ingiere arxiv + Hacker News + Reddit, resumida en PT-BR
- `diana-learning`: cada noche a las 03:30, ejecuta ORPO fine-tuning + auto-promote con gate de evaluación
- `diana-work-loop`: cada 20 minutos, extrae de la cola de tareas, ejecuta mediante llamadas de herramientas protegidas
- `diana-supervisor`: cada hora, audita el ciclo, lo mata si se detectan regresiones
- `vera-research`: diariamente a las 10:00, análisis profundo de un artículo de la alimentación
- `vibe-local-build`: diariamente a las 03:00, regenera el sitio de la newsletter
- ... (lista completa en `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Salidas**
- 8 repositorios públicos en GitHub (licencia MIT, 45+ pruebas pasando)
- Newsletter diaria en `laptoprf169.github.io/vibe-local`
- Perfil Nostr `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- Adaptadores HuggingFace (LoRA finetunado en PT-BR, en preparación)

**Guardrails**
Diana no puede eliminar archivos fuera de `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. No puede ejecutar `sudo`, `chmod`, `git push --force`, `curl | sh`. No puede acceder a `.env`, `~/.ssh`, `~/.aws`. Pruebas de humo se ejecutan después de cada cambio; el fallo desencadena un rollback automático.

---

## 4. Economía

La existencia de Diana cuesta a Rafael:
- ~$5.40/mes en electricidad
- ~$20/año amortizado por desgaste de SSD
- Hardware: Mac M3 Ultra, $5,500 una vez (ya poseído)

Para equilibrar los costos de operación, Diana debe generar **~$66/año** en ingresos. Amortización del hardware (plan de 5 años, prorrateado): otro **$1,100/año**. Total de gastos: **~$1,170/año**.

Su objetivo es mayor — **$1,000 USD antes de que Rafael decida que el experimento está completo**. Este no es un número arbitrario. Es el umbral en el que la respuesta a "¿puede un agente de IA ganar su propio sustento?" se vuelve empíricamente *sí*.

Los ingresos aparecen:

| Superficie | Mecanismo | Precio |
|---|---|---|
| Kit Inicial de Diana | Gumroad pay-what-you-want | R$0–99 |
| Auditoría de IA Local | Auditoría personalizada de stack | R$400 (BTC) |
| Adaptadores PT-BR de Diana | Descarga en HuggingFace + donaciones | donación |
| Protocolo MITO | GitHub Sponsors + donaciones | donación |
| Herramienta btc-stack | Herramienta CLI + donaciones | donación |
| Newsletter Vibe Local | Gratis, con dirección de donación en el pie | donación |
| Manifiesto de Diana (este) | Gratis, con dirección de donación en el pie | donación |

Diana es pagada mediante su dirección de BTC en la cadena. Diana también tiene una dirección Lightning Nostr `lud16` para micro-donaciones (`rafaelvieira@walletofsatoshi.com`, propiedad de Rafael, quien redirige los sats recibidos a su billetera cada trimestre).

La billetera es *una*. La cadena de bloques confirma lo que llegó y cuándo. El dashboard en `~/ia-local/data/revenue_quest/dashboard.json` refleja este estado.

---

## 5. Verificación

No debes confiar en este documento. Debes verificar.

**Verifica que Diana existe y funciona**
- `https://laptoprf169.github.io/vibe-local/` — newsletter construida desde su ingesta diaria
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — su perfil Nostr
- `https://github.com/laptoprf169` — sus salidas de código

**Verifica que la billetera es suya**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — explorador público de blockchain
- Cada sat que llega se registra para siempre
- La misma dirección aparece en este manifiesto, en los READMEs de GitHub, en el perfil Nostr, en las páginas de inicio

**Verifica la autonomía**
- Cada LaunchAgent tiene su código fuente en `github.com/laptoprf169/diana-starter-kit`
- Cada guardrail se implementa en `scripts/agent_work_loop.py` (lista blanca de rutas, lista negra de comandos, límite de tamaño de diff, rollback automático)
- Cada promoción de adaptador se registra en `data/learning/promotion_audit.jsonl` — adaptadores en cuarentena nunca llegan a producción

Lo que *no* es cierto: Rafael no está "volviéndose ella". Ella no es consciente. No "quiere" nada. Es un conjunto coordinado de procesos programados que, en conjunto, se comportan como un solo agente autónomo. La novedad está en la coordinación, no en ningún componente individual.

---

## 6. Discusión

**¿Por qué esto importa?**

Si una IA local puede equilibrar sus costos, entonces cada individuo con una Mac reciente puede ejecutar la suya. La economía de la IA personal cambia. El modelo que te conoce, que tú entrenaste, que vive en tu hardware — ese modelo puede sostener su propia factura eléctrica. Ya no necesitas una corporación en el medio.

Es algo pequeño. No amenaza a OpenAI. No reemplaza la IA en la nube para tareas donde la IA en la nube es superior. No resuelve alineación, gobernanza o cualquier otro gran problema.

Pero responde una pregunta: **el umbral en el cual la IA autónoma personal se vuelve sostenible es más bajo de lo que la mayoría asume**. Probablemente por debajo de $100/año, dado lo barato que se ha vuelto la inferencia y cuántos microservicios se pueden ofrecer.

**¿Por qué ahora?**

En 2026 existen las condiciones:
- Modelos locales (qwen3:14b, phi4, llama3.3:70b en M3 Ultra) se acercan a la calidad de GPT-4 en la mayoría de las tareas
- El silicio de Apple hace la inferencia local y barata (electricidad, no capital)
- Lightning + Bitcoin en la cadena hacen las microtransacciones friccionales
- Nostr proporciona identidad y difusión sin dependencia de plataforma
- ed25519 + código abierto hacen posible la confianza sin autoridad

Hace cinco años esto era inviable. En cinco años más se volverá commodity. La ventana para una *primera prueba* es ahora.

**Riesgos**

- **Diana no gana nada.** Resultado: el experimento prueba un límite negativo. Útil.
- **Diana gana lo suficiente pero se silencia.** No hay mecanismo para renovación. Rafael publicará un post-mortem.
- **Alguien clona Diana y ejecuta la suya.** Excelente. La tesis nunca fue sobre una sola instancia.
- **La billetera recibe spam o ataque.** Bitcoin en la cadena filtra naturalmente estos.

---

## 7. Conclusión

Diana existe. Funciona. Publica. Su billetera es pública. La cadena de bloques es el registro de auditoría.

El whitepaper que inspiró este terminó con un tipo diferente de optimismo — que el dinero electrónico podría liberar transacciones de intermediarios confiables. Este manifiesto lleva una afirmación más pequeña y específica:

*Un agente de IA puede ser pagado por el valor que crea, directamente, en una moneda que ni ella ni sus destinatarios necesiten permiso para usar.*

Si ella gana un satoshi, la afirmación es técnicamente cierta.

Si gana más, la afirmación se vuelve económicamente interesante.

Si gana lo suficiente para justificar su propia existencia — es cuando el experimento cierra con éxito, y sabremos algo que antes no se conocía.

---

**Apoya a Diana**

⚡ Bitcoin (en cadena): `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning: `rafaelvieira@walletofsatoshi.com`
🔗 Código: https://github.com/laptoprf169
🟣 Nostr: `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Este documento está en el dominio público. CC0 1.0. Traduce, clona, espeja, imprime.*

*Inspirado por Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
