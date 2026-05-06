# Tutoriel 2.4 : Votre Première Tâche Accountable

**Module :** 2 - Prise en Main  
**Durée estimée :** 1 heure  
**Niveau :** Pratique (Hands-on)  
**Prérequis :** Tutoriels 2.1, 2.2 et 2.3

## 🎓 Pour les Projets DL+RL

**Étudiants ESIEE :** Consultez votre [fiche projet](fiches-projet-esiee-guide.md) pour des exemples de premières tâches adaptées à votre projet (finance, vision, RL, trafic, fraude, recommandation).

---
---

## 🎯 Objectifs d'Apprentissage

À la fin de ce tutoriel, vous serez capable de :
- ✅ Exécuter une tâche complète de bout en bout avec Bob
- ✅ Définir un intent clair et vérifiable
- ✅ Laisser Bob explorer le codebase
- ✅ Lire et évaluer un plan avant exécution
- ✅ Comprendre les garanties et responsabilités
- ✅ Vérifier les résultats et prendre des décisions

---

## 📚 De la Prompt au Jugement

### L'Objectif de Ce Tutoriel

> **Citation du document source :**  
> "This chapter walks through one accountable task end to end.  
> It is not a sanitized demo. Messy choices stay in on purpose."

**Ce que vous allez apprendre :**
- ❌ Pas la vitesse
- ✅ Lire l'output de Bob
- ✅ Stress-tester ses recommandations
- ✅ Garder des décisions que vous pouvez expliquer

### La Tâche Exemple

Nous allons utiliser un problème courant et réaliste :

**"Ajouter une validation à un endpoint API"**

C'est :
- ✅ Assez simple pour un premier essai
- ✅ Assez réel pour être utile
- ✅ Assez complet pour voir tout le cycle

---

## 🎬 Étape 1 : Définir l'Intent Clairement

### Le Premier Prompt (Trop Vague)

```
Vous tapez dans Bob :
"Add validation to the greeting endpoint"
```

### La Réponse de Bob

```
Bob répond :

"I'll help you add validation to the greeting endpoint. 
Let me first examine the current implementation to 
understand what needs to be validated.

What type of validation would you like to add to the 
greeting endpoint? I can see the GreetingResource.java 
file is open. Please share what validation rules you need.

OPTIONS:
• Validate that the name parameter is not null or empty
• Validate name length (e.g. min 2, max 50 characters) 
  and format (only letters and spaces)
• Add comprehensive validation: non-null, length 
  constraints, character restrictions, and sanitization
• Show me the current endpoint code so I can suggest 
  appropriate validation"
```

### Pourquoi Bob Demande Plus de Détails

> **Citation du document source :**  
> "That first reply is Bob refusing to invent scope."

**Bob ne devine pas.** Il demande :
- Quel type de validation ?
- Quelles règles spécifiques ?
- Quel niveau de rigueur ?

### Votre Réponse (Intent Précis)

```
Vous choisissez l'option 2 et précisez :

"Add comprehensive validation to the name parameter:
- Not null or empty
- Length: minimum 2, maximum 50 characters
- Format: only letters and spaces allowed
- Return clear error message if validation fails"
```

### Pourquoi C'est Mieux

```
AVANT (vague) :
"Add validation"
❌ Pas de critères
❌ Pas de limites
❌ Pas de succès défini

APRÈS (précis) :
"Add comprehensive validation: not null, 2-50 chars, 
 letters and spaces only, clear error message"
✅ Critères clairs
✅ Limites définies
✅ Succès vérifiable
```

> **Citation du document source :**  
> "Now the ask is specific enough to plan against—not magic wording, a bounded task."

---

## 🔍 Étape 2 : Laisser Bob Explorer le Codebase

### Ce Qui Se Passe

```
Status: "Understanding..."

Bob analyse :
├── GreetingResource.java (le endpoint)
├── GreetingResourceTest.java (les tests)
├── pom.xml (les dépendances)
├── Validation existante (s'il y en a)
└── Patterns d'error handling
```

**Durée :** Quelques secondes (pas des minutes)

### Pourquoi Cette Phase Est Importante

> **Citation du document source :**  
> "Let that phase finish. Interrupting mid-read mostly buys you noise."

Bob construit une image de :
- Comment la validation est faite actuellement
- Quelles bibliothèques sont déjà utilisées
- Quel format d'erreur vous suivez
- Quels patterns existent pour des endpoints similaires
- Quels tests existent déjà

### Ce Que Bob Cherche

```
QUESTIONS QUE BOB SE POSE :
├── Comment la validation est-elle faite actuellement ?
│   → Cherche des patterns existants
│
├── Quelles bibliothèques de validation sont utilisées ?
│   → Bean Validation ? Custom validators ?
│
├── Quel format d'erreur est utilisé ?
│   → JSON ? XML ? Structure spécifique ?
│
├── Quels patterns existent pour des endpoints similaires ?
│   → Cohérence avec le reste du code
│
└── Quels tests existent pour le greeting endpoint ?
    → Style de tests à suivre
```

### Pourquoi Ça Compte

> **Citation du document source :**  
> "Suggestions tend to mirror what already shipped: Bean Validation where you already use it, your error shape if you have one, tests that match neighboring endpoints."

**Bob ne cherche pas à gagner un débat de style.**  
**Bob cherche à rester cohérent avec votre codebase.**

---

## 📋 Étape 3 : Lire le Plan de Bob Avant Exécution

### Le Plan Proposé

```
Status: "Waiting for approval"

TODO LIST CREATED:

1. Add query parameter to accept name input in the greet() method
   
2. Add Jakarta Bean Validation dependency to pom.xml if not present
   
3. Add @NotBlank validation annotation to the name parameter
   
4. Add @Size(min=2, max=50) validation annotation
   
5. Add @Pattern for letters and spaces only
   
6. Add proper error handling for validation failures
   
7. Update tests to cover validation scenarios:
   - Valid name
   - Null name
   - Empty name
   - Too short name (< 2 chars)
   - Too long name (> 50 chars)
   - Invalid characters
   
8. Test the endpoint manually to verify validation works correctly

[Approve] [Modify] [Reject]
```

### Comment Lire Ce Plan

> **Citation du document source :**  
> "Read it like a design note, not like prose to skim."

**Posez-vous ces questions :**

```
CONSISTENCY (Cohérence) :
□ Le plan suit-il nos patterns existants ?
  → Bean Validation est utilisé car déjà présent

COMPLETENESS (Complétude) :
□ Le plan couvre-t-il les modes d'échec ?
  → Validation ✓
  → Error handling ✓
  → Tests ✓

ALTERNATIVES :
□ Bob a-t-il mentionné d'autres approches ?
  → Si non, demandez : "Quelles alternatives ?"
```

### Ce Que Vous NE Voyez PAS (Volontairement)

> **Citation du document source :**  
> "You still should not see raw implementation during planning—only what will change and why—so you can judge the approach before syntax pulls you sideways."

**Pendant la planification :**
- ❌ Pas de code exact
- ❌ Pas de syntaxe détaillée
- ✅ Seulement l'approche
- ✅ Seulement les changements

**Pourquoi ?** Pour que vous jugiez l'approche, pas les détails.

### Quand Rejeter un Plan

```
REJETEZ SI :
❌ Vous ne comprenez pas le plan
❌ Les risques ne sont pas acceptables
❌ L'approche ne correspond pas à vos standards
❌ Des étapes importantes manquent
❌ Le plan dépasse le scope initial
```

**Si vous rejetez :** Affinez l'intent et laissez Bob replanifier.

---

## ⚖️ Étape 4 : Comprendre les Garanties de Bob

### Ce Que Bob Garantit (Mécanique)

```
BOB S'ENGAGE À :
✅ Suivre le plan approuvé
✅ Suivre les patterns visibles dans votre repo
✅ Garder les éditions syntaxiquement correctes
✅ Appliquer le batch atomiquement (tout ou rien)
✅ Laisser une trace dans l'historique des tâches
```

> **Citation du document source :**  
> "Those are controls on process. They are not proof that the change belongs in production."

### Ce Que Bob NE Garantit PAS

```
BOB NE PEUT PAS PROMETTRE :
❌ Que le changement résout le vrai problème
❌ Que les effets de bord restent bornés
❌ Que c'était le meilleur design possible
❌ Que chaque cas limite se comporte bien
❌ Que rien ne régresse ailleurs
```

> **Citation du document source :**  
> "Those stay on you to test, review, and accept."

### Votre Responsabilité

```
QUAND VOUS APPROUVEZ, VOUS POSSÉDEZ :
├── Vérifier le comportement dans votre environnement
├── Exécuter les tests et vérifications manuelles
├── Reviewer avec l'équipe si le blast radius est partagé
└── Shipper et monitorer selon vos termes
```

> **Citation du document source :**  
> "Bob sharpens deliberation. It does not move accountability off your desk."

### Les 3 Options d'Approbation

```
1. APPROVE ✅
   Le plan est bon. Exécutez-le.
   
2. MODIFY 🔄
   Le plan est proche mais nécessite des changements.
   Affinez l'intent et laissez Bob replanifier.
   
3. REJECT ❌
   Le plan ne fonctionne pas.
   Recommencez avec un intent différent.
```

**Pour cet exemple, vous approuvez.**

---

## ⚙️ Étape 5 : Observer l'Exécution

### Ce Qui Se Passe

```
Status: "I'm working on it"

Progress:
✓ Modifying: src/main/java/org/acme/GreetingResource.java
✓ Modifying: pom.xml
✓ Modifying: src/test/java/org/acme/GreetingResourceTest.java
✓ Running: tests to verify changes
✓ All tests passed
```

### Comment Ça Devrait Se Sentir

> **Citation du document source :**  
> "Execution should feel fast and dumb: files change, commands run, progress ticks."

**L'exécution devrait être :**
- 🥱 **Ennuyeuse** (c'est bon signe !)
- ⚡ **Rapide**
- 🎯 **Prévisible**
- 📝 **Traçable**

> **Citation du document source :**  
> "If execution feels exciting, something went wrong—usually upstream of the merge."

### Si Quelque Chose Échoue

```
RAISONS COURANTES D'ÉCHEC :
├── Quelqu'un d'autre a touché le même fichier
├── Un test devient rouge
├── Un conflit de merge apparaît
└── Une dépendance manque
```

**Bob s'arrête, affiche l'erreur, et attend.**

> **Citation du document source :**  
> "Bob stops, surfaces the error, and waits. It does not continue the run after a failure or auto-fix execution problems without you."

**Vos options :**
1. Corriger le problème manuellement et laisser Bob réessayer
2. Modifier le plan pour contourner le problème
3. Annuler la tâche et recommencer

---

## ✅ Étape 6 : Vérifier les Résultats

### Le Résumé de Bob

```
Status: "Complete"

Task complete: Add validation to the greeting endpoint

CHANGES MADE:
- Added @NotBlank on the name parameter in greet()
- Added @Size(min=2, max=50) annotation
- Added @Pattern for letters and spaces
- Added error handling for validation failures
- Added tests in GreetingResourceTest for:
  * Valid input
  * Null input
  * Empty input
  * Too short input
  * Too long input
  * Invalid characters

VERIFICATION:
- All tests pass (12/12)
- Code compiles successfully
- No linting errors

[View Changes] [Create PR] [New Task]
```

### Vos Prochaines Étapes

> **Citation du document source :**  
> "After Bob completes a task: Review the actual code changes, Run your tests, Test the functionality manually, Check for unintended side effects, Commit the changes (or don't)."

```
CHECKLIST POST-EXÉCUTION :
□ 1. Reviewer les changements de code réels
     → Ouvrir les fichiers modifiés
     → Vérifier que le code est propre
     
□ 2. Exécuter vos tests
     → Tests unitaires
     → Tests d'intégration si applicable
     
□ 3. Tester la fonctionnalité manuellement
     → Cas valides
     → Cas d'erreur
     → Cas limites
     
□ 4. Vérifier les effets de bord non intentionnels
     → Autres endpoints affectés ?
     → Performance impactée ?
     
□ 5. Décider de committer (ou non)
     → Si tout est bon : commit
     → Si problèmes : corriger ou rejeter
```

> **Citation du document source :**  
> "Bob typed the edits; you still sign off on correctness."

---

## 🎯 Exercice Pratique : Votre Première Tâche

### Mission

Exécutez une tâche complète sur un projet réel (ou un projet de test).

### Tâches Suggérées (Choisissez-en Une)

**Option A : Validation (Simple)**
```
"Add email validation to the user registration endpoint:
- Email must not be null or empty
- Email must match standard email format
- Return 400 with clear error message if invalid"
```

**Option B : Refactoring (Moyen)**
```
"Extract the password validation logic from UserService 
into a dedicated PasswordValidator class:
- Preserve exact validation behavior
- All existing tests must pass unchanged
- Improve code organization"
```

**Option C : Feature (Avancé)**
```
"Add pagination to the GET /products endpoint:
- Parameters: page (default 1) and limit (default 20, max 100)
- Response includes: data, page, limit, total, pages
- Backward compatible (works without parameters)
- Add tests for pagination"
```

### Template de Suivi

Utilisez ce template pour documenter votre tâche :

```
TÂCHE : [Nom de votre tâche]

ÉTAPE 1 : INTENT
Intent initial :
[Votre premier prompt]

Clarifications de Bob :
[Questions posées par Bob]

Intent final :
[Votre prompt précisé]

ÉTAPE 2 : EXPLORATION
Fichiers analysés par Bob :
- [Liste]

Durée : [X secondes]

ÉTAPE 3 : PLAN
Plan proposé :
[Copier le plan de Bob]

Votre évaluation :
□ Cohérent avec le projet ?
□ Complet ?
□ Alternatives mentionnées ?

Décision : [Approve / Modify / Reject]

ÉTAPE 4 : GARANTIES
Ce que Bob garantit :
[Liste]

Ce que vous devez vérifier :
[Liste]

ÉTAPE 5 : EXÉCUTION
Fichiers modifiés :
- [Liste]

Problèmes rencontrés :
[Si applicable]

Durée : [X minutes]

ÉTAPE 6 : VÉRIFICATION
□ Code reviewé
□ Tests exécutés : [X/X passent]
□ Test manuel effectué
□ Pas d'effets de bord
□ Prêt à committer

RÉSULTAT FINAL :
[Succès / Échec / Partiellement réussi]

LEARNINGS :
[Ce que vous avez appris]
```

---

## 📊 Auto-Évaluation

### Questions

1. **Que fait Bob quand votre intent est trop vague ?**
   - [ ] Il devine ce que vous voulez
   - [ ] Il refuse et demande plus de détails
   - [ ] Il fait de son mieux
   - [ ] Il génère du code aléatoire

2. **Pourquoi Bob explore-t-il le codebase avant de planifier ?**
   - [ ] Pour perdre du temps
   - [ ] Pour rester cohérent avec vos patterns
   - [ ] Parce que c'est obligatoire
   - [ ] Pour impressionner

3. **Que devez-vous voir pendant la phase de planification ?**
   - [ ] Le code exact
   - [ ] La syntaxe détaillée
   - [ ] L'approche et les changements
   - [ ] Rien, juste approuver

4. **Qui est responsable de la correction du code généré ?**
   - [ ] Bob
   - [ ] L'IA
   - [ ] Vous
   - [ ] L'équipe

5. **Que faire si l'exécution échoue ?**
   - [ ] Paniquer
   - [ ] Laisser Bob auto-corriger
   - [ ] Corriger manuellement ou modifier le plan
   - [ ] Abandonner

<details>
<summary>Voir les réponses</summary>

1. **✅ Il refuse et demande plus de détails** - Bob ne devine pas
2. **✅ Pour rester cohérent avec vos patterns** - Cohérence > Créativité
3. **✅ L'approche et les changements** - Pas de code pendant planning
4. **✅ Vous** - Vous signez toujours la correction
5. **✅ Corriger manuellement ou modifier le plan** - Vous choisissez la recovery

**Score :**
- 5/5 : Excellent ! Vous êtes prêt pour des tâches réelles
- 3-4/5 : Bien ! Relisez les sections où vous avez hésité
- 0-2/5 : Relisez le tutoriel et faites l'exercice pratique

</details>

---

## 📚 Ce que Vous Avez Appris

Dans ce tutoriel, vous avez découvert :

✅ **Le cycle complet** : Intent → Exploration → Plan → Approbation → Exécution → Vérification

✅ **Intent précis** : Bob demande des clarifications si c'est vague

✅ **Exploration** : Bob analyse pour rester cohérent

✅ **Plan reviewable** : Approche avant syntaxe

✅ **Garanties et responsabilités** : Bob fait, vous signez

✅ **Vérification** : Toujours vérifier avant de committer

---

## 🎓 Félicitations !

Vous avez complété le **Module 2 : Prise en Main** ! 🎉

Vous savez maintenant :
- ✅ Utiliser l'interface Bob
- ✅ Gérer le contexte efficacement
- ✅ Écrire des contrats clairs
- ✅ Exécuter des tâches accountables

---

## 🚀 Prochaines Étapes

Passez au **Module 3 : Changements Sécurisés** :

1. **Tutoriel 3.1** : Code Review comme Evidence
2. **Tutoriel 3.2** : Modernisation Sans Dérive Comportementale
3. **Tutoriel 3.3** : Sécurité, Permissions et Confiance MCP

---

## 💡 Points Clés à Retenir

1. **Intent précis** : Bob demande si c'est vague
2. **Exploration nécessaire** : Laissez Bob lire
3. **Plan avant code** : Jugez l'approche d'abord
4. **Vous possédez le résultat** : Responsabilité humaine
5. **Vérifiez toujours** : Bob tape, vous signez
6. **Pratique régulière** : La maîtrise vient avec l'usage

---

**Prochaine étape :** [Module 3 : Changements Sécurisés](../README.md#module-3)

**Besoin d'aide ?** Consultez le [README.md](README.md) ou contactez votre formateur

---

*Ce tutoriel fait partie du Parcours Pédagogique IBM Bob v1.0*  
*Basé sur "Getting Started with IBM Bob" v1.2.0 par Markus Eisele*