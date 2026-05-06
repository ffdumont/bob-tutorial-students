# Tutoriel 1.2 : Le Cycle de Vie Agentique (Agentic SDLC)

**Module :** 1 - Fondamentaux  
**Durée estimée :** 45 minutes  
**Niveau :** Fondamental  
**Prérequis :** Tutoriel 1.1 - Introduction à IBM Bob

## 🎓 Pour les Projets DL+RL

**Étudiants ESIEE :** Consultez votre [fiche projet](fiches-projet-esiee-guide.md) pour des questions spécifiques sur comment le cycle agentique s'applique à votre projet (finance, vision, RL, trafic, fraude, recommandation).

---
---

## 🎯 Objectifs d'Apprentissage

À la fin de ce tutoriel, vous serez capable de :
- ✅ Comprendre et appliquer la boucle Orient-Bound-Plan-Act-Verify-Explain
- ✅ Distinguer Inner Loop et Outer Loop
- ✅ Utiliser l'Evidence Ledger pour tracer les décisions
- ✅ Adapter le cycle selon votre rôle (dev, architect, PM, QA, etc.)
- ✅ Appliquer le cycle sur une tâche réelle

---

## 📚 Introduction : Un Modèle Simple et Universel

### Le Cycle Agentique en Une Ligne

```
Orient → Bound → Plan → Act → Verify → Explain
```

Ce cycle est **intentionnellement simple** pour que tout le monde puisse l'utiliser :
- Développeurs ✅
- Architectes ✅
- Product Managers ✅
- Testeurs/QA ✅
- Sécurité ✅
- Managers ✅

### Pourquoi Ce Modèle ?

Le cycle ne rend pas le logiciel facile. **Il rend le travail lisible.**

C'est la différence entre :
- ❌ "Bob a fait quelque chose et ça marche (peut-être)"
- ✅ "Voici ce qu'on voulait, comment on l'a borné, le plan approuvé, ce qui a été fait, comment on l'a vérifié, et pourquoi"

---

## 🔄 Les 6 Phases du Cycle

### Phase 1 : Orient 🧭

**Objectif :** Comprendre le système réel avant de demander un changement

#### Que fait-on dans Orient ?

```
COMPRENDRE :
├── Le business goal
├── Le code et configuration existants
├── Le comportement actuel
├── Les tests et modes de défaillance
└── Le contexte d'équipe
```

#### Pourquoi c'est important ?

> **Citation du document source :**  
> "Orient means understanding the real system before asking for change."

Sans Orient, vous risquez de :
- Proposer des solutions qui ne s'intègrent pas
- Ignorer des contraintes existantes
- Casser des comportements non documentés
- Réinventer ce qui existe déjà

#### Exemple Concret

**Mauvais (sans Orient) :**
```
"Bob, ajoute un cache Redis"
```

**Bon (avec Orient) :**
```
"Bob, analyse d'abord :
1. Comment le caching est géré actuellement ?
2. Y a-t-il déjà une connexion Redis ?
3. Quels sont les patterns de cache existants ?
4. Quels services utilisent déjà du cache ?

Ensuite, propose une approche cohérente."
```

---

### Phase 2 : Bound 🎯

**Objectif :** Décider ce qui est autorisé et ce qui ne l'est pas

#### Que fait-on dans Bound ?

```
DÉFINIR LES LIMITES :
├── Fichiers et systèmes in-scope
├── Changements out-of-scope
├── Approbations requises
├── Limites d'environnement
├── Restrictions sécurité/compliance
└── Conditions d'arrêt
```

#### Pourquoi c'est important ?

> **Citation du document source :**  
> "Bound means deciding what is allowed to happen and what is not."

Les contraintes transforment l'intent en quelque chose de **safe** :
- Protègent contre les changements non désirés
- Définissent le périmètre d'action
- Établissent les garde-fous
- Permettent l'autonomie dans des limites claires

#### Exemple Concret

**Mauvais (sans Bound) :**
```
"Bob, améliore les performances"
```

**Bon (avec Bound) :**
```
"Bob, améliore les performances de la recherche :

IN-SCOPE :
- SearchService.java
- SearchRepository.java
- Tests associés

OUT-OF-SCOPE :
- Ne touche PAS à la base de données
- Ne change PAS l'API publique
- Ne modifie PAS les autres services

CONTRAINTES :
- Préserve le comportement exact
- Tous les tests doivent passer
- Pas de nouvelles dépendances sans approbation

STOP SI :
- Les changements nécessitent une migration de données
- L'amélioration nécessite un breaking change"
```

---

### Phase 3 : Plan 📋

**Objectif :** Proposer une approche avant d'exécuter

#### Que fait-on dans Plan ?

```
CRÉER UN PLAN :
├── Quels fichiers seront modifiés
├── Dans quel ordre
├── Quelles dépendances ajouter/modifier
├── Quels tests créer/modifier
├── Quels risques potentiels
└── Quelles alternatives considérées
```

#### Pourquoi c'est important ?

> **Citation du document source :**  
> "Bob separates planning from execution"

Le plan permet de :
- Valider l'approche avant d'investir du temps
- Détecter les problèmes tôt
- Obtenir un feedback rapide
- Garder le contrôle sur la direction

#### Exemple de Plan Bob

```
TODO LIST CREATED:

1. Add caching to SearchService
   - Add @Cacheable annotation to search() method
   - Configure cache name "search-results"
   - Set TTL to 5 minutes

2. Update application.properties
   - Add Redis connection config
   - Configure cache settings

3. Add cache eviction
   - Add @CacheEvict on update operations
   - Ensure cache consistency

4. Update tests
   - Add tests for cached results
   - Add tests for cache eviction
   - Verify cache behavior

5. Update documentation
   - Document caching strategy
   - Add cache monitoring notes

RISKS:
- Cache invalidation complexity
- Potential stale data if TTL too long

ALTERNATIVES CONSIDERED:
- In-memory cache (rejected: not distributed)
- Database query optimization (complementary, not alternative)
```

---

### Phase 4 : Act ⚙️

**Objectif :** Exécuter le plan approuvé

#### Que fait-on dans Act ?

```
EXÉCUTER :
├── Modifier les fichiers selon le plan
├── Ajouter/modifier les tests
├── Exécuter les tests
├── Vérifier la syntaxe
└── Créer les commits/branches
```

#### Pourquoi c'est important ?

> **Citation du document source :**  
> "If execution feels exciting, something went wrong—usually upstream of the merge."

L'exécution devrait être :
- **Rapide** : Pas de surprises
- **Prévisible** : Suit le plan approuvé
- **Traçable** : Chaque action est loggée
- **Ennuyeuse** : C'est bon signe !

#### Ce qui se passe pendant Act

```
STATUS: I'm working on it

✓ Modifying: src/services/SearchService.java
✓ Modifying: src/config/application.properties
✓ Modifying: src/tests/SearchServiceTest.java
✓ Running: mvn test
✓ All tests passed
✓ Creating commit: "Add Redis caching to search"

STATUS: Completed
```

---

### Phase 5 : Verify ✅

**Objectif :** Prouver que le résultat est correct

#### Que fait-on dans Verify ?

```
VÉRIFIER :
├── Les tests passent
├── Le comportement est préservé
├── Les contraintes sont respectées
├── Pas de régression
├── La performance est acceptable
└── La sécurité n'est pas compromise
```

#### Pourquoi c'est important ?

> **Citation du document source :**  
> "Evidence beats assumptions"

La vérification transforme "ça a l'air de marcher" en "voici la preuve que ça marche" :
- Tests automatisés ✅
- Tests manuels si nécessaire ✅
- Métriques de performance ✅
- Scan de sécurité ✅
- Review de code ✅

#### Exemple de Vérification

```
VERIFICATION REPORT:

✅ Unit Tests: 45/45 passed
✅ Integration Tests: 12/12 passed
✅ Behavior Preserved: All existing tests pass
✅ Performance: Search time reduced from 250ms to 45ms
✅ Security Scan: No new vulnerabilities
✅ Code Coverage: 87% (target: 80%)

⚠️ NOTES:
- Cache hit rate will need monitoring in production
- Consider adding cache warming for popular searches

✅ READY FOR REVIEW
```

---

### Phase 6 : Explain 📝

**Objectif :** Documenter les décisions et le contexte

#### Que fait-on dans Explain ?

```
EXPLIQUER :
├── Pourquoi ce changement
├── Quelles alternatives considérées
├── Quels risques identifiés
├── Comment c'est vérifié
├── Quoi surveiller en production
└── Qui a approuvé quoi
```

#### Pourquoi c'est important ?

> **Citation du document source :**  
> "Without that trail, the code lands but the judgment disappears."

L'explication permet :
- La review par d'autres
- L'audit si nécessaire
- La compréhension future
- Le transfert de connaissance
- La responsabilité claire

#### Exemple d'Explication

```
CHANGE SUMMARY:

WHAT: Added Redis caching to search functionality

WHY: Search queries were taking 250ms average, causing 
     poor user experience during peak hours

HOW: 
- Added @Cacheable to SearchService.search()
- Configured 5-minute TTL
- Added cache eviction on updates
- All existing tests pass + 8 new cache tests

ALTERNATIVES CONSIDERED:
- Database query optimization: Complementary, will do next
- In-memory cache: Not suitable for distributed deployment
- Longer TTL: Risk of stale data too high

RISKS & MITIGATION:
- Cache invalidation: Eviction on all update operations
- Stale data: 5-minute TTL balances freshness vs performance
- Memory usage: Monitoring added, alerts configured

VERIFICATION:
- 57 tests pass (45 existing + 12 new)
- Performance improved: 250ms → 45ms
- No security issues found
- Code coverage: 87%

MONITORING:
- Cache hit rate (target: >70%)
- Cache memory usage
- Search response time

APPROVED BY: @tech-lead
REVIEWED BY: @senior-dev
```

---

## 🔁 Inner Loop vs Outer Loop

### Inner Loop : Le Cycle Rapide

**Utilisé pour :** Tâches individuelles, itérations rapides

```
Orient (quick) → Bound (light) → Plan → Act → Verify → Explain (brief)
```

**Exemple :** Ajouter une validation à un champ
- Orient : 30 secondes (lire le fichier)
- Bound : 1 minute (définir le scope)
- Plan : 2 minutes (Bob propose)
- Act : 1 minute (exécution)
- Verify : 2 minutes (tests)
- Explain : 1 minute (commit message)

**Total : ~7 minutes**

### Outer Loop : Le Cycle Complet

**Utilisé pour :** Features complexes, changements multi-fichiers

```
Orient (deep) → Bound (strict) → Plan (detailed) → 
  [Multiple Inner Loops] → 
Verify (comprehensive) → Explain (full)
```

**Exemple :** Migrer un service vers une nouvelle architecture
- Orient : 1-2 heures (analyse complète)
- Bound : 30 minutes (contraintes détaillées)
- Plan : 1 heure (plan multi-étapes)
- Act : Multiple inner loops sur plusieurs jours
- Verify : 2-3 heures (tests complets, review)
- Explain : 1 heure (documentation, ADR)

**Total : Plusieurs jours**

---

## 📊 L'Evidence Ledger

### Qu'est-ce que c'est ?

L'**Evidence Ledger** est la trace complète de votre travail avec Bob :
- Tous les prompts
- Tous les plans
- Toutes les approbations
- Tous les changements
- Toutes les vérifications
- Toutes les explications

### Pourquoi c'est important ?

```
SANS Evidence Ledger :
"Bob a changé quelque chose, ça marche"
❌ Pas auditable
❌ Pas reproductible
❌ Pas compréhensible

AVEC Evidence Ledger :
"Voici l'intent, le plan approuvé, les changements,
les tests, et l'explication"
✅ Auditable
✅ Reproductible
✅ Compréhensible
```

### Exemple d'Evidence Ledger

```
TASK #1234: Add caching to search

ORIENT (2024-05-06 10:00):
- Analyzed SearchService.java
- Reviewed existing cache patterns
- Identified Redis as standard

BOUND (2024-05-06 10:15):
- Scope: SearchService only
- Constraint: No API changes
- Stop condition: If requires DB migration

PLAN (2024-05-06 10:20):
- [Plan details as shown above]
- APPROVED BY: @user at 10:25

ACT (2024-05-06 10:30):
- Modified 3 files
- Added 12 tests
- All tests passed

VERIFY (2024-05-06 10:45):
- 57/57 tests pass
- Performance: 250ms → 45ms
- Security scan: Clean

EXPLAIN (2024-05-06 11:00):
- PR #567 created
- Documentation updated
- Team notified

EVIDENCE:
- Chat transcript: [link]
- Plan approval: [screenshot]
- Test results: [report]
- PR: [link]
```

---

## 👥 Le Cycle Selon Votre Rôle

### Pour les Développeurs

**Focus :** Act et Verify

```
Orient: Comprendre le code existant
Bound: Définir le scope technique
Plan: Valider l'approche
Act: ⭐ Implémenter
Verify: ⭐ Tester rigoureusement
Explain: Documenter dans le PR
```

### Pour les Architectes

**Focus :** Orient et Bound

```
Orient: ⭐ Analyser l'architecture existante
Bound: ⭐ Définir les contraintes architecturales
Plan: Valider la cohérence
Act: Superviser
Verify: Valider l'intégration
Explain: Documenter les décisions (ADR)
```

### Pour les Product Managers

**Focus :** Orient et Explain

```
Orient: ⭐ Définir le business goal
Bound: Définir les priorités
Plan: Valider l'alignement business
Act: Observer
Verify: Valider l'outcome
Explain: ⭐ Communiquer la valeur
```

### Pour les Testeurs/QA

**Focus :** Bound et Verify

```
Orient: Comprendre le comportement attendu
Bound: ⭐ Définir les critères d'acceptation
Plan: Valider la testabilité
Act: Observer
Verify: ⭐ Tester exhaustivement
Explain: Documenter les résultats de test
```

### Pour la Sécurité

**Focus :** Bound et Verify

```
Orient: Identifier les risques
Bound: ⭐ Définir les contraintes de sécurité
Plan: Review pour les risques
Act: Observer
Verify: ⭐ Scan de sécurité, audit
Explain: Documenter les validations
```

### Pour les Managers

**Focus :** Bound et Explain

```
Orient: Comprendre le contexte business
Bound: ⭐ Définir les limites de ressources
Plan: Valider la faisabilité
Act: Observer
Verify: Valider les outcomes
Explain: ⭐ Communiquer aux stakeholders
```

---

## 💡 Exercice 1 : Identifier les Phases

Pour chaque action, identifiez la phase du cycle :

1. "Lire les tests existants pour comprendre le comportement"
2. "Décider que les changements ne doivent pas toucher à l'API publique"
3. "Bob propose de modifier 3 fichiers dans cet ordre"
4. "Bob modifie les fichiers et exécute les tests"
5. "Vérifier que tous les tests passent et qu'il n'y a pas de régression"
6. "Écrire un message de commit expliquant le changement"

<details>
<summary>Voir les réponses</summary>

1. **Orient** 🧭 - Comprendre le système existant
2. **Bound** 🎯 - Définir les contraintes
3. **Plan** 📋 - Proposer une approche
4. **Act** ⚙️ - Exécuter
5. **Verify** ✅ - Vérifier
6. **Explain** 📝 - Documenter

</details>

---

## 🎯 Exercice 2 : Appliquer le Cycle

**Scénario :** Vous devez ajouter une fonctionnalité de pagination à un endpoint qui retourne une liste de produits.

Pour chaque phase, écrivez ce que vous feriez :

### Template

```
ORIENT:
[Que devez-vous comprendre d'abord ?]

BOUND:
[Quelles sont les limites ?]

PLAN:
[Quelle approche proposer ?]

ACT:
[Que faire concrètement ?]

VERIFY:
[Comment vérifier ?]

EXPLAIN:
[Que documenter ?]
```

<details>
<summary>Voir une solution possible</summary>

```
ORIENT:
- Analyser l'endpoint GET /products actuel
- Comprendre comment les données sont récupérées
- Vérifier s'il y a déjà de la pagination ailleurs
- Lire les tests existants
- Vérifier les conventions API du projet

BOUND:
IN-SCOPE:
- ProductController.java
- ProductService.java
- ProductControllerTest.java

OUT-OF-SCOPE:
- Ne pas changer le modèle Product
- Ne pas modifier la base de données

CONTRAINTES:
- Utiliser les paramètres page et limit (query params)
- Valeurs par défaut : page=1, limit=20
- Maximum : limit=100
- Retourner aussi le total et le nombre de pages
- Préserver le comportement pour les clients existants

STOP SI:
- Nécessite un breaking change
- Performance dégradée

PLAN:
1. Ajouter paramètres page et limit au controller
2. Modifier ProductService pour supporter la pagination
3. Créer un PagedResponse<Product> wrapper
4. Ajouter validation des paramètres
5. Mettre à jour les tests existants
6. Ajouter tests pour la pagination
7. Mettre à jour la documentation API

ACT:
- Bob modifie les fichiers selon le plan
- Bob exécute les tests
- Bob crée le commit

VERIFY:
- Tous les tests passent (existants + nouveaux)
- Test manuel avec différentes valeurs de page/limit
- Vérifier que les clients existants fonctionnent toujours
- Vérifier la performance avec de grandes listes
- Code review

EXPLAIN:
PR Description:
"Added pagination to GET /products endpoint

WHY: Current endpoint returns all products, causing 
     performance issues with large catalogs

HOW:
- Added page and limit query parameters
- Default: page=1, limit=20, max=100
- Returns PagedResponse with data, page, limit, total, pages
- Backward compatible: works without parameters

TESTS:
- 15 new tests for pagination
- All existing tests pass
- Manual testing completed

BREAKING CHANGES: None
MIGRATION: None required"
```

</details>

---

## 🔄 Exercice 3 : Inner Loop vs Outer Loop

Pour chaque tâche, déterminez si c'est un Inner Loop ou Outer Loop :

1. Corriger un typo dans un message d'erreur
2. Migrer toute l'application de Java 11 à Java 21
3. Ajouter une validation d'email à un champ
4. Refactorer l'architecture pour passer de monolithe à microservices
5. Renommer une variable pour plus de clarté
6. Implémenter un nouveau module de paiement avec 3 providers

<details>
<summary>Voir les réponses</summary>

1. **Inner Loop** - Tâche simple, un fichier, rapide
2. **Outer Loop** - Changement majeur, multi-fichiers, plusieurs jours
3. **Inner Loop** - Tâche bornée, quelques fichiers, quelques minutes
4. **Outer Loop** - Changement architectural, toute l'app, plusieurs semaines
5. **Inner Loop** - Changement trivial, un fichier, < 1 minute
6. **Outer Loop** - Feature complexe, multi-fichiers, plusieurs jours

**Règle générale :**
- Inner Loop : < 1 heure, < 5 fichiers, impact local
- Outer Loop : > 1 heure, > 5 fichiers, impact global

</details>

---

## 📋 Checklist du Cycle Agentique

Utilisez cette checklist pour chaque tâche :

### Avant de Commencer

- [ ] J'ai défini l'intent clairement
- [ ] Je comprends le business goal
- [ ] J'ai identifié les contraintes

### Orient

- [ ] J'ai analysé le code existant
- [ ] J'ai lu les tests pertinents
- [ ] J'ai compris les patterns du projet
- [ ] J'ai identifié les dépendances

### Bound

- [ ] J'ai défini le scope (in/out)
- [ ] J'ai listé les contraintes
- [ ] J'ai défini les stop conditions
- [ ] J'ai identifié les approbations nécessaires

### Plan

- [ ] Bob a proposé un plan détaillé
- [ ] Le plan est cohérent avec le projet
- [ ] Les risques sont identifiés
- [ ] J'ai approuvé le plan

### Act

- [ ] L'exécution suit le plan
- [ ] Les changements sont tracés
- [ ] Pas de surprises pendant l'exécution

### Verify

- [ ] Tous les tests passent
- [ ] Le comportement est préservé
- [ ] Pas de régression
- [ ] La performance est acceptable
- [ ] La sécurité est validée

### Explain

- [ ] Le changement est documenté
- [ ] Les décisions sont expliquées
- [ ] L'Evidence Ledger est complet
- [ ] L'équipe est informée

---

## 🎯 Exercice Final : Cas Pratique Complet

### Mission

Appliquez le cycle complet sur cette tâche :

**Tâche :** Ajouter un système de rate limiting à une API REST pour prévenir les abus.

### Instructions

1. Écrivez ce que vous feriez pour chaque phase
2. Identifiez si c'est un Inner ou Outer Loop
3. Estimez la durée de chaque phase
4. Créez un mini Evidence Ledger

### Template

```
TYPE DE LOOP: [Inner / Outer]

ORIENT (durée estimée: ___):
[Votre analyse]

BOUND (durée estimée: ___):
[Vos contraintes]

PLAN (durée estimée: ___):
[Votre plan]

ACT (durée estimée: ___):
[Vos actions]

VERIFY (durée estimée: ___):
[Vos vérifications]

EXPLAIN (durée estimée: ___):
[Votre documentation]

DURÉE TOTALE ESTIMÉE: ___

EVIDENCE LEDGER:
[Résumé des traces]
```

<details>
<summary>Voir une solution possible</summary>

```
TYPE DE LOOP: Outer Loop (feature complexe)

ORIENT (durée estimée: 1-2 heures):
- Analyser tous les endpoints de l'API
- Comprendre l'architecture actuelle (filters, interceptors)
- Vérifier s'il existe déjà du rate limiting
- Identifier les patterns de sécurité existants
- Analyser les logs pour comprendre les patterns d'usage
- Rechercher les bibliothèques déjà utilisées

BOUND (durée estimée: 30 minutes):
IN-SCOPE:
- Tous les endpoints publics de l'API
- Configuration du rate limiting
- Tests du rate limiting

OUT-OF-SCOPE:
- Endpoints internes/admin
- Modification de la base de données
- Changement des contrats API

CONTRAINTES:
- Utiliser une solution standard (Bucket4j, Resilience4j)
- Limites : 100 requêtes/minute par IP
- Retourner HTTP 429 avec Retry-After header
- Pas de breaking change
- Performance : < 5ms overhead

STOP CONDITIONS:
- Si nécessite une infrastructure externe (Redis) non disponible
- Si impact performance > 10ms

PLAN (durée estimée: 1 heure):
1. Choisir la bibliothèque (Bucket4j recommandé)
2. Créer un RateLimitFilter
3. Configurer les limites par endpoint
4. Implémenter la logique de rate limiting
5. Ajouter les headers de réponse appropriés
6. Créer les tests unitaires
7. Créer les tests d'intégration
8. Ajouter monitoring/métriques
9. Documenter la configuration
10. Mettre à jour la doc API

RISQUES:
- Faux positifs (bloquer des utilisateurs légitimes)
- Contournement via proxies
- Impact performance

ACT (durée estimée: 3-4 heures):
Inner Loop 1: Setup bibliothèque et configuration
Inner Loop 2: Implémenter le filter
Inner Loop 3: Ajouter les tests
Inner Loop 4: Ajouter monitoring
Inner Loop 5: Documentation

VERIFY (durée estimée: 2 heures):
- Tests unitaires : 20+ tests
- Tests d'intégration : Simuler dépassement de limite
- Test de performance : Vérifier overhead < 5ms
- Test de charge : 1000 req/s pendant 5 minutes
- Security review : Vérifier pas de contournement
- Manual testing : Tester avec Postman

EXPLAIN (durée estimée: 1 heure):
PR Description:
"Implemented rate limiting for public API endpoints

WHY: Prevent API abuse and ensure fair usage

HOW:
- Used Bucket4j for token bucket algorithm
- Limit: 100 requests/minute per IP
- Returns HTTP 429 with Retry-After header
- < 5ms performance overhead
- Configurable per endpoint

CONFIGURATION:
- Default: 100 req/min
- Can be overridden in application.yml
- Monitoring via Micrometer metrics

TESTING:
- 25 unit tests
- 10 integration tests
- Load tested: 1000 req/s sustained
- Performance impact: 3ms average

MONITORING:
- Metric: api.ratelimit.rejected
- Metric: api.ratelimit.allowed
- Alert: > 10% rejection rate

DOCUMENTATION:
- API docs updated with rate limit info
- README updated with configuration
- Runbook created for operations"

DURÉE TOTALE ESTIMÉE: 8-11 heures (1-2 jours)

EVIDENCE LEDGER:
- Chat transcript avec Bob: [link]
- Plan approuvé: [timestamp + approver]
- Commits: [list of commits]
- Test results: [test report]
- Performance results: [benchmark report]
- Security review: [approval]
- PR: #789
- Documentation: [links]
```

</details>

---

## 📊 Auto-Évaluation

### Questions

1. **Quelle est la première phase du cycle agentique ?**
   - [ ] Plan
   - [ ] Orient
   - [ ] Bound
   - [ ] Act

2. **Quelle phase définit ce qui est autorisé et ce qui ne l'est pas ?**
   - [ ] Orient
   - [ ] Bound
   - [ ] Plan
   - [ ] Verify

3. **Pourquoi séparer Plan et Act ?**
   - [ ] Pour ralentir le processus
   - [ ] Pour valider l'approche avant d'investir du temps
   - [ ] Parce que Bob ne peut pas faire les deux
   - [ ] Pour créer plus de documentation

4. **Qu'est-ce que l'Evidence Ledger ?**
   - [ ] Un outil de logging
   - [ ] La trace complète du travail avec Bob
   - [ ] Une base de données
   - [ ] Un rapport de test

5. **Quelle est la différence entre Inner Loop et Outer Loop ?**
   - [ ] Inner Loop est pour les juniors, Outer Loop pour les seniors
   - [ ] Inner Loop est rapide et local, Outer Loop est long et global
   - [ ] Il n'y a pas de différence
   - [ ] Inner Loop utilise Bob, Outer Loop non

<details>
<summary>Voir les réponses</summary>

1. **✅ Orient** - C'est toujours la première phase
2. **✅ Bound** - Définit les limites et contraintes
3. **✅ Pour valider l'approche avant d'investir du temps** - Évite le gaspillage
4. **✅ La trace complète du travail avec Bob** - Pour auditabilité et compréhension
5. **✅ Inner Loop est rapide et local, Outer Loop est long et global** - Selon la complexité

**Score :**
- 5/5 : Excellent ! Vous maîtrisez le cycle
- 3-4/5 : Bien ! Relisez les sections où vous avez hésité
- 0-2/5 : Relisez le tutoriel attentivement

</details>

---

## 📚 Ce que Vous Avez Appris

Dans ce tutoriel, vous avez découvert :

✅ **Le cycle agentique** : Orient → Bound → Plan → Act → Verify → Explain

✅ **Les 6 phases** : Leur objectif et comment les appliquer

✅ **Inner vs Outer Loop** : Quand utiliser chaque approche

✅ **L'Evidence Ledger** : Pourquoi et comment tracer le travail

✅ **Le cycle par rôle** : Comment chaque rôle utilise le cycle différemment

✅ **Application pratique** : Comment appliquer le cycle sur des tâches réelles

---

## 🚀 Prochaines Étapes

Maintenant que vous comprenez le cycle agentique :

1. **Tutoriel 1.3** : Comment Bob Pense (Intent, Evidence, Judgment)
2. **Tutoriel 1.4** : La Transition des Habitudes
3. **Tutoriel 2.1** : L'Interface Bob dans l'IDE
4. **Tutoriel 2.2** : Gestion du Contexte (CRITIQUE !)

---

## 💡 Points Clés à Retenir

1. **Orient avant tout** : Comprendre avant de changer
2. **Bound pour la sécurité** : Les contraintes protègent
3. **Plan avant Act** : Valider l'approche d'abord
4. **Verify systématiquement** : La preuve bat les suppositions
5. **Explain toujours** : Le contexte doit survivre au code
6. **Evidence Ledger** : Tracer pour auditer et comprendre

---

**Prochaine étape :** [Tutoriel 1.3 : Comment Bob Pense](tutoriel-1.3-comment-bob-pense.md)

**Besoin d'aide ?** Consultez le [README.md](README.md) ou contactez votre formateur

---

*Ce tutoriel fait partie du Parcours Pédagogique IBM Bob v1.0*  
*Basé sur "Getting Started with IBM Bob" v1.2.0 par Markus Eisele*