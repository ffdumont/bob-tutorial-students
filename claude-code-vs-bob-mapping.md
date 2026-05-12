# Claude Code ↔ IBM Bob — mapping détaillé

Mapping section par section à partir de la table des matières des *best practices Claude Code*. Les cases marquées **—** indiquent une absence d'équivalent direct dans le livre *Getting Started with IBM Bob* (et donc une différence de design assumée par l'un ou l'autre produit).

## Mapping section par section

| Claude Code | IBM Bob — équivalent |
|---|---|
| **1. Give Claude a way to verify its work** | **Ch.7 Contracts Before Code** — le contrat nomme explicitement la méthode de vérification (tests qui passent, comportement préservé, critère d'acceptation). Renforcé par le beat **Verify** de la boucle OBPAVE. |
| **2. Explore first, then plan, then code** | **Ch.3 The Agentic SDLC — boucle OBPAVE** : Orient → Bound → Plan → Act → Verify → Explain. Bob sépare planning et exécution en deux phases distinctes (Ch.4.3) : pendant Plan, *rien ne s'écrit sur disque*. |
| **3. Provide specific context in your prompts** | **Ch.6 Context Is the Work** — signal vs noise (Ch.6.3), grounding habits (Ch.6.5), "Most hallucinations are context debt" (Ch.6.12). Recettes : un objectif par tâche, fichier+plage de lignes plutôt que dossier entier. |
| **4. Provide rich content** | **Context mentions** (Ch.6.4) : `@file`, `@folder`, `@problems`, `@terminal`, `@git-changes`, `@URL`. Même principe : attacher la preuve réelle, pas une paraphrase. |
| **5. Configure your environment** | — *(voir sous-sections)* |
| &nbsp;&nbsp;&nbsp;**5.1 Write an effective CLAUDE.md** | **`AGENTS.md`** + **`.bob/rules/`** (Ch.15.1, Ch.15.6) — la carte courte qui pointe vers le reste, plus les contraintes qui doivent tenir à chaque tour. |
| &nbsp;&nbsp;&nbsp;**5.2 Configure permissions** | **Ch.11.4 The Permission Ladder** (10 barreaux, monter délibérément) + **Modes** (Ch.5.5, Ch.15.2) qui plafonnent les outils accessibles. |
| &nbsp;&nbsp;&nbsp;**5.3 Use CLI tools** | **Implicite dans Code/Advanced mode** — le livre ne traite pas cela comme une discipline propre. Accès shell mentionné comme barreau 5 de l'échelle de permissions (Ch.11.4), sans recommandation `gh`/`aws`/`gcloud`. *Gap relatif.* |
| &nbsp;&nbsp;&nbsp;**5.4 Connect MCP servers** | **Ch.11.8 MCP and Enterprise Integration** + **Ch.6.15 Docs MCP server**. Configuration dans `~/.bob/mcp_settings.json` / `.bob/mcp.json`, gateway + vault + OBO, `alwaysAllow` vide par défaut. |
| &nbsp;&nbsp;&nbsp;**5.5 Set up hooks** | **— Pas d'équivalent direct.** `.bob/rules/` est *consultatif* (texte que Bob lit), pas déterministe. Aucun mécanisme du type "exécute eslint après chaque edit" décrit dans le livre. *Gap structurel.* |
| &nbsp;&nbsp;&nbsp;**5.6 Create skills** | **Ch.15.3-15.5 Skills** — `.bob/skills/SKILL.md` (résolution projet > global > extensions). Une activation par chat, mode Advanced requis, cycle de vie explicite (notice → capture → package → test → retire). |
| &nbsp;&nbsp;&nbsp;**5.7 Create custom subagents** | **Partiel** : **Orchestrator mode** (Ch.5.4, Ch.15.2) coordonne des sous-tâches, et Ch.6.14 mentionne "helper agents or split flows for exploration" selon l'installation. Pas de définition utilisateur en `.bob/agents/` avec prompt système et modèle dédié. *Gap relatif.* |
| &nbsp;&nbsp;&nbsp;**5.8 Install plugins** | **— Pas d'équivalent direct.** Ch.15.3 mentionne "whatever extensions install" mais pas de marketplace `/plugin`. Distribution se fait par admin (modes/skills/commandes custom). *Gap structurel.* |
| **6. Communicate effectively** | — *(voir sous-sections)* |
| &nbsp;&nbsp;&nbsp;**6.1 Ask codebase questions** | **Ch.13.5 Using Bob for Onboarding and Knowledge Transfer** — "Analyze the UserService", "What would happen if I change this method?", "What does this code do?". Ch.6 ajoute le grounding obligatoire. |
| &nbsp;&nbsp;&nbsp;**6.2 Let Claude interview you** | **Ch.4.5 Why Bob Asks Before It Acts** + **Ch.8.2** — Bob pose des questions de clarification *réactives* avant de planifier ("What type of validation…", "Should I preserve the synchronous audit logging…"). Pas d'outil `AskUserQuestion` invocable explicitement par l'utilisateur. |
| **7. Manage your session** | — *(voir sous-sections)* |
| &nbsp;&nbsp;&nbsp;**7.1 Course-correct early and often** | **Ch.6.10 When Context Goes Bad: Poisoning** + **Ch.12.9 Stop Conditions** — escalade par sévérité. Règle : *"if a second correction still misses, treat it as context drift — restart with a smaller, cleaner context set."* |
| &nbsp;&nbsp;&nbsp;**7.2 Manage context aggressively** | **Ch.6.8 What "200k Tokens" Means** + **Ch.6.13 The Context Pack** — fenêtre partagée (système + history + mentions + tool output), auto-condense vers ~140K, hard cap ~200K. Notion de *context pack* : le minimum d'évidence bornée pour une tâche. |
| &nbsp;&nbsp;&nbsp;**7.3 Use subagents for investigation** | **Partiel** : Ch.6.14 — "isolating broad exploration in a helper flow so the main thread only receives short findings". Pratique recommandée mais pas formalisée avec un répertoire utilisateur dédié. |
| &nbsp;&nbsp;&nbsp;**7.4 Rewind with checkpoints** | **Ch.5.5 / Ch.11.7 Checkpoints** — sauvegarde avant écriture, *restore files* vs *restore files and task*. Explicitement positionné comme complément (non remplacement) de Git. |
| &nbsp;&nbsp;&nbsp;**7.5 Resume conversations** | **— Philosophie inverse.** Ch.6.14 Session Handoff and Long Threads : pas de `--continue`/`--resume` ; le pattern est *"capture a small handoff artifact (souvent un `docs/handoff-[feature].md`) et démarre une tâche propre"*. Le livre déconseille de prolonger un thread long. |
| **8. Automate and scale** | — *(voir sous-sections — couverture globalement faible)* |
| &nbsp;&nbsp;&nbsp;**8.1 Run non-interactive mode** | **— Quasi-absent.** "Bob Shell" est mentionné dans la préface mais le livre ne couvre pas `claude -p` / `--output-format json` / pipes. *Gap éditorial.* |
| &nbsp;&nbsp;&nbsp;**8.2 Run multiple Claude sessions in parallel** | **— Non couvert.** Pas de worktrees, ni de Writer/Reviewer pattern, ni de sessions cloud isolées décrites. |
| &nbsp;&nbsp;&nbsp;**8.3 Fan out across files** | **— Non couvert.** Pas de pattern `for file in $(...); do bob -p "..."; done`. |
| &nbsp;&nbsp;&nbsp;**8.4 Run autonomously with auto mode** | **Ch.11.3 YOLO mode** — *mentionné pour le déconseiller* sur shell/réseau/infra : "It is fast until it is not — one injected prompt can act at machine speed." Posture explicitement défensive. |
| **9. Avoid common failure patterns** | **Ch.12.7 Anti-Patterns When Using Bob** (les 7 : Copy-Paste Developer, Approval Bot, Context-Free Requester, Blame Shifter, Black Box User, Shortcut Seeker, Production Experimenter) + **Ch.12.9 Stop Conditions**. |
| **10. Develop your intuition** | **Ch.17 The Bob Mindset** + **Ch.18 Keeping Bob Boring** — montée par paliers (S1 analyse seule → S2 review → S3 planning → S4 boucle complète), répétition plutôt que collection de patterns. |

## Différences philosophiques

### Conservées de la version précédente

- Bob insiste beaucoup plus sur les **contrats avant le code** (le diff exact n'est pas durable, le contrat l'est).
- La séparation **Intent / Evidence / Judgment** est explicite chez Bob, implicite chez Claude Code.
- Bob a une vraie **échelle de modes** (Ask / Plan / Code / Advanced / Orchestrator) là où Claude Code a plan mode + auto mode.
- Le chapitre **"Keep Bob Boring"** n'a pas d'équivalent direct côté Claude Code — il reflète la posture conservatrice du livre.

### Ajoutées par le mapping complet

- **Pas de hooks chez Bob.** Claude Code rend déterministes certaines actions (eslint après chaque edit, blocage d'écriture dans un dossier). Les `.bob/rules/` sont *consultatifs* — Bob les lit mais peut techniquement les ignorer. C'est un vrai gap fonctionnel pour les équipes qui veulent de la garantie, pas de la suggestion.
- **Pas de subagents utilisateur chez Bob.** Claude Code permet de définir en `.claude/agents/` des assistants spécialisés (avec leur propre prompt système, modèle, outils). Bob a Orchestrator (interne, coordonné par Bob) et des "helper flows" optionnels selon l'installation — mais pas de définition utilisateur first-class.
- **Pas de marketplace de plugins chez Bob.** `/plugin` côté Claude Code packagee skills + hooks + subagents + MCP en unités installables. Bob distribue par admin enterprise, sans modèle communautaire.
- **Modèle de session opposé.** Claude Code mise sur la persistance (`--continue`, `--resume`, `/rename`, checkpoints persistant entre sessions). Bob mise sur la rotation (*"don't drag yesterday's tangent forward"* — handoff note + tâche propre). Pour Francois en pratique : si tu apprécies de reprendre un long thread Claude Code le lendemain, c'est un changement de réflexe avec Bob.
- **Automatisation et fan-out : approches divergentes.** La section "Automate and scale" est l'écart le plus visible. Claude Code documente explicitement le mode non-interactif, le fan-out shell, les sessions parallèles, et l'auto mode comme outils légitimes. Le livre Bob est silencieux sur ces patterns ou les déconseille (YOLO mode). Bob est conçu comme un **cockpit IDE-centric** ; Claude Code accepte mieux le rôle de **CLI-orchestrator** sur des lots de fichiers.
- **Layering de la mémoire d'équipe.** Claude Code superpose : `CLAUDE.md` (advisory) + hooks (déterministes) + skills (workflows) + subagents (spécialistes) + plugins (bundling). Bob superpose : `AGENTS.md` + `.bob/rules/` + slash commands + skills + modes + `.bobignore`. Bob a *plus de couches d'advisory* et zéro couche déterministe ; Claude Code combine les deux registres.
- **OWASP LLM Top 10 comme vocabulaire partagé.** Bob l'explicite (Ch.11.5) comme socle de dialogue avec la sécurité et l'audit. Claude Code ne l'invoque pas directement — la sécurité y est gérée par sandboxing, allowlists et auto mode classifier, pas par un référentiel externe nommé.
