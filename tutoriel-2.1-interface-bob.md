# Tutoriel 2.1 : L'Interface Bob dans l'IDE

**Module :** 2 - Prise en Main  
**Durée estimée :** 45 minutes  
**Niveau :** Pratique  
**Prérequis :** Module 1 complet

## 🎓 Pour les Projets DL+RL

**Étudiants ESIEE :** Consultez votre [fiche projet](fiches-projet-esiee-guide.md) pour des exemples concrets d'utilisation de l'interface Bob dans votre contexte projet (finance, vision, RL, trafic, fraude, recommandation).

---
---

## 🎯 Objectifs d'Apprentissage

À la fin de ce tutoriel, vous serez capable de :
- ✅ Naviguer dans l'interface Bob avec confiance
- ✅ Comprendre les différentes phases d'une tâche
- ✅ Utiliser Tasks, Plans et Findings efficacement
- ✅ Comprendre comment Bob lit votre projet
- ✅ Gérer les approbations et checkpoints

---

## 📚 L'IDE comme Cockpit, Pas comme Banc de Travail

### Une Perspective Importante

> **Citation du document source :**  
> "For many roles, the IDE reads more like a cockpit than a craft bench:  
> it surfaces the system, the evidence, and where approval happens."

**Ce que cela signifie :**

```
COCKPIT (Bob) :
├── Surfaces le système
├── Montre l'evidence
├── Indique où approuver
└── Permet de piloter

≠

BANC DE TRAVAIL (IDE traditionnel) :
├── Éditer directement
├── Compiler
├── Débugger
└── Construire
```

**Vous n'avez pas besoin d'être un développeur full-time pour utiliser Bob.**

Vous avez besoin de :
- ✅ Comprendre l'intent
- ✅ Évaluer l'evidence
- ✅ Prendre des décisions (judgment)
- ✅ Approuver ou rejeter

---

## 🎨 Vue d'Ensemble de l'Interface

### Layout Minimaliste

> **Citation du document source :**  
> "The layout stays sparse on purpose.  
> Bob is not trying to be a second IDE inside your IDE."

```
┌─────────────────────────────────────────┐
│         VOTRE IDE (VS Code, etc.)       │
├─────────────────────────────────────────┤
│                                         │
│  ┌──────────────┐  ┌─────────────────┐ │
│  │              │  │                 │ │
│  │   FICHIERS   │  │   ÉDITEUR       │ │
│  │   PROJET     │  │   CODE          │ │
│  │              │  │                 │ │
│  └──────────────┘  └─────────────────┘ │
│                                         │
│  ┌──────────────────────────────────┐  │
│  │     BOB SIDE PANEL               │  │
│  │  ┌────────────────────────────┐  │  │
│  │  │  Task History              │  │  │
│  │  │  - Task #1: Add validation │  │  │
│  │  │  - Task #2: Fix bug        │  │  │
│  │  └────────────────────────────┘  │  │
│  │  ┌────────────────────────────┐  │  │
│  │  │  Current Task Status       │  │  │
│  │  │  Phase: Planning           │  │  │
│  │  │  [Approve] [Reject]        │  │  │
│  │  └────────────────────────────┘  │  │
│  │  ┌────────────────────────────┐  │  │
│  │  │  Task Input                │  │  │
│  │  │  Type your intent here...  │  │  │
│  │  │  [Send] [/commands]        │  │  │
│  │  └────────────────────────────┘  │  │
│  └──────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

### Les Éléments Clés

Bob vous donne uniquement ce qui correspond à :
- **Intent** : Task Input
- **Evidence** : Plans et Findings
- **Judgment** : Approval gates

Pas de chrome inutile. Pas de fonctionnalités cachées.

---

## 📋 Le Bob Side Panel

### Section 1 : Task Input (En Bas)

**Objectif :** Définir votre intent

```
┌────────────────────────────────────────┐
│  Task Input                            │
│  ┌──────────────────────────────────┐  │
│  │ Add validation to user           │  │
│  │ registration endpoint            │  │
│  └──────────────────────────────────┘  │
│  [Send]  [/ Commands]                  │
└────────────────────────────────────────┘
```

#### Comment Écrire un Bon Intent

**Gardez-le goal-shaped** : symptômes, contraintes, vérifications de succès

**✅ Bons Exemples :**
```
"Add validation to the user registration endpoint"

"Update the database schema to support soft deletes"

"Refactor the payment service to use the new API"
```

**❌ Mauvais Exemples :**
```
"Make the code better"
→ Trop vague

"Fix it"
→ Pas de contexte

"Change UserService.java line 45"
→ Trop spécifique (solution, pas intent)
```

#### Slash Commands (/)

Tapez `/` dans la boîte de chat pour ouvrir les commandes rapides :

```
COMMANDES COURANTES :
/review          → Démarrer une code review
/explain         → Expliquer du code
/test            → Générer des tests
/refactor        → Refactorer du code
/document        → Générer de la documentation
/create-pr       → Créer une pull request

COMMANDES PERSONNALISÉES :
Votre équipe peut ajouter ses propres commandes
```

---

### Section 2 : Current Task Status (Au Milieu)

**Objectif :** Voir où Bob en est dans le processus

```
┌────────────────────────────────────────┐
│  Current Task Status                   │
│  ┌──────────────────────────────────┐  │
│  │ Phase: Planning                  │  │
│  │                                  │  │
│  │ Bob is creating a plan based on  │  │
│  │ the evidence from your codebase  │  │
│  │                                  │  │
│  │ [Waiting for approval...]        │  │
│  └──────────────────────────────────┘  │
└────────────────────────────────────────┘
```

#### Les Phases d'une Tâche

```
1. UNDERSTANDING 🔍
   Bob lit votre intent et examine le code
   
2. PLANNING 📋
   Bob crée un plan basé sur l'evidence
   
3. WAITING FOR APPROVAL ⏸️
   Bob a un plan et attend votre décision
   
4. EXECUTING ⚙️
   Bob fait les changements approuvés
   
5. COMPLETE ✅
   Bob a terminé et montre les résultats
```

#### Exemple de Progression

```
PHASE 1 : UNDERSTANDING
Status: "Reading UserService.java..."
Status: "Analyzing tests..."
Status: "Checking dependencies..."

PHASE 2 : PLANNING
Status: "Creating plan..."
Status: "Identifying risks..."

PHASE 3 : WAITING FOR APPROVAL
Status: "Plan ready for review"
Actions: [Approve] [Modify] [Reject]

PHASE 4 : EXECUTING
Status: "Modifying UserService.java..."
Status: "Running tests..."
Status: "Creating commit..."

PHASE 5 : COMPLETE
Status: "Task completed successfully"
Results: "3 files modified, 12 tests pass"
```

> **Citation du document source :**  
> "Phase and next step stay visible in the status block—you should not have to guess whether Bob is still reading the repo or waiting on you."

---

### Section 3 : Task History (En Haut)

**Objectif :** Votre audit trail

```
┌────────────────────────────────────────┐
│  Task History                          │
│  ┌──────────────────────────────────┐  │
│  │ ✅ Task #3: Add validation       │  │
│  │    2024-05-06 10:30              │  │
│  │                                  │  │
│  │ ✅ Task #2: Fix bug #1234        │  │
│  │    2024-05-06 09:15              │  │
│  │                                  │  │
│  │ ✅ Task #1: Refactor service     │  │
│  │    2024-05-05 16:45              │  │
│  └──────────────────────────────────┘  │
│  [Search] [Export]                     │
└────────────────────────────────────────┘
```

#### Pourquoi C'est Important

L'historique des tâches vous permet de :
- ✅ Reconstruire ce qui a été demandé
- ✅ Voir ce qui a été proposé
- ✅ Comprendre ce qui a été fait
- ✅ Répondre aux questions 6 mois plus tard

**Cas d'usage :**
```
Manager : "Pourquoi avons-nous choisi Redis plutôt que Memcached ?"

Vous : [Recherche dans Task History]
      "Voici la tâche #47 du 15 mars :
       - Intent : Ajouter du cache
       - Plan : Bob a proposé Redis et Memcached
       - Decision : Redis choisi car déjà utilisé ailleurs
       - Evidence : Voir le chat complet"
```

---

## 🎯 Tasks, Plans et Findings

### 1. Tasks (Intent)

**Définition :** Ce que vous voulez accomplir

```
TASK = INTENT
├── Scope (périmètre)
├── Failure mode (mode d'échec)
└── Done-when (critères de succès)
```

#### Exemples de Bonnes Tasks

**Task 1 :**
```
"Add input validation to prevent SQL injection 
in the search endpoint"

✅ Scope : Search endpoint
✅ Failure mode : SQL injection
✅ Done-when : Validation en place, tests passent
```

**Task 2 :**
```
"Refactor AuthService to use dependency injection 
while preserving all existing behavior"

✅ Scope : AuthService
✅ Failure mode : Comportement changé
✅ Done-when : Refactoré, tests inchangés passent
```

#### Bob Pousse Vers la Clarté

Si votre task est vague, Bob pose des questions :

```
Vous : "Make the code better"

Bob : "I need more specific intent. What aspect 
      should be improved?
      
      Options:
      - Performance optimization
      - Code readability
      - Test coverage
      - Security hardening
      - Error handling
      
      Please specify your goal."
```

---

### 2. Plans (Evidence-Based Approach)

**Définition :** La proposition de Bob pour accomplir la task

```
PLAN INCLUT :
├── Quels fichiers seront changés
├── Ce que les changements feront
├── Pourquoi ces changements sont nécessaires
├── Quels risques existent
└── Quelles alternatives ont été considérées
```

#### Exemple de Plan

```
TODO LIST CREATED:

1. Add validation annotations to User model
   - Add @NotBlank to username field
   - Add @Email to email field
   - Add @Size(min=8) to password field

2. Update UserController
   - Add @Valid annotation to request parameter
   - Add error handling for validation failures

3. Create validation tests
   - Test valid user creation
   - Test invalid username (blank)
   - Test invalid email format
   - Test invalid password (too short)

4. Update API documentation
   - Document validation rules
   - Document error responses

RISKS:
- Existing clients may not handle validation errors
- Need to ensure backward compatibility

ALTERNATIVES CONSIDERED:
- Custom validator: More flexible but more code
- Bean Validation: Standard, less code (CHOSEN)

[Approve] [Modify] [Reject]
```

#### Pourquoi Pas de Code Pendant la Planification ?

> **Citation du document source :**  
> "During planning you see descriptions of what will change and why—not raw code on purpose, because syntax pulls attention away from whether the approach is right."

**Focus sur :**
- ✅ L'approche est-elle correcte ?
- ✅ Les risques sont-ils acceptables ?
- ✅ Les alternatives ont-elles été considérées ?

**Pas sur :**
- ❌ La syntaxe exacte
- ❌ Les détails d'implémentation
- ❌ Le style de code

---

### 3. Findings (Evidence)

**Définition :** Problèmes découverts par Bob en examinant votre code

```
FINDINGS INCLUENT :
├── Vulnérabilités de sécurité
├── Problèmes de performance
├── Incohérences avec les patterns
├── Tests manquants
└── Problèmes de configuration
```

#### Structure d'un Finding

```
FINDING #1: SQL Injection Vulnerability
┌────────────────────────────────────────┐
│ SEVERITY: High 🔴                      │
│                                        │
│ LOCATION:                              │
│ src/services/UserService.java:45      │
│                                        │
│ DESCRIPTION:                           │
│ Direct string concatenation in SQL    │
│ query allows SQL injection attacks    │
│                                        │
│ CODE:                                  │
│ String query = "SELECT * FROM users   │
│   WHERE name = '" + userName + "'";   │
│                                        │
│ RISK:                                  │
│ Attacker can execute arbitrary SQL    │
│ commands, potentially accessing or    │
│ modifying sensitive data              │
│                                        │
│ SUGGESTED FIX:                         │
│ Use PreparedStatement with parameters │
│                                        │
│ [Create Task] [Ignore] [More Info]    │
└────────────────────────────────────────┘
```

#### Niveaux de Sévérité

```
🔴 CRITICAL : Doit être corrigé immédiatement
🟠 HIGH     : Doit être corrigé bientôt
🟡 MEDIUM   : Devrait être corrigé
🟢 LOW      : Peut être corrigé
🔵 INFO     : Information seulement
```

#### Findings ≠ Tasks Automatiques

> **Citation du document source :**  
> "Findings do not automatically become tasks.  
> You choose what is worth acting on; Bob does not score your priorities for you."

**Vous décidez :**
- Quel finding mérite une action immédiate
- Quel finding peut attendre
- Quel finding peut être ignoré (avec justification)

---

## 🔍 Comment Bob Lit Votre Projet

### Lecture Complète, Pas Juste le Buffer

> **Citation du document source :**  
> "Bob does not only read the buffer you have focused—it walks the project shape, dependencies, config, tests, prevailing code patterns, and whatever docs you already wrote."

```
BOB ANALYSE :
├── Structure du projet
├── Dépendances (pom.xml, package.json, etc.)
├── Configuration (application.properties, etc.)
├── Tests existants
├── Patterns de code dominants
├── Documentation existante
└── Historique Git (si pertinent)
```

### Questions Pratiques Répondues

Chaque analyse répond à des questions pratiques :

```
QUESTIONS :
├── Où appartient ce changement ?
│   → Structure du projet
│
├── Quelles versions sont utilisées ?
│   → Fichiers de dépendances
│
├── Quel comportement est déjà verrouillé ?
│   → Tests existants
│
├── Quel style l'équipe utilise réellement ?
│   → Patterns de code
│
└── Quelle est la convention de nommage ?
    → Code existant
```

### Pourquoi la Phase de Planning Peut Sembler Calme

> **Citation du document source :**  
> "Only after that pass does it propose diffs, which is why the planning phase can feel quiet for a few seconds."

**C'est normal !** Bob est en train de :
1. Lire votre projet
2. Comprendre les patterns
3. Identifier les dépendances
4. Analyser les tests
5. Construire un plan cohérent

**Patience = Meilleur plan**

---

## 🔒 Ce que Bob Ne Touche Jamais Sans Approbation

### Boundaries First

> **Citation du document source :**  
> "Bob does not make changes without your approval."

```
SANS APPROBATION, BOB NE PEUT PAS :
❌ Modifier des fichiers
❌ Exécuter des commandes
❌ Créer des commits
❌ Pousser du code
❌ Déployer quoi que ce soit
```

### Niveaux d'Approbation

```
1. APPROBATION PAR OUTIL (Per-Tool)
   Bob demande pour chaque outil utilisé
   Exemple : "Puis-je modifier ce fichier ?"
   
2. APPROBATION GLOBALE (Global Tool)
   Vous approuvez tous les outils d'un coup
   Plus rapide mais moins de contrôle
   
3. AUTO-APPROVE
   Pas de prompts, Bob agit directement
   ⚠️ Plus rapide mais plus risqué
   ⚠️ Les erreurs se propagent plus vite
```

**Recommandation :** Gardez les approbations explicites pour tout ce qui touche les fichiers ou les commandes.

### Checkpoints : Points de Restauration

```
CHECKPOINT = POINT DE SAUVEGARDE
├── Sauvegarde l'état des fichiers
├── Garde l'historique du chat
└── Permet de revenir en arrière
```

#### Deux Types de Restauration

**1. Restore Files Only**
```
- Remet les fichiers à l'état du checkpoint
- Garde tout l'historique du chat
- Utile si le code est mauvais mais le chat est bon
```

**2. Restore Files and Task**
```
- Remet les fichiers à l'état du checkpoint
- Supprime les messages après le checkpoint
- Utile si le chat est parti dans la mauvaise direction
```

#### Checkpoints ≠ Git

```
CHECKPOINTS :
✅ Points de restauration rapides
✅ Spécifiques à une tâche Bob
✅ Temporaires

GIT :
✅ Historique permanent
✅ Partagé avec l'équipe
✅ Versionning complet

→ Les checkpoints COMPLÈTENT Git, ne le remplacent pas
```

---

## 🎨 Modes de Bob

### Modes Intégrés

```
ASK MODE 💬
- Poser des questions
- Obtenir des explications
- Pas de changements de code

PLAN MODE 📋
- Créer des plans
- Analyser des approches
- Pas d'exécution

CODE MODE 💻
- Écrire du code
- Modifier des fichiers
- Exécuter des tests

ADVANCED MODE 🚀
- Utiliser MCP (Model Context Protocol)
- Intégrations avancées
- Outils externes

ORCHESTRATOR MODE 🎭
- Coordonner plusieurs agents
- Tâches complexes multi-étapes
- Workflows avancés
```

### Modes Personnalisés

Votre organisation peut créer des modes personnalisés :

```
EXEMPLES DE MODES PERSONNALISÉS :
├── Security Review Mode
│   → Focus sur la sécurité
│   → Checklist OWASP
│
├── Performance Optimization Mode
│   → Focus sur la performance
│   → Benchmarks automatiques
│
└── Documentation Mode
    → Focus sur la doc
    → Templates d'équipe
```

---

## 💡 Exercice 1 : Navigation de l'Interface

### Instructions

Pour chaque action, identifiez où dans l'interface vous la feriez :

1. Démarrer une nouvelle tâche
2. Voir l'historique de vos tâches précédentes
3. Approuver un plan
4. Voir les findings de sécurité
5. Créer un checkpoint
6. Utiliser une commande rapide
7. Changer de mode
8. Restaurer des fichiers

<details>
<summary>Voir les réponses</summary>

1. **Task Input** (en bas du side panel)
2. **Task History** (en haut du side panel)
3. **Current Task Status** (bouton Approve)
4. **Findings** (section dédiée dans le side panel)
5. **Current Task Status** (options de checkpoint)
6. **Task Input** (taper `/`)
7. **Mode Selector** (dropdown en haut)
8. **Current Task Status** (options de restore)

</details>

---

## 🎯 Exercice 2 : Écrire de Bons Intents

### Mission

Transformez ces mauvais intents en bons intents :

**Intent 1 (Mauvais) :**
```
"Fix the bug"
```

**Intent 2 (Mauvais) :**
```
"Change line 45 in UserService.java"
```

**Intent 3 (Mauvais) :**
```
"Make it faster"
```

<details>
<summary>Voir des solutions possibles</summary>

**Intent 1 (Bon) :**
```
"Fix the NullPointerException in UserService.login() 
that occurs when the email field is null.

Expected behavior: Return a validation error instead 
of throwing an exception.

Success: All tests pass, including new test for null email."
```

**Intent 2 (Bon) :**
```
"Refactor the password validation logic in UserService 
to use a dedicated PasswordValidator class.

Goal: Improve code organization and reusability.

Constraints: Preserve exact validation behavior, 
all existing tests must pass unchanged."
```

**Intent 3 (Bon) :**
```
"Optimize the search endpoint response time from 
current 250ms to under 100ms.

Approach: Analyze and fix performance bottlenecks.

Success criteria:
- 95th percentile < 100ms
- All tests pass
- No behavior changes"
```

</details>

---

## 📊 Auto-Évaluation

### Questions

1. **Quelle est la métaphore utilisée pour l'interface Bob ?**
   - [ ] Un banc de travail
   - [ ] Un cockpit
   - [ ] Un tableau de bord
   - [ ] Un terminal

2. **Quelles sont les 5 phases d'une tâche ?**
   - [ ] Start, Plan, Code, Test, Deploy
   - [ ] Understanding, Planning, Waiting, Executing, Complete
   - [ ] Read, Write, Execute, Verify, Explain
   - [ ] Orient, Bound, Plan, Act, Verify

3. **Que sont les Findings ?**
   - [ ] Des bugs automatiquement corrigés
   - [ ] Des problèmes découverts par Bob
   - [ ] Des tâches à faire
   - [ ] Des commits Git

4. **Bob peut-il modifier des fichiers sans approbation ?**
   - [ ] Oui, toujours
   - [ ] Non, jamais (sauf auto-approve activé)
   - [ ] Seulement les fichiers de test
   - [ ] Seulement avec Git

5. **Quelle est la différence entre Checkpoints et Git ?**
   - [ ] Checkpoints remplacent Git
   - [ ] Checkpoints complètent Git
   - [ ] Checkpoints sont meilleurs que Git
   - [ ] Pas de différence

<details>
<summary>Voir les réponses</summary>

1. **✅ Un cockpit** - Pour piloter, pas pour construire
2. **✅ Understanding, Planning, Waiting, Executing, Complete** - Les 5 phases
3. **✅ Des problèmes découverts par Bob** - Evidence, pas tasks automatiques
4. **✅ Non, jamais (sauf auto-approve activé)** - Approbation obligatoire
5. **✅ Checkpoints complètent Git** - Deux outils différents, complémentaires

**Score :**
- 5/5 : Excellent ! Vous maîtrisez l'interface
- 3-4/5 : Bien ! Relisez les sections où vous avez hésité
- 0-2/5 : Relisez le tutoriel attentivement

</details>

---

## 📚 Ce que Vous Avez Appris

Dans ce tutoriel, vous avez découvert :

✅ **L'interface comme cockpit** : Piloter, pas construire

✅ **Le Side Panel** : Task Input, Status, History

✅ **Tasks, Plans, Findings** : Intent, Evidence-based, Evidence

✅ **Les 5 phases** : Understanding → Planning → Waiting → Executing → Complete

✅ **Comment Bob lit** : Projet complet, pas juste le buffer

✅ **Approbations et checkpoints** : Contrôle et sécurité

✅ **Modes** : Intégrés et personnalisés

---

## 🚀 Prochaines Étapes

Maintenant que vous connaissez l'interface :

1. **Tutoriel 2.2** : Gestion du Contexte (CRITIQUE !)
2. **Tutoriel 2.3** : Contrats Avant Code
3. **Tutoriel 2.4** : Votre Première Tâche Accountable

---

## 💡 Points Clés à Retenir

1. **Cockpit, pas banc de travail** : Piloter le système
2. **Intent goal-shaped** : Symptômes, contraintes, succès
3. **5 phases visibles** : Toujours savoir où Bob en est
4. **Findings ≠ Tasks** : Vous choisissez les priorités
5. **Approbation obligatoire** : Vous gardez le contrôle
6. **Checkpoints complètent Git** : Deux outils, deux usages

---

**Prochaine étape :** [Tutoriel 2.2 : Gestion du Contexte](tutoriel-2.2-gestion-contexte.md) ⭐ CRITIQUE

**Besoin d'aide ?** Consultez le [README.md](README.md) ou contactez votre formateur

---

*Ce tutoriel fait partie du Parcours Pédagogique IBM Bob v1.0*  
*Basé sur "Getting Started with IBM Bob" v1.2.0 par Markus Eisele*