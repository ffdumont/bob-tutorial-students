# Tutoriel 1.3 : Comment Bob Pense

**Module :** 1 - Fondamentaux  
**Durée estimée :** 45 minutes  
**Niveau :** Fondamental  
**Prérequis :** Tutoriel 1.1 et 1.2

---

## 🎯 Objectifs d'Apprentissage

À la fin de ce tutoriel, vous serez capable de :
- ✅ Comprendre le modèle mental de Bob (Intent, Evidence, Judgment)
- ✅ Expliquer pourquoi Bob sépare planification et exécution
- ✅ Comprendre l'approche "Constraints Over Creativity"
- ✅ Savoir pourquoi Bob demande avant d'agir
- ✅ Utiliser ce modèle pour mieux travailler avec Bob

---

## 📚 Le Modèle Mental de Bob

### Bob Traite le Repo comme un Système

> **Citation du document source :**  
> "A lot of AI tooling treats the repo as text: patterns in, diff out.  
> Bob treats it as a system with intent."

La différence fondamentale :

```
AUTRES OUTILS :
Repo = Texte → Patterns → Diff
❌ Pas de compréhension du "pourquoi"
❌ Pas de contexte système
❌ Génération basée sur des patterns génériques

BOB :
Repo = Système avec Intent → Compréhension → Plan → Changement
✅ Comprend le "pourquoi"
✅ Analyse le système complet
✅ Suggestions basées sur VOTRE codebase
```

### Ce que Cela Change

Quand vous demandez de l'aide à Bob :
1. **Il ne saute pas directement au code**
2. **Il clarifie ce que vous voulez** (Intent)
3. **Il lit ce qui existe déjà** (Evidence)
4. **Il pense à ce qui pourrait casser** (Risks)
5. **Seulement après, il propose une solution**

Cela coûte plus de temps au début, mais **vous économise plus tard**.

---

## 🧩 Les Trois Piliers : Intent, Evidence, Judgment

### Vue d'Ensemble

```
┌─────────────────────────────────────────┐
│                                         │
│  INTENT          EVIDENCE      JUDGMENT │
│  (Vous)          (Bob lit)     (Vous)   │
│                                         │
│  Que veux-tu  →  Que dit le  →  Que     │
│  accomplir ?     code réel ?    faire ? │
│                                         │
└─────────────────────────────────────────┘
```

> **Citation du document source :**  
> "Intent, evidence, and judgment stay separate on purpose.  
> Mixing them is how you get confident code that solves the wrong problem."

---

### Pilier 1 : Intent (L'Intention) 🎯

**Définition :** Ce que vous essayez d'accomplir. Le problème que vous résolvez.

#### Pourquoi c'est Important

Bob commence toujours par **ce que vous voulez accomplir**, pas par quel fichier toucher.

Cela force la clarté :
- ❌ "Fix the service" → Trop vague
- ❌ "Improve performance" → Pas mesurable
- ✅ "Reduce search response time from 250ms to < 100ms" → Spécifique et vérifiable

#### Caractéristiques d'un Bon Intent

```
BON INTENT :
✅ Spécifique : "Ajouter validation email au champ username"
✅ Mesurable : "Réduire le temps de réponse de 250ms à < 100ms"
✅ Vérifiable : "Tous les tests doivent passer"
✅ Borné : "Uniquement le module d'authentification"

MAUVAIS INTENT :
❌ Vague : "Améliorer le code"
❌ Non mesurable : "Rendre ça plus rapide"
❌ Non vérifiable : "Faire quelque chose de bien"
❌ Illimité : "Refactorer tout le projet"
```

#### Exemple Pratique

**Mauvais Intent :**
```
"Bob, améliore l'authentification"
```

**Bon Intent :**
```
"Bob, ajoute une validation de force de mot de passe 
au processus d'inscription :

OBJECTIF :
- Minimum 8 caractères
- Au moins 1 majuscule, 1 minuscule, 1 chiffre
- Rejeter les mots de passe trop communs

SUCCÈS :
- Les tests existants passent
- Nouveaux tests pour chaque règle
- Message d'erreur clair pour l'utilisateur"
```

---

### Pilier 2 : Evidence (Les Preuves) 📊

**Définition :** L'état actuel du système. Le code réel. Les tests réels. La configuration réelle.

#### Pourquoi c'est Important

> **Citation du document source :**  
> "Bob does not guess what your repo looks like—it reads it."

Bob ne devine pas, il **lit** :
- Les fichiers de code
- Les dépendances
- Les tests
- La configuration
- Le comportement actuel

C'est plus lent que le pattern-matching, mais **les recommandations restent liées à VOTRE système**.

#### Ce que Bob Cherche comme Evidence

```
EVIDENCE TECHNIQUE :
├── Code existant
│   ├── Patterns utilisés
│   ├── Conventions de nommage
│   ├── Architecture
│   └── Dépendances
├── Tests
│   ├── Couverture
│   ├── Style de tests
│   └── Comportement attendu
├── Configuration
│   ├── Environnements
│   ├── Paramètres
│   └── Secrets/Credentials
└── Documentation
    ├── README
    ├── API docs
    └── ADRs
```

#### Exemple Pratique

**Sans Evidence (Mauvais) :**
```
Vous : "Ajoute un cache"

Bob (sans lire) : "J'ai ajouté Memcached"

Problème : Votre projet utilise déjà Redis !
```

**Avec Evidence (Bon) :**
```
Vous : "Ajoute un cache"

Bob (après lecture) : 
"J'ai analysé votre projet :
- Vous utilisez déjà Redis pour les sessions
- Vous avez une connexion Redis configurée
- Les autres services utilisent @Cacheable

Je propose d'utiliser Redis avec @Cacheable 
pour rester cohérent avec votre architecture."
```

---

### Pilier 3 : Judgment (Le Jugement) ⚖️

**Définition :** La décision finale. Quel option choisir. Quel trade-off accepter.

#### Pourquoi c'est Important

> **Citation du document source :**  
> "Judgment is the decision: which option, which trade-off, what you accept if something goes sideways. That call stays with you."

**Bob ne décide PAS à votre place.**

Bob peut :
- ✅ Lister les findings
- ✅ Expliquer les risques
- ✅ Esquisser les options
- ✅ Recommander une approche

Bob ne peut PAS :
- ❌ Décider ce qui est acceptable pour votre équipe
- ❌ Choisir entre sécurité et rapidité
- ❌ Arbitrer les trade-offs business
- ❌ Prendre la responsabilité finale

#### Le Jugement Reste Humain

```
┌─────────────────────────────────────────┐
│         RESPONSABILITÉS                 │
├─────────────────────────────────────────┤
│                                         │
│  BOB                    VOUS            │
│  ────                   ────            │
│  Analyser               Décider         │
│  Proposer               Approuver       │
│  Expliquer              Assumer         │
│  Exécuter               Vérifier        │
│  Rapporter              Shipper         │
│                                         │
└─────────────────────────────────────────┘
```

#### Exemple Pratique

**Scénario :** Bob trouve deux approches pour améliorer les performances

```
Bob : "J'ai identifié deux approches :

OPTION A : Ajouter un index sur la colonne 'email'
  Avantages :
  - Simple à implémenter
  - Amélioration immédiate : 250ms → 50ms
  - Pas de changement de code
  
  Inconvénients :
  - Ralentit les insertions de ~10%
  - Augmente la taille de la DB de ~15%
  
OPTION B : Implémenter un cache Redis
  Avantages :
  - Très rapide : 250ms → 10ms
  - Pas d'impact sur la DB
  - Scalable
  
  Inconvénients :
  - Plus complexe à implémenter
  - Nécessite infrastructure Redis
  - Problèmes de cache invalidation
  
RECOMMANDATION : Option A pour commencer, 
                 Option B si le trafic augmente

Quelle option préférez-vous ?"

VOUS : [Vous décidez en fonction de votre contexte]
```

---

## 🔀 Pourquoi Bob Sépare Planification et Exécution

### Les Deux Phases

```
PHASE 1 : PLANIFICATION
├── Comprendre l'intent
├── Examiner l'evidence
├── Identifier ce qui doit changer
├── Expliquer les risques
├── Suggérer des approches
└── Demander approbation
    ↓
    [CHECKPOINT HUMAIN]
    ↓
PHASE 2 : EXÉCUTION
├── Faire les changements approuvés
├── Suivre le plan exactement
├── Rapporter ce qui a été fait
├── Signaler les problèmes
└── Demander vérification
```

### Pourquoi Cette Séparation ?

> **Citation du document source :**  
> "The split is deliberate: you get a reviewable plan before anything lands in the repo."

#### Avantages de la Séparation

**1. Vous Pouvez Reviewer Avant**
```
Sans séparation :
Code généré → "Oups, ce n'est pas ce que je voulais"
❌ Temps perdu
❌ Code à jeter
❌ Frustration

Avec séparation :
Plan → Review → "Ajuste ça" → Nouveau plan → Approuve → Exécution
✅ Pas de temps perdu
✅ Résultat correct du premier coup
✅ Confiance
```

**2. Vous Gardez le Contrôle**
```
Planification = Vous décidez QUOI faire
Exécution = Bob fait COMMENT le faire
```

**3. Moins de Surprises**
```
Surprises pendant la planification = Bon (vous pouvez ajuster)
Surprises pendant l'exécution = Mauvais (déjà trop tard)
```

### Ce qui se Passe dans Chaque Phase

#### Phase de Planification

**Bob NE fait PAS :**
- ❌ Éditer des fichiers
- ❌ Générer du code
- ❌ Prendre des décisions
- ❌ Verrouiller des choix

**Bob FAIT :**
- ✅ Comprendre votre intent
- ✅ Lire le code existant
- ✅ Identifier les changements nécessaires
- ✅ Expliquer les risques
- ✅ Proposer des approches
- ✅ Attendre votre approbation

#### Phase d'Exécution

**Bob FAIT :**
- ✅ Suivre le plan approuvé
- ✅ Modifier les fichiers
- ✅ Exécuter les tests
- ✅ Rapporter les résultats
- ✅ Signaler les problèmes

**L'exécution devrait être :**
- 🥱 **Ennuyeuse** (c'est bon signe !)
- ⚡ **Rapide**
- 🎯 **Prévisible**
- 📝 **Traçable**

> **Citation du document source :**  
> "If execution feels exciting, something went wrong—usually upstream of the merge."

---

## 🎨 Constraints Over Creativity (Contraintes > Créativité)

### Le Principe

> **Citation du document source :**  
> "Bob is not there to invent clever one-offs. It stays inside your patterns, tests, and policies."

Bob n'est pas là pour être créatif. Il est là pour être **cohérent**.

### Qu'est-ce que les Contraintes ?

Les contraintes sont les règles qui font fonctionner votre système :

```
CONTRAINTES :
├── Standards de code
│   ├── Style de nommage
│   ├── Formatage
│   └── Conventions
├── Patterns architecturaux
│   ├── Layering
│   ├── Dependency injection
│   └── Error handling
├── Exigences de tests
│   ├── Coverage minimum
│   ├── Style de tests
│   └── Mocking strategy
├── Politiques de sécurité
│   ├── Authentication
│   ├── Authorization
│   └── Data protection
└── Conventions d'équipe
    ├── PR process
    ├── Review guidelines
    └── Documentation standards
```

### D'où Viennent les Contraintes ?

Bob infère les contraintes de :
1. **Ce que vous avez déjà shippé** (le code existant)
2. **Les règles que vous lui donnez** (custom instructions)
3. **Les patterns du projet** (architecture, tests, style)

### Pourquoi les Contraintes Sont Importantes

```
CRÉATIVITÉ dans le code applicatif = PROBLÈME
├── Surprises pour le lecteur
├── Attentes brisées
├── Maintenance difficile
└── Incohérence

COHÉRENCE dans le code applicatif = BIEN
├── Prévisible
├── Facile à reviewer
├── Facile à maintenir
└── Facile à remplacer
```

> **Citation du document source :**  
> "Predictable output is easier to review and easier to rip out later. Boring is good."

### Exemple Pratique

**Votre Projet Utilise :**
```java
// Pattern existant : Constructor injection
@Service
public class UserService {
    private final UserRepository repository;
    
    public UserService(UserRepository repository) {
        this.repository = repository;
    }
}
```

**Bob Suggère (Cohérent) :**
```java
// Bob suit le même pattern
@Service
public class OrderService {
    private final OrderRepository repository;
    
    public OrderService(OrderRepository repository) {
        this.repository = repository;
    }
}
```

**Bob NE Suggère PAS (Incohérent) :**
```java
// Créatif mais incohérent avec le projet
@Service
public class OrderService {
    @Autowired
    private OrderRepository repository; // Field injection
}
```

### Quand les Contraintes Entrent en Conflit

Parfois, les contraintes se contredisent :
- La bonne solution casse un pattern local
- L'exception vaut la peine d'être documentée

> **Citation du document source :**  
> "Bob does not pick the winner. It flags the tension."

**Exemple :**
```
Bob : "J'ai détecté un conflit :

PROBLÈME : Pour résoudre ce bug, je dois soit :
  A) Casser le pattern de validation existant
  B) Laisser le bug (pas acceptable)

RECOMMANDATION : Option A avec documentation

JUSTIFICATION :
- Le pattern actuel ne supporte pas ce cas d'usage
- C'est une limitation connue du pattern
- L'exception est justifiée et documentée

Voulez-vous que je procède avec l'option A ?"
```

**Vous décidez** si :
- Le pattern doit plier
- L'exception est justifiée
- Ce qui compte le plus pour cette release

---

## ❓ Pourquoi Bob Demande Avant d'Agir

### Le Checkpoint Obligatoire

> **Citation du document source :**  
> "Bob does not edit the repo without a checkpoint."

Chaque changement nécessite une approbation explicite.

### Pourquoi C'est Important

#### 1. Demander Force la Clarté

```
Pour obtenir l'approbation, Bob doit :
├── Dire ce qui va se passer
├── Expliquer quels fichiers seront modifiés
├── Justifier pourquoi cette approche
└── Expliquer pourquoi c'est mieux que les alternatives

Si l'explication est floue → Signal d'alarme !
```

#### 2. Demander Crée la Responsabilité

```
Quand vous approuvez :
├── Vous possédez l'outcome
├── Le plan était à vous d'accepter
├── Les risques étaient à vous de peser
└── La responsabilité reste humaine
```

> **Citation du document source :**  
> "When you approve, you own the outcome."

#### 3. Demander Permet l'Apprentissage

```
Chaque round d'approbation vous montre :
├── Comment Bob priorise
├── Ce qu'il considère comme risque
├── Ce qu'il traite comme evidence
└── Où il vous demande de choisir

Résultat : Intent plus précis, meilleure compréhension
```

### Quand Demander Devient Automatique

Au début, les interruptions semblent être de la friction.

Après plusieurs répétitions, elles deviennent une **habitude** :
- Une review forcée avant la partie irréversible
- Un moment de réflexion avant l'action
- Un checkpoint de sécurité

> **Citation du document source :**  
> "That is often where Bob earns its keep: less as a typist, more as a thinking partner for what should be typed at all."

---

## 💡 Exercice 1 : Identifier Intent, Evidence, Judgment

Pour chaque situation, identifiez si c'est Intent, Evidence, ou Judgment :

1. "Je veux réduire le temps de réponse de l'API de 250ms à < 100ms"
2. "Le code actuel utilise des requêtes N+1 dans la boucle"
3. "Nous allons implémenter l'option A car elle est plus simple"
4. "Tous les services existants utilisent Redis pour le cache"
5. "L'objectif est d'améliorer l'expérience utilisateur"
6. "Je choisis d'accepter le risque de cache stale pour gagner en performance"

<details>
<summary>Voir les réponses</summary>

1. **Intent** 🎯 - Objectif clair et mesurable
2. **Evidence** 📊 - Observation du code existant
3. **Judgment** ⚖️ - Décision sur quelle option choisir
4. **Evidence** 📊 - Fait observé dans le projet
5. **Intent** 🎯 - But à atteindre (mais pourrait être plus spécifique)
6. **Judgment** ⚖️ - Décision sur un trade-off

</details>

---

## 🎯 Exercice 2 : Améliorer l'Intent

Pour chaque intent vague, proposez une version améliorée :

**Intent 1 (Vague) :**
```
"Améliore les performances"
```

**Intent 2 (Vague) :**
```
"Rends le code plus propre"
```

**Intent 3 (Vague) :**
```
"Ajoute de la sécurité"
```

<details>
<summary>Voir des solutions possibles</summary>

**Intent 1 (Amélioré) :**
```
"Réduis le temps de réponse de l'endpoint GET /products 
de 250ms à < 100ms en optimisant les requêtes database.

SUCCÈS :
- Temps de réponse < 100ms (95e percentile)
- Tous les tests passent
- Pas de changement d'API
- Comportement préservé"
```

**Intent 2 (Amélioré) :**
```
"Refactore la classe UserService pour améliorer la lisibilité :
- Extraire les méthodes de validation dans une classe dédiée
- Réduire la complexité cyclomatique de > 15 à < 10
- Ajouter des commentaires pour la logique métier complexe

SUCCÈS :
- Tous les tests existants passent sans modification
- Couverture de code maintenue à 85%+
- Code review approuvée par 2 seniors"
```

**Intent 3 (Amélioré) :**
```
"Ajoute une validation d'authentification JWT à tous les 
endpoints de l'API sauf /health et /login.

SÉCURITÉ :
- Vérifier la signature JWT
- Vérifier l'expiration
- Extraire les claims utilisateur
- Retourner 401 si invalide

SUCCÈS :
- Tous les endpoints protégés nécessitent un token valide
- Tests de sécurité passent
- Documentation API mise à jour"
```

</details>

---

## 🔄 Exercice 3 : Planification vs Exécution

Pour chaque action, déterminez si elle appartient à la Planification ou à l'Exécution :

1. Bob lit les fichiers du projet
2. Bob modifie UserService.java
3. Bob explique les risques potentiels
4. Bob exécute les tests
5. Bob propose trois approches différentes
6. Bob crée un commit
7. Bob demande votre approbation
8. Bob rapporte que tous les tests passent

<details>
<summary>Voir les réponses</summary>

**PLANIFICATION :**
- 1. Bob lit les fichiers du projet
- 3. Bob explique les risques potentiels
- 5. Bob propose trois approches différentes
- 7. Bob demande votre approbation

**EXÉCUTION :**
- 2. Bob modifie UserService.java
- 4. Bob exécute les tests
- 6. Bob crée un commit
- 8. Bob rapporte que tous les tests passent

</details>

---

## 📊 Auto-Évaluation

### Questions

1. **Quels sont les trois piliers du modèle mental de Bob ?**
   - [ ] Code, Tests, Documentation
   - [ ] Intent, Evidence, Judgment
   - [ ] Plan, Act, Verify
   - [ ] Read, Write, Execute

2. **Qui prend la décision finale (Judgment) ?**
   - [ ] Bob décide automatiquement
   - [ ] L'IA choisit la meilleure option
   - [ ] L'humain décide toujours
   - [ ] Ça dépend de la complexité

3. **Pourquoi Bob sépare-t-il planification et exécution ?**
   - [ ] Pour ralentir le processus
   - [ ] Pour obtenir un plan reviewable avant les changements
   - [ ] Parce que l'IA ne peut pas faire les deux
   - [ ] Pour créer plus de documentation

4. **Que signifie "Constraints Over Creativity" ?**
   - [ ] Bob ne peut pas être créatif
   - [ ] Bob préfère la cohérence à la nouveauté
   - [ ] Bob suit toujours les mêmes patterns
   - [ ] Bob ne peut pas innover

5. **Pourquoi Bob demande-t-il avant d'agir ?**
   - [ ] Pour être poli
   - [ ] Parce que c'est obligatoire légalement
   - [ ] Pour forcer la clarté et créer la responsabilité
   - [ ] Pour ralentir le développement

<details>
<summary>Voir les réponses</summary>

1. **✅ Intent, Evidence, Judgment** - Les trois piliers fondamentaux
2. **✅ L'humain décide toujours** - Le jugement reste humain
3. **✅ Pour obtenir un plan reviewable avant les changements** - Évite les surprises
4. **✅ Bob préfère la cohérence à la nouveauté** - Boring is good
5. **✅ Pour forcer la clarté et créer la responsabilité** - Checkpoint de sécurité

**Score :**
- 5/5 : Excellent ! Vous comprenez le modèle mental de Bob
- 3-4/5 : Bien ! Relisez les sections où vous avez hésité
- 0-2/5 : Relisez le tutoriel attentivement

</details>

---

## 🎯 Exercice Final : Appliquer le Modèle Mental

### Scénario

Vous voulez améliorer la sécurité de votre API en ajoutant une authentification à deux facteurs (2FA).

### Mission

Appliquez le modèle mental de Bob pour structurer cette tâche :

```
INTENT (Ce que vous voulez accomplir) :
[Écrivez un intent clair et spécifique]

EVIDENCE (Ce que Bob devrait lire) :
[Listez les fichiers/informations à analyser]

JUDGMENT (Les décisions que VOUS devrez prendre) :
[Listez les choix que vous devrez faire]

PLANIFICATION (Ce que Bob devrait proposer) :
[Ce que vous attendez dans le plan]

EXÉCUTION (Ce que Bob devrait faire) :
[Les actions concrètes]

CONTRAINTES (Ce qui doit rester cohérent) :
[Les patterns/conventions à respecter]
```

<details>
<summary>Voir une solution possible</summary>

```
INTENT :
"Implémenter l'authentification à deux facteurs (2FA) 
pour tous les comptes utilisateurs.

OBJECTIFS :
- Support TOTP (Time-based One-Time Password)
- QR code pour configuration
- Codes de backup
- Option d'activation/désactivation par utilisateur

SUCCÈS :
- Les utilisateurs peuvent activer 2FA
- Login nécessite le code TOTP si 2FA activé
- Tests couvrent tous les scénarios
- Documentation utilisateur créée"

EVIDENCE (Ce que Bob devrait lire) :
- AuthenticationService.java (système auth actuel)
- UserModel.java (structure utilisateur)
- LoginController.java (flow de login)
- Tests d'authentification existants
- Configuration de sécurité
- Dépendances du projet (pom.xml/package.json)
- Patterns de gestion des secrets

JUDGMENT (Décisions à prendre) :
- Quelle bibliothèque 2FA utiliser ?
- Stocker les secrets 2FA où ? (DB, vault, etc.)
- Rendre 2FA obligatoire ou optionnel ?
- Combien de codes de backup générer ?
- Durée de validité des codes ?
- Que faire si l'utilisateur perd son device ?
- Impact sur les API clients existants ?

PLANIFICATION (Ce que Bob devrait proposer) :
1. Analyse de l'architecture auth actuelle
2. Recommandation de bibliothèque 2FA
3. Modifications nécessaires au modèle User
4. Changements au flow de login
5. Nouveaux endpoints (setup, verify, disable)
6. Stratégie de stockage des secrets
7. Plan de tests
8. Plan de migration pour utilisateurs existants
9. Risques identifiés
10. Alternatives considérées

EXÉCUTION (Ce que Bob devrait faire) :
- Ajouter dépendance 2FA
- Modifier UserModel (champs 2FA)
- Créer TwoFactorService
- Modifier LoginController
- Créer TwoFactorController (setup, verify)
- Ajouter validation 2FA au login
- Créer tests unitaires (20+)
- Créer tests d'intégration
- Mettre à jour documentation API
- Créer guide utilisateur

CONTRAINTES (À respecter) :
- Suivre le pattern de service existant
- Utiliser le même style de tests
- Respecter les conventions de nommage
- Pas de breaking change pour l'API
- Backward compatible (2FA optionnel d'abord)
- Suivre les standards de sécurité du projet
- Chiffrer les secrets 2FA
- Logger les événements de sécurité
```

</details>

---

## 📚 Ce que Vous Avez Appris

Dans ce tutoriel, vous avez découvert :

✅ **Le modèle mental de Bob** : Intent, Evidence, Judgment

✅ **Pourquoi séparer planification et exécution** : Review avant action

✅ **Constraints Over Creativity** : Cohérence > Nouveauté

✅ **Pourquoi Bob demande** : Clarté, responsabilité, apprentissage

✅ **Comment utiliser ce modèle** : Pour mieux travailler avec Bob

---

## 🚀 Prochaines Étapes

Maintenant que vous comprenez comment Bob pense :

1. **Tutoriel 1.4** : La Transition des Habitudes
2. **Tutoriel 2.1** : L'Interface Bob dans l'IDE
3. **Tutoriel 2.2** : Gestion du Contexte (CRITIQUE !)
4. **Tutoriel 2.3** : Contrats Avant Code

---

## 💡 Points Clés à Retenir

1. **Intent, Evidence, Judgment** : Les trois piliers séparés
2. **Bob lit, ne devine pas** : Evidence du code réel
3. **Vous décidez toujours** : Le jugement reste humain
4. **Plan avant Act** : Review avant changement
5. **Boring is good** : Cohérence > Créativité
6. **Bob demande** : Checkpoint de sécurité

---

**Prochaine étape :** [Tutoriel 1.4 : La Transition des Habitudes](tutoriel-1.4-transition-habitudes.md)

**Besoin d'aide ?** Consultez le [README.md](README.md) ou contactez votre formateur

---

*Ce tutoriel fait partie du Parcours Pédagogique IBM Bob v1.0*  
*Basé sur "Getting Started with IBM Bob" v1.2.0 par Markus Eisele*