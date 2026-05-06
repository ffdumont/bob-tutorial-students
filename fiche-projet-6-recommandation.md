---
layout: default
title: Fiche Projet - Système de Recommandation
---

# Fiche Projet : Système de Recommandation
## Guide d'Utilisation de Bob pour Votre Projet

**Équipe :** PRAT, AÏSSAOUI, GUILLERMET-LAOUAD, JMAL  
**Domaine :** Recommandation adaptative  
**Technologies :** Filtrage collaboratif, RL simplifié, Streamlit, MovieLens

---

## 🎯 Vue d'Ensemble du Projet

### Objectif
Développer une application basée sur l'intelligence artificielle capable d'analyser les préférences utilisateur, de recommander du contenu (films) et de s'adapter progressivement aux choix de l'utilisateur.

### Composants Principaux
1. **Filtrage collaboratif** : Recommandations basées sur les similarités utilisateurs/items
2. **RL simplifié** : Apprentissage des choix utilisateur (like/dislike)
3. **Application web Streamlit** : Interface interactive avec feedback temps réel
4. **IA explicable** : Explications des recommandations

### Vos Attentes vis-à-vis de Bob
- Aide à la génération de code
- Assistance conception interface utilisateur
- Génération d'assistant conversationnel
- Aide à l'explication des résultats de l'IA
- Support pour le déploiement de l'application

---

## 📚 Parcours Pédagogique Adapté à Votre Projet

### Module 1 : Fondamentaux (2-3h)

#### 📖 Tutoriel 1.1 : Introduction à IBM Bob

**Questions spécifiques à votre projet :**

❓ **Quels sont les 3 cas d'usage Bob les plus pertinents pour mon projet de recommandation ?**
- Implémentation du système de filtrage collaboratif
- Création de l'interface Streamlit interactive
- Intégration de l'explicabilité (pourquoi cette recommandation ?)

❓ **Où Bob peut-il m'aider le plus dans un projet de recommandation ?**
- Architecture du système (filtrage collaboratif + RL)
- Gestion du cold start (nouveaux utilisateurs)
- Création d'une interface utilisateur engageante
- Génération d'explications compréhensibles

❓ **Où le jugement humain est-il critique dans mon projet ?**
- Validation que les recommandations sont pertinentes
- Décision sur l'équilibre exploration/exploitation
- Interprétation des patterns de préférences
- Validation de l'expérience utilisateur

**💡 Prompt Bob suggéré :**
```
Je travaille sur un système de recommandation de films combinant :
- Filtrage collaboratif (similarité utilisateurs/items)
- RL simplifié pour apprendre des feedbacks (like/dislike)
- Interface Streamlit interactive
- Explications des recommandations

Aide-moi à structurer l'architecture avec :
- Système de recommandation de base (filtrage collaboratif)
- Mécanisme d'apprentissage des préférences
- Interface utilisateur intuitive
- Génération d'explications
```

---

#### 📖 Tutoriel 1.2 : Le Cycle de Vie Agentique

**Application à votre projet :**

**Phase ORIENT** - Comprendre avant de coder
- ❓ Comment le filtrage collaboratif et le RL doivent-ils interagir ?
- ❓ Comment gérer le cold start (nouveaux utilisateurs sans historique) ?
- ❓ Quelle est la fréquence de mise à jour des recommandations ?

**💡 Utilisez Bob pour :**
```
Analyse l'architecture du système de recommandation et identifie :
1. Le flux : Préférences initiales → Recommandations → Feedback → Adaptation
2. Comment combiner filtrage collaboratif et apprentissage des feedbacks
3. Comment gérer le cold start
4. Comment expliquer les recommandations
```

**Phase BOUND** - Définir les contraintes
- ❓ Contrainte de simplicité : système accessible aux non-experts
- ❓ Contrainte de réactivité : adaptation rapide aux feedbacks
- ❓ Contrainte d'explicabilité : recommandations compréhensibles
- ❓ Contrainte de diversité : éviter la bulle de filtrage

**Phase PLAN** - Planifier avant d'exécuter
- ❓ Ordre de développement : Filtrage collaboratif → Interface → RL → Explicabilité ?
- ❓ Comment tester chaque composant indépendamment ?
- ❓ Quelle baseline pour comparer (recommandations aléatoires, populaires) ?

**💡 Prompt Bob suggéré :**
```
Crée un plan de développement pour le système de recommandation :
1. Ordre de développement (filtrage collaboratif, interface, RL, explicabilité)
2. Points de validation à chaque étape
3. Baselines à implémenter (aléatoire, populaire, collaboratif)
4. Stratégie de test utilisateur

Contrainte : interface simple et intuitive pour tous
```

---

#### 📖 Tutoriel 1.3 : Comment Bob Pense

**Intent, Evidence, Judgment pour votre projet :**

**INTENT** - Ce que vous voulez accomplir
- ❓ Mon intent est-il clair ? "Recommander des films" vs "Créer un système qui recommande des films pertinents et s'adapte progressivement aux préférences de l'utilisateur avec explications claires"
- ❓ Ai-je défini les critères de succès ? (Taux de like, diversité, satisfaction utilisateur)

**EVIDENCE** - Les faits que Bob collecte
- ❓ Quels fichiers Bob doit-il lire pour comprendre mon architecture ?
- ❓ Ai-je fourni des exemples du dataset MovieLens ?
- ❓ Bob comprend-il la structure de l'interface souhaitée ?

**JUDGMENT** - Votre décision finale
- ❓ Est-ce que je comprends pourquoi Bob suggère cette approche de filtrage ?
- ❓ Les recommandations générées sont-elles pertinentes ?
- ❓ L'interface est-elle intuitive pour les utilisateurs ?

**💡 Exercice pratique :**
```
Demande à Bob d'analyser ton système de recommandation et de suggérer 
des améliorations.

Avant d'accepter, vérifie :
- Les recommandations sont-elles diversifiées ?
- Le système s'adapte-t-il vraiment aux feedbacks ?
- Les explications sont-elles compréhensibles ?
- Comprends-tu chaque composant du système ?
```

---

#### 📖 Tutoriel 1.4 : La Transition des Habitudes

**Habitudes à changer pour votre projet :**

**Avant (habitudes traditionnelles) :**
- Coder directement sans penser à l'expérience utilisateur
- Recommander sans expliquer pourquoi
- Tester manuellement différentes approches

**Après (habitudes agentiques) :**
- Définir l'expérience utilisateur d'abord
- Laisser Bob générer l'interface et les explications
- Automatiser les comparaisons d'approches

**💡 Plan de transition pour votre équipe :**

**Semaine 1-2 : Filtrage Collaboratif**
- Utilisez Bob pour implémenter le filtrage collaboratif
- Définissez les métriques de qualité
- Testez sur MovieLens

**Semaine 3-4 : Interface Streamlit**
- Bob génère l'interface de base
- Vous testez l'expérience utilisateur
- Bob améliore selon vos retours

**Semaine 5-6 : RL Simplifié**
- Bob implémente l'apprentissage des feedbacks
- Vous testez l'adaptation
- Bob optimise la réactivité

**Semaine 7-8 : Explicabilité**
- Bob génère les explications
- Vous validez leur clarté
- Bob améliore la présentation

**Semaine 9-10 : Finalisation et Déploiement**
- Bob aide au déploiement
- Vous testez avec de vrais utilisateurs
- Documentation finale

---

### Module 2 : Prise en Main (3-4h)

#### 📖 Tutoriel 2.1 : L'Interface Bob

**Configuration pour votre projet :**

**Context Mentions essentiels :**
```
@models/collaborative_filtering.py  # Filtrage collaboratif
@models/rl_recommender.py          # RL simplifié
@utils/explainability.py           # Génération d'explications
@app/streamlit_app.py              # Interface
@data/movielens_loader.py          # Chargement MovieLens
@config/app_config.yaml            # Configuration
```

**💡 Première tâche avec Bob :**
```
@data/movielens_loader.py @config/app_config.yaml

Crée un système de chargement pour MovieLens qui :
1. Télécharge le dataset MovieLens (100k ou 1M)
2. Parse les fichiers (ratings, movies, users)
3. Crée les matrices utilisateur-item
4. Gère le cold start (nouveaux utilisateurs)
5. Fournit des statistiques du dataset

Contraintes :
- Format compatible avec filtrage collaboratif
- Gestion efficace de la mémoire
- API simple et claire
```

---

#### 📖 Tutoriel 2.2 : Gestion du Contexte ⭐ CRITIQUE

**Contexte spécifique à votre projet de recommandation :**

**Signal (à inclure) :**
- ✅ Filtrage collaboratif (models/collaborative_filtering.py)
- ✅ RL simplifié (models/rl_recommender.py)
- ✅ Explicabilité (utils/explainability.py)
- ✅ Interface (app/streamlit_app.py)
- ✅ Configuration (config/)
- ✅ Loader MovieLens (data/movielens_loader.py)

**Noise (à exclure) :**
- ❌ Dataset MovieLens complet (trop volumineux)
- ❌ Matrices utilisateur-item complètes
- ❌ Historiques de sessions utilisateurs
- ❌ Logs d'interactions
- ❌ Modèles entraînés

**💡 Context Pack pour votre projet :**

Créez un fichier `.bobcontext` :
```yaml
# Context Pack - Projet Recommandation
include:
  - models/**/*.py
  - utils/**/*.py
  - app/**/*.py
  - data/movielens_loader.py
  - config/*.yaml
  - README.md
  
exclude:
  - data/ml-*/**
  - models/saved/**
  - logs/**
  - user_sessions/**
  
priority_files:
  - models/collaborative_filtering.py
  - models/rl_recommender.py
  - app/streamlit_app.py
  - utils/explainability.py
```

**❓ Questions de grounding :**
- Avant chaque tâche : "Bob, as-tu lu ma configuration de recommandation ?"
- Après modification : "Bob, confirme que l'interface est intuitive"
- En cas de doute : "Bob, montre-moi comment les composants interagissent"

**💡 Gestion du contexte pour recommandation :**
```
Pour les modifications d'interface, toujours inclure :
@app/streamlit_app.py @models/collaborative_filtering.py @utils/explainability.py

Bob, analyse l'expérience utilisateur et propose des améliorations 
pour rendre l'interface plus engageante.
```

---

#### 📖 Tutoriel 2.3 : Contrats Avant Code

**Contrat type pour votre projet :**

**Exemple : Interface Streamlit Interactive**

```markdown
## Contrat : Interface de Recommandation Interactive

### Intent
Créer une interface Streamlit intuitive et engageante qui permet aux 
utilisateurs de découvrir des films, donner leur avis et voir les 
recommandations s'adapter en temps réel.

### Success Criteria
- Interface claire et attractive
- Sélection initiale de préférences (3-5 films)
- Affichage de 5 recommandations avec posters
- Boutons like/dislike pour chaque film
- Mise à jour en temps réel des recommandations
- Explications claires (pourquoi ce film ?)
- Historique des interactions visible

### Non-Goals
- Ne pas gérer plusieurs utilisateurs simultanés (v1)
- Ne pas persister les données entre sessions (v1)
- Ne pas recommander autre chose que des films

### Preserved Behavior
- Compatible avec le système de recommandation
- Logging des interactions
- Format de données cohérent

### Verification
- Tests utilisateur (5 personnes minimum)
- Validation que les recommandations changent avec les feedbacks
- Vérification que les explications sont compréhensibles
- Test de l'expérience complète (sélection → recommandations → feedbacks)

### Stop Conditions
- Si l'interface est confuse → simplifier
- Si les recommandations ne changent pas → revoir le RL
- Si les explications sont incompréhensibles → reformuler
```

**💡 Utilisez ce contrat avec Bob :**
```
@app/streamlit_app.py @models/collaborative_filtering.py

Implémente l'interface Streamlit selon le contrat ci-dessus.
Commence par me proposer un mockup de l'interface avec les différentes sections.
```

---

#### 📖 Tutoriel 2.4 : Votre Première Tâche Accountable

**Tâche guidée : Créer le système de filtrage collaboratif**

**Étape 1 : Intent clair**
```
Je veux créer un système de filtrage collaboratif qui :
1. Charge le dataset MovieLens (100k ratings)
2. Calcule les similarités utilisateur-utilisateur ou item-item
3. Génère des recommandations personnalisées
4. Gère le cold start (nouveaux utilisateurs)
5. Fournit des explications (films similaires à ceux aimés)

Contraintes critiques :
- Recommandations pertinentes (diversité + précision)
- Temps de calcul raisonnable (< 1s par recommandation)
- Gestion du cold start (demander préférences initiales)
```

**Étape 2 : Laisser Bob explorer**
```
@data/movielens_loader.py @config/app_config.yaml

Bob, explore d'abord le dataset MovieLens et ma configuration.
Dis-moi ce que tu comprends de la structure avant de proposer 
une approche de filtrage collaboratif.
```

**Étape 3 : Lire le plan**
- ❓ Bob a-t-il compris la structure de MovieLens ?
- ❓ L'approche proposée (user-based ou item-based) est-elle justifiée ?
- ❓ La gestion du cold start est-elle appropriée ?
- ❓ Les explications sont-elles prévues ?

**Étape 4 : Exécution et vérification**
```
Après implémentation, vérifie :
- Les recommandations sont pertinentes (test manuel)
- Le système gère le cold start
- Les calculs sont rapides (< 1s)
- Les explications sont générées
- La diversité est présente
```

---

### Module 3 : Changements Sécurisés (2-3h)

#### 📖 Tutoriel 3.1 : Code Review comme Evidence

**Review spécifique à votre projet :**

**Avant d'intégrer le RL :**
```
@models/rl_recommender.py @models/collaborative_filtering.py

Bob, fais une code review du système de recommandation et identifie :
1. Les risques de bulle de filtrage (manque de diversité)
2. Les problèmes de performance (calculs lents)
3. Les bugs potentiels (gestion du cold start)
4. Les violations de bonnes pratiques

Focus particulier sur :
- L'équilibre exploration/exploitation
- La diversité des recommandations
- La réactivité aux feedbacks
- La qualité des explications
```

**💡 Checklist de review pour code de recommandation :**
- [ ] Diversité des recommandations (pas que des films similaires)
- [ ] Gestion du cold start fonctionnelle
- [ ] Réactivité aux feedbacks (adaptation visible)
- [ ] Explications claires et compréhensibles
- [ ] Performance acceptable (< 1s par recommandation)
- [ ] Pas de biais évidents

---

#### 📖 Tutoriel 3.2 : Modernisation Sans Dérive

**Cas pratique : Amélioration de la diversité**

**Situation :** Votre système recommande toujours des films très similaires (bulle de filtrage).

**Contrat de modernisation :**
```markdown
## Modernisation : Amélioration de la Diversité

### Comportement à Préserver
- Pertinence des recommandations (pas de films aléatoires)
- Réactivité aux feedbacks
- Performance (< 1s)

### Améliorations Souhaitées
- Augmenter la diversité (genres variés, années variées)
- Équilibrer pertinence et découverte
- Paramètre de diversité configurable

### Vérification
- Mesurer la diversité (nombre de genres différents)
- Valider que les recommandations restent pertinentes
- Tester avec différents profils utilisateurs
- Comparer avec version précédente
```

**💡 Prompt Bob :**
```
@models/collaborative_filtering.py @models/rl_recommender.py

Améliore le système pour augmenter la diversité des recommandations.
CRITIQUE : Les recommandations doivent rester pertinentes.

Propose d'abord un plan avec plusieurs approches :
1. Diversification par genre
2. Diversification temporelle (années variées)
3. Exploration aléatoire (ε-greedy)
4. MMR (Maximal Marginal Relevance)

Pour chaque approche, estime l'impact sur pertinence et diversité.
```

---

### Module 4 : Ce que Bob Ne Doit PAS Faire (1h)

#### 📖 Tutoriel 4.1 : Limites et Jugement Humain

**Décisions que VOUS devez prendre :**

❌ **Bob ne doit PAS décider :**
- L'équilibre entre pertinence et diversité
- Le nombre de recommandations à afficher
- Le design de l'interface utilisateur
- Comment interpréter les préférences utilisateur

✅ **Vous devez décider :**
- "Cet équilibre pertinence/diversité est-il satisfaisant ?"
- "Cette interface est-elle intuitive pour les utilisateurs ?"
- "Ces explications sont-elles compréhensibles ?"
- "Ce système respecte-t-il la vie privée des utilisateurs ?"

**💡 Exemple de mauvaise utilisation :**
```
❌ "Bob, crée un système qui collecte toutes les données utilisateur 
   possibles pour améliorer les recommandations"
→ Risque de violation de la vie privée

✅ "Bob, crée un système qui utilise uniquement les feedbacks explicites 
   (like/dislike) et explique clairement comment les données sont utilisées"
```

---

#### 📖 Tutoriel 4.2 : Anti-Patterns

**Anti-patterns spécifiques à votre projet :**

❌ **Anti-pattern 1 : Bulle de filtrage**
```
"Bob, recommande toujours les films les plus similaires à ceux aimés"
→ Risque de manquer de diversité
```

✅ **Bonne pratique :**
```
"Bob, crée un système qui équilibre similarité (80%) et découverte (20%), 
avec un paramètre de diversité configurable"
```

❌ **Anti-pattern 2 : Pas d'explicabilité**
```
"Bob, recommande des films et c'est tout"
→ Utilisateur ne comprend pas pourquoi
```

✅ **Bonne pratique :**
```
"Bob, pour chaque recommandation, explique pourquoi elle est suggérée 
(ex: 'Parce que vous avez aimé [Film X] qui est similaire')"
```

❌ **Anti-pattern 3 : Ignorer le cold start**
```
"Bob, recommande directement sans connaître l'utilisateur"
→ Recommandations aléatoires ou populaires uniquement
```

✅ **Bonne pratique :**
```
"Bob, demande à l'utilisateur de sélectionner 3-5 films qu'il aime 
pour initialiser son profil, puis adapte progressivement"
```

---

### Module 5 : Travail en Équipe (2-3h)

#### 📖 Tutoriel 5.1 : Bob en Équipe

**Workflow d'équipe pour votre projet :**

**Répartition des tâches :**
- **Membre 1 (PRAT)** : Filtrage collaboratif + RL
- **Membre 2 (AÏSSAOUI)** : Interface Streamlit
- **Membre 3 (GUILLERMET-LAOUAD)** : Explicabilité
- **Membre 4 (JMAL)** : Tests utilisateur + Documentation

**💡 Template de PR avec Bob :**
```markdown
## PR : [Composant] - [Description]

### Généré avec Bob
- [ ] Oui, Bob a aidé à générer ce code
- [ ] Non, code manuel

### Contrat Respecté
- [ ] Intent clair défini
- [ ] Success criteria validés
- [ ] Tests utilisateur passent
- [ ] Code reviewé

### Changements
- [Liste des fichiers modifiés]
- [Impact sur l'expérience utilisateur]

### Métriques
- Pertinence : [X]/5 (test utilisateur)
- Diversité : [Y] genres différents
- Temps de réponse : [Z]ms

### Vérification
- [ ] Tests utilisateur (5 personnes)
- [ ] Recommandations pertinentes
- [ ] Explications claires
- [ ] Interface intuitive

### Review Bob
[Coller ici les findings de Bob si applicable]
```

---

#### 📖 Tutoriel 5.2 : Rôles dans l'Agentic SDLC

**Pour votre équipe :**

**Développeur ML (PRAT) :**
- Utiliser Bob pour implémenter le filtrage collaboratif
- Définir le système RL avec Bob
- Optimiser les algorithmes

**Développeur Interface (AÏSSAOUI) :**
- Utiliser Bob pour créer l'interface Streamlit
- Tester l'expérience utilisateur
- Améliorer le design

**Développeur Explicabilité (GUILLERMET-LAOUAD) :**
- Utiliser Bob pour générer les explications
- Valider leur clarté
- Créer les visualisations

**Testeur/Documenteur (JMAL) :**
- Organiser les tests utilisateur
- Documenter le système
- Créer les tutoriels utilisateur

---

#### 📖 Tutoriel 5.3 : Skills Personnalisés

**Skill personnalisé pour votre projet :**

Créez un skill "recommend-and-explain" :

```yaml
name: recommend-and-explain
description: Générer des recommandations avec explications
trigger: /recommend

steps:
  - Charger le profil utilisateur
  - Générer 5 recommandations
  - Pour chaque recommandation, créer une explication
  - Formater pour l'affichage Streamlit
  - Logger les recommandations
```

**💡 Utilisation :**
```
@models/collaborative_filtering.py /recommend

User ID : 123
Nombre de recommandations : 5
```

**Skill "user-test-report" :**

```yaml
name: user-test-report
description: Générer un rapport de test utilisateur
trigger: /user-test

steps:
  - Analyser les feedbacks utilisateur
  - Calculer les métriques (satisfaction, diversité)
  - Identifier les points d'amélioration
  - Générer un rapport avec recommandations
```

---

#### 📖 Tutoriel 5.4 : Mesurer Bob

**Métriques pour votre projet :**

**À mesurer :**
- ✅ Temps gagné sur l'implémentation (baseline vs avec Bob)
- ✅ Qualité de l'interface (tests utilisateur)
- ✅ Satisfaction utilisateur
- ✅ Bugs détectés en review

**À NE PAS mesurer :**
- ❌ Nombre de lignes générées par Bob
- ❌ Pourcentage de code écrit par Bob
- ❌ Vitesse de développement brute

**💡 Tableau de bord suggéré :**
```markdown
## Métriques Projet Recommandation

### Satisfaction Utilisateur
- Note moyenne : 4.2/5 (objectif : > 4.0) ✅
- Pertinence : 4.5/5
- Diversité : 3.8/5
- Clarté explications : 4.3/5

### Performance Système
- Temps de recommandation : 0.8s (objectif : < 1s) ✅
- Diversité : 4.2 genres/5 films (objectif : > 3) ✅
- Adaptation : visible après 3 feedbacks ✅

### Développement avec Bob
- Temps d'implémentation : 4 jours (vs 12 jours sans Bob)
- Itérations interface : 8 (vs 3 sans Bob)
- Bugs détectés : 10

### Qualité
- Couverture de tests : 75%
- Documentation : 100%
- Tests utilisateur : 15 personnes
```

---

### Module 6 : Mindset et Pratiques Avancées (1-2h)

#### 📖 Tutoriel 6.1 : Le Mindset Bob

**Shift mental pour votre projet :**

**Avant :** "Je dois coder un algorithme de recommandation"  
**Après :** "Je dois concevoir une expérience utilisateur engageante"

**Avant :** "Je vais recommander les films les plus similaires"  
**Après :** "Je vais équilibrer pertinence et découverte"

**Avant :** "Je teste moi-même l'interface"  
**Après :** "Je fais tester par de vrais utilisateurs"

**💡 Questions à vous poser :**
- ❓ Est-ce que je pense en termes d'expérience utilisateur ou d'algorithme ?
- ❓ Est-ce que mes recommandations sont diversifiées ?
- ❓ Est-ce que mes explications sont compréhensibles ?

---

#### 📖 Tutoriel 6.2 : Garder Bob Boring

**Workflows "boring" mais efficaces pour votre projet :**

**Workflow 1 : Amélioration interface**
1. Identifier un point de friction
2. Bob propose des améliorations
3. Vous testez avec utilisateurs
4. Bob implémente la meilleure
5. Vous validez

**Workflow 2 : Optimisation recommandations**
1. Analyser les feedbacks utilisateur
2. Bob identifie les patterns
3. Bob propose des ajustements
4. Vous testez
5. Bob implémente

**Workflow 3 : Amélioration explications**
1. Collecter les retours sur les explications
2. Bob reformule
3. Vous validez la clarté
4. Bob intègre
5. Vous testez avec utilisateurs

**💡 Gardez ces workflows simples et répétables !**

---

## 🎯 Checklist Finale pour Votre Projet

### Système de Recommandation
- [ ] Filtrage collaboratif fonctionnel
- [ ] Gestion du cold start (sélection initiale)
- [ ] Recommandations pertinentes
- [ ] Diversité présente (genres variés)
- [ ] Temps de calcul < 1s

### RL Simplifié
- [ ] Apprentissage des feedbacks (like/dislike)
- [ ] Adaptation visible après quelques feedbacks
- [ ] Équilibre exploration/exploitation
- [ ] Pas de sur-adaptation (bulle de filtrage)

### Interface Streamlit
- [ ] Design clair et attractif
- [ ] Sélection initiale de préférences
- [ ] Affichage des recommandations avec posters
- [ ] Boutons like/dislike fonctionnels
- [ ] Mise à jour en temps réel
- [ ] Historique des interactions

### Explicabilité
- [ ] Explications pour chaque recommandation
- [ ] Explications compréhensibles
- [ ] Visualisations claires
- [ ] Transparence sur l'utilisation des données

### Tests Utilisateur
- [ ] Tests avec au moins 10 personnes
- [ ] Satisfaction > 4/5
- [ ] Retours documentés
- [ ] Améliorations implémentées

### Code et Documentation
- [ ] Tests unitaires pour chaque composant
- [ ] Code reviewé (par Bob et humains)
- [ ] Documentation complète
- [ ] Tutoriel utilisateur

---

## 💡 Prompts Bob Prêts à l'Emploi

### Démarrage du projet
```
Je démarre un projet de système de recommandation de films combinant 
filtrage collaboratif et RL. Crée la structure avec :
- Loader MovieLens
- Filtrage collaboratif (user-based ou item-based)
- RL simplifié pour apprendre des feedbacks
- Interface Streamlit interactive
- Génération d'explications
```

### Filtrage collaboratif
```
@data/movielens_loader.py @models/collaborative_filtering.py

Implémente un système de filtrage collaboratif pour MovieLens :
- Approche : item-based (similarité cosinus)
- Input : profil utilisateur (films aimés)
- Output : top 10 recommandations
- Gestion du cold start : demander 3-5 films initiaux
- Diversité : au moins 3 genres différents dans les recommandations

Contraintes :
- Temps de calcul < 1s
- Explications générées (films similaires)
```

### RL simplifié
```
@models/rl_recommender.py @models/collaborative_filtering.py

Crée un système RL simplifié qui apprend des feedbacks :
- État : profil utilisateur (films aimés/pas aimés)
- Action : recommander un film
- Récompense : +1 si like, -1 si dislike
- Algorithme : ε-greedy simple ou bandit multi-bras
- Mise à jour : après chaque feedback

Objectif : adapter les recommandations progressivement
```

### Interface Streamlit
```
@app/streamlit_app.py @models/ @utils/

Crée une interface Streamlit engageante pour les recommandations :

1. Page d'accueil :
   - Titre et description
   - Sélection de 3-5 films initiaux (avec recherche)

2. Page de recommandations :
   - Affichage de 5 films avec posters et infos
   - Boutons 👍 / 👎 pour chaque film
   - Explication sous chaque film
   - Bouton "Nouvelles recommandations"

3. Sidebar :
   - Historique des interactions
   - Statistiques (films aimés, genres préférés)
   - Paramètres (diversité, nombre de recommandations)

Design : moderne, coloré, intuitif
```

### Génération d'explications
```
@utils/explainability.py @models/collaborative_filtering.py

Crée un module de génération d'explications pour les recommandations :

Pour chaque film recommandé, générer une explication du type :
- "Parce que vous avez aimé [Film X] qui est similaire"
- "Basé sur vos préférences pour le genre [Genre]"
- "Populaire parmi les utilisateurs avec des goûts similaires"

Format : texte court (1-2 phrases) + score de confiance
```

### Gestion du cold start
```
@utils/cold_start.py @data/movielens_loader.py

Crée un système de gestion du cold start :

1. Sélection initiale :
   - Afficher 20 films populaires variés (genres différents)
   - Utilisateur sélectionne 3-5 films qu'il aime
   - Créer le profil initial

2. Recommandations initiales :
   - Utiliser le filtrage collaboratif sur le profil initial
   - Ajouter de la diversité (exploration)

3. Adaptation progressive :
   - Mettre à jour le profil avec les feedbacks
   - Réduire l'exploration au fil du temps
```

### Tests utilisateur
```
@tests/user_testing.py @app/

Crée un framework de test utilisateur :

1. Scénarios de test :
   - Nouvel utilisateur (cold start)
   - Utilisateur avec préférences claires
   - Utilisateur avec goûts variés

2. Métriques à collecter :
   - Satisfaction (échelle 1-5)
   - Pertinence des recommandations
   - Clarté des explications
   - Facilité d'utilisation

3. Rapport :
   - Synthèse des retours
   - Points forts / points faibles
   - Recommandations d'amélioration
```

### Dashboard de métriques
```
@utils/metrics_dashboard.py @models/

Crée un dashboard de métriques pour le système :

1. Métriques de recommandation :
   - Taux de like/dislike
   - Diversité (genres, années)
   - Couverture du catalogue

2. Métriques utilisateur :
   - Satisfaction moyenne
   - Temps d'interaction
   - Nombre de feedbacks

3. Visualisations :
   - Évolution des préférences
   - Distribution des genres recommandés
   - Heatmap des interactions

Format : dashboard Streamlit séparé
```

---

## 📚 Ressources Complémentaires

### Pour les Systèmes de Recommandation
- "Recommender Systems Handbook" - Ricci et al.
- Papers sur filtrage collaboratif
- Surprise library documentation

### Pour le RL en Recommandation
- "Deep Reinforcement Learning for Recommendation" papers
- Contextual bandits
- Exploration vs exploitation

### Pour l'Explicabilité
- "Explainable Recommendation Systems" papers
- Best practices en UX pour recommandations
- Transparency in AI

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
- [ ] Itérations basées sur tests utilisateur

**Qualité Technique (40%) :**
- [ ] Recommandations pertinentes et diversifiées
- [ ] Adaptation aux feedbacks visible
- [ ] Performance acceptable (< 1s)
- [ ] Explicabilité intégrée

**Expérience Utilisateur (20%) :**
- [ ] Interface intuitive et engageante
- [ ] Tests utilisateur positifs (> 4/5)
- [ ] Documentation claire
- [ ] Système accessible à tous

---

**Bonne chance avec votre projet de Recommandation ! 🚀🎬**

*N'oubliez pas : L'expérience utilisateur est primordiale. Testez avec de vrais utilisateurs et itérez !*