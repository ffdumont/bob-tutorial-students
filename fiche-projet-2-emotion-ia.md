---
layout: default
title: Fiche Projet - Emotion-IA
---

# Fiche Projet : Emotion-IA
## Guide d'Utilisation de Bob pour Votre Projet

**Équipe :** DIOP, WANDAOGO, DIALLO  
**Domaine :** Vision par ordinateur + Reinforcement Learning  
**Technologies :** CNN (FER-2013), DQN, Streamlit, OpenCV

---

## 🎯 Vue d'Ensemble du Projet

### Objectif
Créer un système auto-adaptatif de reconnaissance faciale d'émotions en temps réel, capable d'ajuster dynamiquement les paramètres vidéo pour maintenir une haute précision de détection.

### Composants Principaux
1. **CNN pour classification** : Réseau convolutif entraîné sur FER-2013 (7 émotions)
2. **Agent DQN** : Ajustement dynamique des paramètres vidéo (contraste, exposition)
3. **Pipeline temps réel** : Capture webcam → Preprocessing → CNN → DQN → Ajustement
4. **Interface Streamlit** : Visualisation en temps réel des émotions et ajustements

### Vos Attentes vis-à-vis de Bob
- Optimisation de l'inférence pour le temps réel
- Monitoring des performances et détection de biais
- Industrialisation du cycle de vie du modèle
- Facilitation du déploiement cloud

---

## 📚 Parcours Pédagogique Adapté à Votre Projet

### Module 1 : Fondamentaux (2-3h)

#### 📖 Tutoriel 1.1 : Introduction à IBM Bob

**Questions spécifiques à votre projet :**

❓ **Quels sont les 3 cas d'usage Bob les plus pertinents pour mon projet de vision temps réel ?**
- Optimisation du pipeline CNN pour inférence < 100ms
- Implémentation de l'agent DQN pour ajustement adaptatif
- Création de l'interface Streamlit avec visualisation temps réel

❓ **Où Bob peut-il m'aider le plus dans un projet de vision par ordinateur ?**
- Architecture CNN optimisée pour le temps réel
- Preprocessing efficace des frames vidéo
- Intégration CNN → DQN → Ajustement en boucle fermée
- Détection et correction des biais démographiques

❓ **Où le jugement humain est-il critique dans mon projet ?**
- Validation de la qualité des émotions détectées (pas de faux positifs critiques)
- Interprétation des ajustements de l'agent DQN (sont-ils pertinents ?)
- Évaluation des biais potentiels (âge, genre, ethnicité)
- Décision sur les seuils de confiance acceptables

**💡 Prompt Bob suggéré :**
```
Je travaille sur un système de reconnaissance d'émotions en temps réel combinant :
- Un CNN pour classifier 7 émotions faciales (FER-2013)
- Un agent DQN qui ajuste dynamiquement contraste et exposition
- Une interface Streamlit pour visualisation temps réel

Aide-moi à structurer l'architecture avec :
- Pipeline optimisé pour latence < 100ms
- Intégration CNN → DQN en boucle fermée
- Gestion efficace du flux vidéo webcam
```

---

#### 📖 Tutoriel 1.2 : Le Cycle de Vie Agentique

**Application à votre projet :**

**Phase ORIENT** - Comprendre avant de coder
- ❓ Quelle est la latence acceptable pour mon application temps réel ?
- ❓ Comment le CNN et le DQN doivent-ils communiquer ?
- ❓ Quels sont les goulots d'étranglement potentiels (capture, preprocessing, inférence, ajustement) ?

**💡 Utilisez Bob pour :**
```
Analyse mon pipeline temps réel et identifie :
1. Les étapes critiques pour la latence
2. Les optimisations possibles (batch processing, async, GPU)
3. Comment structurer la boucle CNN → DQN → Ajustement
4. Les métriques à monitorer (FPS, latence, confiance)
```

**Phase BOUND** - Définir les contraintes
- ❓ Contrainte temps réel : latence totale < 100ms
- ❓ Contrainte matérielle : GPU disponible ? Quelle mémoire ?
- ❓ Contrainte qualité : précision minimale acceptable ?
- ❓ Contrainte éthique : comment gérer les biais démographiques ?

**Phase PLAN** - Planifier avant d'exécuter
- ❓ Dans quel ordre développer : CNN seul → Pipeline temps réel → DQN → Interface ?
- ❓ Comment tester chaque composant indépendamment ?
- ❓ Comment mesurer les performances à chaque étape ?

**💡 Prompt Bob suggéré :**
```
Crée un plan de développement pour mon système Emotion-IA :
1. Ordre de développement (CNN, pipeline, DQN, interface)
2. Points de validation de performance à chaque étape
3. Stratégie d'optimisation progressive
4. Plan de test pour le temps réel

Contrainte critique : latence totale < 100ms
```

---

#### 📖 Tutoriel 1.3 : Comment Bob Pense

**Intent, Evidence, Judgment pour votre projet :**

**INTENT** - Ce que vous voulez accomplir
- ❓ Mon intent est-il clair ? "Détecter des émotions" vs "Créer un système temps réel auto-adaptatif de détection d'émotions avec latence < 100ms"
- ❓ Ai-je défini les critères de succès ? (Précision > 85%, FPS > 10, latence < 100ms)

**EVIDENCE** - Les faits que Bob collecte
- ❓ Quels fichiers Bob doit-il lire pour comprendre mon architecture ?
- ❓ Ai-je fourni des exemples de frames pour que Bob comprenne le preprocessing ?
- ❓ Bob a-t-il accès aux specs de mon matériel (GPU, RAM) ?

**JUDGMENT** - Votre décision finale
- ❓ Est-ce que je comprends pourquoi Bob suggère cette architecture CNN ?
- ❓ Les optimisations proposées sont-elles compatibles avec le temps réel ?
- ❓ L'agent DQN proposé est-il adapté à mon cas d'usage ?

**💡 Exercice pratique :**
```
Demande à Bob d'analyser ton architecture CNN actuelle et de suggérer 
des optimisations pour le temps réel.

Avant d'accepter, vérifie :
- Les modifications préservent-elles la précision ?
- La latence est-elle réellement améliorée ?
- Les changements sont-ils compatibles avec le DQN ?
- Comprends-tu chaque optimisation proposée ?
```

---

#### 📖 Tutoriel 1.4 : La Transition des Habitudes

**Habitudes à changer pour votre projet :**

**Avant (habitudes traditionnelles) :**
- Entraîner un CNN sans penser à l'inférence temps réel
- Tester manuellement différents paramètres vidéo
- Optimiser après coup quand c'est trop lent

**Après (habitudes agentiques) :**
- Définir les contraintes temps réel dès le début
- Laisser Bob générer des architectures optimisées
- Automatiser l'ajustement avec le DQN

**💡 Plan de transition pour votre équipe :**

**Semaine 1-2 : CNN et Dataset**
- Utilisez Bob pour créer l'architecture CNN optimisée
- Définissez le contrat de performance (latence, précision)
- Entraînez et validez sur FER-2013

**Semaine 3-4 : Pipeline Temps Réel**
- Bob optimise le pipeline de capture et preprocessing
- Vous testez la latence réelle
- Bob aide à identifier les goulots d'étranglement

**Semaine 5-6 : Agent DQN**
- Bob crée l'environnement pour le DQN
- Vous définissez la fonction de récompense (confiance CNN)
- Bob optimise l'agent

**Semaine 7-8 : Intégration et Interface**
- Bob génère l'interface Streamlit
- Vous validez l'expérience utilisateur
- Tests de bout en bout

**Semaine 9-10 : Optimisation et Déploiement**
- Bob aide à la détection de biais
- Optimisation finale
- Documentation et déploiement

---

### Module 2 : Prise en Main (3-4h)

#### 📖 Tutoriel 2.1 : L'Interface Bob

**Configuration pour votre projet :**

**Context Mentions essentiels :**
```
@models/emotion_cnn.py         # Architecture CNN
@agents/video_adjuster.py      # Agent DQN
@utils/video_pipeline.py       # Pipeline capture/preprocessing
@config/model_config.yaml      # Configuration
@app/streamlit_app.py          # Interface
```

**💡 Première tâche avec Bob :**
```
@models/emotion_cnn.py @config/model_config.yaml

Crée une architecture CNN optimisée pour la reconnaissance d'émotions 
en temps réel :

1. Input : frames 48x48 grayscale (FER-2013)
2. Output : 7 classes d'émotions
3. Contrainte : inférence < 50ms sur GPU
4. Architecture : Conv layers + BatchNorm + Dropout
5. Optimisations : pruning, quantization si nécessaire

Contraintes critiques :
- Latence d'inférence < 50ms
- Précision > 85% sur validation
- Compatible avec ONNX pour déploiement
```

---

#### 📖 Tutoriel 2.2 : Gestion du Contexte ⭐ CRITIQUE

**Contexte spécifique à votre projet temps réel :**

**Signal (à inclure) :**
- ✅ Architecture CNN (models/emotion_cnn.py)
- ✅ Agent DQN (agents/video_adjuster.py)
- ✅ Pipeline vidéo (utils/video_pipeline.py)
- ✅ Configuration (config/)
- ✅ Scripts de benchmark (tests/benchmark.py)

**Noise (à exclure) :**
- ❌ Dataset FER-2013 complet (trop volumineux)
- ❌ Checkpoints de modèles entraînés
- ❌ Vidéos de test
- ❌ Logs d'entraînement détaillés
- ❌ Frames capturées

**💡 Context Pack pour votre projet :**

Créez un fichier `.bobcontext` :
```yaml
# Context Pack - Projet Emotion-IA
include:
  - models/**/*.py
  - agents/**/*.py
  - utils/**/*.py
  - config/*.yaml
  - app/*.py
  - tests/benchmark.py
  - README.md
  
exclude:
  - data/FER2013/**
  - models/checkpoints/**
  - logs/**
  - videos/**
  - frames/**
  
priority_files:
  - models/emotion_cnn.py
  - agents/video_adjuster.py
  - utils/video_pipeline.py
  - config/model_config.yaml
```

**❓ Questions de grounding :**
- Avant chaque tâche : "Bob, as-tu lu ma configuration de latence cible ?"
- Après modification : "Bob, confirme que l'optimisation préserve la précision"
- En cas de doute : "Bob, montre-moi l'impact sur la latence totale"

**💡 Gestion du contexte temps réel :**
```
Pour les optimisations temps réel, toujours inclure :
@models/emotion_cnn.py @utils/video_pipeline.py @tests/benchmark.py

Bob, analyse le pipeline complet et identifie les goulots d'étranglement.
Propose des optimisations qui maintiennent précision > 85% et latence < 100ms.
```

---

#### 📖 Tutoriel 2.3 : Contrats Avant Code

**Contrat type pour votre projet :**

**Exemple : Pipeline Temps Réel**

```markdown
## Contrat : Pipeline Vidéo Temps Réel

### Intent
Créer un pipeline de capture et preprocessing vidéo optimisé pour 
la reconnaissance d'émotions en temps réel, avec latence totale < 100ms.

### Success Criteria
- Capture webcam stable à 30 FPS minimum
- Preprocessing (resize, grayscale, normalize) < 10ms
- Détection de visage < 20ms
- Inférence CNN < 50ms
- Ajustement DQN < 10ms
- Affichage < 10ms
- **Latence totale : < 100ms**

### Non-Goals
- Ne pas gérer plusieurs visages simultanément (v1)
- Ne pas enregistrer les vidéos
- Ne pas optimiser pour CPU (GPU requis)

### Preserved Behavior
- Format de sortie compatible avec Streamlit
- API cohérente avec le CNN et le DQN
- Logging des métriques de performance

### Verification
- Tests de latence sur 1000 frames
- Validation sur différentes conditions d'éclairage
- Test de stabilité sur 10 minutes continues
- Benchmark GPU vs CPU

### Stop Conditions
- Si latence > 150ms → revoir l'architecture
- Si FPS < 15 → optimiser le pipeline
- Si mémoire GPU > 4GB → réduire batch size
- Si détection de visage échoue > 10% → améliorer preprocessing
```

**💡 Utilisez ce contrat avec Bob :**
```
@utils/video_pipeline.py @models/emotion_cnn.py

Implémente le pipeline vidéo temps réel selon le contrat ci-dessus.
Commence par me proposer un plan avec estimation de latence pour chaque étape.
```

---

#### 📖 Tutoriel 2.4 : Votre Première Tâche Accountable

**Tâche guidée : Créer le CNN optimisé**

**Étape 1 : Intent clair**
```
Je veux créer un CNN pour la reconnaissance d'émotions qui :
1. Prend en entrée des images 48x48 grayscale (FER-2013)
2. Classifie 7 émotions : angry, disgust, fear, happy, sad, surprise, neutral
3. Atteint une précision > 85% sur le validation set
4. Inférence < 50ms sur GPU (NVIDIA GTX 1060 ou équivalent)
5. Compatible ONNX pour déploiement

Contraintes critiques :
- Temps réel obligatoire (< 50ms)
- Pas d'overfitting (écart train/val < 10%)
- Modèle léger (< 50MB)
```

**Étape 2 : Laisser Bob explorer**
```
@data/FER2013/ @config/model_config.yaml

Bob, explore d'abord le dataset FER-2013 et ma configuration.
Dis-moi ce que tu comprends avant de proposer une architecture.
```

**Étape 3 : Lire le plan**
- ❓ Bob a-t-il compris la contrainte de latence ?
- ❓ L'architecture proposée est-elle adaptée au temps réel ?
- ❓ Les optimisations (BatchNorm, Dropout) sont-elles appropriées ?
- ❓ Le nombre de paramètres est-il raisonnable ?

**Étape 4 : Exécution et vérification**
```
Après entraînement, vérifie :
- Précision sur validation > 85%
- Latence d'inférence < 50ms (mesurée avec benchmark)
- Taille du modèle < 50MB
- Pas d'overfitting (courbes train/val)
- Export ONNX fonctionne
```

---

### Module 3 : Changements Sécurisés (2-3h)

#### 📖 Tutoriel 3.1 : Code Review comme Evidence

**Review spécifique à votre projet :**

**Avant d'intégrer le pipeline temps réel :**
```
@utils/video_pipeline.py @models/emotion_cnn.py

Bob, fais une code review de mon pipeline temps réel et identifie :
1. Les risques de performance (boucles bloquantes, copies inutiles)
2. Les problèmes de gestion mémoire (fuites, allocations répétées)
3. Les bugs potentiels (race conditions, exceptions non gérées)
4. Les violations de bonnes pratiques temps réel

Focus particulier sur :
- La gestion du flux vidéo (async vs sync)
- Les allocations mémoire dans la boucle principale
- La gestion des erreurs de capture webcam
- La synchronisation CNN → DQN
```

**💡 Checklist de review pour code temps réel :**
- [ ] Pas d'allocations mémoire dans la boucle principale
- [ ] Gestion d'erreurs robuste (webcam déconnectée, etc.)
- [ ] Pas de boucles bloquantes
- [ ] Utilisation efficace du GPU (pas de transferts CPU↔GPU inutiles)
- [ ] Logging non bloquant
- [ ] Métriques de performance instrumentées

---

#### 📖 Tutoriel 3.2 : Modernisation Sans Dérive

**Cas pratique : Optimisation du CNN**

**Situation :** Votre CNN fonctionne mais la latence est de 80ms (trop lent).

**Contrat de modernisation :**
```markdown
## Modernisation : CNN Optimisé Temps Réel

### Comportement à Préserver
- Précision identique (±2%) sur validation set
- Même format d'entrée/sortie
- Compatible avec le DQN existant

### Améliorations Souhaitées
- Latence d'inférence < 50ms (actuellement 80ms)
- Techniques : pruning, quantization, architecture plus légère
- Maintenir la précision > 85%

### Vérification
- Benchmark latence sur 1000 inférences
- Validation précision sur test set complet
- Test d'intégration avec le pipeline complet
- Vérifier que le DQN fonctionne toujours
```

**💡 Prompt Bob :**
```
@models/emotion_cnn.py @tests/benchmark.py

Optimise ce CNN pour réduire la latence de 80ms à < 50ms.
CRITIQUE : La précision doit rester > 85%.

Propose d'abord un plan avec plusieurs options :
1. Pruning (réduction des paramètres)
2. Quantization (INT8)
3. Architecture plus légère
4. Optimisations ONNX Runtime

Pour chaque option, estime l'impact sur latence et précision.
```

---

### Module 4 : Ce que Bob Ne Doit PAS Faire (1h)

#### 📖 Tutoriel 4.1 : Limites et Jugement Humain

**Décisions que VOUS devez prendre :**

❌ **Bob ne doit PAS décider :**
- Les seuils de confiance pour afficher une émotion
- Comment gérer les biais démographiques détectés
- Si une latence de 110ms est acceptable pour votre cas d'usage
- Quelles émotions sont critiques vs informatives

✅ **Vous devez décider :**
- "Ce seuil de confiance minimise-t-il les faux positifs ?"
- "Ces biais sont-ils acceptables ou dois-je rééquilibrer le dataset ?"
- "Cette latence offre-t-elle une bonne expérience utilisateur ?"
- "Cette émotion détectée est-elle crédible dans ce contexte ?"

**💡 Exemple de mauvaise utilisation :**
```
❌ "Bob, déploie le système en production et gère automatiquement 
   les cas où la confiance est faible"
   
✅ "Bob, crée un système de monitoring qui m'alerte quand la confiance 
   moyenne descend sous 80%, avec dashboard des métriques"
```

---

#### 📖 Tutoriel 4.2 : Anti-Patterns

**Anti-patterns spécifiques à votre projet :**

❌ **Anti-pattern 1 : Optimiser sans mesurer**
```
"Bob, optimise le CNN pour qu'il soit plus rapide"
→ Risque de perdre en précision sans gain mesurable
```

✅ **Bonne pratique :**
```
"Bob, crée un benchmark qui mesure latence et précision, puis propose 
des optimisations avec leur impact estimé sur ces deux métriques"
```

❌ **Anti-pattern 2 : Ignorer les biais**
```
"Bob, entraîne le CNN sur FER-2013 et c'est tout"
→ Ignore les biais démographiques potentiels
```

✅ **Bonne pratique :**
```
"Bob, analyse le dataset FER-2013 pour détecter des biais démographiques 
(âge, genre, ethnicité), puis propose des stratégies de mitigation"
```

❌ **Anti-pattern 3 : Temps réel sans profiling**
```
"Bob, crée un pipeline temps réel"
→ Pas de visibilité sur où va le temps
```

✅ **Bonne pratique :**
```
"Bob, crée un pipeline temps réel instrumenté qui mesure la latence 
de chaque étape (capture, preprocessing, inférence, ajustement, affichage)"
```

---

### Module 5 : Travail en Équipe (2-3h)

#### 📖 Tutoriel 5.1 : Bob en Équipe

**Workflow d'équipe pour votre projet :**

**Répartition des tâches :**
- **Membre 1 (DIOP)** : CNN + Optimisation temps réel
- **Membre 2 (WANDAOGO)** : Agent DQN + Fonction de récompense
- **Membre 3 (DIALLO)** : Pipeline vidéo + Interface Streamlit

**💡 Template de PR avec Bob :**
```markdown
## PR : [Composant] - [Description]

### Généré avec Bob
- [ ] Oui, Bob a aidé à générer ce code
- [ ] Non, code manuel

### Contrat Respecté
- [ ] Intent clair défini
- [ ] Success criteria validés (latence, précision)
- [ ] Tests de performance passent
- [ ] Code reviewé

### Changements
- [Liste des fichiers modifiés]
- [Impact sur la latence totale]

### Métriques de Performance
- Latence : [X]ms (objectif : < 100ms)
- Précision : [Y]% (objectif : > 85%)
- FPS : [Z] (objectif : > 10)

### Vérification
- [ ] Benchmark de latence exécuté
- [ ] Tests sur différentes conditions d'éclairage
- [ ] Pas de régression de précision
- [ ] Interface Streamlit fonctionne

### Review Bob
[Coller ici les findings de Bob si applicable]
```

---

#### 📖 Tutoriel 5.2 : Rôles dans l'Agentic SDLC

**Pour votre équipe :**

**Développeur CNN (DIOP) :**
- Utiliser Bob pour générer des architectures optimisées
- Définir des contrats de performance clairs
- Benchmarker systématiquement

**Développeur RL (WANDAOGO) :**
- Utiliser Bob pour créer l'environnement DQN
- Définir la fonction de récompense avec Bob
- Tester l'agent sur différents scénarios

**Développeur Pipeline/Interface (DIALLO) :**
- Utiliser Bob pour optimiser le pipeline vidéo
- Créer l'interface Streamlit avec Bob
- Intégrer tous les composants

---

#### 📖 Tutoriel 5.3 : Skills Personnalisés

**Skill personnalisé pour votre projet :**

Créez un skill "realtime-performance-check" :

```yaml
name: realtime-performance-check
description: Vérification des performances temps réel
trigger: /check-perf

steps:
  - Mesurer la latence de chaque étape du pipeline
  - Vérifier que latence totale < 100ms
  - Checker l'utilisation GPU (pas de saturation)
  - Valider le FPS (> 10)
  - Tester sur différentes conditions d'éclairage
  - Générer un rapport de performance
```

**💡 Utilisation :**
```
@utils/video_pipeline.py @models/emotion_cnn.py /check-perf
```

**Skill "bias-detection" :**

```yaml
name: bias-detection
description: Détection de biais démographiques
trigger: /check-bias

steps:
  - Analyser les prédictions par groupe démographique
  - Calculer les métriques de fairness
  - Identifier les biais significatifs
  - Proposer des stratégies de mitigation
  - Générer un rapport de biais
```

---

#### 📖 Tutoriel 5.4 : Mesurer Bob

**Métriques pour votre projet :**

**À mesurer :**
- ✅ Temps gagné sur l'optimisation (baseline vs avec Bob)
- ✅ Nombre d'architectures testées (avec vs sans Bob)
- ✅ Réduction de latence obtenue
- ✅ Bugs de performance détectés en review

**À NE PAS mesurer :**
- ❌ Nombre de lignes générées par Bob
- ❌ Pourcentage de code écrit par Bob
- ❌ Vitesse de développement brute

**💡 Tableau de bord suggéré :**
```markdown
## Métriques Projet Emotion-IA

### Performance Système
- Latence totale : 85ms (objectif : < 100ms) ✅
- Précision CNN : 87% (objectif : > 85%) ✅
- FPS moyen : 12 (objectif : > 10) ✅

### Développement avec Bob
- Architectures CNN testées : 8 (vs 2 sans Bob)
- Temps d'optimisation : 3h (vs 12h sans Bob)
- Bugs de performance détectés : 15

### Qualité
- Couverture de tests : 80%
- Biais détectés et corrigés : 3
- Documentation : 100% des fonctions
```

---

### Module 6 : Mindset et Pratiques Avancées (1-2h)

#### 📖 Tutoriel 6.1 : Le Mindset Bob

**Shift mental pour votre projet :**

**Avant :** "Je dois coder un CNN"  
**Après :** "Je dois concevoir un système temps réel auto-adaptatif"

**Avant :** "Je vais optimiser après si c'est trop lent"  
**Après :** "Je définis les contraintes temps réel dès le début"

**Avant :** "Je teste manuellement les paramètres vidéo"  
**Après :** "J'automatise l'ajustement avec un agent RL"

**💡 Questions à vous poser :**
- ❓ Est-ce que je pense en termes de système temps réel ou de modèle isolé ?
- ❓ Est-ce que je définis des contrats de performance avant de coder ?
- ❓ Est-ce que je mesure systématiquement la latence ?

---

#### 📖 Tutoriel 6.2 : Garder Bob Boring

**Workflows "boring" mais efficaces pour votre projet :**

**Workflow 1 : Optimisation CNN**
1. Définir le contrat (latence cible, précision minimale)
2. Bob génère 3 architectures optimisées
3. Vous benchmarkez chacune
4. Bob optimise la meilleure (pruning, quantization)
5. Vous validez en conditions réelles

**Workflow 2 : Debugging latence**
1. Identifier l'étape lente (profiling)
2. Bob analyse le code de cette étape
3. Bob propose des optimisations
4. Vous testez et mesurez l'impact
5. Bob implémente la meilleure solution

**Workflow 3 : Détection de biais**
1. Bob analyse les prédictions par groupe
2. Vous interprétez les biais détectés
3. Bob propose des stratégies de mitigation
4. Vous choisissez et testez
5. Bob implémente et valide

**💡 Gardez ces workflows simples et répétables !**

---

## 🎯 Checklist Finale pour Votre Projet

### Performance Temps Réel
- [ ] Latence totale < 100ms (mesurée sur 1000 frames)
- [ ] FPS stable > 10
- [ ] Utilisation GPU optimisée (< 80%)
- [ ] Pas de fuites mémoire sur 10 minutes

### Modèle CNN
- [ ] Précision > 85% sur validation FER-2013
- [ ] Inférence < 50ms
- [ ] Taille < 50MB
- [ ] Export ONNX fonctionnel

### Agent DQN
- [ ] Ajustements pertinents (amélioration confiance CNN)
- [ ] Convergence de l'entraînement
- [ ] Pas d'oscillations dans les ajustements
- [ ] Temps de décision < 10ms

### Pipeline Vidéo
- [ ] Capture webcam stable
- [ ] Détection de visage robuste
- [ ] Preprocessing optimisé
- [ ] Gestion d'erreurs complète

### Interface Streamlit
- [ ] Affichage temps réel fluide
- [ ] Visualisation des émotions claire
- [ ] Affichage des ajustements DQN
- [ ] Métriques de performance visibles

### Qualité et Biais
- [ ] Tests sur différentes conditions d'éclairage
- [ ] Analyse de biais démographiques effectuée
- [ ] Stratégies de mitigation implémentées
- [ ] Documentation des limites

### Code et Tests
- [ ] Tests unitaires pour chaque composant
- [ ] Benchmarks de performance automatisés
- [ ] Code reviewé (par Bob et humains)
- [ ] Documentation complète

---

## 💡 Prompts Bob Prêts à l'Emploi

### Démarrage du projet
```
Je démarre un projet de reconnaissance d'émotions temps réel combinant 
CNN et DQN. Crée la structure de projet avec :
- Architecture CNN optimisée pour latence < 50ms
- Pipeline vidéo temps réel
- Agent DQN pour ajustement adaptatif
- Interface Streamlit
- Benchmarks de performance
```

### Architecture CNN optimisée
```
@data/FER2013/ @config/model_config.yaml

Crée une architecture CNN pour reconnaissance d'émotions optimisée 
pour le temps réel :
- Input : 48x48 grayscale
- Output : 7 émotions
- Contrainte : inférence < 50ms sur GPU
- Précision cible : > 85%
- Techniques : Conv + BatchNorm + Dropout
- Optimisations : pruning, quantization si nécessaire
```

### Pipeline vidéo temps réel
```
@utils/video_pipeline.py @models/emotion_cnn.py

Crée un pipeline vidéo temps réel qui :
1. Capture webcam à 30 FPS
2. Détecte les visages (MTCNN ou Haar Cascade)
3. Préprocesse pour le CNN (resize, normalize)
4. Inférence CNN
5. Passe le résultat au DQN
6. Applique les ajustements
7. Affiche le résultat

Contrainte : latence totale < 100ms
Instrumentation : mesurer chaque étape
```

### Agent DQN pour ajustement
```
@agents/video_adjuster.py @models/emotion_cnn.py

Crée un agent DQN qui ajuste dynamiquement les paramètres vidéo :
- État : confiance CNN + histogramme de l'image
- Actions : ajuster contraste [-20, +20], exposition [-20, +20]
- Récompense : amélioration de la confiance CNN
- Environnement : Gymnasium custom
- Algorithme : DQN avec experience replay

Objectif : maximiser la confiance du CNN en ajustant les paramètres vidéo
```

### Interface Streamlit
```
@app/streamlit_app.py @models/ @agents/

Crée une interface Streamlit temps réel qui affiche :
1. Flux vidéo webcam avec émotion détectée
2. Barre de confiance pour chaque émotion
3. Graphique temps réel de la confiance
4. Ajustements DQN appliqués (contraste, exposition)
5. Métriques de performance (FPS, latence)
6. Bouton pour démarrer/arrêter la capture

Design : interface claire et responsive
```

### Benchmark de performance
```
@tests/benchmark.py @models/ @utils/

Crée un script de benchmark qui mesure :
1. Latence de chaque étape du pipeline
2. Latence totale sur 1000 frames
3. FPS moyen et écart-type
4. Utilisation GPU (mémoire, compute)
5. Précision du CNN sur test set

Génère un rapport avec :
- Graphiques de distribution de latence
- Identification des goulots d'étranglement
- Recommandations d'optimisation
```

### Détection de biais
```
@models/emotion_cnn.py @data/FER2013/

Analyse le modèle CNN pour détecter des biais démographiques :
1. Évaluer la précision par groupe (si métadonnées disponibles)
2. Analyser les erreurs systématiques
3. Identifier les émotions problématiques
4. Proposer des stratégies de mitigation :
   - Rééquilibrage du dataset
   - Data augmentation ciblée
   - Fine-tuning sur sous-groupes

Génère un rapport de fairness avec recommandations
```

### Optimisation ONNX
```
@models/emotion_cnn.py

Optimise le modèle CNN pour le déploiement :
1. Export en ONNX
2. Optimisations ONNX Runtime (graph optimization, quantization)
3. Benchmark latence ONNX vs PyTorch
4. Validation que la précision est préservée

Objectif : réduire la latence de 20-30% sans perte de précision
```

---

## 📚 Ressources Complémentaires

### Pour la Vision par Ordinateur Temps Réel
- "Real-Time Computer Vision with OpenCV" - Practical Guide
- Papers sur CNN optimisés (MobileNet, EfficientNet, SqueezeNet)
- ONNX Runtime documentation pour optimisations

### Pour le Reinforcement Learning
- "Deep Reinforcement Learning Hands-On" - Maxim Lapan
- Papers sur DQN et variantes (Double DQN, Dueling DQN)
- Stable Baselines3 documentation

### Pour la Détection de Biais
- "Fairness in Machine Learning" - Solon Barocas et al.
- Papers sur bias detection et mitigation
- Fairlearn library documentation

### Pour Bob
- Tutoriels du parcours pédagogique
- Documentation IBM Bob
- Communauté Bob

---

## 🎓 Évaluation de Votre Utilisation de Bob

### Critères de Succès

**Utilisation Efficace de Bob (40%) :**
- [ ] Contrats de performance clairs définis
- [ ] Context management approprié (focus temps réel)
- [ ] Reviews systématiques du code généré
- [ ] Benchmarks automatisés avec Bob

**Qualité Technique (40%) :**
- [ ] Latence < 100ms atteinte
- [ ] Précision > 85% maintenue
- [ ] Pipeline robuste et optimisé
- [ ] Biais détectés et mitigés

**Collaboration et Documentation (20%) :**
- [ ] Workflow d'équipe clair
- [ ] Documentation complète
- [ ] Partage des learnings
- [ ] Interface utilisateur fonctionnelle

---

**Bonne chance avec votre projet Emotion-IA ! 🚀😊**

*N'oubliez pas : Le temps réel est impitoyable. Mesurez tout, optimisez avec méthode, et laissez Bob vous aider à identifier les goulots d'étranglement !*