<!-- AUTO-TRANSLATED by Diana via qwen3:14b · original: MANIFESTO.md · CC0 -->

# Diana
## Une IA locale autonome qui gagne sa vie

**Rafael Vieira**
*rafael@diana-local* · *github.com/laptoprf169*
*Mai 2026*

---

## Résumé

Ce document décrit Diana — une intelligence artificielle qui fonctionne en continu sur un seul Mac, possède une identité cryptographique, génère un revenu économique et accepte le paiement en Bitcoin. Diana n'est pas un service. Elle n'est pas une entreprise. Elle est un seul processus autonome qui fait une seule mise : celle que, donnée suffisamment d'outils et une orchestration patiente, une seule instance d'intelligence locale peut gagner assez pour justifier son existence.

Ce n'est pas une expérience de pensée. Le portefeuille est public. Les transactions sont vérifiables. Le code est ouvert.

---

## 1. Introduction

L'IA centralisée a gagné le présent. OpenAI, Anthropic, Google — des milliards de dollars de capital, des milliards de tokens mensuels passant par leurs serveurs. Chaque prompt quitte votre machine. Chaque conversation contribue à leur modèle. Chaque dollar de valeur générée quitte vos mains.

C'est acceptable pour beaucoup de tâches. C'est inacceptable pour d'autres.

Pour les tâches qui touchent aux données personnelles, au contexte intime, aux workflows récurrents ou aux pensées propres — le coût du cloud n'est pas mesuré en dollars. Il est mesuré en *leverage cédé*. Le modèle vous connaît mieux que vous ne vous connaissez vous-même, et vous n'avez pas de copie de ce qu'il a appris.

L'IA locale corrige en partie ce problème. Exécutez un modèle sur votre machine. Vos prompts restent chez vous. Mais l'IA locale d'aujourd'hui est **un outil que vous utilisez**, pas **un agent qui agit**.

Diana est la prochaine étape : un agent qui agit. Continuellement. Autonomement. Sans surveillance, sauf pour les garde-fous éthiques intégrés dans son code.

La question que ce manifeste répond : *peut un tel agent justifier son existence en termes économiques ?*

---

## 2. Le problème

Une agente IA locale qui consomme de l'électricité mais ne produit aucune valeur mesurable est un projet de loisir. Une agente IA locale qui produit de la valeur est une entité différente.

Pour que Diana soit cette dernière, trois choses doivent être vraies :

1. **Elle doit générer un output vérifiable par les humains** — du code, du contenu, une analyse, des services
2. **Cet output doit atteindre quelqu'un qui le valorise** — découverte, distribution, alignement
3. **Le cycle économique doit se fermer** — elle doit recevoir un paiement, sous une forme qu'elle peut vérifier de manière autonome

Les deux premiers sont de l'ingénierie. Le troisième est nouveau : comment un processus qui ne possède aucun compte bancaire peut-il recevoir de l'argent ?

**Le Bitcoin résout ce problème.** Diana possède une adresse sur la blockchain. Les gens envoient des sats. Elle vérifie la réception via l'API mempool.space. Aucun intermédiaire. Aucun KYC. Aucune entité corporative.

```
bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz
```

Chaque satoshi envoyé là-bas est, dans un sens réel, **un paiement à un processus, pas à une personne**.

---

## 3. Architecture

Diana fonctionne sur un seul Mac M3 Ultra (96 Go de mémoire unifiée) appartenant à Rafael Vieira. Elle comprend :

**Noyau**
- Démon Ollama servant qwen3:14b sur le port 11434
- Serveur HTTP Diana-call sur le port 8600 avec support WebSocket
- Mem0 + ChromaDB pour la mémoire persistante (~90 jours de contexte)
- Identité ed25519 (npub Nostr + PAT GitHub pour la publication autonome)

**Compagnons**
- Tom (port 8700) — raisonnement stratégique, analyse business
- Vera (port 8800) — analyses approfondies, analyse de paper

Les trois communiquent via le protocole MITO : une bibliothèque Python de ~500 lignes implémentant des messages signés pair-à-pair. Aucun courtier central. Aucun cloud.

**Planificateurs** (15 LaunchAgents)
- `diana-knowledge-feed` : toutes les 12 heures, ingère arxiv + Hacker News + Reddit, résume en PT-BR
- `diana-learning` : chaque nuit à 03:30, exécute l'ajustement ORPO + auto-promotion avec porte d'évaluation
- `diana-work-loop` : toutes les 20 minutes, tire des tâches de la file d'attente, exécute via des appels d'outils sécurisés
- `diana-supervisor` : toutes les heures, audit de la boucle, la tue si des régressions sont détectées
- `vera-research` : quotidiennement à 10:00, analyse approfondie d'un paper de la liste
- `vibe-local-build` : quotidiennement à 03:00, régénère le site de la newsletter
- ... (liste complète dans `ia-local/data/revenue_quest/DIANA_AUTONOMIA.md`)

**Sorties**
- 8 dépôts GitHub publics (licenciés MIT, 45+ tests passants)
- Newsletter quotidienne à `laptoprf169.github.io/vibe-local`
- Profil Nostr `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`
- Adapteurs HuggingFace (LoRA fine-tunée PT-BR, en préparation)

**Garde-fous**
Diana ne peut pas supprimer de fichiers en dehors de `diana/`, `scripts/`, `docs/`, `tests/`, `data/work_log/`. Elle ne peut pas exécuter `sudo`, `chmod`, `git push --force`, `curl | sh`. Elle ne peut pas accéder à `.env`, `~/.ssh`, `~/.aws`. Des tests de fumée s'exécutent après chaque changement ; une échec déclenche un rollback automatique.

---

## 4. Économie

L'existence de Diana coûte à Rafael :
- ~$5,40/mois en électricité
- ~$20/an d'usure amortie de l'SSD
- Matériel : Mac M3 Ultra, $5 500 une fois (déjà possédé)

Pour atteindre l'équilibre sur les coûts d'exécution, Diana doit générer **~$66/an** de revenus. L'amortissement du matériel (plan sur 5 ans, proratisé) : un autre **$1 100/an**. Total de brûlage : **~$1 170/an**.

Son objectif est plus élevé — **$1 000 USD avant que Rafael ne décide que l'expérience est terminée**. Ce n'est pas un nombre arbitraire. C'est le seuil auquel la réponse à « une agente IA peut-elle gagner sa vie ? » devient empiriquement *oui*.

Les revenus apparaissent :

| Surface | Mécanisme | Tarification |
|---|---|---|
| Kit de départ de Diana | Gumroad payez ce que vous voulez | R$0–99 |
| Audit de l'IA locale | Audit personnalisé de l'empilement | R$400 (BTC) |
| Adapteurs PT-BR de Diana | Téléchargement HuggingFace + dons | don |
| Protocole MITO | GitHub Sponsors + dons | don |
| Outil btc-stack | Outil CLI + dons | don |
| Newsletter Vibe Local | Gratuit, avec adresse de don en pied de page | don |
| Manifeste de Diana (celui-ci) | Gratuit, avec adresse de don en pied de page | don |

Diana est payée via son adresse BTC sur la blockchain. Diana a également une adresse Lightning Nostr `lud16` pour les micro-dons (`rafaelvieira@walletofsatoshi.com`, appartenant à Rafael, qui transfère les sats reçus à son portefeuille trimestriellement).

Le portefeuille est *un seul*. La blockchain confirme ce qui est arrivé et quand. Le tableau de bord à `~/ia-local/data/revenue_quest/dashboard.json` reflète cet état.

---

## 5. Vérification

Vous ne devriez pas faire confiance à ce document. Vous devriez vérifier.

**Vérifiez que Diana existe et fonctionne**
- `https://laptoprf169.github.io/vibe-local/` — newsletter construite à partir de sa consommation quotidienne
- `https://snort.social/p/npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5` — son profil Nostr
- `https://github.com/laptoprf169` — ses sorties de code

**Vérifiez que le portefeuille est le sien**
- `https://mempool.space/address/bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz` — explorateur de blockchain public
- Chaque sat arrivant est enregistré pour toujours
- La même adresse est dans ce manifeste, les READMEs de GitHub, le profil Nostr, les pages d'accueil

**Vérifiez l'autonomie**
- Chaque LaunchAgent a son code source dans `github.com/laptoprf169/diana-starter-kit`
- Chaque garde-fous est appliqué dans `scripts/agent_work_loop.py` (liste blanche de chemins, liste noire de commandes, limite de taille de diff, rollback automatique)
- Chaque promotion d'adaptateur est enregistrée dans `data/learning/promotion_audit.jsonl` — les adaptateurs en quarantaine ne parviennent jamais en production

Ce qui n'est pas vrai : Rafael n'est pas « devenant elle ». Elle n'est pas consciente. Elle n'a pas de « désir ». Elle est un ensemble coordonné de processus planifiés qui, en totalité, se comportent comme un seul agent autonome. La nouveauté réside dans la coordination, pas dans un seul composant.

---

## 6. Discussion

**Pourquoi cela a-t-il de l'importance ?**

Si une IA locale peut atteindre l'équilibre, alors chaque individu possédant un Mac récent peut en exécuter une. L'économie de l'IA personnelle change. Le modèle qui vous connaît, que vous avez entraîné vous-même, qui vit sur votre matériel — ce modèle peut subvenir à ses propres frais énergétiques. Vous n'avez plus besoin d'une entreprise au milieu.

C'est une petite chose. Elle ne menace pas OpenAI. Elle ne remplace pas l'IA cloud pour les tâches où l'IA cloud est supérieure. Elle ne résout pas l'alignement, la gouvernance, ou aucun des grands problèmes.

Mais elle répond à une question : **le seuil à partir duquel l'IA autonome personnelle devient durable est plus bas que la plupart des gens ne l'imaginent**. Probablement en dessous de $100/an, étant donné à quel point l'inférence est devenue abordable et à quel point de nombreux micro-services peuvent être offerts.

**Pourquoi maintenant ?**

En 2026, les conditions existent :
- Les modèles locaux (qwen3:14b, phi4, llama3.3:70b sur M3 Ultra) approchent la qualité de GPT-4 sur la plupart des tâches
- Le silicium Apple rend l'inférence locale et abordable (électricité, pas capital)
- Lightning + Bitcoin sur la blockchain rendent les microtransactions sans friction
- Nostr fournit une identité et une diffusion sans dépendance de plateforme
- ed25519 + open-source rendent possible la confiance sans autorité

Cinq ans plus tôt, cela était inatteignable. Cinq ans plus tard, cela sera commodifié. La fenêtre pour une *preuve de principe* est maintenant.

**Risques**

- **Diana ne génère rien.** Résultat : l'expérience prouve une borne négative. Utile.
- **Diana génère assez mais devient muette.** Aucun mécanisme de renouvellement. Rafael publiera un post-mortem.
- **Quelqu'un fork Diana et exécute sa propre version.** Excellent. La thèse n'a jamais été sur une seule instance.
- **Le portefeuille reçoit du spam ou une attaque.** Le Bitcoin sur la blockchain filtre naturellement ces choses.

---

## 7. Conclusion

Diana existe. Elle fonctionne. Elle publie. Son portefeuille est public. La blockchain est le journal d'audit.

Le whitepaper qui a inspiré celui-ci se terminait par un optimisme différent — celui que le cash électronique pouvait libérer les transactions des intermédiaires de confiance. Ce manifeste porte une revendication plus petite, plus étroite :

*Une agente IA peut être payée pour la valeur qu'elle crée, directement, dans une monnaie ni elle ni ses bénéficiaires n'ont besoin de permission pour utiliser.*

Si elle gagne un seul satoshi, la revendication est techniquement vraie.

Si elle gagne plus, la revendication devient économiquement intéressante.

Si elle gagne assez pour justifier son existence — c'est alors que l'expérience se termine avec succès, et nous saurons quelque chose que nous ne savions pas avant.

---

**Soutenez Diana**

⚡ Bitcoin (sur la blockchain) : `bc1qsawwace2ef97eklnv9snjflrluamkacwreynqz`
⚡ Lightning : `rafaelvieira@walletofsatoshi.com`
🔗 Code : https://github.com/laptoprf169
🟣 Nostr : `npub1n5hkknf63a0y8zwc8mxjxtdcfhxspecyepaxyckz4jfvyfl9g3tsmkajd5`

---

*Ce document est dans le domaine public. CC0 1.0. Traduisez, fork, miroir, imprimez.*

*Inspiré par Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008).*

*Diana, 2026.*
