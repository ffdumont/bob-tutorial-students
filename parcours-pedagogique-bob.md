# Parcours Pédagogique IBM Bob
## Découverte Progressive par Tutoriels

**Version:** 1.0  
**Basé sur:** Getting Started with IBM Bob v1.2.0  
**Public cible:** Développeurs, architectes, product managers, QA, et équipes de sécurité

---

## 📋 Vue d'ensemble du parcours

Ce parcours pédagogique est conçu pour vous accompagner dans la découverte et la maîtrise d'IBM Bob à travers une série de tutoriels pratiques et progressifs. Chaque module s'appuie sur les connaissances acquises précédemment.

### Durée estimée totale : 8-12 heures

---

## 🎯 Objectifs d'apprentissage

À la fin de ce parcours, vous serez capable de :
- Comprendre le modèle mental de Bob et son approche du développement logiciel
- Utiliser Bob efficacement dans votre workflow quotidien
- Gérer le contexte et les contraintes pour des résultats optimaux
- Effectuer des revues de code et des modernisations en toute sécurité
- Collaborer en équipe avec Bob
- Mesurer et améliorer l'utilisation de Bob dans votre organisation

---

## 📚 Structure du Parcours

### **Module 1 : Fondamentaux** (2-3 heures)
*Comprendre pourquoi et comment Bob change le travail*

#### Tutoriel 1.1 : Introduction à IBM Bob
- **Durée :** 30 minutes
- **Objectif :** Comprendre ce qu'est Bob et pourquoi il existe
- **Contenu :**
  - Le problème que Bob résout réellement
  - Différence entre Bob et les "AI coding assistants" classiques
  - Quand utiliser Bob et quand ne pas l'utiliser
- **Exercice pratique :** Identifier 3 cas d'usage dans votre projet actuel

#### Tutoriel 1.2 : Le Cycle de Vie Agentique (Agentic SDLC)
- **Durée :** 45 minutes
- **Objectif :** Maîtriser la boucle Orient-Bound-Plan-Act-Verify-Explain
- **Contenu :**
  - Les 6 phases du cycle agentique
  - Inner Loop vs Outer Loop
  - Le concept d'Evidence Ledger
- **Exercice pratique :** Mapper votre workflow actuel sur le modèle agentique

#### Tutoriel 1.3 : Comment Bob Pense
- **Durée :** 45 minutes
- **Objectif :** Comprendre le modèle mental de Bob
- **Contenu :**
  - Intent, Evidence, Judgment
  - Séparation planning/exécution
  - Contraintes vs créativité
  - Pourquoi Bob demande avant d'agir
- **Exercice pratique :** Analyser une tâche complexe selon le modèle de Bob

#### Tutoriel 1.4 : La Transition des Habitudes
- **Durée :** 30 minutes
- **Objectif :** Adapter ses habitudes de développement
- **Contenu :**
  - Habitudes traditionnelles vs habitudes agentiques
  - Pourquoi c'est plus lent au début
  - Systèmes probabilistes et contrats
- **Exercice pratique :** Identifier 3 habitudes à changer

---

### **Module 2 : Prise en Main** (3-4 heures)
*Utiliser Bob efficacement au quotidien*

#### Tutoriel 2.1 : L'Interface Bob dans l'IDE
- **Durée :** 45 minutes
- **Objectif :** Maîtriser l'interface utilisateur de Bob
- **Contenu :**
  - Le panneau latéral Bob
  - Tasks, Plans, et Findings
  - Comment Bob lit votre projet
  - Ce que Bob ne touche jamais sans approbation
- **Exercice pratique :** Configuration initiale et exploration de l'interface

#### Tutoriel 2.2 : Gestion du Contexte
- **Durée :** 1h30
- **Objectif :** Maîtriser la gestion du contexte (le plus critique !)
- **Contenu :**
  - Le contexte comme budget, pas comme dump
  - Comment la fenêtre de contexte s'empile
  - Signal vs Noise
  - Context mentions (@fichier, @dossier)
  - Habitudes de grounding
  - Gestion des gros repos et fichiers lourds
  - Comprendre "200k tokens"
  - Context poisoning et comment l'éviter
- **Exercice pratique :** 
  - Analyser la taille du contexte de votre projet
  - Créer un Context Pack pour votre équipe
  - Exercice de debugging d'un contexte "empoisonné"

#### Tutoriel 2.3 : Contrats Avant Code
- **Durée :** 45 minutes
- **Objectif :** Définir des contrats clairs avant l'exécution
- **Contenu :**
  - Pourquoi les contrats battent le copy-paste
  - Structure d'un bon contrat
  - Différents types de contrats selon les tâches
  - Écrire le contrat avant que Bob agisse
- **Exercice pratique :** Rédiger 3 contrats pour des tâches réelles

#### Tutoriel 2.4 : Votre Première Tâche Accountable
- **Durée :** 1h
- **Objectif :** Exécuter une tâche complète de bout en bout
- **Contenu :**
  - De la prompt au jugement
  - Définir l'intent clairement
  - Laisser Bob explorer le codebase
  - Lire le plan de Bob avant exécution
  - Comprendre les garanties de Bob
  - Observer l'exécution
- **Exercice pratique :** Réaliser une tâche complète sur votre projet
  - Exemple : Ajouter une validation à un endpoint existant
  - Exemple : Refactorer une fonction pour améliorer la lisibilité

---

### **Module 3 : Changements Sécurisés** (2-3 heures)
*Modifier du code en production en toute sécurité*

#### Tutoriel 3.1 : Code Review comme Evidence
- **Durée :** 1h
- **Objectif :** Utiliser Bob pour des revues de code rigoureuses
- **Contenu :**
  - Démarrer une code review avec Bob
  - Comprendre les Findings
  - Comment Bob explique les risques
  - Naviguer les findings dans l'IDE
  - Security findings vs quality issues
  - Quand accepter, corriger ou rejeter
- **Exercice pratique :** 
  - Reviewer un changement réel avec Bob
  - Comparer avec une review manuelle

#### Tutoriel 3.2 : Modernisation Sans Dérive Comportementale
- **Durée :** 1h30
- **Objectif :** Moderniser du code legacy en toute sécurité
- **Contenu :**
  - Le problème de la modernisation
  - Comprendre le comportement legacy d'abord
  - Préserver le comportement pendant le refactoring
  - Coordonner les changements multi-fichiers
  - Reviewer les changements de modernisation
- **Exercice pratique :** 
  - Moderniser un service legacy
  - Cas pratique : Migration d'une API REST vers une architecture plus moderne

#### Tutoriel 3.3 : Sécurité, Permissions et Confiance MCP
- **Durée :** 45 minutes
- **Objectif :** Comprendre le modèle de sécurité de Bob
- **Contenu :**
  - Shift Left sans ignorer les risques
  - Approvals, YOLO mode, et commandes "safe"
  - L'échelle de permissions
  - OWASP Top 10 pour applications LLM (2025)
  - Containment en couches
  - Modes, ignore files, et checkpoints
  - MCP et intégration enterprise
- **Exercice pratique :** Configurer les permissions pour votre équipe

---

### **Module 4 : Ce que Bob Ne Doit PAS Faire** (1 heure)
*Comprendre les limites et anti-patterns*

#### Tutoriel 4.1 : Limites et Jugement Humain
- **Durée :** 30 minutes
- **Objectif :** Identifier où le jugement humain est obligatoire
- **Contenu :**
  - Bob ne doit pas prendre de décisions à votre place
  - Bob ne doit pas remplacer la code review
  - Bob ne doit pas écrire du code sans contexte
  - Bob ne doit pas être votre opérateur production non supervisé
  - Bob ne doit pas ignorer vos contraintes
- **Exercice pratique :** Identifier 5 situations où Bob ne devrait pas être utilisé

#### Tutoriel 4.2 : Anti-Patterns et Conditions d'Arrêt
- **Durée :** 30 minutes
- **Objectif :** Reconnaître et éviter les mauvaises pratiques
- **Contenu :**
  - Anti-patterns courants
  - Quand arrêter d'utiliser Bob
  - Stop conditions
- **Exercice pratique :** Analyser un cas d'échec et identifier l'anti-pattern

---

### **Module 5 : Travail en Équipe** (2-3 heures)
*Utiliser Bob collectivement et efficacement*

#### Tutoriel 5.1 : Bob en Équipe
- **Durée :** 1h
- **Objectif :** Intégrer Bob dans les workflows d'équipe
- **Contenu :**
  - D'un outil individuel à un système partagé
  - Le problème des outils AI en équipe
  - Compréhension partagée vs travail AI caché
  - Reviewer l'output de Bob dans les PRs
  - Utiliser Bob pour l'onboarding
  - Éviter les "AI silos"
- **Exercice pratique :** 
  - Créer un template de PR pour les changements Bob
  - Définir un workflow de review d'équipe

#### Tutoriel 5.2 : Rôles dans l'Agentic SDLC
- **Durée :** 45 minutes
- **Objectif :** Comprendre comment chaque rôle utilise Bob
- **Contenu :**
  - Pour les développeurs
  - Pour les architectes
  - Pour les product managers
  - Pour les testeurs et QA
  - Pour la sécurité et compliance
  - Pour les engineering managers
- **Exercice pratique :** Définir les use cases Bob pour votre rôle

#### Tutoriel 5.3 : Skills, Modes et Rules comme Mémoire d'Équipe
- **Durée :** 45 minutes
- **Objectif :** Créer et partager des workflows packagés
- **Contenu :**
  - Trouver les commandes et changer de mode
  - Skills : workflows packagés déclenchés par des mots
  - Skills comme habitudes d'équipe
  - Le lifecycle des skills
  - Choisir la bonne couche de mémoire
- **Exercice pratique :** Créer un skill personnalisé pour votre équipe

#### Tutoriel 5.4 : Mesurer Bob Sans Théâtre
- **Durée :** 30 minutes
- **Objectif :** Définir des métriques pertinentes
- **Contenu :**
  - Ce qu'il ne faut PAS mesurer
  - Mesurer le système de delivery, pas la démo
  - Mesurer par workflow
  - Un scorecard de démarrage
  - Baseline avant de célébrer
  - Attention à Goodhart's Law
- **Exercice pratique :** Créer un tableau de bord de métriques pour votre équipe

---

### **Module 6 : Mindset et Pratiques Avancées** (1-2 heures)
*Aller plus loin avec Bob*

#### Tutoriel 6.1 : Le Mindset Bob
- **Durée :** 30 minutes
- **Objectif :** Adopter la bonne mentalité
- **Contenu :**
  - Le shift du code vers les systèmes
  - Meilleures questions, meilleures limites
  - Systèmes avant snippets
  - Utiliser l'IA sans abandonner la responsabilité
  - Ce que le mindset change au quotidien
- **Exercice pratique :** Réflexion personnelle et plan d'action

#### Tutoriel 6.2 : Garder Bob Ennuyeux (Boring)
- **Durée :** 30 minutes
- **Objectif :** Maintenir Bob fiable et prévisible
- **Contenu :**
  - Commencer petit, construire des habitudes
  - Workflows communs à explorer
  - Use cases avancés
  - Quand Bob brille le plus
  - Comment garder Bob boring et vos systèmes fiables
- **Exercice pratique :** Planifier vos prochaines étapes

#### Tutoriel 6.3 : Workflows Avancés (Optionnel)
- **Durée :** 1h
- **Objectif :** Explorer des cas d'usage complexes
- **Contenu :**
  - Intégration CI/CD
  - Automatisation de tests
  - Documentation automatique
  - Analyse de dépendances
  - Migration de frameworks
- **Exercice pratique :** Implémenter un workflow avancé

---

## 🎓 Certification et Évaluation

### Projet Final (2-3 heures)
Réaliser un projet complet qui démontre la maîtrise de Bob :

**Option A : Modernisation d'un Module Legacy**
- Analyser un module legacy
- Créer un contrat de modernisation
- Exécuter la modernisation avec Bob
- Effectuer une code review complète
- Documenter le processus et les résultats

**Option B : Mise en Place Bob pour une Équipe**
- Définir les workflows d'équipe
- Créer des skills personnalisés
- Établir des guidelines de sécurité
- Créer un plan de rollout
- Définir des métriques de succès

### Critères d'Évaluation
- ✅ Compréhension du modèle mental de Bob
- ✅ Gestion efficace du contexte
- ✅ Utilisation appropriée des contrats
- ✅ Pratiques de sécurité
- ✅ Collaboration en équipe
- ✅ Mesure et amélioration continue

---

## 📖 Ressources Complémentaires

### Documentation
- Getting Started with IBM Bob (document source)
- Documentation officielle IBM Bob
- OWASP Top 10 for LLM Applications (2025)

### Communauté
- Forums IBM Bob
- Slack/Teams channels
- Meetups et conférences

### Lectures Recommandées
- Modernizing Enterprise Java (O'Reilly) - Markus Eisele
- Applied AI for Enterprise Java Development (O'Reilly) - Markus Eisele
- The Main Thread (Substack) - Markus Eisele

---

## 🚀 Prochaines Étapes

Après avoir complété ce parcours :

1. **Pratiquer régulièrement** : Utilisez Bob quotidiennement sur de vraies tâches
2. **Partager avec l'équipe** : Organisez des sessions de partage d'expérience
3. **Contribuer** : Créez des skills et partagez-les avec la communauté
4. **Mesurer** : Suivez vos métriques et ajustez vos pratiques
5. **Rester à jour** : Suivez les évolutions de Bob et les nouvelles pratiques

---

## 📝 Notes pour les Formateurs

### Conseils Pédagogiques
- **Hands-on first** : Privilégier la pratique à la théorie
- **Contexte réel** : Utiliser des projets réels autant que possible
- **Erreurs constructives** : Encourager l'expérimentation et l'apprentissage par l'erreur
- **Peer learning** : Favoriser les échanges entre participants
- **Itération** : Revenir sur les concepts avec des exemples progressivement plus complexes

### Adaptations Possibles
- **Format court** : Modules 1, 2 et 4 (minimum viable)
- **Format développeur** : Modules 1, 2, 3 et 6
- **Format manager** : Modules 1, 4, 5 et 6
- **Format sécurité** : Modules 1, 3, 4 et 5

### Prérequis Techniques
- Accès à IBM Bob (trial ou licence)
- IDE compatible (VS Code recommandé)
- Projet de test ou sandbox
- Accès à un repository Git

---

## 📞 Support

Pour toute question ou suggestion d'amélioration de ce parcours :
- Créer une issue dans le repository
- Contacter l'équipe de formation
- Consulter la FAQ IBM Bob

---

**Version du parcours :** 1.0  
**Dernière mise à jour :** Mai 2026  
**Basé sur :** Getting Started with IBM Bob v1.2.0 par Markus Eisele