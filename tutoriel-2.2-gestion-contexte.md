# Tutoriel 2.2 : Gestion du Contexte avec IBM Bob

**Module :** 2 - Prise en Main  
**Durée estimée :** 1h30  
**Niveau :** Fondamental (CRITIQUE)  
**Prérequis :** Tutoriel 2.1 - L'Interface Bob dans l'IDE

---

## 🎯 Objectifs d'Apprentissage

À la fin de ce tutoriel, vous serez capable de :
- ✅ Comprendre pourquoi le contexte est un budget, pas un dump
- ✅ Gérer efficacement la fenêtre de contexte
- ✅ Distinguer le signal du noise
- ✅ Utiliser les context mentions (@fichier, @dossier)
- ✅ Appliquer les habitudes de grounding
- ✅ Gérer les gros repos et fichiers volumineux
- ✅ Comprendre ce que signifie "200k tokens"
- ✅ Éviter et corriger le context poisoning
- ✅ Créer un Context Pack pour votre équipe

---

## 📚 Contexte Théorique

### Pourquoi le Contexte est CRITIQUE

> **Citation du document source :**  
> "Most Hallucinations Are Context Debt"

Le contexte est LA ressource la plus importante quand vous travaillez avec Bob. La plupart des problèmes que vous rencontrerez (hallucinations, réponses incorrectes, suggestions inappropriées) sont en réalité des problèmes de contexte mal géré.

### Le Contexte comme Budget

Pensez au contexte comme à un budget limité :
- Vous avez environ **200,000 tokens** disponibles
- Chaque fichier, message, et information consomme ce budget
- Quand le budget est épuisé, les informations les plus anciennes sont perdues
- Un contexte mal géré = des décisions basées sur des informations incomplètes

### Comment la Fenêtre de Contexte S'Empile

```
┌─────────────────────────────────────┐
│ System Prompt (Bob's instructions)  │ ← Toujours présent
├─────────────────────────────────────┤
│ Custom Instructions (vos règles)    │ ← Persistant
├─────────────────────────────────────┤
│ Context Mentions (@files, @folders) │ ← Vous contrôlez
├─────────────────────────────────────┤
│ Conversation History                │ ← Grandit avec le temps
├─────────────────────────────────────┤
│ Current Task Context                │ ← Change par tâche
└─────────────────────────────────────┘
        ↓
   200k tokens max
```

---

## 🔍 Partie 1 : Signal vs Noise

### Qu'est-ce que le Signal ?

**Signal** = Information qui aide Bob à prendre la bonne décision :
- ✅ Le fichier exact que vous voulez modifier
- ✅ Les tests qui définissent le comportement attendu
- ✅ La documentation d'architecture pertinente
- ✅ Les contraintes de sécurité applicables
- ✅ Les exemples de code similaires dans le projet

### Qu'est-ce que le Noise ?

**Noise** = Information qui dilue le contexte sans aider :
- ❌ Fichiers non pertinents pour la tâche actuelle
- ❌ Historique de conversation trop long
- ❌ Documentation générique non applicable
- ❌ Dépendances externes complètes
- ❌ Logs ou outputs volumineux

### Exercice 1 : Identifier Signal et Noise

**Scénario :** Vous voulez ajouter une validation d'email à un endpoint REST.

Classez ces éléments en Signal ou Noise :

1. Le fichier du controller REST concerné
2. Tous les fichiers du package `utils`
3. Les tests existants du controller
4. Le fichier `package.json` complet
5. La classe de validation d'email existante
6. Tous les fichiers de configuration
7. La documentation de l'API REST
8. L'historique Git du projet

<details>
<summary>Voir la solution</summary>

**Signal :**
- ✅ 1. Le fichier du controller REST concerné
- ✅ 3. Les tests existants du controller
- ✅ 5. La classe de validation d'email existante
- ✅ 7. La documentation de l'API REST (si elle définit le format attendu)

**Noise :**
- ❌ 2. Tous les fichiers du package `utils` (trop large)
- ❌ 4. Le fichier `package.json` complet (sauf si vous ajoutez une dépendance)
- ❌ 6. Tous les fichiers de configuration (trop large)
- ❌ 8. L'historique Git du projet (non pertinent pour cette tâche)

</details>

---

## 🎯 Partie 2 : Context Mentions

### Syntaxe des Context Mentions

Bob supporte plusieurs types de mentions :

```
@fichier.js              → Mentionne un fichier spécifique
@dossier/                → Mentionne tous les fichiers d'un dossier
@dossier/**/*.test.js    → Pattern matching
```

### Bonnes Pratiques

#### ✅ DO : Soyez Spécifique

```
Mauvais :
"Regarde le code et ajoute une validation"

Bon :
"@src/controllers/UserController.js 
@src/validators/EmailValidator.js
@tests/controllers/UserController.test.js

Ajoute une validation d'email à la méthode createUser() 
en utilisant le pattern de EmailValidator"
```

#### ❌ DON'T : Mentionnez Tout

```
Mauvais :
"@src/ @tests/ @config/ @docs/
Ajoute une validation d'email"

Pourquoi c'est mauvais :
- Consomme tout le budget de contexte
- Dilue l'information pertinente
- Augmente le risque d'hallucination
```

### Exercice 2 : Écrire des Context Mentions Efficaces

Pour chaque tâche, écrivez les context mentions appropriées :

**Tâche A :** Refactorer une fonction de calcul de prix dans un service e-commerce

<details>
<summary>Voir une solution possible</summary>

```
@src/services/PricingService.js
@src/models/Product.js
@tests/services/PricingService.test.js
@docs/pricing-rules.md

Refactore la méthode calculatePrice() pour améliorer 
la lisibilité tout en préservant le comportement exact 
défini dans les tests.
```

</details>

**Tâche B :** Ajouter un nouveau endpoint REST pour récupérer les commandes d'un utilisateur

<details>
<summary>Voir une solution possible</summary>

```
@src/controllers/OrderController.js
@src/services/OrderService.js
@src/models/Order.js
@tests/controllers/OrderController.test.js
@docs/api-conventions.md

Ajoute un endpoint GET /users/:userId/orders qui retourne 
les commandes d'un utilisateur, en suivant les conventions 
API existantes.
```

</details>

---

## 📏 Partie 3 : Comprendre "200k Tokens"

### Qu'est-ce qu'un Token ?

Un token ≈ 4 caractères en moyenne (pour l'anglais)
- "Hello" = 1 token
- "Hello, world!" = 3 tokens
- Un fichier de 1000 lignes ≈ 3000-5000 tokens

### Estimation Rapide

| Type de Contenu | Tokens Approximatifs |
|-----------------|---------------------|
| Message court (50 mots) | ~65 tokens |
| Fichier source moyen (200 lignes) | ~800-1200 tokens |
| Gros fichier (1000 lignes) | ~4000-6000 tokens |
| Documentation complète | ~10000-20000 tokens |
| Conversation de 20 messages | ~5000-10000 tokens |

### Budget de 200k Tokens : Exemples

**Scénario 1 : Contexte Léger (Bon)**
```
System + Instructions:     ~5,000 tokens
3 fichiers sources:       ~3,000 tokens
2 fichiers de tests:      ~2,000 tokens
Documentation:            ~2,000 tokens
Conversation (10 msgs):   ~3,000 tokens
─────────────────────────────────────
Total:                   ~15,000 tokens
Marge restante:         185,000 tokens ✅
```

**Scénario 2 : Contexte Lourd (Attention)**
```
System + Instructions:     ~5,000 tokens
Dossier complet @src/:   ~50,000 tokens
Tous les tests:          ~30,000 tokens
Toute la doc:            ~20,000 tokens
Conversation (50 msgs):  ~15,000 tokens
─────────────────────────────────────
Total:                  ~120,000 tokens
Marge restante:          80,000 tokens ⚠️
```

**Scénario 3 : Contexte Saturé (Problème)**
```
System + Instructions:     ~5,000 tokens
@src/ @tests/ @docs/:    ~150,000 tokens
Conversation longue:      ~50,000 tokens
─────────────────────────────────────
Total:                  ~205,000 tokens
DÉPASSEMENT:              ~5,000 tokens ❌
→ Perte d'informations anciennes
→ Risque d'hallucinations
```

### Exercice 3 : Estimer Votre Budget

1. Ouvrez un de vos projets
2. Comptez approximativement :
   - Nombre de fichiers sources principaux : ___
   - Nombre de fichiers de tests : ___
   - Taille de la documentation : ___
3. Estimez le total de tokens nécessaires
4. Est-ce que tout rentre dans 200k tokens ?

---

## 🛡️ Partie 4 : Habitudes de Grounding

### Qu'est-ce que le Grounding ?

**Grounding** = Ancrer Bob dans la réalité de votre codebase avec des faits vérifiables.

### Les 5 Habitudes de Grounding

#### 1. Commencez Chaque Session avec le Contexte Minimal

```
❌ Mauvais :
"Bob, aide-moi avec mon projet"

✅ Bon :
"@src/services/AuthService.js
@tests/services/AuthService.test.js

Je veux ajouter une authentification à deux facteurs.
Analyse d'abord le code existant et propose un plan."
```

#### 2. Ajoutez du Contexte Progressivement

```
Tour 1: Fichier principal
Tour 2: Tests associés
Tour 3: Dépendances nécessaires
Tour 4: Documentation si besoin
```

#### 3. Vérifiez les Hypothèses de Bob

```
Vous: "Ajoute une validation d'email"

Bob: "Je vais utiliser la bibliothèque validator.js"

Vous: "Vérifie d'abord si validator.js est déjà 
      dans les dépendances. @package.json"
```

#### 4. Utilisez des Exemples Concrets

```
❌ Vague :
"Ajoute une validation"

✅ Concret :
"Ajoute une validation qui rejette les emails 
sans @ et sans domaine, comme dans 
@src/validators/PhoneValidator.js"
```

#### 5. Créez des Checkpoints

```
Après chaque changement majeur :
1. Demandez à Bob de résumer ce qui a été fait
2. Vérifiez que c'est correct
3. Créez un nouveau chat si nécessaire
```

### Exercice 4 : Pratiquer le Grounding

**Scénario :** Vous voulez migrer une fonction de callback vers async/await.

Écrivez une séquence de 3 messages qui applique les habitudes de grounding :

<details>
<summary>Voir une solution possible</summary>

**Message 1 : Contexte minimal**
```
@src/services/DataService.js

Analyse la fonction fetchUserData() qui utilise 
des callbacks. Je veux la migrer vers async/await.
```

**Message 2 : Vérification**
```
Avant de procéder, vérifie :
1. Quelles autres fonctions appellent fetchUserData() ?
2. Y a-t-il des tests existants ?

@tests/services/DataService.test.js
```

**Message 3 : Exécution avec contraintes**
```
Parfait. Maintenant migre fetchUserData() vers async/await :
- Préserve exactement le même comportement
- Mets à jour tous les appelants
- Assure-toi que les tests passent toujours
```

</details>

---

## 📦 Partie 5 : Gros Repos et Fichiers Lourds

### Stratégies pour les Gros Repositories

#### Stratégie 1 : Navigation Progressive

```
Étape 1: Structure globale
"@. liste les dossiers principaux et explique l'architecture"

Étape 2: Zone ciblée
"@src/modules/payment/ explique ce module"

Étape 3: Fichier spécifique
"@src/modules/payment/PaymentService.js analyse ce service"
```

#### Stratégie 2 : Utiliser list_code_definition_names

```
"Liste les classes et fonctions principales dans 
@src/modules/payment/ sans charger tout le code"
```

#### Stratégie 3 : Lecture par Plages de Lignes

```
"@src/services/LargeService.js:1-50
Analyse uniquement la section d'initialisation"

"@src/services/LargeService.js:200-250
Maintenant regarde la méthode processPayment()"
```

### Gestion des Fichiers Volumineux

#### Pour les Spreadsheets et Documents

```
❌ Ne pas faire :
"@data/huge-spreadsheet.xlsx analyse tout"

✅ Faire :
"@data/huge-spreadsheet.xlsx 
Extrais uniquement les colonnes A, B, C 
des lignes 1-100"
```

#### Pour les Logs

```
❌ Ne pas faire :
"@logs/application.log trouve l'erreur"

✅ Faire :
"Recherche dans @logs/application.log 
les lignes contenant 'ERROR' des 30 dernières minutes"
```

### Exercice 5 : Naviguer un Gros Repo

Imaginez un repo avec cette structure :
```
project/
├── src/
│   ├── modules/
│   │   ├── auth/ (50 fichiers)
│   │   ├── payment/ (80 fichiers)
│   │   ├── inventory/ (120 fichiers)
│   │   └── reporting/ (200 fichiers)
│   └── shared/ (30 fichiers)
├── tests/ (500 fichiers)
└── docs/ (100 fichiers)
```

Vous devez ajouter une fonctionnalité de remboursement dans le module payment.

Écrivez une séquence de 4 messages pour naviguer efficacement :

<details>
<summary>Voir une solution possible</summary>

**Message 1 : Vue d'ensemble**
```
@src/modules/payment/
Liste les fichiers principaux et explique l'architecture 
du module payment
```

**Message 2 : Identification**
```
Identifie quel fichier gère les transactions de paiement 
et les remboursements existants (s'il y en a)
```

**Message 3 : Analyse ciblée**
```
@src/modules/payment/TransactionService.js
@src/modules/payment/RefundService.js (si existe)
@tests/modules/payment/TransactionService.test.js

Analyse comment les transactions sont gérées actuellement
```

**Message 4 : Plan d'action**
```
Propose un plan pour ajouter la fonctionnalité de remboursement :
- Quels fichiers modifier
- Quels nouveaux fichiers créer
- Quels tests ajouter
```

</details>

---

## ⚠️ Partie 6 : Context Poisoning

### Qu'est-ce que le Context Poisoning ?

Le **context poisoning** se produit quand :
- Des informations incorrectes s'accumulent dans le contexte
- Bob base ses décisions sur ces informations erronées
- Les erreurs se propagent et s'amplifient

### Symptômes de Context Poisoning

🚨 **Signes d'alerte :**
- Bob répète les mêmes erreurs
- Bob ignore vos corrections
- Bob "hallucine" des fonctions ou fichiers qui n'existent pas
- Bob mélange des concepts de différentes parties du code
- Les réponses deviennent de plus en plus incohérentes

### Causes Communes

1. **Conversation trop longue**
   - Plus de 30-40 messages
   - Contexte accumulé > 150k tokens

2. **Informations contradictoires**
   - Vous corrigez Bob mais le contexte garde l'erreur
   - Plusieurs versions d'un même fichier dans le contexte

3. **Contexte obsolète**
   - Le code a changé mais Bob travaille sur une ancienne version
   - Les tests ont été mis à jour mais pas le code (ou inverse)

4. **Surcharge de contexte**
   - Trop de fichiers mentionnés
   - Documentation contradictoire

### Comment Éviter le Context Poisoning

#### ✅ Prévention

```
1. Gardez les conversations courtes (< 20 messages)
2. Créez un nouveau chat pour chaque tâche majeure
3. Vérifiez régulièrement que Bob a les bonnes informations
4. Utilisez des checkpoints
5. Nettoyez le contexte régulièrement
```

#### 🔧 Correction

```
Si vous détectez du poisoning :

1. STOP immédiatement
2. Créez un NOUVEAU chat
3. Rechargez UNIQUEMENT le contexte nécessaire
4. Vérifiez les informations avant de continuer
5. Documentez ce qui s'est mal passé
```

### Exercice 6 : Détecter et Corriger le Poisoning

**Scénario :** Vous travaillez avec Bob depuis 45 minutes. Voici les symptômes :

- Bob suggère d'utiliser une fonction `validateUser()` qui n'existe pas
- Vous lui dites que la fonction s'appelle `verifyUser()`
- 3 messages plus tard, Bob utilise encore `validateUser()`
- Bob mélange des concepts de deux services différents

**Questions :**
1. Est-ce du context poisoning ?
2. Quelles sont les causes probables ?
3. Que devez-vous faire ?

<details>
<summary>Voir la solution</summary>

**1. Est-ce du context poisoning ?**
Oui, clairement. Les symptômes sont :
- Hallucination de fonctions inexistantes
- Ignore les corrections
- Mélange de concepts

**2. Causes probables :**
- Conversation trop longue (45 minutes)
- Contexte surchargé avec trop d'informations
- Informations contradictoires accumulées

**3. Actions à prendre :**

```
IMMÉDIAT :
1. Arrêtez la conversation actuelle
2. Créez un nouveau chat
3. Rechargez UNIQUEMENT :
   - Le fichier que vous modifiez
   - Les tests associés
   - La documentation pertinente

ENSUITE :
4. Vérifiez explicitement :
   "La fonction s'appelle verifyUser(), pas validateUser(). 
   Confirme que tu as bien compris."

5. Procédez avec la tâche

PRÉVENTION FUTURE :
6. Créez un nouveau chat toutes les 15-20 minutes
7. Utilisez des context mentions plus précis
8. Documentez les noms corrects dans vos custom instructions
```

</details>

---

## 📋 Partie 7 : Le Context Pack

### Qu'est-ce qu'un Context Pack ?

Un **Context Pack** est un ensemble standardisé de fichiers et d'informations que votre équipe utilise systématiquement avec Bob.

### Structure d'un Context Pack

```
context-pack/
├── README.md                    # Vue d'ensemble du projet
├── ARCHITECTURE.md              # Architecture et décisions
├── CONVENTIONS.md               # Standards de code
├── SECURITY.md                  # Guidelines de sécurité
├── examples/
│   ├── controller-example.js   # Template de controller
│   ├── service-example.js      # Template de service
│   └── test-example.js         # Template de test
└── bob-instructions.md         # Instructions spécifiques pour Bob
```

### Exemple de bob-instructions.md

```markdown
# Instructions Bob pour le Projet XYZ

## Architecture
- Nous utilisons une architecture hexagonale
- Les controllers ne doivent PAS contenir de logique métier
- Toute logique métier va dans les services

## Conventions de Code
- Utiliser async/await, jamais de callbacks
- Tous les services doivent avoir des tests unitaires
- Les noms de fonctions doivent être en camelCase
- Les constantes en UPPER_SNAKE_CASE

## Sécurité
- Toujours valider les inputs utilisateur
- Utiliser les fonctions de @src/utils/sanitize.js
- Ne JAMAIS logger de données sensibles
- Toutes les routes API doivent avoir une authentification

## Tests
- Utiliser Jest
- Coverage minimum : 80%
- Suivre le pattern AAA (Arrange, Act, Assert)
- Mocker les dépendances externes

## Quand Demander Confirmation
- Avant de modifier les fichiers de configuration
- Avant d'ajouter de nouvelles dépendances
- Avant de modifier les schémas de base de données
- Avant de changer les interfaces publiques
```

### Exercice 7 : Créer Votre Context Pack

Créez un Context Pack minimal pour votre projet :

1. **README.md** : Décrivez votre projet en 200 mots
2. **CONVENTIONS.md** : Listez 5 conventions de code importantes
3. **bob-instructions.md** : Écrivez 5 règles spécifiques pour Bob

<details>
<summary>Voir un exemple</summary>

**README.md**
```markdown
# Projet E-Commerce API

API REST pour une plateforme e-commerce.

## Stack
- Node.js 18 + Express
- PostgreSQL
- Redis pour le cache
- Jest pour les tests

## Modules Principaux
- auth: Authentification et autorisation
- products: Gestion du catalogue
- orders: Gestion des commandes
- payments: Intégration paiements

## Architecture
Architecture en couches :
- Controllers (routes)
- Services (logique métier)
- Repositories (accès données)
- Models (entités)
```

**CONVENTIONS.md**
```markdown
# Conventions de Code

1. **Async/Await** : Toujours utiliser async/await
2. **Error Handling** : Utiliser try/catch et logger les erreurs
3. **Validation** : Valider tous les inputs avec Joi
4. **Tests** : Minimum 80% de coverage
5. **Naming** : camelCase pour fonctions, PascalCase pour classes
```

**bob-instructions.md**
```markdown
# Instructions Bob

1. Toujours lire les tests existants avant de modifier du code
2. Préserver le comportement exact sauf instruction contraire
3. Demander confirmation avant d'ajouter des dépendances
4. Suivre les patterns existants dans le code
5. Créer des tests pour tout nouveau code
```

</details>

---

## 🔄 Partie 8 : Boucle Minimale de Grounding

### La Boucle en 4 Étapes

```
1. ORIENT
   ↓
   "Où suis-je ? Quel est le contexte minimal ?"
   
2. BOUND
   ↓
   "Quelles sont les contraintes ? Qu'est-ce qui ne doit PAS changer ?"
   
3. VERIFY
   ↓
   "Bob a-t-il les bonnes informations ? Dois-je corriger quelque chose ?"
   
4. ACT
   ↓
   "Maintenant, exécute avec ce contexte propre"
```

### Exemple Pratique

**Tâche :** Ajouter un cache Redis à une fonction de recherche

```
1. ORIENT
"@src/services/SearchService.js
@tests/services/SearchService.test.js

Analyse la fonction search() actuelle"

2. BOUND
"Contraintes :
- Le comportement de recherche doit rester identique
- Le cache doit expirer après 5 minutes
- Les tests existants doivent toujours passer
- Utiliser la connexion Redis existante dans @src/config/redis.js"

3. VERIFY
"Confirme que tu as compris :
- Quelle fonction modifier ?
- Où est la connexion Redis ?
- Quelle est la durée du cache ?"

4. ACT
"Parfait. Maintenant implémente le cache avec ces contraintes"
```

### Exercice 8 : Appliquer la Boucle

Pour chaque tâche, écrivez les 4 étapes de la boucle :

**Tâche A :** Ajouter une pagination à un endpoint qui retourne une liste de produits

<details>
<summary>Voir une solution</summary>

```
1. ORIENT
"@src/controllers/ProductController.js
@src/services/ProductService.js
@tests/controllers/ProductController.test.js

Analyse l'endpoint GET /products et comment il retourne 
actuellement les produits"

2. BOUND
"Contraintes :
- Ajouter les paramètres page et limit (query params)
- Valeurs par défaut : page=1, limit=20
- Maximum : limit=100
- Retourner aussi le total et le nombre de pages
- Format de réponse : { data: [], page: 1, limit: 20, total: 150, pages: 8 }
- Les tests existants doivent passer"

3. VERIFY
"Confirme :
- Quels fichiers vas-tu modifier ?
- Quel est le format de réponse attendu ?
- Quelles sont les valeurs par défaut ?"

4. ACT
"Implémente la pagination avec ces spécifications"
```

</details>

---

## ✅ Checklist de Contexte Sain

Utilisez cette checklist avant chaque session importante avec Bob :

### Avant de Commencer

- [ ] J'ai identifié les 3-5 fichiers les plus pertinents
- [ ] J'ai vérifié que ces fichiers sont à jour
- [ ] J'ai préparé mes context mentions
- [ ] J'ai défini mes contraintes clairement
- [ ] J'ai un Context Pack si c'est un projet d'équipe

### Pendant la Session

- [ ] Je mentionne uniquement les fichiers nécessaires
- [ ] Je vérifie les hypothèses de Bob
- [ ] Je corrige immédiatement les erreurs
- [ ] Je garde la conversation < 20 messages
- [ ] Je crée des checkpoints réguliers

### Signes d'Alerte

- [ ] Bob répète les mêmes erreurs → Context poisoning
- [ ] Bob ignore mes corrections → Nouveau chat nécessaire
- [ ] Bob hallucine des fonctions → Contexte trop large
- [ ] Réponses incohérentes → Contexte contradictoire
- [ ] Conversation > 30 messages → Redémarrer

### Après la Session

- [ ] J'ai documenté ce qui a bien fonctionné
- [ ] J'ai noté les problèmes de contexte rencontrés
- [ ] J'ai mis à jour le Context Pack si nécessaire
- [ ] J'ai partagé les learnings avec l'équipe

---

## 🎯 Exercice Final : Cas Pratique Complet

### Scénario

Vous travaillez sur une API de gestion de bibliothèque. Vous devez :
1. Ajouter une fonctionnalité de réservation de livres
2. Le système doit vérifier la disponibilité
3. Un utilisateur ne peut réserver que 3 livres maximum
4. Les réservations expirent après 7 jours

### Votre Mission

Écrivez une séquence complète de messages à Bob qui :
1. Utilise les bonnes context mentions
2. Applique la boucle de grounding
3. Évite le context poisoning
4. Reste dans le budget de tokens

### Structure Suggérée

```
Message 1: Orient (contexte minimal)
Message 2: Bound (contraintes)
Message 3: Verify (vérification)
Message 4: Act (exécution)
Message 5: Review (vérification du résultat)
```

<details>
<summary>Voir une solution complète</summary>

**Message 1: Orient**
```
@src/models/Book.js
@src/models/Reservation.js (si existe)
@src/services/BookService.js
@tests/services/BookService.test.js

Analyse l'architecture actuelle pour la gestion des livres.
Y a-t-il déjà un système de réservation ?
```

**Message 2: Bound**
```
Je veux ajouter un système de réservation avec ces contraintes :

RÈGLES MÉTIER :
- Un utilisateur peut réserver max 3 livres simultanément
- Les réservations expirent après 7 jours
- On ne peut réserver que des livres disponibles
- Un livre réservé n'est plus disponible pour d'autres

TECHNIQUE :
- Créer un modèle Reservation si nécessaire
- Ajouter les méthodes dans BookService
- Suivre les patterns existants du projet
- Créer les tests unitaires

SÉCURITÉ :
- Valider l'ID utilisateur
- Valider l'ID livre
- Vérifier les permissions

Propose d'abord un plan détaillé.
```

**Message 3: Verify**
```
Avant d'implémenter, confirme :

1. Quels fichiers vas-tu créer/modifier ?
2. Quelle structure de données pour Reservation ?
3. Comment vas-tu gérer l'expiration des réservations ?
4. Quels tests vas-tu créer ?

@src/config/database.js
Vérifie aussi comment sont gérées les autres entités.
```

**Message 4: Act**
```
Parfait. Implémente maintenant :

ÉTAPE 1 : Modèle Reservation
- Crée le modèle avec les champs nécessaires
- Ajoute les relations avec User et Book

ÉTAPE 2 : Service
- Méthode createReservation(userId, bookId)
- Méthode cancelReservation(reservationId)
- Méthode getUserReservations(userId)
- Méthode cleanExpiredReservations()

ÉTAPE 3 : Tests
- Tests unitaires pour chaque méthode
- Tests des règles métier
- Tests des cas d'erreur

Commence par l'étape 1.
```

**Message 5: Review**
```
@src/models/Reservation.js
@src/services/ReservationService.js
@tests/services/ReservationService.test.js

Vérifie que :
1. Toutes les contraintes sont respectées
2. Les tests couvrent tous les cas
3. Le code suit les conventions du projet
4. La gestion d'erreurs est complète

Lance les tests et montre-moi les résultats.
```

</details>

---

## 📊 Auto-Évaluation

Évaluez votre compréhension :

### Niveau 1 : Compréhension (5 points)
- [ ] Je comprends pourquoi le contexte est un budget
- [ ] Je peux expliquer la différence entre signal et noise
- [ ] Je connais les symptômes du context poisoning
- [ ] Je comprends ce que signifie "200k tokens"
- [ ] Je sais quand créer un nouveau chat

### Niveau 2 : Application (5 points)
- [ ] Je peux écrire des context mentions efficaces
- [ ] J'applique la boucle de grounding systématiquement
- [ ] Je détecte le context poisoning rapidement
- [ ] Je gère efficacement les gros repos
- [ ] J'utilise des checkpoints réguliers

### Niveau 3 : Maîtrise (5 points)
- [ ] J'ai créé un Context Pack pour mon équipe
- [ ] Je peux diagnostiquer des problèmes de contexte complexes
- [ ] J'optimise le contexte pour des tâches spécifiques
- [ ] Je forme d'autres personnes à la gestion du contexte
- [ ] Je contribue à améliorer les pratiques d'équipe

**Score :**
- 13-15 : Excellent ! Vous maîtrisez la gestion du contexte
- 10-12 : Très bien ! Continuez à pratiquer
- 7-9 : Bon début ! Refaites les exercices
- < 7 : Relisez le tutoriel et pratiquez davantage

---

## 🎓 Certification

Pour valider ce tutoriel, réalisez le projet suivant :

### Projet : Optimisation de Contexte

1. **Prenez un de vos projets réels**
2. **Analysez le contexte actuel** :
   - Combien de fichiers ?
   - Estimation de tokens ?
   - Quels sont les fichiers critiques ?
3. **Créez un Context Pack** avec :
   - README.md
   - CONVENTIONS.md
   - bob-instructions.md
   - 2-3 exemples de code
4. **Documentez** :
   - Les problèmes de contexte rencontrés
   - Les solutions appliquées
   - Les améliorations mesurées
5. **Partagez avec votre équipe**

### Critères de Validation
- ✅ Context Pack complet et utilisable
- ✅ Documentation claire des problèmes/solutions
- ✅ Démonstration d'amélioration (avant/après)
- ✅ Partage avec au moins 2 collègues

---

## 📚 Ressources Complémentaires

### Pour Aller Plus Loin
- Tutoriel 2.3 : Contrats Avant Code
- Tutoriel 3.1 : Code Review comme Evidence
- Documentation : Context Management Best Practices

### Lectures Recommandées
- "Context Windows and Token Budgets" (IBM Bob Docs)
- "Avoiding Hallucinations in LLM Applications" (OWASP)
- "Prompt Engineering for Developers" (OpenAI)

### Communauté
- Forum IBM Bob : Section "Context Management"
- Slack Channel : #bob-context-tips
- Weekly Office Hours : Jeudis 15h CET

---

## 💡 Points Clés à Retenir

1. **Le contexte est un budget** : Gérez-le comme de l'argent
2. **Signal > Noise** : Moins c'est souvent plus
3. **Context mentions précis** : Soyez spécifique
4. **Grounding systématique** : Ancrez Bob dans la réalité
5. **Détectez le poisoning tôt** : Créez un nouveau chat si nécessaire
6. **Context Pack** : Standardisez pour l'équipe
7. **Checkpoints réguliers** : Vérifiez et nettoyez
8. **200k tokens** : Connaissez votre budget

---

**Prochaine étape :** [Tutoriel 2.3 : Contrats Avant Code](tutoriel-2.3-contrats-avant-code.md)

**Besoin d'aide ?** Contactez votre formateur ou postez dans le forum.

---

*Ce tutoriel fait partie du Parcours Pédagogique IBM Bob v1.0*  
*Basé sur "Getting Started with IBM Bob" v1.2.0 par Markus Eisele*