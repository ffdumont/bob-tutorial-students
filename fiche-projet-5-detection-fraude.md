---
layout: default
title: Fiche Projet - Détection de Fraude
---

# Fiche Projet : Détection de Fraude Bancaire
## Guide d'Utilisation de Bob pour Votre Projet

**Équipe :** DEBBAGH, JABRY, GUEDIRI  
**Domaine :** Sécurité financière - Deep Learning  
**Technologies :** DL pour classification, Dataset déséquilibré, Streamlit

---

## 🎯 Vue d'Ensemble du Projet

### Objectif
Détecter efficacement des transactions frauduleuses dans un dataset massivement déséquilibré (0.17% de fraudes), en temps réel, tout en minimisant les faux positifs.

### Composants Principaux
1. **Modèle DL** : Classification binaire (fraude/non-fraude) sur dataset déséquilibré
2. **Gestion du déséquilibre** : Techniques de sampling, poids de classe, métriques adaptées
3. **Interface Streamlit** : Test en temps réel avec explications (SHAP/LIME)
4. **Optimisation temps réel** : Inférence rapide pour production

### Vos Attentes vis-à-vis de Bob
- Structuration et simplification du développement
- Organisation du travail
- Automatisation (entraînement, tests)
- Facilitation de la mise en valeur de la solution

---

## 📚 Parcours Pédagogique Adapté à Votre Projet

### Module 1 : Fondamentaux (2-3h)

#### 📖 Tutoriel 1.1 : Introduction à IBM Bob

**Questions spécifiques à votre projet :**

❓ **Quels sont les 3 cas d'usage Bob les plus pertinents pour mon projet de détection de fraude ?**
- Gestion du dataset déséquilibré (techniques de sampling, métriques)
- Optimisation du modèle pour le temps réel
- Création de l'interface Streamlit avec explications

❓ **Où Bob peut-il m'aider le plus dans un projet de détection de fraude ?**
- Implémentation des techniques de gestion du déséquilibre
- Choix et calcul des métriques appropriées (F1, AUC-ROC, pas accuracy)
- Intégration de l'explicabilité (SHAP, LIME)
- Optimisation pour l'inférence temps réel

❓ **Où le jugement humain est-il critique dans mon projet ?**
- Définition du seuil de décision (trade-off faux positifs/négatifs)
- Interprétation des explications du modèle
- Validation que les features utilisées sont éthiques
- Décision sur les cas limites (confiance faible)

**💡 Prompt Bob suggéré :**
```
Je travaille sur un projet de détection de fraude bancaire avec :
- Dataset massivement déséquilibré (0.17% de fraudes)
- Besoin de temps réel (inférence rapide)
- Interface Streamlit pour test et explications
- Métriques adaptées (F1-score, AUC-ROC, précision/rappel)

Aide-moi à structurer le projet avec :
- Gestion appropriée du déséquilibre
- Modèle optimisé pour le temps réel
- Intégration de l'explicabilité (SHAP)
```

---

#### 📖 Tutoriel 1.2 : Le Cycle de Vie Agentique

**Application à votre projet :**

**Phase ORIENT** - Comprendre avant de coder
- ❓ Quelle est la nature du déséquilibre (0.17% de fraudes) ?
- ❓ Quelles features sont disponibles et lesquelles sont éthiques à utiliser ?
- ❓ Quel est le coût d'un faux positif vs faux négatif ?

**💡 Utilisez Bob pour :**
```
Analyse le dataset de fraude bancaire et identifie :
1. La distribution des classes (déséquilibre exact)
2. Les features disponibles et leur importance potentielle
3. Les corrélations entre features
4. Les techniques de gestion du déséquilibre appropriées
```

**Phase BOUND** - Définir les contraintes
- ❓ Contrainte métier : minimiser les faux négatifs (fraudes non détectées)
- ❓ Contrainte utilisateur : limiter les faux positifs (clients bloqués à tort)
- ❓ Contrainte temps réel : inférence < 100ms
- ❓ Contrainte éthique : pas de biais démographiques

**Phase PLAN** - Planifier avant d'exécuter
- ❓ Ordre de développement : Baseline → Gestion déséquilibre → Optimisation → Interface ?
- ❓ Quelles techniques de sampling tester (SMOTE, undersampling, hybrid) ?
- ❓ Quelles métriques suivre (F1, AUC-ROC, précision, rappel) ?

**💡 Prompt Bob suggéré :**
```
Crée un plan de développement pour la détection de fraude :
1. Ordre de développement (baseline, sampling, modèle, interface)
2. Techniques de gestion du déséquilibre à tester
3. Métriques à suivre (pas accuracy !)
4. Stratégie de validation (cross-validation stratifiée)

Contrainte critique : dataset 0.17% de fraudes
```

---

#### 📖 Tutoriel 1.3 : Comment Bob Pense

**Intent, Evidence, Judgment pour votre projet :**

**INTENT** - Ce que vous voulez accomplir
- ❓ Mon intent est-il clair ? "Détecter les fraudes" vs "Créer un système de détection de fraudes avec F1-score > 0.85, minimisant les faux négatifs tout en gardant les faux positifs < 5%"
- ❓ Ai-je défini les critères de succès ? (F1-score, AUC-ROC, précision, rappel)

**EVIDENCE** - Les faits que Bob collecte
- ❓ Quels fichiers Bob doit-il lire pour comprendre mon dataset ?
- ❓ Ai-je fourni des statistiques sur le déséquilibre ?
- ❓ Bob comprend-il les contraintes métier (coût des erreurs) ?

**JUDGMENT** - Votre décision finale
- ❓ Est-ce que je comprends pourquoi Bob suggère SMOTE plutôt qu'undersampling ?
- ❓ Le seuil de décision proposé est-il approprié pour mon cas d'usage ?
- ❓ Les features utilisées sont-elles éthiques ?

**💡 Exercice pratique :**
```
Demande à Bob d'analyser ton approche de gestion du déséquilibre 
et de suggérer des améliorations.

Avant d'accepter, vérifie :
- La technique préserve-t-elle les patterns de fraude ?
- Les métriques sont-elles appropriées (pas accuracy) ?
- Le modèle est-il robuste face au déséquilibre ?
- Comprends-tu l'impact de chaque technique ?
```

---

#### 📖 Tutoriel 1.4 : La Transition des Habitudes

**Habitudes à changer pour votre projet :**

**Avant (habitudes traditionnelles) :**
- Utiliser accuracy comme métrique principale
- Entraîner directement sans gérer le déséquilibre
- Tester manuellement différents seuils de décision

**Après (habitudes agentiques) :**
- Définir des métriques appropriées (F1, AUC-ROC)
- Laisser Bob générer et comparer différentes techniques de sampling
- Automatiser l'optimisation du seuil de décision

**💡 Plan de transition pour votre équipe :**

**Semaine 1-2 : Exploration et Baseline**
- Utilisez Bob pour analyser le dataset
- Créez une baseline simple
- Définissez les métriques appropriées

**Semaine 3-4 : Gestion du Déséquilibre**
- Bob implémente SMOTE, undersampling, hybrid
- Vous comparez les approches
- Bob aide à choisir la meilleure

**Semaine 5-6 : Modèle et Optimisation**
- Bob crée le modèle DL
- Vous optimisez les hyperparamètres
- Bob optimise pour le temps réel

**Semaine 7-8 : Explicabilité**
- Bob intègre SHAP/LIME
- Vous validez les explications
- Bob crée les visualisations

**Semaine 9-10 : Interface et Finalisation**
- Bob génère l'interface Streamlit
- Vous testez avec des cas réels
- Documentation finale

---

### Module 2 : Prise en Main (3-4h)

#### 📖 Tutoriel 2.1 : L'Interface Bob

**Configuration pour votre projet :**

**Context Mentions essentiels :**
```
@data/creditcard.csv           # Dataset (ou chemin)
@models/fraud_detector.py      # Modèle de détection
@utils/sampling.py             # Techniques de sampling
@utils/metrics.py              # Métriques personnalisées
@config/model_config.yaml      # Configuration
@app/streamlit_app.py          # Interface
```

**💡 Première tâche avec Bob :**
```
@data/creditcard.csv @config/model_config.yaml

Analyse le dataset de fraude bancaire et crée un rapport qui inclut :
1. Statistiques de déséquilibre (% de fraudes)
2. Distribution des features
3. Corrélations entre features
4. Features les plus discriminantes (analyse préliminaire)
5. Recommandations pour la gestion du déséquilibre

Contrainte : dataset avec 284,807 transactions, 492 fraudes (0.17%)
```

---

#### 📖 Tutoriel 2.2 : Gestion du Contexte ⭐ CRITIQUE

**Contexte spécifique à votre projet de fraude :**

**Signal (à inclure) :**
- ✅ Modèle de détection (models/fraud_detector.py)
- ✅ Techniques de sampling (utils/sampling.py)
- ✅ Métriques personnalisées (utils/metrics.py)
- ✅ Configuration (config/)
- ✅ Scripts d'explicabilité (utils/explainability.py)
- ✅ Interface Streamlit (app/)

**Noise (à exclure) :**
- ❌ Dataset complet (trop volumineux)
- ❌ Checkpoints de modèles entraînés
- ❌ Logs d'entraînement détaillés
- ❌ Résultats d'expériences passées
- ❌ Visualisations générées

**💡 Context Pack pour votre projet :**

Créez un fichier `.bobcontext` :
```yaml
# Context Pack - Projet Détection de Fraude
include:
  - models/**/*.py
  - utils/**/*.py
  - config/*.yaml
  - app/*.py
  - tests/*.py
  - README.md
  
exclude:
  - data/creditcard.csv
  - models/checkpoints/**
  - logs/**
  - results/**
  - visualizations/**
  
priority_files:
  - models/fraud_detector.py
  - utils/sampling.py
  - utils/metrics.py
  - config/model_config.yaml
```

**❓ Questions de grounding :**
- Avant chaque tâche : "Bob, as-tu lu ma configuration de déséquilibre ?"
- Après modification : "Bob, confirme que les métriques sont appropriées"
- En cas de doute : "Bob, montre-moi l'impact sur les faux positifs/négatifs"

**💡 Gestion du contexte pour dataset déséquilibré :**
```
Pour les modifications liées au déséquilibre, toujours inclure :
@models/fraud_detector.py @utils/sampling.py @utils/metrics.py

Bob, analyse l'approche de gestion du déséquilibre et identifie 
les améliorations possibles pour maximiser le F1-score.
```

---

#### 📖 Tutoriel 2.3 : Contrats Avant Code

**Contrat type pour votre projet :**

**Exemple : Modèle de Détection avec Gestion du Déséquilibre**

```markdown
## Contrat : Détecteur de Fraude Bancaire

### Intent
Créer un modèle de détection de fraude qui gère efficacement 
le déséquilibre extrême (0.17% de fraudes) et optimise le F1-score.

### Success Criteria
- F1-score > 0.85 sur test set
- AUC-ROC > 0.95
- Rappel (recall) > 0.90 (détecter 90% des fraudes)
- Précision > 0.80 (limiter les faux positifs)
- Inférence < 100ms

### Non-Goals
- Ne pas optimiser pour accuracy (métrique trompeuse)
- Ne pas utiliser de features démographiques (éthique)
- Ne pas viser 100% de rappel (trop de faux positifs)

### Preserved Behavior
- Format de sortie : probabilité + décision binaire
- Compatible avec Streamlit
- Logging des métriques détaillées

### Verification
- Tests sur test set stratifié
- Validation croisée stratifiée (5-fold)
- Analyse des faux positifs et faux négatifs
- Test de robustesse (différents seuils)
- Benchmark temps d'inférence

### Stop Conditions
- Si rappel < 0.85 → revoir la technique de sampling
- Si trop de faux positifs (précision < 0.75) → ajuster le seuil
- Si inférence > 150ms → optimiser le modèle
```

**💡 Utilisez ce contrat avec Bob :**
```
@models/fraud_detector.py @utils/sampling.py

Implémente le détecteur de fraude selon le contrat ci-dessus.
Commence par me proposer plusieurs approches de gestion du déséquilibre 
avec leurs avantages/inconvénients.
```

---

#### 📖 Tutoriel 2.4 : Votre Première Tâche Accountable

**Tâche guidée : Créer le système de gestion du déséquilibre**

**Étape 1 : Intent clair**
```
Je veux créer un système de gestion du déséquilibre qui :
1. Implémente 3 techniques : SMOTE, undersampling, hybrid
2. Compare leurs performances (F1-score, AUC-ROC, précision, rappel)
3. Permet de choisir la meilleure approche
4. Est facilement configurable

Contraintes critiques :
- Dataset : 284,807 transactions, 492 fraudes (0.17%)
- Métriques : F1-score, AUC-ROC, précision, rappel (pas accuracy)
- Validation : cross-validation stratifiée
```

**Étape 2 : Laisser Bob explorer**
```
@data/creditcard.csv @config/model_config.yaml

Bob, explore d'abord le dataset et ma configuration.
Dis-moi ce que tu comprends du déséquilibre avant de proposer des techniques.
```

**Étape 3 : Lire le plan**
- ❓ Bob a-t-il compris l'ampleur du déséquilibre (0.17%) ?
- ❓ Les techniques proposées sont-elles appropriées ?
- ❓ Les métriques de comparaison sont-elles pertinentes ?
- ❓ La validation croisée est-elle stratifiée ?

**Étape 4 : Exécution et vérification**
```
Après implémentation, vérifie :
- Les 3 techniques sont implémentées correctement
- La comparaison utilise les bonnes métriques
- La validation croisée est stratifiée
- Les résultats sont reproductibles (seeds)
- La meilleure technique est identifiable
```

---

### Module 3 : Changements Sécurisés (2-3h)

#### 📖 Tutoriel 3.1 : Code Review comme Evidence

**Review spécifique à votre projet :**

**Avant d'intégrer le modèle :**
```
@models/fraud_detector.py @utils/metrics.py

Bob, fais une code review du détecteur de fraude et identifie :
1. Les risques de data leakage (utilisation de features du futur)
2. Les problèmes de métriques (utilisation d'accuracy)
3. Les bugs potentiels (gestion du déséquilibre)
4. Les violations de bonnes pratiques ML

Focus particulier sur :
- La gestion du déséquilibre (sampling correct)
- Les métriques utilisées (F1, AUC-ROC, pas accuracy)
- Le seuil de décision (optimisé pour le cas d'usage)
- L'absence de biais démographiques
```

**💡 Checklist de review pour code de détection de fraude :**
- [ ] Pas de data leakage (features du futur)
- [ ] Métriques appropriées (F1, AUC-ROC, pas accuracy)
- [ ] Gestion correcte du déséquilibre
- [ ] Validation croisée stratifiée
- [ ] Seuil de décision optimisé
- [ ] Pas de biais démographiques

---

#### 📖 Tutoriel 3.2 : Modernisation Sans Dérive

**Cas pratique : Optimisation pour le temps réel**

**Situation :** Votre modèle fonctionne mais l'inférence prend 200ms (trop lent).

**Contrat de modernisation :**
```markdown
## Modernisation : Optimisation Temps Réel

### Comportement à Préserver
- F1-score identique (±0.02)
- AUC-ROC identique (±0.01)
- Même seuil de décision

### Améliorations Souhaitées
- Inférence < 100ms (actuellement 200ms)
- Techniques : simplification modèle, quantization, ONNX
- Maintenir F1-score > 0.85

### Vérification
- Benchmark inférence sur 1000 transactions
- Validation F1-score sur test set complet
- Test de robustesse (différents seuils)
- Vérifier que les explications SHAP fonctionnent toujours
```

**💡 Prompt Bob :**
```
@models/fraud_detector.py

Optimise ce modèle pour réduire l'inférence de 200ms à < 100ms.
CRITIQUE : Le F1-score doit rester > 0.85.

Propose d'abord un plan avec plusieurs options :
1. Simplification du modèle (moins de couches)
2. Quantization (INT8)
3. Export ONNX avec optimisations
4. Feature selection (réduire le nombre de features)

Pour chaque option, estime l'impact sur latence et F1-score.
```

---

### Module 4 : Ce que Bob Ne Doit PAS Faire (1h)

#### 📖 Tutoriel 4.1 : Limites et Jugement Humain

**Décisions que VOUS devez prendre :**

❌ **Bob ne doit PAS décider :**
- Le seuil de décision (trade-off faux positifs/négatifs)
- Le coût relatif d'un faux positif vs faux négatif
- Si une feature est éthique à utiliser
- Comment gérer les cas limites (confiance faible)

✅ **Vous devez décider :**
- "Ce seuil minimise-t-il le coût total pour la banque ?"
- "Ces features respectent-elles la vie privée des clients ?"
- "Ce taux de faux positifs est-il acceptable pour les clients ?"
- "Cette explication du modèle est-elle compréhensible ?"

**💡 Exemple de mauvaise utilisation :**
```
❌ "Bob, déploie le modèle en production et bloque automatiquement 
   les transactions suspectes"
→ Risque de bloquer des clients légitimes

✅ "Bob, crée un système qui signale les transactions suspectes 
   pour review humaine, avec explications SHAP pour aider la décision"
```

---

#### 📖 Tutoriel 4.2 : Anti-Patterns

**Anti-patterns spécifiques à votre projet :**

❌ **Anti-pattern 1 : Utiliser accuracy**
```
"Bob, optimise le modèle pour maximiser l'accuracy"
→ Métrique trompeuse avec déséquilibre extrême
```

✅ **Bonne pratique :**
```
"Bob, optimise le modèle pour maximiser le F1-score, avec contrainte 
de rappel > 0.90 (détecter 90% des fraudes)"
```

❌ **Anti-pattern 2 : Ignorer le déséquilibre**
```
"Bob, entraîne un modèle standard sur le dataset"
→ Le modèle va prédire "non-fraude" pour tout
```

✅ **Bonne pratique :**
```
"Bob, implémente et compare 3 techniques de gestion du déséquilibre 
(SMOTE, undersampling, hybrid) et choisis la meilleure selon le F1-score"
```

❌ **Anti-pattern 3 : Pas d'explicabilité**
```
"Bob, crée un modèle de détection et c'est tout"
→ Impossible de comprendre pourquoi une transaction est suspecte
```

✅ **Bonne pratique :**
```
"Bob, crée un modèle de détection avec intégration SHAP pour expliquer 
chaque prédiction (top 5 features contributrices)"
```

---

### Module 5 : Travail en Équipe (2-3h)

#### 📖 Tutoriel 5.1 : Bob en Équipe

**Workflow d'équipe pour votre projet :**

**Répartition des tâches :**
- **Membre 1 (DEBBAGH)** : Modèle + Gestion déséquilibre
- **Membre 2 (JABRY)** : Explicabilité + Métriques
- **Membre 3 (GUEDIRI)** : Interface Streamlit + Tests

**💡 Template de PR avec Bob :**
```markdown
## PR : [Composant] - [Description]

### Généré avec Bob
- [ ] Oui, Bob a aidé à générer ce code
- [ ] Non, code manuel

### Contrat Respecté
- [ ] Intent clair défini
- [ ] Success criteria validés (F1-score, AUC-ROC)
- [ ] Tests passent
- [ ] Code reviewé

### Changements
- [Liste des fichiers modifiés]
- [Impact sur les métriques]

### Métriques
- F1-score : [X] (objectif : > 0.85)
- AUC-ROC : [Y] (objectif : > 0.95)
- Rappel : [Z] (objectif : > 0.90)
- Précision : [W] (objectif : > 0.80)

### Vérification
- [ ] Tests sur test set stratifié
- [ ] Validation croisée stratifiée
- [ ] Pas de data leakage
- [ ] Métriques appropriées (pas accuracy)

### Review Bob
[Coller ici les findings de Bob si applicable]
```

---

#### 📖 Tutoriel 5.2 : Rôles dans l'Agentic SDLC

**Pour votre équipe :**

**Développeur ML (DEBBAGH) :**
- Utiliser Bob pour implémenter les techniques de sampling
- Définir le modèle avec Bob
- Optimiser les hyperparamètres

**Développeur Explicabilité (JABRY) :**
- Utiliser Bob pour intégrer SHAP/LIME
- Créer les visualisations d'explicabilité
- Valider les explications

**Développeur Interface (GUEDIRI) :**
- Utiliser Bob pour créer l'interface Streamlit
- Intégrer le modèle et l'explicabilité
- Tester l'expérience utilisateur

---

#### 📖 Tutoriel 5.3 : Skills Personnalisés

**Skill personnalisé pour votre projet :**

Créez un skill "fraud-model-eval" :

```yaml
name: fraud-model-eval
description: Évaluation complète du modèle de détection de fraude
trigger: /eval-fraud

steps:
  - Charger le modèle et le test set
  - Calculer F1-score, AUC-ROC, précision, rappel
  - Générer la matrice de confusion
  - Analyser les faux positifs et faux négatifs
  - Créer un rapport avec visualisations
```

**💡 Utilisation :**
```
@models/fraud_detector.py /eval-fraud
```

**Skill "explain-prediction" :**

```yaml
name: explain-prediction
description: Expliquer une prédiction de fraude avec SHAP
trigger: /explain

steps:
  - Charger le modèle et la transaction
  - Calculer les SHAP values
  - Identifier les top 5 features contributrices
  - Générer un waterfall plot
  - Créer une explication textuelle
```

---

#### 📖 Tutoriel 5.4 : Mesurer Bob

**Métriques pour votre projet :**

**À mesurer :**
- ✅ Temps gagné sur l'implémentation (baseline vs avec Bob)
- ✅ Nombre de techniques de sampling testées
- ✅ Amélioration du F1-score
- ✅ Bugs détectés en review

**À NE PAS mesurer :**
- ❌ Nombre de lignes générées par Bob
- ❌ Pourcentage de code écrit par Bob
- ❌ Vitesse de développement brute

**💡 Tableau de bord suggéré :**
```markdown
## Métriques Projet Détection de Fraude

### Performance Modèle
- F1-score : 0.87 (objectif : > 0.85) ✅
- AUC-ROC : 0.96 (objectif : > 0.95) ✅
- Rappel : 0.92 (objectif : > 0.90) ✅
- Précision : 0.83 (objectif : > 0.80) ✅
- Inférence : 85ms (objectif : < 100ms) ✅

### Développement avec Bob
- Techniques de sampling testées : 5 (vs 1 sans Bob)
- Temps d'implémentation : 3 jours (vs 10 jours sans Bob)
- Bugs détectés : 12

### Qualité
- Couverture de tests : 90%
- Documentation : 100%
- Explicabilité : SHAP intégré
```

---

### Module 6 : Mindset et Pratiques Avancées (1-2h)

#### 📖 Tutoriel 6.1 : Le Mindset Bob

**Shift mental pour votre projet :**

**Avant :** "Je dois coder un classifieur"  
**Après :** "Je dois concevoir un système de détection de fraude robuste"

**Avant :** "Je vais maximiser l'accuracy"  
**Après :** "Je vais optimiser le F1-score avec contraintes métier"

**Avant :** "Je teste sur le dataset complet"  
**Après :** "Je valide avec cross-validation stratifiée"

**💡 Questions à vous poser :**
- ❓ Est-ce que j'utilise les bonnes métriques (pas accuracy) ?
- ❓ Est-ce que je gère correctement le déséquilibre ?
- ❓ Est-ce que mon modèle est explicable ?

---

#### 📖 Tutoriel 6.2 : Garder Bob Boring

**Workflows "boring" mais efficaces pour votre projet :**

**Workflow 1 : Nouvelle technique de sampling**
1. Définir la technique
2. Bob l'implémente
3. Vous comparez avec les autres
4. Bob génère le rapport
5. Vous choisissez la meilleure

**Workflow 2 : Optimisation du seuil**
1. Définir les contraintes (rappel min, précision min)
2. Bob teste différents seuils
3. Bob génère les courbes (précision-rappel, ROC)
4. Vous choisissez le seuil optimal
5. Bob l'intègre au modèle

**Workflow 3 : Analyse des erreurs**
1. Identifier les faux positifs/négatifs
2. Bob analyse leurs caractéristiques
3. Bob visualise les patterns
4. Vous identifiez les améliorations
5. Bob les implémente

**💡 Gardez ces workflows simples et répétables !**

---

## 🎯 Checklist Finale pour Votre Projet

### Gestion du Déséquilibre
- [ ] Techniques de sampling implémentées (SMOTE, undersampling, hybrid)
- [ ] Meilleure technique identifiée
- [ ] Validation croisée stratifiée
- [ ] Pas de data leakage

### Modèle
- [ ] F1-score > 0.85
- [ ] AUC-ROC > 0.95
- [ ] Rappel > 0.90
- [ ] Précision > 0.80
- [ ] Inférence < 100ms

### Métriques
- [ ] F1-score, AUC-ROC, précision, rappel calculés
- [ ] Matrice de confusion générée
- [ ] Courbes ROC et précision-rappel
- [ ] Pas d'utilisation d'accuracy

### Explicabilité
- [ ] SHAP ou LIME intégré
- [ ] Explications pour chaque prédiction
- [ ] Visualisations claires
- [ ] Top features identifiées

### Interface Streamlit
- [ ] Test de transactions en temps réel
- [ ] Affichage de la prédiction
- [ ] Affichage des explications
- [ ] Métriques du modèle visibles

### Code et Tests
- [ ] Tests unitaires pour chaque composant
- [ ] Tests sur test set stratifié
- [ ] Code reviewé (par Bob et humains)
- [ ] Documentation complète

---

## 💡 Prompts Bob Prêts à l'Emploi

### Démarrage du projet
```
Je démarre un projet de détection de fraude bancaire avec dataset 
massivement déséquilibré (0.17% de fraudes). Crée la structure avec :
- Techniques de gestion du déséquilibre (SMOTE, undersampling, hybrid)
- Modèle de classification optimisé
- Métriques appropriées (F1, AUC-ROC, pas accuracy)
- Explicabilité (SHAP)
- Interface Streamlit
```

### Analyse du dataset
```
@data/creditcard.csv

Analyse ce dataset de fraude bancaire et génère un rapport avec :
1. Statistiques de déséquilibre (% exact de fraudes)
2. Distribution de chaque feature
3. Corrélations entre features
4. Features les plus discriminantes (analyse univariée)
5. Recommandations pour la gestion du déséquilibre

Dataset : 284,807 transactions, 492 fraudes
```

### Techniques de sampling
```
@utils/sampling.py @data/creditcard.csv

Implémente 3 techniques de gestion du déséquilibre :
1. SMOTE (Synthetic Minority Over-sampling)
2. Random undersampling de la classe majoritaire
3. Hybrid (SMOTE + undersampling)

Pour chaque technique :
- Implémentation propre et réutilisable
- Validation que le déséquilibre est corrigé
- Préservation des patterns de fraude
```

### Modèle de détection
```
@models/fraud_detector.py @utils/sampling.py

Crée un modèle de détection de fraude :
- Architecture : réseau de neurones (3 couches denses)
- Input : 30 features (après PCA du dataset)
- Output : probabilité de fraude
- Loss : binary crossentropy avec poids de classe
- Métriques : F1-score, AUC-ROC, précision, rappel

Contraintes :
- Gestion du déséquilibre (utiliser sampling.py)
- Optimisation du seuil de décision
- Inférence < 100ms
```

### Métriques et évaluation
```
@utils/metrics.py @models/fraud_detector.py

Crée un module d'évaluation complet qui calcule :
1. F1-score, AUC-ROC, précision, rappel
2. Matrice de confusion
3. Courbe ROC
4. Courbe précision-rappel
5. Analyse des faux positifs et faux négatifs

Génère un rapport avec visualisations et recommandations.
```

### Explicabilité SHAP
```
@utils/explainability.py @models/fraud_detector.py

Intègre SHAP pour expliquer les prédictions :
1. Calculer les SHAP values pour chaque prédiction
2. Identifier les top 5 features contributrices
3. Générer un waterfall plot
4. Créer une explication textuelle compréhensible

Format : "Cette transaction est suspecte car [raisons]"
```

### Interface Streamlit
```
@app/streamlit_app.py @models/ @utils/

Crée une interface Streamlit pour tester le modèle :
1. Input : saisie manuelle ou upload CSV d'une transaction
2. Prédiction : affichage probabilité + décision (fraude/non-fraude)
3. Explication : SHAP waterfall plot + texte
4. Métriques : affichage F1-score, AUC-ROC du modèle
5. Historique : liste des dernières prédictions

Design : interface claire et professionnelle
```

### Optimisation du seuil
```
@utils/threshold_optimization.py @models/fraud_detector.py

Crée un script pour optimiser le seuil de décision :
1. Tester différents seuils (0.1 à 0.9, step 0.05)
2. Pour chaque seuil, calculer précision, rappel, F1-score
3. Générer les courbes précision-rappel
4. Identifier le seuil optimal selon contraintes :
   - Rappel minimum : 0.90
   - Maximiser F1-score

Génère un rapport avec recommandation de seuil.
```

---

## 📚 Ressources Complémentaires

### Pour les Datasets Déséquilibrés
- "Learning from Imbalanced Data" - He & Garcia
- Papers sur SMOTE et variantes
- Imbalanced-learn library documentation

### Pour la Détection de Fraude
- "Credit Card Fraud Detection: A Realistic Modeling" papers
- Kaggle Credit Card Fraud Detection discussions
- Best practices en production

### Pour l'Explicabilité
- "A Unified Approach to Interpreting Model Predictions" (SHAP paper)
- SHAP library documentation
- LIME documentation

### Pour Bob
- Tutoriels du parcours pédagogique
- Documentation IBM Bob
- Communauté Bob

---

## 🎓 Évaluation de Votre Utilisation de Bob

### Critères de Succès

**Utilisation Efficace de Bob (40%) :**
- [ ] Contrats clairs définis
- [ ] Context management approprié
- [ ] Reviews systématiques du code généré
- [ ] Métriques appropriées utilisées

**Qualité Technique (40%) :**
- [ ] Gestion correcte du déséquilibre
- [ ] F1-score > 0.85 atteint
- [ ] Explicabilité intégrée
- [ ] Optimisation temps réel

**Interface et Documentation (20%) :**
- [ ] Interface Streamlit fonctionnelle
- [ ] Documentation complète
- [ ] Explications claires
- [ ] Tests complets

---

**Bonne chance avec votre projet de Détection de Fraude ! 🚀🔒**

*N'oubliez pas : Les datasets déséquilibrés nécessitent des métriques appropriées. N'utilisez jamais accuracy comme métrique principale !*