---
layout: default
title: Fiche Projet - SmartFlow
---

# Fiche Projet : SmartFlow
## Guide d'Utilisation de Bob pour Votre Projet

**Équipe :** VOLCY, GUIRAUDEN  
**Domaine :** Vision par ordinateur + RL pour gestion de trafic urbain  
**Technologies :** YOLO/Faster R-CNN, PPO, SUMO, Dashboard web

---

## 🎯 Vue d'Ensemble du Projet

### ⏰ Contrainte Temporelle Critique
**Deadline : 5 juin 2026** (environ 1 mois)

Ce projet doit être **terminé en 4 semaines maximum**. Cette contrainte impose :
- ✅ Priorisation stricte des fonctionnalités (MVP d'abord)
- ✅ Utilisation intensive de Bob pour accélérer le développement
- ✅ Focus sur les composants essentiels, pas la perfection
- ✅ Itérations rapides avec validation continue

**Stratégie recommandée :**
- **Semaine 1** : Setup SUMO + Détection YOLO de base + Environnement Gymnasium
- **Semaine 2** : Agent PPO + Fonction de récompense multi-objectifs
- **Semaine 3** : Intégration DL→RL + Scénarios (urgences, accidents)
- **Semaine 4** : Dashboard, métriques, tests, documentation

### Objectif
Concevoir un agent intelligent capable de percevoir son environnement via des flux vidéo (Deep Learning) et de prendre des décisions optimales en temps réel (Reinforcement Learning) pour fluidifier le trafic à une intersection complexe.

### Composants Principaux
1. **Détection d'objets (YOLO/Faster R-CNN)** : Identification et classification des véhicules
2. **Agent RL (PPO)** : Optimisation des feux de signalisation
3. **Simulation SUMO** : Environnement de trafic urbain réaliste
4. **Dashboard web** : Visualisation temps réel et métriques

### Vos Attentes vis-à-vis de Bob
- Puissance de calcul GPU pour entraînement intensif
- Gestion de modèles (MLflow/Watson Studio)
- Facilité de déploiement (API + dashboard)
- Feedback sur intégration des bibliothèques RL

---

## 📚 Parcours Pédagogique Adapté à Votre Projet

### Module 1 : Fondamentaux (2-3h)

#### 📖 Tutoriel 1.1 : Introduction à IBM Bob

**Questions spécifiques à votre projet :**

❓ **Quels sont les 3 cas d'usage Bob les plus pertinents pour mon projet de trafic urbain ?**
- Intégration YOLO → Environnement Gymnasium → Agent PPO
- Création du wrapper SUMO pour Gymnasium
- Développement du dashboard de visualisation temps réel

❓ **Où Bob peut-il m'aider le plus dans un projet de gestion de trafic ?**
- Architecture du pipeline (Détection → État → Décision → Action)
- Définition de la fonction de récompense multi-objectifs
- Intégration avec SUMO (complexe)
- Création des visualisations et métriques

❓ **Où le jugement humain est-il critique dans mon projet ?**
- Définition des priorités (temps d'attente vs émissions vs urgences)
- Validation que les décisions de l'agent sont sûres
- Interprétation des métriques urbaines
- Décision sur les scénarios de test (accidents, urgences)

**💡 Prompt Bob suggéré :**
```
Je travaille sur un système de gestion intelligente du trafic urbain combinant :
- YOLO pour détecter et classifier les véhicules depuis caméras
- SUMO pour simuler le trafic urbain
- PPO pour optimiser les feux de signalisation
- Dashboard web pour visualisation temps réel

Aide-moi à structurer l'architecture avec :
- Wrapper Gymnasium pour SUMO
- Intégration YOLO → État RL
- Agent PPO multi-objectifs (temps d'attente, émissions, urgences)
```

---

#### 📖 Tutoriel 1.2 : Le Cycle de Vie Agentique

**Application à votre projet :**

**Phase ORIENT** - Comprendre avant de coder
- ❓ Comment YOLO doit-il communiquer avec l'environnement SUMO ?
- ❓ Quelle est la fréquence de décision optimale (chaque seconde ? 5 secondes ?) ?
- ❓ Comment modéliser l'état pour l'agent RL (matrice de densité ? files d'attente ?) ?

**💡 Utilisez Bob pour :**
```
Analyse l'architecture SmartFlow et identifie :
1. Le flux de données : Caméras → YOLO → État → Agent → SUMO
2. Les points de synchronisation critiques
3. Comment définir l'espace d'états (densité, vitesse, types de véhicules)
4. Comment définir l'espace d'actions (durée des phases, ordre)
```

**Phase BOUND** - Définir les contraintes
- ❓ Contrainte de sécurité : pas de changements trop fréquents (min 5s par phase)
- ❓ Contrainte de réalisme : respecter les règles de circulation
- ❓ Contrainte de performance : décision en temps réel (< 1s)
- ❓ Contrainte multi-objectifs : équilibrer temps d'attente, émissions, urgences

**Phase PLAN** - Planifier avant d'exécuter
- ❓ Ordre de développement : SUMO seul → YOLO seul → Intégration → Agent RL ?
- ❓ Comment tester chaque composant indépendamment ?
- ❓ Quelles baselines pour comparer (feux fixes, feux adaptatifs simples) ?

**💡 Prompt Bob suggéré :**
```
Crée un plan de développement pour SmartFlow :
1. Ordre de développement (SUMO wrapper, YOLO, intégration, RL)
2. Points de validation à chaque étape
3. Baselines à implémenter (feux fixes, actuated traffic lights)
4. Stratégie de test (scénarios simples → complexes)

Contrainte : architecture modulaire permettant de tester sans YOLO (état simulé)
```

---

#### 📖 Tutoriel 1.3 : Comment Bob Pense

**Intent, Evidence, Judgment pour votre projet :**

**INTENT** - Ce que vous voulez accomplir
- ❓ Mon intent est-il clair ? "Optimiser le trafic" vs "Créer un système qui réduit le temps d'attente moyen de 30% tout en priorisant les véhicules d'urgence et en réduisant les émissions de 15%"
- ❓ Ai-je défini les critères de succès ? (Temps d'attente, débit, émissions, sécurité)

**EVIDENCE** - Les faits que Bob collecte
- ❓ Quels fichiers Bob doit-il lire pour comprendre mon architecture ?
- ❓ Ai-je fourni des exemples de configurations SUMO ?
- ❓ Bob comprend-il la structure de l'espace d'états et d'actions ?

**JUDGMENT** - Votre décision finale
- ❓ Est-ce que je comprends pourquoi Bob suggère cette fonction de récompense ?
- ❓ Les décisions de l'agent sont-elles sûres et réalistes ?
- ❓ L'intégration YOLO → SUMO est-elle robuste ?

**💡 Exercice pratique :**
```
Demande à Bob d'analyser ta fonction de récompense et de suggérer des améliorations.

Avant d'accepter, vérifie :
- Les objectifs sont-ils bien équilibrés (temps vs émissions vs urgences) ?
- Les pénalités sont-elles appropriées (changements trop fréquents) ?
- La récompense guide-t-elle vers des comportements sûrs ?
- Comprends-tu l'impact de chaque terme ?
```

---

#### 📖 Tutoriel 1.4 : La Transition des Habitudes

**Habitudes à changer pour votre projet :**

**Avant (habitudes traditionnelles) :**
- Coder directement sans comprendre SUMO
- Tester manuellement différentes stratégies de feux
- Optimiser sans baseline de comparaison

**Après (habitudes agentiques) :**
- Définir des contrats clairs pour chaque composant
- Laisser Bob générer le wrapper SUMO
- Automatiser les comparaisons avec baselines

**💡 Plan de transition pour votre équipe :**

**Semaine 1-2 : SUMO et Environnement**
- Utilisez Bob pour créer le wrapper Gymnasium pour SUMO
- Définissez l'espace d'états et d'actions
- Testez avec un agent aléatoire

**Semaine 3-4 : Détection YOLO**
- Bob aide à intégrer YOLO (pré-entraîné ou fine-tuné)
- Vous testez la détection sur vidéos de trafic
- Bob crée le pont YOLO → État RL

**Semaine 5-6 : Agent RL**
- Bob implémente l'agent PPO
- Vous définissez la fonction de récompense multi-objectifs
- Bob optimise l'agent

**Semaine 7-8 : Scénarios Complexes**
- Bob ajoute les événements (accidents, urgences)
- Vous testez la robustesse
- Bob aide au debugging

**Semaine 9-10 : Dashboard et Finalisation**
- Bob génère le dashboard web
- Vous validez les visualisations
- Documentation et démo

---

### Module 2 : Prise en Main (3-4h)

#### 📖 Tutoriel 2.1 : L'Interface Bob

**Configuration pour votre projet :**

**Context Mentions essentiels :**
```
@envs/sumo_env.py              # Wrapper SUMO pour Gymnasium
@models/yolo_detector.py       # Détection YOLO
@agents/traffic_agent.py       # Agent PPO
@utils/reward_function.py      # Fonction de récompense
@config/sumo_config.yaml       # Configuration SUMO
@dashboard/app.py              # Dashboard web
```

**💡 Première tâche avec Bob :**
```
@envs/sumo_env.py @config/sumo_config.yaml

Crée un wrapper Gymnasium pour SUMO qui :
1. Lance la simulation SUMO
2. Définit l'espace d'observation (densité par voie, vitesse moyenne, files d'attente)
3. Définit l'espace d'actions (durée phase verte pour chaque direction)
4. Calcule la récompense (temps d'attente, débit, émissions)
5. Gère les épisodes (reset, step)

Contraintes :
- Compatible avec Stable Baselines3
- Décision toutes les 5 secondes (configurable)
- Logging des métriques SUMO
```

---

#### 📖 Tutoriel 2.2 : Gestion du Contexte ⭐ CRITIQUE

**Contexte spécifique à votre projet urbain :**

**Signal (à inclure) :**
- ✅ Wrapper SUMO (envs/sumo_env.py)
- ✅ Détecteur YOLO (models/yolo_detector.py)
- ✅ Agent RL (agents/traffic_agent.py)
- ✅ Fonction de récompense (utils/reward_function.py)
- ✅ Configuration (config/)
- ✅ Scripts de scénarios (scenarios/)

**Noise (à exclure) :**
- ❌ Fichiers SUMO volumineux (.net.xml, .rou.xml complets)
- ❌ Checkpoints de modèles entraînés
- ❌ Logs de simulation SUMO
- ❌ Vidéos de trafic
- ❌ Résultats d'expériences passées

**💡 Context Pack pour votre projet :**

Créez un fichier `.bobcontext` :
```yaml
# Context Pack - Projet SmartFlow
include:
  - envs/**/*.py
  - models/**/*.py
  - agents/**/*.py
  - utils/**/*.py
  - config/*.yaml
  - scenarios/*.py
  - dashboard/*.py
  - README.md
  
exclude:
  - data/sumo/**/*.xml
  - models/checkpoints/**
  - logs/**
  - videos/**
  - results/**
  
priority_files:
  - envs/sumo_env.py
  - agents/traffic_agent.py
  - utils/reward_function.py
  - config/sumo_config.yaml
```

**❓ Questions de grounding :**
- Avant chaque tâche : "Bob, as-tu lu ma configuration SUMO ?"
- Après modification : "Bob, confirme que l'intégration YOLO → SUMO fonctionne"
- En cas de doute : "Bob, montre-moi le flux de données complet"

**💡 Gestion du contexte pour intégration complexe :**
```
Pour les modifications d'intégration, toujours inclure :
@envs/sumo_env.py @models/yolo_detector.py @agents/traffic_agent.py

Bob, analyse le pipeline complet et identifie les points de couplage.
Propose des améliorations pour rendre l'intégration plus robuste.
```

---

#### 📖 Tutoriel 2.3 : Contrats Avant Code

**Contrat type pour votre projet :**

**Exemple : Fonction de Récompense Multi-Objectifs**

```markdown
## Contrat : Fonction de Récompense SmartFlow

### Intent
Créer une fonction de récompense qui optimise simultanément :
1. Temps d'attente moyen des véhicules
2. Débit de l'intersection (véhicules/heure)
3. Émissions de CO2
4. Priorisation des véhicules d'urgence

### Success Criteria
- Réduction temps d'attente : -30% vs feux fixes
- Augmentation débit : +20% vs feux fixes
- Réduction émissions : -15% vs feux fixes
- Temps de réponse urgences : < 30s
- Pas de famine (aucune voie bloquée > 2 minutes)

### Non-Goals
- Ne pas optimiser pour plusieurs intersections (v1)
- Ne pas gérer les piétons (v1)
- Ne pas optimiser pour conditions météo

### Preserved Behavior
- Respect des contraintes de sécurité (durée min/max phases)
- Logging de toutes les composantes de la récompense
- Compatible avec PPO et autres algos RL

### Verification
- Tests sur scénarios synthétiques (trafic léger, moyen, dense)
- Validation que chaque objectif est pris en compte
- Test de priorisation des urgences
- Vérification absence de famine

### Stop Conditions
- Si un objectif domine complètement les autres → revoir les poids
- Si l'agent ne converge pas → simplifier la récompense
- Si comportements dangereux → ajouter des pénalités
```

**💡 Utilisez ce contrat avec Bob :**
```
@utils/reward_function.py @envs/sumo_env.py

Implémente la fonction de récompense multi-objectifs selon le contrat ci-dessus.
Commence par me proposer plusieurs formulations avec leurs avantages/inconvénients.
```

---

#### 📖 Tutoriel 2.4 : Votre Première Tâche Accountable

**Tâche guidée : Créer le wrapper SUMO**

**Étape 1 : Intent clair**
```
Je veux créer un wrapper Gymnasium pour SUMO qui :
1. Lance une simulation SUMO d'une intersection à 4 voies
2. Observe : densité par voie, vitesse moyenne, longueur files d'attente
3. Agit : ajuster la durée des phases vertes (5-60 secondes)
4. Récompense : combinaison temps d'attente, débit, émissions
5. Épisode : 1 heure de simulation (3600 secondes)

Contraintes critiques :
- Compatible Stable Baselines3
- Décision toutes les 5 secondes
- Gestion propre du processus SUMO (pas de zombies)
- Logging des métriques SUMO
```

**Étape 2 : Laisser Bob explorer**
```
@config/sumo_config.yaml @scenarios/

Bob, explore d'abord ma configuration SUMO et mes scénarios.
Dis-moi ce que tu comprends de la structure avant de proposer le wrapper.
```

**Étape 3 : Lire le plan**
- ❓ Bob a-t-il compris la structure de SUMO (TraCI) ?
- ❓ L'espace d'observation est-il bien défini ?
- ❓ L'espace d'actions est-il réaliste ?
- ❓ La gestion du processus SUMO est-elle robuste ?

**Étape 4 : Exécution et vérification**
```
Après implémentation, vérifie :
- Le wrapper est compatible avec Stable Baselines3
- SUMO se lance et se ferme proprement
- Les observations sont cohérentes
- Les actions sont appliquées correctement
- La récompense est calculée
- Les épisodes se terminent proprement
```

---

### Module 3 : Changements Sécurisés (2-3h)

#### 📖 Tutoriel 3.1 : Code Review comme Evidence

**Review spécifique à votre projet :**

**Avant d'intégrer l'agent RL :**
```
@agents/traffic_agent.py @utils/reward_function.py

Bob, fais une code review de l'agent de trafic et identifie :
1. Les risques de sécurité (décisions dangereuses, changements trop fréquents)
2. Les problèmes de performance (goulots d'étranglement)
3. Les bugs potentiels (gestion d'erreurs SUMO, états invalides)
4. Les violations de bonnes pratiques RL

Focus particulier sur :
- La fonction de récompense (équilibre des objectifs)
- La gestion des véhicules d'urgence
- Les contraintes de sécurité (durée min/max phases)
- La robustesse face aux scénarios extrêmes
```

**💡 Checklist de review pour code de trafic urbain :**
- [ ] Respect des contraintes de sécurité (durée phases)
- [ ] Priorisation des urgences fonctionnelle
- [ ] Pas de famine (toutes les voies sont servies)
- [ ] Gestion d'erreurs SUMO robuste
- [ ] Métriques urbaines correctes (temps d'attente, émissions)
- [ ] Logging complet pour analyse

---

#### 📖 Tutoriel 3.2 : Modernisation Sans Dérive

**Cas pratique : Amélioration de la fonction de récompense**

**Situation :** Votre fonction de récompense fonctionne mais ne priorise pas assez les urgences.

**Contrat de modernisation :**
```markdown
## Modernisation : Priorisation des Urgences

### Comportement à Préserver
- Performance globale identique (temps d'attente, débit, émissions)
- Pas de régression sur scénarios sans urgences

### Améliorations Souhaitées
- Détection automatique des véhicules d'urgence (via YOLO ou SUMO)
- Bonus de récompense important pour passage rapide
- Pénalité si urgence bloquée > 30s
- Métriques spécifiques aux urgences

### Vérification
- Tester sur scénarios avec urgences
- Vérifier que temps de passage < 30s
- Valider que performance globale est préservée
- Comparer avec baseline (sans priorisation)
```

**💡 Prompt Bob :**
```
@utils/reward_function.py @agents/traffic_agent.py

Améliore la fonction de récompense pour mieux prioriser les urgences.
CRITIQUE : La performance globale doit être préservée.

Propose d'abord un plan avec :
1. Détection des urgences (YOLO ou SUMO)
2. Modification de la récompense
3. Stratégie de validation
```

---

### Module 4 : Ce que Bob Ne Doit PAS Faire (1h)

#### 📖 Tutoriel 4.1 : Limites et Jugement Humain

**Décisions que VOUS devez prendre :**

❌ **Bob ne doit PAS décider :**
- Les poids de la fonction de récompense (temps vs émissions vs urgences)
- Les seuils de sécurité (durée min/max des phases)
- L'interprétation des métriques urbaines
- Si un comportement de l'agent est acceptable en conditions réelles

✅ **Vous devez décider :**
- "Ces poids reflètent-ils les priorités de la ville ?"
- "Ces décisions de l'agent sont-elles sûres ?"
- "Ces métriques montrent-elles une vraie amélioration ?"
- "Ce comportement est-il acceptable pour les usagers ?"

**💡 Exemple de mauvaise utilisation :**
```
❌ "Bob, déploie l'agent sur une vraie intersection"
→ Risque de décisions dangereuses

✅ "Bob, crée un système de simulation et de validation exhaustive 
   avant tout déploiement réel, avec monitoring humain continu"
```

---

#### 📖 Tutoriel 4.2 : Anti-Patterns

**Anti-patterns spécifiques à votre projet :**

❌ **Anti-pattern 1 : Optimiser un seul objectif**
```
"Bob, maximise le débit de l'intersection"
→ Risque de négliger les émissions et les urgences
```

✅ **Bonne pratique :**
```
"Bob, crée une fonction de récompense multi-objectifs avec :
- Temps d'attente (poids 0.4)
- Débit (poids 0.3)
- Émissions (poids 0.2)
- Urgences (poids 0.1)
Et permet d'ajuster ces poids facilement"
```

❌ **Anti-pattern 2 : Pas de baseline**
```
"Bob, entraîne l'agent RL et c'est tout"
→ Impossible de savoir si c'est mieux que des feux fixes
```

✅ **Bonne pratique :**
```
"Bob, implémente 3 baselines :
1. Feux fixes (cycles prédéfinis)
2. Actuated traffic lights (détection simple)
3. Agent RL
Et compare leurs performances sur les mêmes scénarios"
```

❌ **Anti-pattern 3 : Ignorer les cas extrêmes**
```
"Bob, teste sur un scénario de trafic moyen"
→ Pas de robustesse face aux situations exceptionnelles
```

✅ **Bonne pratique :**
```
"Bob, crée des scénarios de test variés :
1. Trafic léger (nuit)
2. Trafic moyen (journée normale)
3. Trafic dense (heure de pointe)
4. Accident bloquant une voie
5. Passage de véhicules d'urgence
6. Événement spécial (match, concert)"
```

---

### Module 5 : Travail en Équipe (2-3h)

#### 📖 Tutoriel 5.1 : Bob en Équipe

**Workflow d'équipe pour votre projet :**

**Répartition des tâches :**
- **Membre 1 (VOLCY)** : SUMO + Agent RL
- **Membre 2 (GUIRAUDEN)** : YOLO + Dashboard

**💡 Template de PR avec Bob :**
```markdown
## PR : [Composant] - [Description]

### Généré avec Bob
- [ ] Oui, Bob a aidé à générer ce code
- [ ] Non, code manuel

### Contrat Respecté
- [ ] Intent clair défini
- [ ] Success criteria validés (métriques urbaines)
- [ ] Tests sur scénarios variés passent
- [ ] Code reviewé

### Changements
- [Liste des fichiers modifiés]
- [Impact sur les métriques]

### Métriques Urbaines
- Temps d'attente : [X]s (objectif : -30% vs baseline)
- Débit : [Y] véh/h (objectif : +20% vs baseline)
- Émissions : [Z] kg CO2 (objectif : -15% vs baseline)

### Vérification
- [ ] Tests sur trafic léger, moyen, dense
- [ ] Test avec véhicules d'urgence
- [ ] Pas de famine (toutes voies servies)
- [ ] Dashboard affiche correctement

### Review Bob
[Coller ici les findings de Bob si applicable]
```

---

#### 📖 Tutoriel 5.2 : Rôles dans l'Agentic SDLC

**Pour votre équipe :**

**Développeur SUMO/RL (VOLCY) :**
- Utiliser Bob pour créer le wrapper SUMO
- Définir la fonction de récompense avec Bob
- Entraîner et optimiser l'agent

**Développeur Vision/Dashboard (GUIRAUDEN) :**
- Utiliser Bob pour intégrer YOLO
- Créer le dashboard avec Bob
- Visualiser les métriques

---

#### 📖 Tutoriel 5.3 : Skills Personnalisés

**Skill personnalisé pour votre projet :**

Créez un skill "traffic-scenario-test" :

```yaml
name: traffic-scenario-test
description: Tester l'agent sur différents scénarios de trafic
trigger: /test-traffic

steps:
  - Lancer SUMO avec le scénario spécifié
  - Exécuter l'agent pendant 1 heure simulée
  - Collecter les métriques (temps d'attente, débit, émissions)
  - Comparer avec baseline (feux fixes)
  - Générer un rapport avec visualisations
```

**💡 Utilisation :**
```
@agents/traffic_agent.py /test-traffic

Scénario : "rush_hour"
Baseline : "fixed_lights"
```

**Skill "urban-metrics-report" :**

```yaml
name: urban-metrics-report
description: Générer un rapport complet des métriques urbaines
trigger: /urban-report

steps:
  - Analyser les logs SUMO
  - Calculer temps d'attente moyen, débit, émissions
  - Comparer avec baselines
  - Générer graphiques temporels
  - Créer rapport markdown avec recommandations
```

---

#### 📖 Tutoriel 5.4 : Mesurer Bob

**Métriques pour votre projet :**

**À mesurer :**
- ✅ Temps gagné sur l'intégration SUMO (avec vs sans Bob)
- ✅ Nombre de scénarios testés
- ✅ Amélioration des métriques urbaines
- ✅ Bugs détectés en review

**À NE PAS mesurer :**
- ❌ Nombre de lignes générées par Bob
- ❌ Pourcentage de code écrit par Bob
- ❌ Vitesse de développement brute

**💡 Tableau de bord suggéré :**
```markdown
## Métriques Projet SmartFlow

### Performance Urbaine
- Temps d'attente : -35% vs feux fixes ✅
- Débit : +25% vs feux fixes ✅
- Émissions : -18% vs feux fixes ✅
- Temps réponse urgences : 22s (objectif : < 30s) ✅

### Développement avec Bob
- Temps d'intégration SUMO : 2 jours (vs 7 jours sans Bob)
- Scénarios testés : 12 (vs 3 sans Bob)
- Bugs détectés : 18

### Qualité
- Couverture de tests : 85%
- Documentation : 100%
- Baselines implémentées : 3
```

---

### Module 6 : Mindset et Pratiques Avancées (1-2h)

#### 📖 Tutoriel 6.1 : Le Mindset Bob

**Shift mental pour votre projet :**

**Avant :** "Je dois coder un agent RL"  
**Après :** "Je dois concevoir un système de gestion urbaine intelligente"

**Avant :** "Je vais optimiser le temps d'attente"  
**Après :** "Je vais équilibrer plusieurs objectifs urbains"

**Avant :** "Je teste sur un scénario simple"  
**Après :** "Je teste sur des scénarios variés et réalistes"

**💡 Questions à vous poser :**
- ❓ Est-ce que je pense en termes de système urbain ou de code isolé ?
- ❓ Est-ce que je considère tous les objectifs (temps, émissions, urgences) ?
- ❓ Est-ce que je teste sur des scénarios réalistes ?

---

#### 📖 Tutoriel 6.2 : Garder Bob Boring

**Workflows "boring" mais efficaces pour votre projet :**

**Workflow 1 : Nouveau scénario**
1. Définir le scénario (trafic, événements)
2. Bob génère la configuration SUMO
3. Vous lancez la simulation
4. Bob génère les métriques
5. Vous analysez et ajustez

**Workflow 2 : Amélioration récompense**
1. Identifier le problème (ex: urgences pas assez prioritaires)
2. Bob propose des modifications
3. Vous testez sur scénarios
4. Bob compare avec version précédente
5. Vous validez ou itérez

**Workflow 3 : Debugging comportement**
1. Identifier le comportement anormal
2. Bob instrumente le code
3. Vous collectez les données
4. Bob visualise
5. Vous identifiez la cause

**💡 Gardez ces workflows simples et répétables !**

---

## 🎯 Checklist Finale pour Votre Projet

### Environnement SUMO
- [ ] Wrapper Gymnasium fonctionnel
- [ ] Espace d'observation bien défini
- [ ] Espace d'actions réaliste
- [ ] Gestion propre du processus SUMO

### Détection YOLO
- [ ] Détection de véhicules fonctionnelle
- [ ] Classification (voiture, camion, bus, urgence)
- [ ] Intégration avec SUMO
- [ ] Performance acceptable (FPS)

### Agent RL
- [ ] PPO entraîné et convergent
- [ ] Fonction de récompense multi-objectifs
- [ ] Priorisation des urgences
- [ ] Pas de famine

### Métriques Urbaines
- [ ] Temps d'attente : -30% vs baseline
- [ ] Débit : +20% vs baseline
- [ ] Émissions : -15% vs baseline
- [ ] Temps réponse urgences : < 30s

### Scénarios de Test
- [ ] Trafic léger, moyen, dense
- [ ] Accidents simulés
- [ ] Véhicules d'urgence
- [ ] Événements spéciaux

### Dashboard
- [ ] Visualisation temps réel SUMO
- [ ] Métriques affichées
- [ ] Comparaison avec baselines
- [ ] Interface intuitive

### Code et Documentation
- [ ] Tests pour chaque composant
- [ ] Code reviewé (par Bob et humains)
- [ ] Documentation complète
- [ ] Baselines implémentées

---

## 💡 Prompts Bob Prêts à l'Emploi

### Démarrage du projet
```
Je démarre un projet de gestion intelligente du trafic urbain combinant 
YOLO, SUMO et RL. Crée la structure de projet avec :
- Wrapper Gymnasium pour SUMO
- Intégration YOLO pour détection
- Agent PPO multi-objectifs
- Dashboard web de visualisation
- Scripts de scénarios de test
```

### Wrapper SUMO
```
@config/sumo_config.yaml @scenarios/

Crée un wrapper Gymnasium pour SUMO :
- Observation : densité par voie, vitesse, files d'attente
- Action : durée phases vertes (5-60s)
- Récompense : temps d'attente + débit + émissions
- Épisode : 1 heure de simulation
- Décision : toutes les 5 secondes

Contraintes :
- Compatible Stable Baselines3
- Gestion propre du processus SUMO
- Logging des métriques
```

### Fonction de récompense multi-objectifs
```
@utils/reward_function.py @envs/sumo_env.py

Crée une fonction de récompense qui optimise :
1. Temps d'attente moyen (poids 0.4)
2. Débit de l'intersection (poids 0.3)
3. Émissions de CO2 (poids 0.2)
4. Priorisation urgences (poids 0.1)

Contraintes :
- Normalisation appropriée de chaque terme
- Pénalité pour changements trop fréquents
- Bonus pour passage rapide des urgences
- Logging de chaque composante
```

### Intégration YOLO
```
@models/yolo_detector.py @envs/sumo_env.py

Intègre YOLO pour détecter les véhicules :
1. Charger modèle YOLO pré-entraîné (ou fine-tuné)
2. Détecter et classifier (voiture, camion, bus, urgence)
3. Convertir détections en état pour l'agent RL
4. Synchroniser avec SUMO

Options :
- Utiliser caméras virtuelles SUMO
- Ou simuler les détections depuis SUMO directement (v1)
```

### Agent PPO
```
@agents/traffic_agent.py @utils/reward_function.py

Crée un agent PPO pour optimiser les feux :
- Algorithme : PPO (Stable Baselines3)
- Réseau : MLP (2 couches de 64 neurones)
- Hyperparamètres : learning_rate=3e-4, n_steps=2048
- Entraînement : 1M steps

Contraintes :
- Respect des durées min/max des phases
- Logging des métriques urbaines
- Checkpoints réguliers
```

### Scénarios de test
```
@scenarios/ @config/

Crée des scénarios SUMO variés :
1. Trafic léger (100 véh/h)
2. Trafic moyen (500 véh/h)
3. Trafic dense (1000 véh/h)
4. Accident bloquant une voie
5. Passage de 3 véhicules d'urgence
6. Événement spécial (2000 véh/h)

Pour chaque scénario :
- Fichier .rou.xml (routes)
- Configuration SUMO
- Script de lancement
```

### Dashboard web
```
@dashboard/app.py @agents/ @envs/

Crée un dashboard web (Flask ou Streamlit) qui affiche :
1. Visualisation SUMO en temps réel
2. Métriques actuelles (temps d'attente, débit, émissions)
3. Graphiques temporels des métriques
4. Comparaison avec baselines (feux fixes, actuated)
5. Contrôles (démarrer, arrêter, changer scénario)

Design : interface claire et professionnelle
```

### Baselines
```
@baselines/ @envs/

Implémente 3 baselines pour comparaison :
1. Feux fixes : cycles prédéfinis (30s vert, 5s jaune, 30s rouge)
2. Actuated lights : détection simple (prolonge vert si véhicules)
3. Agent RL : notre solution

Pour chaque baseline :
- Même interface que l'agent RL
- Logging des mêmes métriques
- Script de comparaison automatique
```

---

## 📚 Ressources Complémentaires

### Pour SUMO
- SUMO Documentation officielle
- TraCI (Traffic Control Interface) guide
- Papers sur traffic light optimization

### Pour le RL en Trafic Urbain
- "Deep Reinforcement Learning for Traffic Light Control" papers
- "Multi-Agent RL for Traffic Signal Control"
- Stable Baselines3 documentation

### Pour la Vision par Ordinateur
- YOLO documentation
- Papers sur vehicle detection and classification
- UA-DETRAC dataset

### Pour Bob
- Tutoriels du parcours pédagogique
- Documentation IBM Bob
- Communauté Bob

---

## 🎓 Évaluation de Votre Utilisation de Bob

### Critères de Succès

**Utilisation Efficace de Bob (40%) :**
- [ ] Contrats clairs pour chaque composant
- [ ] Context management approprié (focus intégration)
- [ ] Reviews systématiques du code généré
- [ ] Baselines implémentées avec Bob

**Qualité Technique (40%) :**
- [ ] Intégration SUMO robuste
- [ ] Fonction de récompense équilibrée
- [ ] Métriques urbaines améliorées
- [ ] Scénarios variés testés

**Impact Urbain et Documentation (20%) :**
- [ ] Amélioration mesurable du trafic
- [ ] Dashboard fonctionnel
- [ ] Documentation complète
- [ ] Présentation convaincante

---

**Bonne chance avec votre projet SmartFlow ! 🚀🚦**

*N'oubliez pas : La gestion du trafic urbain est complexe et multi-objectifs. Équilibrez les différents objectifs et testez sur des scénarios réalistes !*