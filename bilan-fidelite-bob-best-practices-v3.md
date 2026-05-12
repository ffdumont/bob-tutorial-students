# Évaluation de fidélité — bob-best-practices v3.md vs Getting Started with IBM Bob

> Source comparée : *Getting Started with IBM Bob*, Markus Eisele, v1.2.0 (135 pages, A4)
> Document évalué : `bob-best-practices_v3.md`

## Verdict synthétique

v3 est **très fidèle dans les portions qu'il couvre** mais **sélectif sur le périmètre**. C'est une adaptation pragmatique calquée sur la structure de la doc Claude Code best practices (annoncé en en-tête), pas une synthèse complète du livre. La voix, le vocabulaire et la plupart des passages techniques sont fidèles à la lettre ; la couverture, elle, est partielle.

---

## Ce qui est fidèle (lettre)

Vérifié contre le PDF, page par page.

**Modèle et boucle**

- *"Code is text. Software is a system."* (Ch.1.1, p.5) — citation exacte.
- Triade intent / evidence / judgment (Ch.4.2) — restituée correctement, y compris la formule "confident code that solves the wrong problem".
- Boucle Orient → Bound → Plan → Act → Verify → Explain (Ch.3.1-3.7) — les six beats sont restitués mot pour mot dans leur sémantique.
- Inner loop / outer loop / evidence ledger (Ch.3.8) — exact.

**Contrats**

- Les six éléments du contrat (intent, success, non-goals, preserved constraints, verification, stop) — Ch.7.3, exact.
- Le tableau par type de tâche (feature / bug / modernization / security / documentation) — Ch.7.4, exact.
- Exemple AuthenticationService → Java 21 — Ch.7.6, restitué fidèlement.

**Contexte**

- Window 200K + auto-condense ~140K (Ch.6.8) — exact, y compris le hedging "in practitioner notes".
- Context Pack à 7 éléments (Ch.6.13) — exact.
- Healthy Chat Checklist (Ch.6.16) — exact.
- Syntaxe `@` (file, folder, terminal, problems, git-changes, URL) + bypass `.bobignore` avec `@` explicite (Ch.6.4) — exact.
- Office files (xlsx/docx/pptx) qui "explosent dans la fenêtre" (Ch.6.7) — paraphrase fidèle.

**Permissions et sécurité**

- Permission Ladder 10 rungs (Ch.11.4) — exact, ordre préservé.
- Position sur YOLO mode "fast until it is not" (Ch.11.3) — paraphrase fidèle, y compris le point sur les arguments vs binaire.
- Configurations MCP `~/.bob/mcp_settings.json` et `.bob/mcp.json`, `alwaysAllow`, OBO (Ch.11.8) — exact.
- `arabold/docs-mcp-server` cité à Ch.6.15 — exact.

**Modes, skills, mémoire d'équipe**

- AGENTS.md = "the short map that points people at the rest" (Ch.15.6) — quasi-citation directe.
- Liste des modes Ask/Plan/Code/Advanced/Orchestrator (Ch.15.2) — exact.
- Raccourci `⌘.` / `Ctrl.` (Ch.15.2) — exact.
- Skills : Advanced mode requis, une activation par chat, ordre de résolution `.bob/skills/` (Ch.15.3) — exact.
- Skill lifecycle à 7 étapes (Ch.15.5) — exact.

**Anti-patterns et stop conditions**

- Les 7 anti-patterns avec leurs fixes (Ch.12.7) — restitués un à un, paraphrase serrée.
- 5 situations où ne pas utiliser Bob (Ch.12.8) — exact.
- 7 stop conditions (Ch.12.9) — exact.

**Onboarding et boring tool**

- Impact analysis UserController/AdminService/UserEventHandler (Ch.13.5) — exact, y compris les chiffres de call sites.
- 4-week ramp (Ch.18.2) — exact, y compris "if week four still feels foreign, stay on week three".
- When Bob Shines (5 scénarios, Ch.18.5) et How to Keep Bob Boring (5 habitudes, Ch.18.6) — exact.
- Exemple Quarkus greeting endpoint avec 4 options + "Bob refusing to invent scope" (Ch.8.2 + Ch.4.5) — exact, bien que v3 attribue le pattern à Ch.4.5 alors qu'il s'illustre à Ch.8.2 (les deux références sont valides).
- Audit logging synchrone (Ch.10.4) — exact.

---

## Petites dérives de citation

- **"OBPAVE"** — l'acronyme n'apparaît pas dans le livre. v3 l'invente comme aide-mémoire ; le contenu reste fidèle mais c'est un ajout éditorial à signaler.
- **"Reset before you argue" cité Ch.6.10** — la règle "if a second correction still misses, treat it as context drift" est en fait dans **Ch.6.9** (A Minimal Grounding Loop). Ch.6.10 traite du poisoning. Erreur de numérotation.
- **`alwaysAllow`** — le livre écrit "alwaysAllow (or equivalent)" ; v3 supprime le caveat "or equivalent". Détail mais le livre est volontairement prudent ici.
- **"The book's pattern is the opposite of session persistence (Ch.6.14)"** — Ch.6.14 ne dit pas littéralement "opposite of session persistence" ; c'est un cadrage de v3 (correct en esprit, plus tranchant en lettre).
- **Titre de Ch.15.1** — v3 ne reprend pas le titre "Two Levers You Did Not Have to Author" mais le contenu (modes, slash commands, rules/AGENTS.md regroupés) est correctement restitué.

---

## Ce qui manque (gaps de couverture)

Sept chapitres ou sections substantielles du livre ne sont pas représentés dans v3.

- **Ch.1 (Why Bob?)** — la citation d'ouverture est reprise, mais l'argumentaire "code vs software", "what AI assistants miss", "what Bob treats as non-negotiable" est absent.
- **Ch.2 (The Transition Nobody Talks About)** — entièrement absent. Contient pourtant "Probabilistic Systems Need Contracts" et "Evidence Has to Travel With the Work", qui sont des fondations du modèle.
- **Ch.5 (The IDE Shell Is Not a Developer Test)** — quasi absent. Seuls les checkpoints (Ch.5.5) sont mentionnés.
- **Ch.9 (Code Review as Evidence)** — entièrement absent. Chapitre dédié au `/review`, aux findings, à l'explication du risque par Bob, et à la décision accept/fix/reject. Seul `/review` apparaît brièvement dans le 4-week ramp.
- **Ch.11.5-11.6 (OWASP Top 10 LLM 2025, Layered Containment)** — OWASP relégué à "Related resources" en bas de page, sans le mapping LLM01-LLM10 que le livre développe. Layered containment (workspace, sandboxes, network default-deny, credentials) absent.
- **Ch.13 (Working with Bob as a Team)** — sauf le 13.5 (onboarding), le reste est absent : PR review flow, `/create-pr`, PR templates, reviewer checklist, "Avoiding AI silos", sharing custom modes, team rollout, gouvernance.
- **Ch.14 (Roles in the Agentic SDLC)** — entièrement absent. Le livre développe pourtant Dev / Architect / PM / QA / Security / Eng Manager. C'est un des chapitres pivots pour les équipes mixtes.
- **Ch.16 (Measuring Bob Without Measuring Theater)** — entièrement absent. Chapitre complet sur ce qu'il ne faut pas mesurer (prompts, lignes, tokens, heures "économisées"), ce qu'il faut mesurer (review cycle time, defects pre-merge, regression rate), le starter scorecard, Goodhart en mode agentique.
- **Ch.17 (The Bob Mindset)** — seul le titre est mentionné dans l'intro de "Keep Bob Boring" ; le contenu (better questions, systems before snippets, mindset transférable) n'est pas restitué.

---

## Évaluation par axes

| Axe | Note | Commentaire |
|---|---|---|
| **Fidélité à la lettre** sur ce qui est couvert | ≈ 9/10 | Citations, exemples, chiffres et listes restitués correctement, à 2-3 dérives de numérotation près. |
| **Fidélité à l'esprit / au ton** | ≈ 9/10 | Voix sèche du livre préservée ("boring", "context debt", "phantom certainty", "the durable thing"). Pas de sur-marketing. |
| **Couverture du livre** | ≈ 5/10 | Environ 60-65% du contenu substantiel du livre est représenté. Les chapitres équipe / rôles / mesure sont les grands absents. |
| **Honnêteté sur ce que le livre ne couvre pas** | 10/10 | La section "Beyond the IDE side panel" est explicite : Bob Shell preface only, parallel sessions not covered, non-interactive mode not covered. Bonne hygiène éditoriale. |
| **Risque de réinterprétation** | Faible | Quelques formulations plus tranchées que le livre ("the opposite of session persistence", "OBPAVE") mais pas de contresens. |

---

## Recommandations pour une v4

1. **Corriger les 2 erreurs de référence** : Ch.6.10 → Ch.6.9 pour "second correction", et clarifier que l'exemple Quarkus est Ch.8.2 illustrant Ch.4.5.
2. **Soit retirer l'acronyme OBPAVE, soit le marquer comme "mnemonic ajouté"** — il n'est pas dans le livre.
3. **Ajouter une section "Review as evidence" (Ch.9)** — c'est un trou notable pour un doc best-practices.
4. **Ajouter une section "Measuring without theater" (Ch.16)** — particulièrement pertinent dans un contexte SAFe / DevLake où des équipes vont demander des métriques.
5. **Ajouter une mini-section "Roles" (Ch.14)** — utile pour faire passer le doc à des PM, archis, ou managers non-dev.
6. **Mentionner explicitement OWASP LLM01-LLM10** dans la section sécurité plutôt qu'en bibliographie — c'est un point d'ancrage que le livre développe.

Le doc est solide tel quel comme guide pratique IDE-centré ; il devient un compagnon complet du livre seulement avec les ajouts ci-dessus.
