# Tutoriel 2.3 : Contrats Avant Code

**Module :** 2 - Prise en Main  
**Durée estimée :** 45 minutes  
**Niveau :** Pratique  
**Prérequis :** Tutoriels 2.1 et 2.2

---

## 🎯 Objectifs d'Apprentissage

À la fin de ce tutoriel, vous serez capable de :
- ✅ Comprendre pourquoi les contrats sont essentiels
- ✅ Écrire des contrats clairs et vérifiables
- ✅ Adapter les contrats selon le type de tâche
- ✅ Utiliser les contrats pour accélérer les reviews
- ✅ Éviter les pièges courants

---

## 📚 La Chose Durable N'Est Pas le Code

### Le Principe Fondamental

> **Citation du document source :**  
> "The durable thing in agentic work is not the exact code Bob happened to write.  
> It is the contract around the change."

```
CE QUI COMPTE :
❌ Le diff exact que Bob a généré
✅ Le contrat qui définit le succès

POURQUOI :
- Le code peut varier d'une exécution à l'autre
- Le contrat reste constant
- Le contrat permet de juger si le code est correct
```

### Exemple Concret

**Sans Contrat :**
```
Vous : "Améliore AuthService"

Bob génère du code...

Review : "Est-ce que c'est bon ?"
❓ Impossible à dire sans critères
```

**Avec Contrat :**
```
Vous : "Modernise AuthService vers Java 21 :
       - Préserve tout le comportement login
       - Préserve token refresh
       - Préserve audit
       - Pas de changement d'API publique
       - Tous les tests passent inchangés"

Bob génère du code...

Review : "Est-ce que ça respecte le contrat ?"
✅ Critères clairs pour juger
```

---

## 🆚 Contrats vs Copy-Paste

### Le Problème du Copy-Paste

> **Citation du document source :**  
> "Copy-paste tutorials assume one best path and one expected output.  
> Agentic work does not behave that neatly."

```
TUTORIELS COPY-PASTE :
├── Un seul chemin "correct"
├── Un seul output attendu
├── Déterministe
└── Fragile (casse si contexte différent)

TRAVAIL AGENTIQUE :
├── Plusieurs chemins possibles
├── Outputs variables mais corrects
├── Probabiliste
└── Robuste (s'adapte au contexte)
```

### Ce Que Vous Voulez Vraiment

Pas une implémentation figée, mais un **accord borné** :

```
ACCORD BORNÉ (CONTRAT) :
├── Quel outcome compte
├── Qu'est-ce qui doit rester inchangé
├── Quelle evidence prouve le succès
├── Quel niveau de risque est acceptable
└── Qu'est-ce qui devrait arrêter la tâche
```

> **Citation du document source :**  
> "That agreement keeps the work reviewable even when the implementation is not identical from one run to the next."

---

## 📋 Structure d'un Bon Contrat

### Les 6 Éléments Essentiels

```
CONTRAT COMPLET :
├── 1. Task Intent (L'intention)
├── 2. Success Condition (Condition de succès)
├── 3. Non-Goals (Ce qui n'est PAS l'objectif)
├── 4. Preserved Constraints (Contraintes préservées)
├── 5. Verification Method (Méthode de vérification)
└── 6. Stop Condition (Condition d'arrêt)
```

### Détail de Chaque Élément

#### 1. Task Intent (L'Intention)

**Définition :** Ce que vous essayez d'accomplir

```
EXEMPLE :
"Ajouter une authentification à deux facteurs (2FA) 
pour améliorer la sécurité des comptes utilisateurs"
```

#### 2. Success Condition (Condition de Succès)

**Définition :** Comment savoir que c'est terminé et correct

```
EXEMPLE :
"Succès quand :
- Les utilisateurs peuvent activer 2FA
- Le login nécessite le code TOTP si 2FA activé
- Les codes de backup fonctionnent
- Tous les tests passent (existants + nouveaux)"
```

#### 3. Non-Goals (Ce qui N'est PAS l'Objectif)

**Définition :** Ce qui est explicitement hors scope

```
EXEMPLE :
"Non-goals :
- Ne PAS rendre 2FA obligatoire (optionnel seulement)
- Ne PAS supporter SMS (TOTP uniquement)
- Ne PAS changer l'UI de login existante
- Ne PAS migrer les utilisateurs existants automatiquement"
```

#### 4. Preserved Constraints (Contraintes Préservées)

**Définition :** Ce qui ne doit JAMAIS changer

```
EXEMPLE :
"Doit préserver :
- Le flow de login existant pour utilisateurs sans 2FA
- L'API publique d'authentification
- Les performances de login (< 200ms)
- La compatibilité avec les clients existants"
```

#### 5. Verification Method (Méthode de Vérification)

**Définition :** Comment prouver que ça marche

```
EXEMPLE :
"Vérification :
- 20+ tests unitaires (setup, verify, disable 2FA)
- 5 tests d'intégration (flow complet)
- Test manuel avec Google Authenticator
- Security scan (pas de nouvelles vulnérabilités)
- Performance test (login < 200ms maintenu)"
```

#### 6. Stop Condition (Condition d'Arrêt)

**Définition :** Quand arrêter au lieu de continuer

```
EXEMPLE :
"Arrêter si :
- Nécessite un breaking change de l'API
- Impact performance > 50ms
- Nécessite migration de données
- Complexité > 2 jours de travail"
```

---

## 📝 Exemple Complet de Contrat

### Mauvais Contrat (Vague)

```
"Modernize AuthenticationService."
```

**Problèmes :**
- ❌ Pas de critères de succès
- ❌ Pas de contraintes
- ❌ Pas de vérification
- ❌ Impossible à reviewer

### Bon Contrat (Clair)

```
TASK: Modernize AuthenticationService to Java 21

INTENT:
Refactor AuthenticationService to use modern Java 21 
features (records, pattern matching, virtual threads) 
while maintaining exact behavior.

SUCCESS CONDITION:
- Code uses Java 21 idioms
- All existing tests pass WITHOUT modification
- Code coverage maintained at 85%+
- No public API changes

NON-GOALS:
- Do NOT change authentication logic
- Do NOT add new features
- Do NOT modify database schema
- Do NOT change error messages

PRESERVED CONSTRAINTS:
- All login behavior (password, token, refresh)
- All audit logging
- All error handling
- All security checks
- Performance characteristics (< 100ms login)

VERIFICATION METHOD:
- All 47 existing tests pass unchanged
- Manual testing of login flow
- Performance benchmark (before/after comparison)
- Security scan shows no new issues
- Code review by 2 senior developers

STOP CONDITIONS:
- If refactor requires behavior change
- If tests need modification to pass
- If performance degrades > 10%
- If new dependencies required
```

**Avantages :**
- ✅ Critères clairs
- ✅ Contraintes explicites
- ✅ Vérification définie
- ✅ Facile à reviewer

---

## 🎯 Contrats Selon le Type de Tâche

### 1. Contrat pour une Feature

```
TYPE: Feature (Nouvelle fonctionnalité)

STRUCTURE:
├── Ce que l'utilisateur peut faire après
├── Ce qui ne doit pas régresser
├── Quels comportements comptent comme "done"
└── Critères d'acceptation

EXEMPLE: Pagination d'une liste de produits
─────────────────────────────────────────
INTENT:
Ajouter pagination à GET /products pour améliorer 
les performances avec de grandes listes.

SUCCESS:
- Paramètres page et limit fonctionnent
- Réponse inclut total, pages, data
- Valeurs par défaut : page=1, limit=20
- Maximum : limit=100

NON-GOALS:
- Ne PAS changer le modèle Product
- Ne PAS modifier la base de données

PRESERVED:
- Comportement sans paramètres (backward compatible)
- Format de réponse pour clients existants
- Performance pour petites listes

VERIFICATION:
- 15 tests de pagination
- Tests existants passent
- Test avec 10,000 produits
- Documentation API mise à jour

STOP IF:
- Breaking change nécessaire
- Performance dégradée pour petites listes
```

---

### 2. Contrat pour un Bug

```
TYPE: Bug Fix

STRUCTURE:
├── Test qui échoue actuellement
├── Test qui passe après le fix
├── Comportement adjacent intact
└── Pas de régression

EXEMPLE: NullPointerException dans le login
─────────────────────────────────────────
INTENT:
Fix NullPointerException in AuthService.login() 
when email is null.

SUCCESS:
- Test testLoginWithNullEmail() passes
- Returns validation error instead of exception
- HTTP 400 with clear error message

NON-GOALS:
- Ne PAS changer la logique de login valide
- Ne PAS modifier l'API

PRESERVED:
- Tous les cas de login valides
- Tous les autres cas d'erreur
- Format des messages d'erreur

VERIFICATION:
- Nouveau test testLoginWithNullEmail() passe
- Tous les 23 tests existants passent
- Test manuel avec email null
- Pas de nouvelle exception dans les logs

STOP IF:
- Fix nécessite changement de comportement
- Fix impacte les cas valides
```

---

### 3. Contrat pour une Modernisation

```
TYPE: Modernization/Refactoring

STRUCTURE:
├── Comportement préservé
├── Tests existants passent
├── Interfaces publiques fixes
├── Changements intentionnels nommés
└── Pas de changements smuggled

EXEMPLE: Refactor vers async/await
─────────────────────────────────────────
INTENT:
Migrate DataService from callbacks to async/await 
for better readability and error handling.

SUCCESS:
- All methods use async/await
- No callbacks remain
- Code is more readable
- Error handling improved

NON-GOALS:
- Ne PAS changer le comportement
- Ne PAS modifier l'API publique
- Ne PAS ajouter de features

PRESERVED:
- Exact same behavior for all methods
- Same error types thrown
- Same performance characteristics
- Same return values

VERIFICATION:
- All 34 existing tests pass WITHOUT modification
- Manual testing of all flows
- Performance benchmark (no degradation)
- Code review confirms readability improvement

STOP IF:
- Tests need modification to pass
- Behavior changes detected
- Performance degrades
- Breaking changes required
```

---

### 4. Contrat pour la Sécurité

```
TYPE: Security Fix

STRUCTURE:
├── Réduction de menace
├── Pas de nouvelle exposition
├── Pas juste "fix the warning"
└── Vérification de sécurité

EXEMPLE: Fix SQL Injection
─────────────────────────────────────────
INTENT:
Fix SQL injection vulnerability in search endpoint 
by using PreparedStatement.

SUCCESS:
- No SQL injection possible
- All queries use PreparedStatement
- Security scan shows vulnerability fixed
- No new vulnerabilities introduced

NON-GOALS:
- Ne PAS changer la logique de recherche
- Ne PAS modifier les résultats

PRESERVED:
- Search functionality
- Search results accuracy
- Search performance
- API contract

VERIFICATION:
- Security scan (OWASP ZAP) passes
- Penetration test with injection attempts
- All tests pass
- Code review by security team

STOP IF:
- Fix introduces new vulnerability
- Fix breaks search functionality
- Performance impact > 20%
```

---

### 5. Contrat pour la Documentation

```
TYPE: Documentation

STRUCTURE:
├── Exactitude contre comportement shippé
├── Pas juste du texte plausible
├── Vérifiable contre le code
└── Utile pour les utilisateurs

EXEMPLE: API Documentation
─────────────────────────────────────────
INTENT:
Document all REST API endpoints with examples, 
parameters, and error codes.

SUCCESS:
- All endpoints documented
- Request/response examples for each
- All parameters described
- All error codes explained
- Examples are tested and work

NON-GOALS:
- Ne PAS documenter les endpoints internes
- Ne PAS inclure les endpoints deprecated

PRESERVED:
- Documentation accuracy
- Consistency with actual behavior

VERIFICATION:
- All examples tested manually
- All examples work as documented
- Technical writer review
- Developer review for accuracy
- User testing for clarity

STOP IF:
- Documentation contradicts actual behavior
- Examples don't work
- Too complex for target audience
```

---

## ⏰ Écrire le Contrat AVANT l'Exécution

### Le Bon Moment

> **Citation du document source :**  
> "The right moment to define the contract is before execution, not after a good-looking diff appears."

```
MAUVAIS TIMING :
Code généré → "Est-ce que c'est bon ?" → Essayer de définir des critères
❌ Trop tard
❌ Biais de confirmation
❌ Difficile de rejeter

BON TIMING :
Contrat défini → Code généré → "Est-ce que ça respecte le contrat ?"
✅ Critères clairs avant
✅ Jugement objectif
✅ Facile de rejeter si non conforme
```

### Un Moment de Discipline

> **Citation du document source :**  
> "That does not mean weeks of ceremony. It means one moment of discipline."

**4 Questions Essentielles :**

```
1. Qu'essayons-nous d'accomplir ?
   → Intent clair

2. Qu'est-ce qui doit rester vrai ?
   → Contraintes préservées

3. Comment allons-nous le vérifier ?
   → Méthode de vérification

4. Qu'est-ce qui nous ferait arrêter ?
   → Stop conditions
```

**Si ces réponses sont floues, la tâche est sous-spécifiée.**

---

## 🚀 Les Contrats Accélèrent les Reviews

### Comment les Contrats Aident les Reviewers

> **Citation du document source :**  
> "A clear contract helps more than Bob. It helps reviewers ask better questions."

```
SANS CONTRAT :
Reviewer : "Est-ce que ce code est bon ?"
❓ Question vague
❓ Review basée sur le goût
❓ Débats subjectifs

AVEC CONTRAT :
Reviewer : 
✅ "Le changement satisfait-il l'outcome déclaré ?"
✅ "Les comportements préservés sont-ils préservés ?"
✅ "La vérification est-elle assez forte pour le risque ?"
✅ "Le diff dépasse-t-il le scope approuvé ?"
```

### Exemple de Review Avec Contrat

```
CONTRAT :
"Ajouter validation email, préserver comportement,
 tous les tests passent"

REVIEW CHECKLIST :
□ Validation email ajoutée ? → OUI
□ Validation fonctionne correctement ? → OUI
□ Comportement préservé ? → Vérifier tests
□ Tous les tests passent ? → OUI (47/47)
□ Pas de changement hors scope ? → OUI
□ Documentation mise à jour ? → OUI

DÉCISION : APPROVE ✅
```

> **Citation du document source :**  
> "Without a contract, reviews drift into taste and guesswork."

---

## 💡 Exercice 1 : Identifier les Éléments Manquants

Pour chaque contrat incomplet, identifiez ce qui manque :

**Contrat A :**
```
"Add caching to improve performance.
Success: Response time < 100ms."
```

**Contrat B :**
```
"Refactor UserService.
Preserve all behavior.
All tests must pass."
```

**Contrat C :**
```
"Fix the bug in login.
Test should pass.
No breaking changes."
```

<details>
<summary>Voir les réponses</summary>

**Contrat A - Manque :**
- ❌ Non-goals (quel type de cache ? où ?)
- ❌ Preserved constraints (quoi ne pas changer ?)
- ❌ Verification method (comment mesurer ?)
- ❌ Stop conditions (quand arrêter ?)

**Contrat B - Manque :**
- ❌ Intent spécifique (pourquoi refactorer ?)
- ❌ Success condition détaillée
- ❌ Non-goals
- ❌ Verification method (quels tests ?)
- ❌ Stop conditions

**Contrat C - Manque :**
- ❌ Intent clair (quel bug exactement ?)
- ❌ Success condition (quel test ?)
- ❌ Non-goals
- ❌ Preserved constraints
- ❌ Verification method détaillée
- ❌ Stop conditions

</details>

---

## 🎯 Exercice 2 : Écrire un Contrat Complet

### Mission

Écrivez un contrat complet pour cette tâche :

**Tâche :** "Ajouter un système de rate limiting à l'API pour prévenir les abus"

Utilisez le template :

```
INTENT:
[Votre intent]

SUCCESS CONDITION:
[Vos critères de succès]

NON-GOALS:
[Ce qui n'est PAS l'objectif]

PRESERVED CONSTRAINTS:
[Ce qui doit rester inchangé]

VERIFICATION METHOD:
[Comment vérifier]

STOP CONDITIONS:
[Quand arrêter]
```

<details>
<summary>Voir une solution possible</summary>

```
INTENT:
Implémenter rate limiting sur tous les endpoints publics 
de l'API pour prévenir les abus et assurer une utilisation 
équitable des ressources.

SUCCESS CONDITION:
- Rate limit de 100 requêtes/minute par IP
- Retourne HTTP 429 avec Retry-After header
- Monitoring des rejets en place
- Configuration flexible par endpoint
- Performance impact < 5ms par requête

NON-GOALS:
- Ne PAS limiter les endpoints internes/admin
- Ne PAS implémenter de système de quotas payants
- Ne PAS bloquer définitivement les IPs
- Ne PAS nécessiter d'infrastructure externe (Redis)

PRESERVED CONSTRAINTS:
- Tous les endpoints fonctionnent normalement
- Pas de breaking change pour les clients
- Performance globale maintenue
- Compatibilité avec load balancer existant
- Logs et monitoring existants

VERIFICATION METHOD:
- 25 tests unitaires (limite, dépassement, reset)
- 10 tests d'intégration (flow complet)
- Load test : 1000 req/s pendant 5 minutes
- Test manuel avec différentes IPs
- Performance test : overhead < 5ms
- Monitoring dashboard configuré

STOP CONDITIONS:
- Si nécessite infrastructure externe non disponible
- Si impact performance > 10ms
- Si breaking change pour clients existants
- Si complexité > 3 jours de travail
- Si faux positifs > 1% en test
```

</details>

---

## 📊 Auto-Évaluation

### Questions

1. **Quelle est la chose durable dans le travail agentique ?**
   - [ ] Le code exact généré
   - [ ] Le contrat autour du changement
   - [ ] La conversation avec Bob
   - [ ] Le nombre de lignes de code

2. **Combien d'éléments essentiels dans un contrat complet ?**
   - [ ] 3
   - [ ] 6
   - [ ] 10
   - [ ] Ça dépend

3. **Quand doit-on écrire le contrat ?**
   - [ ] Après avoir vu le code généré
   - [ ] Avant l'exécution
   - [ ] Pendant la review
   - [ ] À la fin du projet

4. **Que signifie "Non-Goals" ?**
   - [ ] Les objectifs négatifs
   - [ ] Ce qui n'est PAS l'objectif
   - [ ] Les objectifs impossibles
   - [ ] Les objectifs rejetés

5. **Comment les contrats aident-ils les reviews ?**
   - [ ] Ils les rendent plus longues
   - [ ] Ils permettent des questions objectives
   - [ ] Ils remplacent les reviews
   - [ ] Ils sont optionnels

<details>
<summary>Voir les réponses</summary>

1. **✅ Le contrat autour du changement** - Le code peut varier, le contrat reste
2. **✅ 6** - Intent, Success, Non-Goals, Preserved, Verification, Stop
3. **✅ Avant l'exécution** - Définir les critères avant de générer
4. **✅ Ce qui n'est PAS l'objectif** - Explicitement hors scope
5. **✅ Ils permettent des questions objectives** - Critères clairs vs goût

**Score :**
- 5/5 : Excellent ! Vous maîtrisez les contrats
- 3-4/5 : Bien ! Relisez les sections où vous avez hésité
- 0-2/5 : Relisez le tutoriel attentivement

</details>

---

## 📚 Ce que Vous Avez Appris

Dans ce tutoriel, vous avez découvert :

✅ **La chose durable** : Le contrat, pas le code exact

✅ **Contrats vs Copy-Paste** : Accord borné vs implémentation figée

✅ **6 éléments essentiels** : Intent, Success, Non-Goals, Preserved, Verification, Stop

✅ **Contrats par type** : Feature, Bug, Modernization, Security, Documentation

✅ **Timing** : Avant l'exécution, pas après

✅ **Reviews accélérées** : Questions objectives vs goût

---

## 🚀 Prochaines Étapes

Maintenant que vous savez écrire des contrats :

1. **Tutoriel 2.4** : Votre Première Tâche Accountable (applique tout !)
2. **Tutoriel 3.1** : Code Review comme Evidence
3. **Tutoriel 3.2** : Modernisation Sans Dérive Comportementale

---

## 💡 Points Clés à Retenir

1. **Contrat > Code** : Le contrat est durable, le code peut varier
2. **6 éléments** : Intent, Success, Non-Goals, Preserved, Verification, Stop
3. **Avant, pas après** : Définir avant d'exécuter
4. **Adapter au type** : Feature ≠ Bug ≠ Modernization
5. **Reviews objectives** : Critères clairs vs goût
6. **Un moment de discipline** : 4 questions essentielles

---

**Prochaine étape :** [Tutoriel 2.4 : Votre Première Tâche Accountable](tutoriel-2.4-premiere-tache.md)

**Besoin d'aide ?** Consultez le [README.md](README.md) ou contactez votre formateur

---

*Ce tutoriel fait partie du Parcours Pédagogique IBM Bob v1.0*  
*Basé sur "Getting Started with IBM Bob" v1.2.0 par Markus Eisele*