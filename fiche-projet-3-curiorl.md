---
layout: default
title: Fiche Projet - CurioRL
---

# Fiche Projet : CurioRL
## Guide d'Utilisation de Bob pour Votre Projet

**Équipe :** DOMONQ  
**Domaine :** Recherche en Reinforcement Learning  
**Technologies :** VAE/CNN, Clustering (k-means/DBSCAN), PPO/DQN, MiniGrid

---

## 🎯 Vue d'Ensemble du Projet

### Objectif
Créer un agent d'exploration autonome par curiosité intrinsèque dans MiniGrid, capable d'explorer efficacement sans récompenses externes denses en utilisant une forme de "curiosité" endogène.

### Composants Principaux
1. **Encodeur VAE/CNN** : Compression des observations visuelles en espace latent
2. **Clustering dynamique** : Identification de "situations types" (k-means/DBSCAN)
3. **Récompenses intrinsèques** : Signal de curiosité basé sur la rareté des clusters
4. **Agent RL (PPO/DQN)** : Optimisation de politique combinant récompenses externes et intrinsèques

### Vos Attentes vis-à-vis de Bob
- Génération et structuration du code (scaffolding)
- Revue de code agentique (performance, fuites mémoire GPU)
- Refactorisation et maintien de la modularité
- Génération de tests et documentation
- Debugging assisté avec compréhension contextuelle

---

## 📚 Parcours Pédagogique Adapté à Votre Projet

### Module 1 : Fondamentaux (2-3h)

#### 📖 Tutoriel 1.1 : Introduction à IBM Bob

**Questions spécifiques à votre projet :**

❓ **Quels sont les 3 cas d'usage Bob les plus pertinents pour mon projet de recherche ?**
- Structuration de l'architecture complexe (VAE + Clustering + RL)
- Génération de code modulaire avec faible couplage
- Debugging de comportements émergents (collapse de politique, clusters dégénérés)

❓ **Où Bob peut-il m'aider le plus dans un projet de recherche RL ?**
- Architecture modulaire permettant l'expérimentation rapide
- Implémentation de métriques de curiosité
- Visualisation de l'espace latent et des clusters
- Documentation des expérimentations

❓ **Où le jugement humain est-il critique dans mon projet ?**
- Interprétation des clusters (correspondent-ils à des situations réelles ?)
- Validation que la curiosité guide bien l'exploration
- Analyse des comportements émergents de l'agent
- Décision sur les hyperparamètres de curiosité

**💡 Prompt Bob suggéré :**
```
Je travaille sur un projet de recherche en RL combinant :
- Un VAE pour encoder les observations MiniGrid en espace latent
- Un clustering dynamique (k-means/DBSCAN) sur cet espace
- Des récompenses intrinsèques basées sur la rareté des clusters
- Un agent PPO qui optimise récompenses externes + intrinsèques

Aide-moi à structurer l'architecture avec :
- Séparation claire des 3 modules (encodage, clustering, RL)
- Faible couplage pour faciliter l'expérimentation
- Interfaces bien définies entre modules
```

---

#### 📖 Tutoriel 1.2 : Le Cycle de Vie Agentique

**Application à votre projet :**

**Phase ORIENT** - Comprendre avant de coder
- ❓ Comment les trois composants (VAE, clustering, RL) interagissent-ils ?
- ❓ Quelle est la fréquence de mise à jour du clustering ?
- ❓ Comment les récompenses intrinsèques influencent-elles l'apprentissage ?

**💡 Utilisez Bob pour :**
```
Analyse l'architecture CurioRL et identifie :
1. Les dépendances entre VAE, clustering et agent RL
2. Les points de synchronisation critiques
3. Les hyperparamètres clés (fréquence clustering, poids curiosité)
4. Les métriques à suivre (couverture espace latent, diversité clusters)
```

**Phase BOUND** - Définir les contraintes
- ❓ Contrainte de modularité : chaque composant doit être testable indépendamment
- ❓ Contrainte de performance : pas de ralentissement > 20% vs RL standard
- ❓ Contrainte de reproductibilité : seeds fixés, expérimentations documentées
- ❓ Contrainte de recherche : faciliter l'ablation study

**Phase PLAN** - Planifier avant d'exécuter
- ❓ Ordre de développement : VAE seul → Clustering sur données fixes → Intégration RL → Curiosité dynamique ?
- ❓ Comment valider chaque composant indépendamment ?
- ❓ Quelles expériences de baseline pour comparer ?

**💡 Prompt Bob suggéré :**
```
Crée un plan de développement pour CurioRL :
1. Ordre de développement des modules
2. Points de validation indépendante
3. Expériences de baseline (RL sans curiosité, curiosité aléatoire)
4. Stratégie d'ablation study

Contrainte : architecture modulaire permettant de désactiver chaque composant
```

---

#### 📖 Tutoriel 1.3 : Comment Bob Pense

**Intent, Evidence, Judgment pour votre projet :**

**INTENT** - Ce que vous voulez accomplir
- ❓ Mon intent est-il clair ? "Faire de l'exploration" vs "Créer un agent qui explore efficacement les labyrinthes MiniGrid en utilisant la curiosité intrinsèque basée sur la rareté des états dans l'espace latent"
- ❓ Ai-je défini les critères de succès ? (Couverture de l'environnement, nombre d'états uniques visités, performance sur tâches à récompenses éparses)

**EVIDENCE** - Les faits que Bob collecte
- ❓ Quels fichiers Bob doit-il lire pour comprendre mon architecture ?
- ❓ Ai-je fourni des exemples d'observations MiniGrid ?
- ❓ Bob comprend-il la structure de l'espace latent ?

**JUDGMENT** - Votre décision finale
- ❓ Est-ce que je comprends pourquoi Bob suggère cette architecture de VAE ?
- ❓ Le calcul de curiosité proposé est-il cohérent avec la littérature ?
- ❓ Les hyperparamètres suggérés sont-ils raisonnables ?

**💡 Exercice pratique :**
```
Demande à Bob d'analyser ton architecture VAE et de suggérer des améliorations.

Avant d'accepter, vérifie :
- L'espace latent a-t-il une dimension appropriée (ni trop petit, ni trop grand) ?
- La reconstruction est-elle suffisante pour capturer les features importantes ?
- Le VAE est-il compatible avec le clustering en temps réel ?
- Comprends-tu l'impact de chaque modification sur la curiosité ?
```

---

#### 📖 Tutoriel 1.4 : La Transition des Habitudes

**Habitudes à changer pour votre projet :**

**Avant (habitudes traditionnelles) :**
- Coder tout d'un bloc sans modularité
- Tester manuellement différentes architectures
- Débugger en ajoutant des prints partout

**Après (habitudes agentiques) :**
- Définir des interfaces claires entre modules
- Laisser Bob générer des variantes à comparer
- Utiliser Bob pour instrumenter et analyser

**💡 Plan de transition pour votre projet :**

**Semaine 1-2 : VAE et Espace Latent**
- Utilisez Bob pour créer l'architecture VAE
- Définissez le contrat (dimension latent, qualité reconstruction)
- Visualisez l'espace latent

**Semaine 3-4 : Clustering Dynamique**
- Bob implémente k-means et DBSCAN
- Vous comparez les deux approches
- Bob aide à visualiser les clusters

**Semaine 5-6 : Récompenses Intrinsèques**
- Bob crée le module de calcul de curiosité
- Vous testez différentes formules
- Bob instrumente pour analyser l'impact

**Semaine 7-8 : Agent RL avec Curiosité**
- Bob intègre tout dans l'agent PPO
- Vous lancez les expérimentations
- Bob aide au debugging des comportements

**Semaine 9-10 : Expérimentations et Analyse**
- Bob génère les scripts d'ablation study
- Vous analysez les résultats
- Bob aide à la visualisation et documentation

---

### Module 2 : Prise en Main (3-4h)

#### 📖 Tutoriel 2.1 : L'Interface Bob

**Configuration pour votre projet :**

**Context Mentions essentiels :**
```
@models/vae_encoder.py         # Encodeur VAE
@models/clustering.py          # Clustering dynamique
@agents/curious_agent.py       # Agent RL avec curiosité
@utils/intrinsic_reward.py     # Calcul récompenses intrinsèques
@config/experiment_config.yaml # Configuration expériences
@envs/minigrid_wrapper.py      # Wrapper MiniGrid
```

**💡 Première tâche avec Bob :**
```
@models/vae_encoder.py @envs/minigrid_wrapper.py

Crée un encodeur VAE pour les observations MiniGrid :

1. Input : observations MiniGrid (grille 7x7x3 ou similaire)
2. Encoder : CNN → espace latent de dimension 32
3. Decoder : reconstruction de l'observation
4. Loss : reconstruction + KL divergence

Contraintes :
- Espace latent structuré (pas de collapse)
- Reconstruction suffisante pour identifier les situations
- Compatible avec clustering en temps réel
- Encodage rapide (< 10ms)
```

---

#### 📖 Tutoriel 2.2 : Gestion du Contexte ⭐ CRITIQUE

**Contexte spécifique à votre projet de recherche :**

**Signal (à inclure) :**
- ✅ Architecture VAE (models/vae_encoder.py)
- ✅ Module de clustering (models/clustering.py)
- ✅ Agent RL (agents/curious_agent.py)
- ✅ Calcul de curiosité (utils/intrinsic_reward.py)
- ✅ Configuration expériences (config/)
- ✅ Scripts de visualisation (viz/)

**Noise (à exclure) :**
- ❌ Checkpoints de modèles entraînés
- ❌ Logs d'entraînement détaillés
- ❌ Données de replay buffer
- ❌ Visualisations générées
- ❌ Résultats d'expériences passées

**💡 Context Pack pour votre projet :**

Créez un fichier `.bobcontext` :
```yaml
# Context Pack - Projet CurioRL
include:
  - models/**/*.py
  - agents/**/*.py
  - utils/**/*.py
  - envs/**/*.py
  - config/*.yaml
  - viz/visualization.py
  - experiments/run_experiment.py
  - README.md
  
exclude:
  - checkpoints/**
  - logs/**
  - replay_buffers/**
  - results/**
  - viz/outputs/**
  
priority_files:
  - models/vae_encoder.py
  - models/clustering.py
  - agents/curious_agent.py
  - utils/intrinsic_reward.py
  - config/experiment_config.yaml
```

**❓ Questions de grounding :**
- Avant chaque tâche : "Bob, as-tu lu ma configuration de dimension latente ?"
- Après modification : "Bob, confirme que le clustering reste compatible avec le VAE"
- En cas de doute : "Bob, montre-moi comment les modules interagissent"

**💡 Gestion du contexte pour recherche :**
```
Pour les expérimentations, toujours inclure :
@models/vae_encoder.py @models/clustering.py @agents/curious_agent.py 
@config/experiment_config.yaml

Bob, analyse l'architecture complète et identifie les points de couplage.
Propose des améliorations pour faciliter l'ablation study.
```

---

#### 📖 Tutoriel 2.3 : Contrats Avant Code

**Contrat type pour votre projet :**

**Exemple : Module de Curiosité Intrinsèque**

```markdown
## Contrat : Récompenses Intrinsèques par Curiosité

### Intent
Créer un module qui calcule des récompenses intrinsèques basées sur 
la rareté des états dans l'espace latent, pour encourager l'exploration.

### Success Criteria
- Récompense élevée pour états rares (nouveaux clusters ou clusters peu visités)
- Récompense faible pour états fréquents
- Calcul rapide (< 5ms par step)
- Pas de memory leak (clustering dynamique)
- Métriques de couverture de l'espace latent

### Non-Goals
- Ne pas optimiser pour des environnements autres que MiniGrid (v1)
- Ne pas gérer des espaces latents > 64 dimensions
- Ne pas persister l'historique complet des états

### Preserved Behavior
- Compatible avec l'API Gymnasium
- Fonctionne avec PPO et DQN
- Logging des statistiques de curiosité

### Verification
- Tests unitaires sur états synthétiques
- Validation que nouveaux états → haute récompense
- Validation que états répétés → faible récompense
- Benchmark de performance (< 5ms)
- Test de memory leak sur 1M steps

### Stop Conditions
- Si calcul > 10ms → optimiser l'algorithme
- Si memory leak détecté → revoir la gestion des clusters
- Si pas d'amélioration exploration vs baseline → revoir la formule
```

**💡 Utilisez ce contrat avec Bob :**
```
@utils/intrinsic_reward.py @models/clustering.py

Implémente le module de curiosité intrinsèque selon le contrat ci-dessus.
Commence par me proposer plusieurs formules de curiosité avec leurs avantages/inconvénients.
```

---

#### 📖 Tutoriel 2.4 : Votre Première Tâche Accountable

**Tâche guidée : Créer le VAE pour MiniGrid**

**Étape 1 : Intent clair**
```
Je veux créer un VAE qui encode les observations MiniGrid en espace latent :
1. Input : observations MiniGrid (grille 7x7x3 typiquement)
2. Encoder : CNN → espace latent de dimension 32
3. Decoder : reconstruction de l'observation
4. Loss : reconstruction (MSE ou BCE) + β * KL divergence
5. Entraînement : sur trajectoires collectées par agent aléatoire

Contraintes critiques :
- Espace latent structuré (pas de posterior collapse)
- Reconstruction suffisante pour distinguer situations
- Encodage rapide (< 10ms)
- Compatible avec clustering k-means/DBSCAN
```

**Étape 2 : Laisser Bob explorer**
```
@envs/minigrid_wrapper.py @config/experiment_config.yaml

Bob, explore d'abord l'environnement MiniGrid et ma configuration.
Dis-moi ce que tu comprends de la structure des observations avant de proposer une architecture VAE.
```

**Étape 3 : Lire le plan**
- ❓ Bob a-t-il compris la structure des observations MiniGrid ?
- ❓ L'architecture CNN proposée est-elle adaptée ?
- ❓ La dimension latente (32) est-elle justifiée ?
- ❓ Le β-VAE est-il approprié pour éviter le collapse ?

**Étape 4 : Exécution et vérification**
```
Après entraînement, vérifie :
- Pas de posterior collapse (variance latente > seuil)
- Reconstruction visuelle acceptable
- Espace latent structuré (visualisation t-SNE)
- Encodage rapide (< 10ms)
- Compatible avec clustering
```

---

### Module 3 : Changements Sécurisés (2-3h)

#### 📖 Tutoriel 3.1 : Code Review comme Evidence

**Review spécifique à votre projet :**

**Avant d'intégrer le module de curiosité :**
```
@utils/intrinsic_reward.py @models/clustering.py

Bob, fais une code review du module de curiosité et identifie :
1. Les risques de performance (calculs répétés, allocations)
2. Les problèmes de mémoire (croissance des clusters, fuites)
3. Les bugs potentiels (division par zéro, clusters vides)
4. Les violations de bonnes pratiques RL

Focus particulier sur :
- La gestion de la mémoire du clustering dynamique
- Le calcul de distance dans l'espace latent
- La normalisation des récompenses intrinsèques
- La compatibilité avec différents algorithmes RL
```

**💡 Checklist de review pour code de recherche :**
- [ ] Reproductibilité garantie (seeds, déterminisme)
- [ ] Métriques instrumentées (logging complet)
- [ ] Pas de memory leak (clustering dynamique)
- [ ] Ablation study facilitée (flags pour désactiver composants)
- [ ] Visualisations intégrées (espace latent, clusters)
- [ ] Documentation des choix d'architecture

---

#### 📖 Tutoriel 3.2 : Modernisation Sans Dérive

**Cas pratique : Refactoring du VAE**

**Situation :** Votre VAE fonctionne mais le code est monolithique et difficile à expérimenter.

**Contrat de modernisation :**
```markdown
## Modernisation : VAE Modulaire

### Comportement à Préserver
- Espace latent identique (même dimension, même distribution)
- Reconstruction équivalente (même MSE)
- Compatibilité avec le clustering existant

### Améliorations Souhaitées
- Séparer encoder / decoder / loss
- Externaliser les hyperparamètres (β, learning rate)
- Faciliter l'expérimentation (différentes architectures CNN)
- Ajouter des hooks pour visualisation

### Vérification
- Comparer les embeddings avant/après sur 1000 observations
- Vérifier que la reconstruction est identique
- Tester que le clustering donne les mêmes résultats
- Valider que l'agent RL performe pareil
```

**💡 Prompt Bob :**
```
@models/vae_encoder.py

Refactorise ce VAE pour le rendre modulaire et faciliter l'expérimentation.
CRITIQUE : L'espace latent doit rester identique (même distribution).

Propose d'abord un plan de refactoring avec :
1. Séparation des composants
2. Points d'extension pour expérimentation
3. Stratégie de validation que le comportement est préservé
```

---

### Module 4 : Ce que Bob Ne Doit PAS Faire (1h)

#### 📖 Tutoriel 4.1 : Limites et Jugement Humain

**Décisions que VOUS devez prendre :**

❌ **Bob ne doit PAS décider :**
- La formule de curiosité à utiliser (count-based, prediction error, etc.)
- Les hyperparamètres de curiosité (poids, normalisation)
- L'interprétation des clusters (correspondent-ils à des situations réelles ?)
- Si un comportement émergent est intéressant ou un bug

✅ **Vous devez décider :**
- "Cette formule de curiosité guide-t-elle bien l'exploration ?"
- "Ces clusters correspondent-ils à des situations distinctes ?"
- "Ce comportement est-il de l'exploration intelligente ou du bruit ?"
- "Ces hyperparamètres sont-ils cohérents avec la littérature ?"

**💡 Exemple de mauvaise utilisation :**
```
❌ "Bob, trouve automatiquement la meilleure formule de curiosité"
→ Risque d'overfitting sur l'environnement de test

✅ "Bob, implémente 3 formules de curiosité de la littérature 
   (count-based, ICM, RND) et crée un framework pour les comparer"
```

---

#### 📖 Tutoriel 4.2 : Anti-Patterns

**Anti-patterns spécifiques à votre projet :**

❌ **Anti-pattern 1 : Couplage fort**
```
"Bob, intègre tout dans une seule classe Agent"
→ Impossible de tester les composants indépendamment
```

✅ **Bonne pratique :**
```
"Bob, crée une architecture avec 3 modules indépendants (VAE, Clustering, RL)
communiquant via des interfaces bien définies"
```

❌ **Anti-pattern 2 : Pas de baseline**
```
"Bob, implémente CurioRL et c'est tout"
→ Impossible de savoir si la curiosité aide vraiment
```

✅ **Bonne pratique :**
```
"Bob, crée un framework permettant de lancer :
1. RL standard (sans curiosité)
2. RL avec curiosité aléatoire
3. RL avec curiosité basée sur clustering
4. Comparaison automatique des résultats"
```

❌ **Anti-pattern 3 : Pas de visualisation**
```
"Bob, entraîne l'agent et affiche la récompense"
→ Pas de compréhension de ce qui se passe
```

✅ **Bonne pratique :**
```
"Bob, crée des visualisations pour :
1. Espace latent (t-SNE) avec clusters
2. Heatmap de visite des états
3. Évolution de la curiosité au cours du temps
4. Trajectoires de l'agent dans l'environnement"
```

---

### Module 5 : Travail en Équipe (2-3h)

#### 📖 Tutoriel 5.1 : Bob en Équipe

**Workflow pour projet solo de recherche :**

Même en solo, structurez votre travail comme une équipe :

**"Vous" en tant que chercheur :**
- Définir les hypothèses et expériences
- Interpréter les résultats
- Décider des directions de recherche

**"Bob" en tant qu'assistant :**
- Implémenter les variantes
- Générer les scripts d'expérimentation
- Créer les visualisations
- Documenter les résultats

**💡 Template de commit avec Bob :**
```markdown
## Commit : [Expérience] - [Description]

### Hypothèse
[Quelle hypothèse teste cette expérience ?]

### Implémentation avec Bob
- [ ] Bob a généré le code de l'expérience
- [ ] Bob a créé les scripts de lancement
- [ ] Bob a généré les visualisations

### Résultats
- [Métriques clés]
- [Observations]

### Conclusion
- [ ] Hypothèse validée / invalidée
- [ ] Prochaines étapes

### Code Review Bob
[Findings de Bob si applicable]
```

---

#### 📖 Tutoriel 5.2 : Rôles dans l'Agentic SDLC

**Pour votre projet de recherche :**

**Vous en tant que Chercheur :**
- Définir les questions de recherche
- Concevoir les expériences
- Interpréter les résultats
- Écrire le paper

**Bob en tant qu'Assistant de Recherche :**
- Implémenter les architectures
- Générer les variantes pour ablation study
- Créer les scripts d'expérimentation
- Produire les visualisations
- Documenter le code

**Workflow typique :**
1. Vous : "Je veux tester si le clustering DBSCAN est meilleur que k-means"
2. Bob : Implémente les deux variantes
3. Vous : Lancez les expériences
4. Bob : Génère les visualisations comparatives
5. Vous : Interprétez et décidez

---

#### 📖 Tutoriel 5.3 : Skills Personnalisés

**Skill personnalisé pour votre projet :**

Créez un skill "research-experiment" :

```yaml
name: research-experiment
description: Lancer une expérience de recherche complète
trigger: /experiment

steps:
  - Créer un dossier d'expérience avec timestamp
  - Copier la configuration actuelle
  - Lancer l'entraînement avec logging
  - Générer les visualisations
  - Créer un rapport markdown avec résultats
  - Commit automatique avec tag
```

**💡 Utilisation :**
```
@config/experiment_config.yaml /experiment

Nom : "curiosity_dbscan_vs_kmeans"
Description : "Comparaison DBSCAN vs k-means pour clustering"
```

**Skill "visualize-latent-space" :**

```yaml
name: visualize-latent-space
description: Visualiser l'espace latent et les clusters
trigger: /viz-latent

steps:
  - Collecter des observations de l'environnement
  - Encoder avec le VAE
  - Appliquer t-SNE ou UMAP
  - Colorier par cluster
  - Générer le plot interactif
  - Sauvegarder en HTML
```

---

#### 📖 Tutoriel 5.4 : Mesurer Bob

**Métriques pour votre projet de recherche :**

**À mesurer :**
- ✅ Temps gagné sur l'implémentation (baseline vs avec Bob)
- ✅ Nombre de variantes testées (avec vs sans Bob)
- ✅ Qualité du code (modularité, tests)
- ✅ Bugs détectés en review

**À NE PAS mesurer :**
- ❌ Nombre de lignes générées par Bob
- ❌ Pourcentage de code écrit par Bob
- ❌ Vitesse de développement brute

**💡 Tableau de bord suggéré :**
```markdown
## Métriques Projet CurioRL

### Expérimentations
- Variantes testées : 15 (vs 4 sans Bob)
- Temps moyen par variante : 2h (vs 8h sans Bob)
- Expériences documentées : 100%

### Qualité Code
- Modularité : 3 modules indépendants
- Couverture de tests : 75%
- Documentation : 100% des fonctions

### Recherche
- Papers lus et implémentés : 8
- Ablation studies complètes : 5
- Visualisations générées : 50+
```

---

### Module 6 : Mindset et Pratiques Avancées (1-2h)

#### 📖 Tutoriel 6.1 : Le Mindset Bob

**Shift mental pour votre projet :**

**Avant :** "Je dois coder un agent RL"  
**Après :** "Je dois concevoir un système d'exploration par curiosité"

**Avant :** "Je vais tout implémenter puis tester"  
**Après :** "Je définis des modules testables indépendamment"

**Avant :** "Je lance des expériences et je vois"  
**Après :** "Je définis des hypothèses et je teste systématiquement"

**💡 Questions à vous poser :**
- ❓ Est-ce que je pense en termes de système modulaire ou de code monolithique ?
- ❓ Est-ce que je définis des hypothèses avant d'expérimenter ?
- ❓ Est-ce que je documente systématiquement mes expériences ?

---

#### 📖 Tutoriel 6.2 : Garder Bob Boring

**Workflows "boring" mais efficaces pour votre projet :**

**Workflow 1 : Nouvelle variante**
1. Définir l'hypothèse
2. Bob génère la variante
3. Vous lancez l'expérience
4. Bob génère les visualisations
5. Vous interprétez et documentez

**Workflow 2 : Debugging comportement**
1. Identifier le comportement anormal
2. Bob instrumente le code
3. Vous collectez les données
4. Bob visualise
5. Vous identifiez la cause

**Workflow 3 : Ablation study**
1. Définir les composants à ablater
2. Bob génère les configurations
3. Vous lancez toutes les expériences
4. Bob compare les résultats
5. Vous concluez

**💡 Gardez ces workflows simples et répétables !**

---

## 🎯 Checklist Finale pour Votre Projet

### Architecture
- [ ] 3 modules indépendants (VAE, Clustering, RL)
- [ ] Interfaces bien définies entre modules
- [ ] Faible couplage (ablation study facile)
- [ ] Configuration externalisée

### VAE
- [ ] Pas de posterior collapse
- [ ] Reconstruction acceptable
- [ ] Espace latent structuré (t-SNE)
- [ ] Encodage rapide (< 10ms)

### Clustering
- [ ] k-means et DBSCAN implémentés
- [ ] Clustering dynamique (pas de memory leak)
- [ ] Métriques de qualité (silhouette, etc.)
- [ ] Visualisation des clusters

### Curiosité
- [ ] Récompenses intrinsèques calculées
- [ ] Normalisation appropriée
- [ ] Pas de domination sur récompenses externes
- [ ] Métriques de couverture

### Agent RL
- [ ] PPO ou DQN fonctionnel
- [ ] Intégration récompenses externes + intrinsèques
- [ ] Convergence de l'entraînement
- [ ] Performance sur tâches à récompenses éparses

### Expérimentations
- [ ] Baseline (RL sans curiosité) implémentée
- [ ] Ablation study complète
- [ ] Résultats reproductibles (seeds)
- [ ] Visualisations générées

### Code et Documentation
- [ ] Tests unitaires pour chaque module
- [ ] Code reviewé (par Bob)
- [ ] Documentation complète
- [ ] Expériences documentées

---

## 💡 Prompts Bob Prêts à l'Emploi

### Démarrage du projet
```
Je démarre un projet de recherche sur l'exploration par curiosité intrinsèque.
Crée la structure de projet avec :
- Module VAE pour encodage
- Module clustering (k-means + DBSCAN)
- Module de calcul de curiosité
- Agent RL (PPO) avec récompenses intrinsèques
- Scripts d'expérimentation
- Visualisations
```

### VAE pour MiniGrid
```
@envs/minigrid_wrapper.py @config/experiment_config.yaml

Crée un VAE pour encoder les observations MiniGrid :
- Input : grille 7x7x3
- Encoder : CNN → latent 32D
- Decoder : reconstruction
- Loss : MSE + β * KL (β=1.0)
- Entraînement : sur trajectoires agent aléatoire

Contraintes :
- Pas de posterior collapse
- Reconstruction visuelle acceptable
- Encodage < 10ms
```

### Clustering dynamique
```
@models/clustering.py @models/vae_encoder.py

Crée un module de clustering dynamique sur l'espace latent :
- Algorithmes : k-means et DBSCAN
- Update : tous les N steps (configurable)
- Métriques : silhouette score, nombre de clusters
- Visualisation : t-SNE avec couleurs par cluster

Contraintes :
- Pas de memory leak
- Calcul rapide (< 5ms)
- Compatible avec curiosité en temps réel
```

### Récompenses intrinsèques
```
@utils/intrinsic_reward.py @models/clustering.py

Crée un module de calcul de récompenses intrinsèques :
- Formule : r_int = 1 / sqrt(count(cluster))
- Normalisation : running mean/std
- Logging : statistiques de curiosité

Implémente aussi 2 baselines :
1. Curiosité aléatoire
2. Count-based simple (sans clustering)

Pour faciliter la comparaison
```

### Agent RL avec curiosité
```
@agents/curious_agent.py @utils/intrinsic_reward.py

Crée un agent PPO qui combine récompenses externes et intrinsèques :
- Récompense totale : r_total = r_ext + λ * r_int
- λ configurable (défaut : 0.1)
- Logging séparé des deux types de récompenses
- Compatible avec MiniGrid

Contraintes :
- Pas de ralentissement > 20% vs PPO standard
- Métriques de couverture de l'environnement
```

### Framework d'expérimentation
```
@experiments/run_experiment.py @config/

Crée un framework pour lancer des expériences :
1. Charger la configuration
2. Initialiser l'environnement et l'agent
3. Entraîner avec logging
4. Générer les visualisations
5. Sauvegarder les résultats
6. Créer un rapport markdown

Fonctionnalités :
- Sweep d'hyperparamètres
- Comparaison de variantes
- Reproductibilité (seeds)
```

### Ablation study
```
@experiments/ablation_study.py

Crée un script d'ablation study qui teste :
1. RL standard (pas de curiosité)
2. RL + curiosité aléatoire
3. RL + curiosité count-based
4. RL + curiosité clustering k-means
5. RL + curiosité clustering DBSCAN

Pour chaque variante :
- 5 seeds différents
- Même environnement
- Mêmes hyperparamètres RL
- Logging complet

Génère un rapport comparatif avec graphiques
```

### Visualisations
```
@viz/visualization.py @models/ @agents/

Crée des visualisations pour :
1. Espace latent (t-SNE) avec clusters colorés
2. Heatmap de visite des états dans MiniGrid
3. Évolution de la curiosité au cours du temps
4. Trajectoires de l'agent (avant/après curiosité)
5. Distribution des récompenses intrinsèques

Format : plots interactifs (plotly) + exports PNG
```

---

## 📚 Ressources Complémentaires

### Pour la Curiosité Intrinsèque
- "Curiosity-driven Exploration by Self-supervised Prediction" (ICM paper)
- "Exploration by Random Network Distillation" (RND paper)
- "Never Give Up: Learning Directed Exploration Strategies" (NGU paper)

### Pour les VAE
- "Auto-Encoding Variational Bayes" (VAE paper)
- "β-VAE: Learning Basic Visual Concepts with a Constrained Variational Framework"
- "Understanding disentangling in β-VAE"

### Pour le Clustering
- "Density-Based Spatial Clustering" (DBSCAN paper)
- Scikit-learn clustering documentation

### Pour Bob
- Tutoriels du parcours pédagogique
- Documentation IBM Bob
- Communauté Bob

---

## 🎓 Évaluation de Votre Utilisation de Bob

### Critères de Succès

**Utilisation Efficace de Bob (40%) :**
- [ ] Architecture modulaire définie avec Bob
- [ ] Context management approprié (focus recherche)
- [ ] Reviews systématiques du code généré
- [ ] Expérimentations facilitées par Bob

**Qualité Technique (40%) :**
- [ ] Architecture modulaire et testable
- [ ] Pas de memory leak
- [ ] Reproductibilité garantie
- [ ] Visualisations complètes

**Recherche et Documentation (20%) :**
- [ ] Hypothèses clairement définies
- [ ] Ablation study complète
- [ ] Résultats documentés
- [ ] Code bien commenté

---

**Bonne chance avec votre projet CurioRL ! 🚀🔍**

*N'oubliez pas : La recherche est itérative. Utilisez Bob pour accélérer l'implémentation, mais gardez le contrôle sur les hypothèses et l'interprétation !*