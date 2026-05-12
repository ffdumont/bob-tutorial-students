# Bonnes pratiques pour IBM Bob

> Source : *Getting Started with IBM Bob*, Markus Eisele (v1.2.0)
> Structure alignée sur : https://code.claude.com/docs/en/best-practices

Bob est un partenaire IA pour le cycle de vie du développement logiciel. La prémisse est sans détour : le code est du texte, le logiciel est un système. Écrire du code n'a jamais été aussi facile ; concevoir des systèmes, les modifier sans casse, et leur garder de la valeur dans le temps, ça l'est toujours.

Le modèle mental de Bob a trois parties, séparées à dessein :

- **Intent** — ce que tu cherches à accomplir
- **Evidence** — ce qui existe réellement dans le dépôt
- **Judgment** — ce qui doit être fait

Les mélanger produit du code confiant qui résout le mauvais problème.

---

## Le contrat avant le code

Le diff exact que Bob écrit n'est pas l'artefact durable — sur une nouvelle exécution, Bob peut prendre un chemin différent mais tout aussi raisonnable. Ce qui demeure, c'est le contrat : la manière dont l'équipe reconnaît un résultat correct même quand l'implémentation varie.

Un contrat utile nomme six choses :

- intention de la tâche
- condition de succès
- non-objectifs
- contraintes à préserver
- méthode de vérification
- condition d'arrêt

La forme du contrat change selon la nature du travail :

- **Feature** — critères d'acceptation
- **Bug** — un test rouge qui devient vert, plus la garantie que le comportement adjacent reste intact
- **Modernisation** — comportement préservé ; les tests existants doivent toujours passer ; tout changement de comportement intentionnel est nommé, pas glissé en douce
- **Sécurité** — réduction de la menace plus aucune nouvelle exposition
- **Documentation** — exactitude par rapport au comportement effectivement livré, pas une formulation qui sonne plausible

Exemple de contrat pour une tâche de modernisation :

> *"Modernize AuthenticationService to Java 21 style while preserving all existing login, token refresh, and audit behavior. No public API changes. All existing tests must pass unchanged. Stop if the refactor requires a behavior change we cannot explain in the PR."*

Le bon moment pour écrire le contrat est avant l'exécution, pas après qu'un diff séduisant soit apparu.

*See Ch.7 (Contracts Before Code).*

---

## Orient, bound, plan — puis act

La boucle d'opération canonique a six temps : **Orient → Bound → Plan → Act → Verify → Explain** (OBPAVE).

**Orient** — Bob lit le dépôt, les fichiers liés, les tests, l'historique. Les modes Ask et Plan sont en lecture seule ; ce temps se passe avant toute écriture sur disque.

**Bound** — nommer ce qui est autorisé : fichiers dans le périmètre, changements hors périmètre, approbations requises, limites d'environnement, conditions d'arrêt. La confiance n'est pas l'autorisation.

**Plan** — Bob propose un chemin. Un plan utile nomme ce qui va changer, pourquoi, ce qui peut casser, ce qui reste inchangé, et comment le résultat sera vérifié. Pendant ce temps, rien n'est généré sur disque — la séparation entre plan et exécution est délibérée.

**Act** — n'exécuter que la tranche approuvée. L'exécution doit être mécanique : prévisible, ennuyeuse. Les surprises appartiennent à la phase de planification, tant que tu peux encore changer d'avis.

**Verify** — vérifier le comportement, pas le mouvement. Tests, revue de diff, inspection manuelle, vérification du comportement préservé, critères d'acceptation.

**Explain** — laisser derrière soi des éléments qu'un autre pourra relire plus tard. Historique de tâche, description de PR, ticket, court ADR, notes de release.

La boucle tourne à deux échelles : une **inner loop** (la tâche immédiate) et une **outer loop** (règles partagées, modes, habitudes de revue à l'échelle de l'équipe). L'**evidence ledger** — plans, findings, historique de tâche, diffs, notes de vérification — les connecte, pour qu'une tâche devienne un apprentissage organisationnel plutôt qu'un échange de chat isolé.

*See Ch.3 (The Agentic SDLC), Ch.4.3 (Why Bob Separates Planning from Execution).*

---

## Signal contre bruit

Le contexte est un budget, pas un dépotoir. Deux requêtes avec la même intention peuvent obtenir des réponses très différentes selon ce qui occupe la fenêtre :

| Signal fort | Signal faible |
|---|---|
| Extrait de fichier exact et objectif explicite | Code paraphrasé et intention vague |
| Stack trace réelle ou sortie terminal | Souvenir d'une erreur « quelque part dans utils » |
| Une mission par fil | Plusieurs buts non liés dans un même chat |
| Doc ou specs courantes de l'API visée | Hypothèses tirées d'un rappel libre dépassé |

Habitudes d'ancrage (*grounding habits*) :

- Mentionne les fichiers exacts et plages de lignes quand tu le peux
- Ne paraphrase pas du code de mémoire quand `@` peut chercher le texte réel
- Colle des stack traces réelles ou utilise `@terminal` / `@problems`
- Garde un seul objectif clair par fil de tâche
- Lie la doc ou la spec faisant autorité quand la réponse doit coller à un contrat externe
- Ne traite pas les tours de chat précédents comme une mémoire durable entre sessions — ré-ancre avec des `@` quand c'est important

La plupart des « hallucinations » sont de la *context debt* : une contrainte manquante, une source de vérité manquante, une attente de test manquante, une règle métier qui n'est jamais entrée dans la tâche.

*See Ch.6.3 (Signal Versus Noise), Ch.6.5 (Grounding Habits), Ch.6.12 (Most Hallucinations Are Context Debt).*

---

## Pointer Bob vers la vérité

Taper `@` attache des artefacts du workspace volontairement. Recette : `@` mentions précises, texte d'erreur exact (ou `@terminal` / `@problems`), et un objectif en une phrase.

- `@/chemin/fichier` — contenu exact du fichier ; sur les gros fichiers, utilise une plage de lignes, ex. `@/chemin/Fichier.java:80-120`
- `@/chemin/dossier` — fichiers frères ; les mentions de dossier ne sont pas récursives
- `@problems` — diagnostics du panneau Problems
- `@terminal` — sortie de build ou CLI comme preuve
- `@git-changes` ou un hash de commit — quand tu raisonnes sur des diffs, des commits, du non-commité
- `@` plus une URL — la doc externe ou les specs ancrent la réponse

Les fichiers Office paraissent petits sur disque et explosent dans la fenêtre : `.xlsx`, `.docx`, `.pptx` traînent feuilles, métadonnées de révision, slide masters, notes d'orateur, plages cachées. Filtre les lignes, masque les feuilles inutiles, exporte des CSV bornés.

Les `@` explicites sur fichier ou dossier contournent `.bobignore` et `.gitignore` lors de la récupération de texte. `.bobignore` garde secrets, clés et chemins bruyants hors des lectures de routine ; un `@` explicite est l'override quand tu veux délibérément tirer un chemin.

*See Ch.6.4 (Point Bob at the Truth: context mentions), Ch.6.7 (Large spreadsheets, documents, and slides).*

---

## Mettre en place la mémoire d'équipe

### Écrire ce que « normal » veut dire ici

Trois couches portent la mémoire d'équipe :

- **Modes** plafonnent ce que Bob peut faire pendant un chat
- **Slash commands** glissent des prompts pré-rédigés — `.bob/commands/` (équipe) ou `~/.bob/commands/` (personnel)
- **Rules et project briefs** portent le matériel qui bouge plus lentement — `AGENTS.md`, `.bob/rules/`, et autres textes locaux au dépôt qui disent ce que « normal » veut dire ici

`AGENTS.md` est la carte courte qui pointe vers le reste. `.bob/rules/` porte les contraintes qui doivent tenir à chaque tour. Les deux sont lus chaque fois que Bob planifie, les deux sont relus comme du code, les deux vivent dans le dépôt.

*See Ch.15.1 (Two Levers You Did Not Have to Author), Ch.15.6 (Choose the Right Memory Layer).*

### Gravir l'échelle des permissions

Les permissions de l'agent sont une échelle, pas un interrupteur binaire :

1. Lire des fichiers et expliquer
2. Résumer et planifier
3. Éditer des fichiers
4. Exécuter des tests
5. Exécuter des commandes shell
6. Utiliser le réseau
7. Utiliser des outils MCP
8. Toucher des environnements partagés
9. Préparer des changements de production
10. Exécuter des changements de production

Monte seulement quand la tâche le justifie ; jamais plusieurs barreaux à la fois sous prétexte que le modèle a l'air confiant.

Choisis le mode avant de peaufiner la phrase :

- **Ask** — explications sans modifications
- **Plan** — stratégie avant commit
- **Code** — quand le dépôt et le shell suffisent
- **Advanced** — quand il faut le navigateur, MCP, ou les skills
- **Orchestrator** — pour le travail qui traverse vraiment plusieurs spécialités ; coordonne des sous-tâches plutôt que de forcer un seul mode à tout posséder

Cycle entre les modes avec `⌘.` (macOS) ou `Ctrl.` (Windows/Linux).

Le mode YOLO (tout auto-approuvé) laisse shell, fichiers et réseau s'exécuter sans pause humaine — rapide jusqu'à ce qu'un prompt injecté agisse à la vitesse machine. Désactive l'auto-approbation globale pour shell, réseau sortant et outils qui modifient l'infrastructure. Autoriser un nom de commande n'empêche pas des flags hostiles sur ce même binaire ; le risque tient rarement au binaire seul, il tient aux arguments.

*See Ch.11.3 (Approvals, YOLO Mode, and "Safe" Commands), Ch.11.4 (The Permission Ladder), Ch.15.2 (Finding Commands and Switching Mode).*

### Accès shell via le mode Code

Les modes Code et Advanced peuvent lancer un shell — barreau 5 de l'échelle des permissions. La même posture que pour le reste de l'échelle s'applique : garde les arguments visibles, préfère les approbations par action plutôt que les allowlists de noms d'exécutable, et souviens-toi que le risque vit dans les arguments, pas dans le nom du binaire.

*See Ch.11.4 (The Permission Ladder).*

### MCP et intégration entreprise

MCP connecte Bob à des systèmes externes et fait partie de ta surface d'attaque.

- La configuration vit dans `~/.bob/mcp_settings.json` (utilisateur) et `.bob/mcp.json` (projet). Traite ces fichiers comme des configs d'intégration de production ; relis-les en pull request ; ne commit pas de secrets à longue durée de vie en clair.
- La liste `alwaysAllow` exécute des outils nommés sans demande d'approbation — un petit YOLO. Garde-la vide pour tout ce qui écrit, lance des commandes ou touche des systèmes sensibles.
- Place MCP derrière une gateway avec des credentials à durée courte émises par un coffre.
- Les systèmes en aval doivent voir l'identité du développeur (On-Behalf-Of), pas un compte de service partagé surdoté.

Chaque serveur MCP est un pont vers un autre système — credentials, scopes et exécutions silencieuses d'outils méritent le même scepticisme que livrer une nouvelle dépendance microservice. `arabold/docs-mcp-server` est un motif utile pour indexer de la doc versionnée afin que les réponses s'ancrent sur les versions courantes plutôt que sur les *training priors* statiques.

*See Ch.11.8 (MCP and Enterprise Integration), Ch.6.15 (Docs MCP server).*

### Rules et project briefs

`AGENTS.md` et `.bob/rules/` portent le matériel de pilotage qui bouge lentement, lu chaque fois que Bob planifie. `AGENTS.md` est la carte courte ; les règles sont les contraintes qui doivent tenir à chaque tour. Les deux sont relus comme du code et committés avec le dépôt.

Associe la couche mémoire au cas d'usage :

- **Slash commands** — les demandes répétées que tu veux à un raccourci
- **Modes** — posture et permissions pour des fils entiers
- **Rules** — contraintes qui doivent tenir à chaque tour
- **Skills** — flux de travail multi-étapes avec outils et attentes de revue intégrés
- **AGENTS.md** — la carte courte qui pointe vers le reste

*See Ch.15.6 (Choose the Right Memory Layer).*

### Skills : flux déclenchés par des mots

Les skills sont des flux de travail que quelqu'un a déjà packagés — revues, contrôles de migration, passes de doc. Les utiliser ne veut pas dire éditer `SKILL.md` directement ; ça veut dire formuler la tâche pour que Bob fasse correspondre la description de la skill.

- Le mode Advanced est requis ; les skills supposent la surface d'outils complète
- Une activation par chat — la correspondance utilise tes mots et le texte de la skill ; si rien ne colle, tu obtiens une réponse générique
- Ordre de résolution : `.bob/skills/...` du projet bat le même nom en global, puis `~/.bob/skills/`, plus ce que les extensions installent
- Nomme le livrable dans la demande — *"security review of `src/api/auth.ts`"* ou *"release notes for the last twenty commits"* — plutôt que *"help with this file"*

Cycle de vie d'une skill :

1. Repère du travail répété ou de la confusion répétée
2. Capture le meilleur flux actuel en langage simple
3. Transforme-le en skill, command, mode ou rule seulement quand le motif est assez stable pour mériter d'être partagé
4. Teste-la sur de vrais exemples
5. Documente quand l'utiliser et quand ne pas l'utiliser
6. Relis-la comme du code
7. Retire-la quand l'équipe ou le produit change

Une skill périmée n'est pas neutre — c'est une habitude désuète mieux packagée.

*See Ch.15.3 (Skills: Packaged Workflows You Trigger With Words), Ch.15.4 (Skills Are Team Habits in Package Form), Ch.15.5 (The Skill Lifecycle).*

### Orchestrator et flux auxiliaires

Pour le travail qui traverse vraiment plusieurs spécialités, le mode **Orchestrator** coordonne les sous-tâches plutôt que de tout entasser dans un seul mode. Ce n'est pas « tous les outils dans un seul paquet aveugle » — il route des sous-tâches vers des contextes bornés.

Certaines installations exposent aussi des **helper agents ou split flows** pour l'exploration. Quand ils sont disponibles, ils permettent au fil principal de ne recevoir que des findings courts et cités, sans porter toute l'exploration dans la même fenêtre.

*See Ch.11.7 (Modes, Ignore Files, and Checkpoints), Ch.15.2 (Finding Commands and Switching Mode), Ch.6.14 (Session Handoff and Long Threads).*

### Distribution des assets personnalisés

Les modes, règles, skills et slash commands personnalisés sont distribués via les mêmes répertoires `.bob/...` que pour l'usage personnel. Les assets partagés équipe vivent dans le dépôt (`.bob/commands/`, `.bob/skills/`, `.bob/rules/`, `AGENTS.md`) ; les personnels vivent sous `~/.bob/`. Les extensions et l'outillage admin peuvent installer d'autres assets qui résolvent en dessous de ceux du projet dans l'ordre de lookup.

*See Ch.15.1 (Two Levers You Did Not Have to Author), Ch.15.3 (Skills: Packaged Workflows You Trigger With Words).*

---

## Demande, et laisse Bob te questionner

### Lire le code via Bob

Bob reflète les motifs déjà présents dans le dépôt quand il répond — les nouveaux arrivants ressentent le style maison par répétition. Demandes utiles (telles qu'écrites dans le livre) :

- *"Analyze this service and explain what it does"*
- *"Explain this pattern"*
- *"What does this code do?"*
- *"What would happen if I change this method signature?"*

La dernière produit une analyse d'impact. Pour une méthode appelée à plusieurs endroits, Bob renvoie quelque chose comme :

> *This method is called by: UserController (3 places), AdminService (1 place), UserEventHandler (2 places). Changing the signature would require updating all 6 call sites.*

Une répétition à bas coût bat le fait de corriger six sites d'appel après coup.

Démarre en mode Ask pour l'exploration en lecture seule.

*See Ch.13.5 (Using Bob for Onboarding and Knowledge Transfer).*

### Laisser Bob refuser d'inventer le périmètre

Bob n'édite pas le dépôt sans un point de contrôle ; ce point de contrôle force la clarté. Exemple canonique appliqué à un endpoint Quarkus de salutation : l'utilisateur tape *"Add validation to the greeting endpoint."* La première réponse de Bob refuse d'inventer le périmètre et propose des options :

- *Validate that the name parameter is not null or empty*
- *Validate name length (e.g. min 2, max 50 characters) and format (only letters and spaces)*
- *Add comprehensive validation: non-null, length constraints, character restrictions, and sanitization*
- *Show me the current endpoint code so I can suggest appropriate validation*

Choisis une option et l'intention se resserre assez pour qu'on puisse planifier.

Le même motif apparaît en modernisation, où Bob pose des questions sur les frontières de comportement avant de proposer un plan :

> - *Should I preserve the synchronous audit logging behavior, or is it okay to make it asynchronous?*
> - *Should I preserve the "email failures don't block" behavior, or should we add retry logic?*
> - *Should I add pagination to list queries, or keep the current behavior?*
> - *What Java version are we targeting?*

Ce sont des questions sur des frontières de comportement, pas du bruit ligne à ligne.

*See Ch.4.5 (Why Bob Asks Before It Acts), Ch.8.2 (Defining Intent Clearly), Ch.10.4 (Preserving Behavior While Refactoring).*

---

## Garder la fenêtre honnête

### Repartir à zéro avant de t'obstiner

Règle d'escalade quand le contexte va mal : si une seconde correction rate à nouveau, traite cela comme une dérive de contexte — redémarre avec un jeu de contexte plus petit et plus propre, au lieu d'argumenter en place.

Conditions d'arrêt — moments pour faire pause :

- Bob se répète sans ajouter de preuves
- Le plan change sans information nouvelle
- Tu ne peux pas expliquer le diff en langage clair
- La fenêtre est encombrée de matériel obsolète ou contradictoire
- Tu demandes à Bob de compenser une intention floue
- L'outil demande des permissions plus larges que ce que la tâche mérite
- L'approbation est devenue mécanique parce que tu es fatigué

La correction fiable n'est généralement pas « argumenter plus longtemps » ; c'est *reset context and re-ground*. Souvent, la correction est un nouveau chat avec un jeu de contexte minuscule et honnête.

*See Ch.6.10 (When Context Goes Bad: Poisoning), Ch.12.9 (Stop Conditions).*

### Le contexte est un budget, pas un dépotoir

La fenêtre est de l'ordre de 200K tokens, large mais partagée. Règles système, historique de chat, attachements `@` et sorties d'outils tirent tous du même pool. L'auto-condense (quand le produit résume les tours plus anciens) est citée autour de 140K ; le cap dur est dans le même ordre de grandeur que la taille annoncée de la fenêtre.

Le **Context Pack** est la plus petite évidence bornée dont Bob a besoin pour une tâche :

- intention de la tâche
- fichiers pertinents
- contraintes connues
- tests ou comportement attendu
- ticket ou scénario client lié
- non-objectifs
- condition d'arrêt

Livre un paquet qu'un autre relecteur pourrait suivre — pas un brain dump.

Checklist d'une conversation saine :

- **Avant** — un seul objectif par tâche, `@` direct quand possible, erreurs exactes depuis Problems ou terminal
- **Pendant** — surveille la pression token, relis itérativement, garde le périmètre de dossier serré
- **Avant de partir** — écris une handoff note (commit-la quand l'équipe trace les décisions dans Git)
- **Interdiction stricte** — pas de secrets dans le chat, pas de gros dumps Office bruts, ne pas prétendre que le chat d'hier est une mémoire permanente

*See Ch.6.1 (Why Context Is a Budget, Not a Dump), Ch.6.8 (What "200k Tokens" Means), Ch.6.13 (The Context Pack), Ch.6.16 (Healthy Chat Checklist).*

### Isoler l'exploration dans des flux auxiliaires

Quand l'exploration large risque d'encombrer la fenêtre, isole-la dans un flux auxiliaire pour que le fil principal ne reçoive que des findings courts. Là où l'installation expose des helper agents ou des split flows, utilise-les ; sinon, lance l'exploration dans une tâche séparée et référence ses findings courts et cités depuis le fil principal.

*See Ch.6.14 (Session Handoff and Long Threads).*

### Snapshot avant écriture

Avant les changements de fichiers, Bob peut sauvegarder un checkpoint — un point de restauration pour cette tâche :

- **Restore files** annule les fichiers et garde le chat
- **Restore files and task** annule les fichiers *et* tronque les messages postérieurs quand le fil a mal tourné

Les checkpoints complètent Git — ils ne le remplacent pas.

*See Ch.5.5 (What Bob Never Touches Unless You Approve It), Ch.11.7 (Modes, Ignore Files, and Checkpoints).*

### Passer le relais, ne pas reprendre

Avant de changer de sujet ou d'abandonner un long fil, capture un petit artefact de passation — typiquement un fichier Markdown sous `docs/` — et utilise-le comme ancre pour la tâche suivante.

Template :

```markdown
docs/handoff-[feature].md

## Goal
## Decisions
## Files touched
## Open questions

Use only what we agreed.
Stop. Do not implement yet.
```

Motifs adjacents : stubs d'ADR (contraintes, approche retenue, alternatives rejetées) et notes de repro/runbook (commandes exactes, attendu versus observé, jeu de `@` minimum). Arrête de payer un loyer de fenêtre pour du travail que tu n'as plus besoin de voir.

*See Ch.6.14 (Session Handoff and Long Threads).*

---

## Au-delà du panneau latéral de l'IDE

Bob est centré sur le panneau latéral de l'IDE avec une approbation humaine à chaque étape. Les sections ci-dessous couvrent les surfaces et les choix de posture qui entrent en jeu quand le flux quitte le panneau latéral.

### Bob Shell : préface uniquement

La surface produit de Bob inclut Bob Shell aux côtés du panneau latéral de l'IDE. Les habitudes de pratique pour l'invocation non interactive en pipe (flags de sortie structurée, streaming, scripting) vivent dans la documentation produit IBM Bob, pas dans les habitudes collectées ici.

*See preface.*

### Sessions parallèles : hors livre

Les motifs pour exécuter plusieurs sessions Bob en parallèle — worktrees, agents parallèles, VMs isolées, paires writer/reviewer — ne font pas partie des habitudes de pratique collectées ici. La posture du panneau latéral suppose un fil, un approbateur humain à la fois.

### Un seul plan sur plusieurs fichiers

Pour le travail multi-fichiers, le motif Bob est la planification coordonnée. Bob analyse d'abord le rayon de propagation — *"What files will be affected if I modernize UserService?"* — et propose un plan coordonné unique couvrant tous les fichiers affectés. Le mode Orchestrator est conçu pour le travail qui traverse vraiment plusieurs spécialités.

Forme de l'analyse d'impact que Bob renvoie :

> - **Files that must change** — UserService.java (primary target), UserServiceTest.java (tests need updates for new patterns)
> - **Files that might need changes** — UserController.java (if method signatures change), UserEventHandler.java (if event handling changes)
> - **Files that should not change** — UserRepository.java, EmailService.java, AuditLogger.java (interfaces stay the same)
> - **Recommendation** — keep UserService interface unchanged; refactor internal implementation only

C'est de la cartographie du rayon de propagation : ce qui doit bouger, ce qui pourrait bouger, ce qui doit rester en place. Un plan relisible, une piste d'audit.

*See Ch.10.5 (Coordinating Multi-File Changes), Ch.15.2 (Finding Commands and Switching Mode).*

### Rapide, jusqu'à ce que ça ne le soit plus

Le mode YOLO (tout auto-approuvé) laisse shell, fichiers et réseau s'exécuter sans pause humaine. Certaines configurations hybrides auto-approuvent les étapes « à faible risque » ; ça craque pour le terminal, où le risque tient rarement au nom du binaire mais aux arguments. Recommandations :

- Désactive l'auto-approbation globale pour shell, réseau sortant et outils qui modifient l'infrastructure, sauf si tu as des contrôles éprouvés
- Préfère les prompts granulaires par action
- Ne te repose pas sur des allowlists par exécutable seul tant que les lignes de commande complètes ne sont pas validées — ou garde ces chemins manuels

*See Ch.11.3 (Approvals, YOLO Mode, and "Safe" Commands).*

---

## Anti-patterns à l'usage de Bob

Sept anti-patterns récurrents :

| Anti-pattern | Correctif |
|---|---|
| **The Copy-Paste Developer** — livrer le diff de Bob sans le lire | Lis, exécute, et prépare-toi à justifier chaque ligne que tu gardes |
| **The Approval Bot** — tamponner les plans qui ont l'air confiants | Questionne le périmètre, les alternatives et les modes de défaillance avant chaque approve |
| **The Context-Free Requester** — pinger « fix it » sans `@` ni exemplars | Ancre la tâche dans des fichiers et des contraintes avant de demander des edits |
| **The Blame Shifter** — blâmer le modèle quand la prod déraille | Assume les résultats des outils que tu as autorisés |
| **The Black Box User** — utiliser Bob hors fil, laissant l'équipe deviner d'où sort le code | Mets intention, plans et usage d'outils là où les relecteurs regardent déjà — commits, PRs, tickets |
| **The Shortcut Seeker** — demander des réponses pour sauter la construction du modèle mental | Utilise les explications comme support pédagogique ; vérifie les claims contre le dépôt |
| **The Production Experimenter** — pointer l'automatisation vers la prod sans staging ni revue | Mêmes gardes-fous que n'importe quel changement privilégié : revue, staging, humains aux approbations, posture MCP et auto-approve resserrée |

Cinq situations où aller chercher Bob d'abord est la mauvaise décision :

- Apprendre quelque chose de nouveau — laisse Bob t'enseigner après que tu as senti les contours
- Prototyper — ne laisse pas la première réponse polie verrouiller le design
- Urgence — la latence de chat et le jugement ne doivent pas se mettre entre toi et le pager
- Problèmes que tu ne comprends pas — analyse jusqu'à ce que le mode de défaillance soit nommé, puis automatise les corrections
- Décisions d'architecture — la propriété reste avec les gens qui maintiendront les conséquences

*See Ch.12.7 (Anti-Patterns When Using Bob), Ch.12.8 (When to Stop Using Bob).*

---

## Garder Bob ennuyeux

L'excitation chez un assistant signifie de la variance, et pour le travail de production tu veux l'inverse.

Montée par paliers sur quatre semaines :

- **Semaine 1 — Analyse seule.** Travail en lecture seule : *"Analyze this service and explain what it does"*, *"Explain why this test is failing"*, *"What would break if I change this method?"* Objectif : preuve avant frappes clavier.
- **Semaine 2 — Ajouter la revue de code.** Lance `/review` avant chaque commit ; lis les findings ; corrige ce avec quoi tu es d'accord ; documente ce qui a été trouvé.
- **Semaine 3 — Ajouter la planification.** Définis l'intention clairement ; demande à Bob de créer un plan ; relis le plan ; approuve et exécute.
- **Semaine 4 — Workflow complet.** Analyse → plan → exécution → revue comme un seul rythme.

Si la semaine 4 te semble encore étrangère, reste plus longtemps en semaine 3.

Quand Bob brille le plus : changer du code non familier ; coordonner des changements multi-fichiers complexes ; maintenir la cohérence avec les conventions d'équipe ; attraper les problèmes tôt via revue et passes orientées sécurité ; onboarding et transfert de connaissances.

Comment garder Bob ennuyeux :

- Utilise des workflows cohérents — choisis quelques chemins et exécute-les jusqu'à ce que la mémoire musculaire arrive
- Documente les motifs — modes, règles et conventions appartiennent à l'écrit, pas au folklore
- Relis et améliore régulièrement — une fois par mois : ce qui a marché, ce qui a paru bancal, quel petit ajustement enlèverait le plus de friction
- Partage avec ton équipe — les habitudes partagées battent les éclats isolés
- Résiste à la tentation de la cleverness — un prompting créatif est amusant pour les démos ; un prompting ennuyeux passe en production

*See Ch.17 (The Bob Mindset), Ch.18 (Keeping Bob Boring).*

---

## Ressources liées

- *Getting Started with IBM Bob*, Markus Eisele (v1.2.0) — source des références chapitres ci-dessus
- **IBM Bob documentation** — Modes, Skills, Slash commands, Context mentions, Context window management, Security guidance
- **OWASP Top 10 for LLM Applications (2025)** — vocabulaire partagé avec sécurité et audit (LLM01 prompt injection à LLM10 unbounded consumption) ; Bob aligne son modèle de menace sur cette taxonomie
