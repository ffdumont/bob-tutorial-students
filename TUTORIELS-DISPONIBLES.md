# Tutoriels Disponibles - Parcours Pédagogique IBM Bob

**Version :** 1.0  
**Date :** Mai 2026  
**Basé sur :** Getting Started with IBM Bob v1.2.0 par Markus Eisele

---

## 📚 Vue d'Ensemble

Ce document liste tous les tutoriels disponibles dans le parcours pédagogique IBM Bob. Chaque tutoriel est conçu pour être pratique, avec des exercices et des exemples concrets.

### Statut Actuel

✅ **Module 1 : Fondamentaux** - 4 tutoriels (COMPLET)  
✅ **Module 2 : Prise en Main** - 4 tutoriels (COMPLET)  
📝 **Module 3 : Changements Sécurisés** - À développer  
📝 **Module 4 : Limites** - À développer  
📝 **Module 5 : Travail en Équipe** - À développer  
📝 **Module 6 : Mindset et Pratiques Avancées** - À développer

---

## ✅ Module 1 : Fondamentaux (COMPLET)

**Durée totale :** 2-3 heures  
**Objectif :** Comprendre pourquoi et comment Bob change le travail

### Tutoriel 1.1 : Introduction à IBM Bob
📄 **Fichier :** `tutoriel-1.1-introduction-bob.md`  
⏱️ **Durée :** 30 minutes  
🎯 **Niveau :** Débutant

**Contenu :**
- Ce qu'est IBM Bob et pourquoi il existe
- Le problème que Bob résout réellement
- Différence avec les "AI coding assistants" classiques
- Quand utiliser Bob et quand ne pas l'utiliser
- Exercices d'identification de cas d'usage

**Points clés :**
- Bob est un partenaire, pas un remplaçant
- Le contexte est essentiel
- Bob propose, vous décidez

---

### Tutoriel 1.2 : Le Cycle de Vie Agentique
📄 **Fichier :** `tutoriel-1.2-cycle-vie-agentique.md`  
⏱️ **Durée :** 45 minutes  
🎯 **Niveau :** Fondamental

**Contenu :**
- La boucle Orient → Bound → Plan → Act → Verify → Explain
- Les 6 phases détaillées avec exemples
- Inner Loop vs Outer Loop
- L'Evidence Ledger
- Le cycle selon votre rôle (dev, architect, PM, QA, etc.)

**Points clés :**
- Orient avant tout : comprendre avant de changer
- Bound pour la sécurité : les contraintes protègent
- Plan avant Act : valider l'approche d'abord

---

### Tutoriel 1.3 : Comment Bob Pense
📄 **Fichier :** `tutoriel-1.3-comment-bob-pense.md`  
⏱️ **Durée :** 45 minutes  
🎯 **Niveau :** Fondamental

**Contenu :**
- Le modèle mental de Bob : Intent, Evidence, Judgment
- Pourquoi Bob sépare planification et exécution
- Constraints Over Creativity (Contraintes > Créativité)
- Pourquoi Bob demande avant d'agir
- Exercices pratiques d'application

**Points clés :**
- Intent, Evidence, Judgment : les trois piliers séparés
- Bob lit, ne devine pas
- Vous décidez toujours : le jugement reste humain

---

### Tutoriel 1.4 : La Transition des Habitudes
📄 **Fichier :** `tutoriel-1.4-transition-habitudes.md`  
⏱️ **Durée :** 30 minutes  
🎯 **Niveau :** Fondamental

**Contenu :**
- Pourquoi le travail avec Bob semble différent
- Habitudes traditionnelles vs habitudes agentiques
- Pourquoi c'est plus lent avant d'être plus rapide
- Changements nécessaires pour chaque rôle
- Plan de transition sur 3 mois

**Points clés :**
- L'unité de travail change : plus de cadrage, moins de codage direct
- C'est normal d'être plus lent au début
- Tous les rôles changent, pas que les développeurs

---

## ✅ Module 2 : Prise en Main (COMPLET)

**Durée totale :** 3-4 heures  
**Objectif :** Utiliser Bob efficacement au quotidien

### Tutoriel 2.1 : L'Interface Bob dans l'IDE
📄 **Fichier :** `tutoriel-2.1-interface-bob.md`  
⏱️ **Durée :** 45 minutes  
🎯 **Niveau :** Pratique

**Contenu :**
- L'IDE comme cockpit, pas comme banc de travail
- Le Bob Side Panel (Task Input, Status, History)
- Tasks, Plans et Findings
- Les 5 phases d'une tâche
- Comment Bob lit votre projet
- Approbations et checkpoints

**Points clés :**
- Cockpit, pas banc de travail : piloter le système
- Intent goal-shaped : symptômes, contraintes, succès
- Findings ≠ Tasks : vous choisissez les priorités

---

### Tutoriel 2.2 : Gestion du Contexte ⭐ CRITIQUE
📄 **Fichier :** `tutoriel-2.2-gestion-contexte.md`  
⏱️ **Durée :** 1h30  
🎯 **Niveau :** Fondamental (CRITIQUE)

**Contenu :**
- Pourquoi le contexte est un budget, pas un dump
- Signal vs Noise
- Context Mentions (@fichier, @dossier)
- Comprendre "200k tokens"
- Habitudes de grounding
- Gros repos et fichiers lourds
- Context Poisoning et comment l'éviter
- Le Context Pack

**Points clés :**
- Le contexte est LA ressource la plus importante
- "Most Hallucinations Are Context Debt"
- Context mentions précis : soyez spécifique
- Détectez le poisoning tôt

**Note :** C'est le tutoriel le plus important du parcours !

---

### Tutoriel 2.3 : Contrats Avant Code
📄 **Fichier :** `tutoriel-2.3-contrats-avant-code.md`  
⏱️ **Durée :** 45 minutes  
🎯 **Niveau :** Pratique

**Contenu :**
- Pourquoi les contrats sont essentiels
- Structure d'un bon contrat (6 éléments)
- Contrats selon le type de tâche (Feature, Bug, Modernization, Security, Documentation)
- Écrire le contrat AVANT l'exécution
- Les contrats accélèrent les reviews

**Points clés :**
- Contrat > Code : le contrat est durable, le code peut varier
- 6 éléments : Intent, Success, Non-Goals, Preserved, Verification, Stop
- Avant, pas après : définir avant d'exécuter

---

### Tutoriel 2.4 : Votre Première Tâche Accountable
📄 **Fichier :** `tutoriel-2.4-premiere-tache.md`  
⏱️ **Durée :** 1 heure  
🎯 **Niveau :** Pratique (Hands-on)

**Contenu :**
- Walkthrough complet d'une tâche de bout en bout
- Définir un intent clair
- Laisser Bob explorer le codebase
- Lire et évaluer un plan
- Comprendre les garanties et responsabilités
- Vérifier les résultats
- Exercice pratique guidé

**Points clés :**
- Intent précis : Bob demande si c'est vague
- Exploration nécessaire : laissez Bob lire
- Plan avant code : jugez l'approche d'abord
- Vous possédez le résultat : responsabilité humaine

---

## 📝 Modules À Développer

### Module 3 : Changements Sécurisés (2-3h)

**Tutoriels prévus :**
- 3.1 : Code Review comme Evidence
- 3.2 : Modernisation Sans Dérive Comportementale
- 3.3 : Sécurité, Permissions et Confiance MCP

### Module 4 : Ce que Bob Ne Doit PAS Faire (1h)

**Tutoriels prévus :**
- 4.1 : Limites et Jugement Humain
- 4.2 : Anti-Patterns et Conditions d'Arrêt

### Module 5 : Travail en Équipe (2-3h)

**Tutoriels prévus :**
- 5.1 : Bob en Équipe
- 5.2 : Rôles dans l'Agentic SDLC
- 5.3 : Skills, Modes et Rules comme Mémoire d'Équipe
- 5.4 : Mesurer Bob Sans Théâtre

### Module 6 : Mindset et Pratiques Avancées (1-2h)

**Tutoriels prévus :**
- 6.1 : Le Mindset Bob
- 6.2 : Garder Bob Ennuyeux (Boring)
- 6.3 : Workflows Avancés

---

## 🎯 Parcours Recommandés

### Pour Débutants (4-5h)
```
1. Tutoriel 1.1 : Introduction à IBM Bob
2. Tutoriel 1.2 : Le Cycle de Vie Agentique
3. Tutoriel 2.1 : L'Interface Bob
4. Tutoriel 2.2 : Gestion du Contexte ⭐
5. Tutoriel 2.4 : Première Tâche Accountable
```

### Pour Développeurs (6-8h)
```
Module 1 : Complet (4 tutoriels)
Module 2 : Complet (4 tutoriels)
+ Module 3 quand disponible
```

### Pour Managers (3-4h)
```
1. Tutoriel 1.1 : Introduction
2. Tutoriel 1.2 : Cycle de Vie Agentique
3. Tutoriel 1.4 : Transition des Habitudes
4. Tutoriel 2.2 : Gestion du Contexte (sections pertinentes)
+ Module 5 quand disponible
```

### Pour Architectes (5-6h)
```
Module 1 : Complet
Module 2 : 2.1, 2.2, 2.3
+ Modules 3 et 5 quand disponibles
```

---

## 📊 Statistiques du Parcours

### Tutoriels Créés
- **Total :** 8 tutoriels
- **Module 1 :** 4 tutoriels (100%)
- **Module 2 :** 4 tutoriels (100%)
- **Modules 3-6 :** 0 tutoriels (0%)

### Contenu Produit
- **Pages totales :** ~8,000 lignes de contenu
- **Exercices pratiques :** 40+
- **Exemples concrets :** 100+
- **Auto-évaluations :** 8
- **Cas pratiques :** 8

### Durée Totale
- **Modules 1-2 :** 5-7 heures
- **Parcours complet prévu :** 8-12 heures

---

## 🎓 Utilisation des Tutoriels

### Format de Chaque Tutoriel

Tous les tutoriels suivent une structure cohérente :

```
1. Objectifs d'Apprentissage
2. Contexte Théorique
3. Contenu Détaillé (avec exemples)
4. Exercices Pratiques
5. Auto-Évaluation
6. Ce que Vous Avez Appris
7. Prochaines Étapes
8. Points Clés à Retenir
```

### Éléments Pédagogiques

Chaque tutoriel inclut :
- ✅ Citations du document source
- ✅ Exemples concrets
- ✅ Exercices avec solutions
- ✅ Cas pratiques
- ✅ Auto-évaluation
- ✅ Checklists
- ✅ Templates réutilisables

---

## 🚀 Comment Utiliser Ce Parcours

### Pour les Apprenants

1. **Commencez par le README.md** pour comprendre la structure
2. **Suivez les modules dans l'ordre** (1 → 2 → 3 → etc.)
3. **Faites tous les exercices** pratiques
4. **Pratiquez sur vos projets réels** après chaque tutoriel
5. **Complétez les auto-évaluations** pour valider votre compréhension

### Pour les Formateurs

1. **Utilisez les tutoriels comme support de cours**
2. **Adaptez le contenu** selon votre audience
3. **Créez des sessions pratiques** avec des projets réels
4. **Utilisez le tutoriel 2.2 comme modèle** pour créer d'autres tutoriels
5. **Mesurez la progression** avec les auto-évaluations

### Pour les Équipes

1. **Organisez des sessions de formation** par module
2. **Créez un Context Pack** pour votre projet (voir tutoriel 2.2)
3. **Définissez des workflows d'équipe** avec Bob
4. **Partagez les learnings** entre membres
5. **Mesurez l'impact** avec les métriques suggérées

---

## 📁 Structure des Fichiers

```
parcours-pedagogique-bob/
├── README.md                              # Guide principal
├── parcours-pedagogique-bob.md            # Structure complète
├── TUTORIELS-DISPONIBLES.md              # Ce fichier
├── getting-started-with-bob.txt          # Document source
│
├── Module 1 - Fondamentaux/
│   ├── tutoriel-1.1-introduction-bob.md
│   ├── tutoriel-1.2-cycle-vie-agentique.md
│   ├── tutoriel-1.3-comment-bob-pense.md
│   └── tutoriel-1.4-transition-habitudes.md
│
└── Module 2 - Prise en Main/
    ├── tutoriel-2.1-interface-bob.md
    ├── tutoriel-2.2-gestion-contexte.md      ⭐ CRITIQUE
    ├── tutoriel-2.3-contrats-avant-code.md
    └── tutoriel-2.4-premiere-tache.md
```

---

## 🔄 Prochaines Étapes

### Priorité Haute (Modules 3-4)
1. Développer le Module 3 : Changements Sécurisés
2. Développer le Module 4 : Limites
3. Créer des vidéos de démonstration pour les tutoriels clés

### Priorité Moyenne (Modules 5-6)
4. Développer le Module 5 : Travail en Équipe
5. Développer le Module 6 : Mindset et Pratiques Avancées
6. Créer des templates et exemples de code

### Priorité Basse (Améliorations)
7. Ajouter des cas d'usage par industrie
8. Créer des traductions (FR, DE, ES, etc.)
9. Développer des exercices interactifs
10. Créer une certification formelle

---

## 💡 Contributions

### Comment Contribuer

Si vous souhaitez contribuer au parcours :

1. **Créer des tutoriels supplémentaires** (modules 3-6)
2. **Ajouter des exercices pratiques**
3. **Partager des cas d'usage réels**
4. **Améliorer les exemples existants**
5. **Traduire le contenu**
6. **Créer des vidéos de démonstration**

### Template de Tutoriel

Utilisez le tutoriel 2.2 comme modèle de référence pour créer de nouveaux tutoriels.

---

## 📞 Support

### Obtenir de l'Aide

- Consultez le [README.md](README.md) principal
- Consultez le [parcours-pedagogique-bob.md](parcours-pedagogique-bob.md)
- Contactez votre formateur
- Rejoignez la communauté IBM Bob

### Signaler des Problèmes

- Créez une issue dans le repository
- Suggérez des améliorations
- Partagez vos retours d'expérience

---

## 📝 Changelog

### Version 1.0 (Mai 2026)
- ✅ Module 1 complet (4 tutoriels)
- ✅ Module 2 complet (4 tutoriels)
- ✅ 8 tutoriels détaillés avec exercices
- ✅ 40+ exercices pratiques
- ✅ 8 auto-évaluations
- ✅ Documentation complète

### Versions Futures Prévues
- 📝 Module 3 : Changements Sécurisés
- 📝 Module 4 : Limites
- 📝 Module 5 : Travail en Équipe
- 📝 Module 6 : Mindset et Pratiques Avancées
- 📝 Vidéos de démonstration
- 📝 Traductions

---

## 🎉 Conclusion

Ce parcours pédagogique vous fournit une base solide pour maîtriser IBM Bob. Les modules 1 et 2 couvrent les fondamentaux et la prise en main, vous permettant de commencer à utiliser Bob efficacement dès maintenant.

**Commencez votre apprentissage dès aujourd'hui !**

1. Lisez le [README.md](README.md)
2. Commencez par le [Tutoriel 1.1](tutoriel-1.1-introduction-bob.md)
3. Pratiquez avec le [Tutoriel 2.2](tutoriel-2.2-gestion-contexte.md) ⭐
4. Complétez votre première tâche avec le [Tutoriel 2.4](tutoriel-2.4-premiere-tache.md)

**Bonne formation avec IBM Bob ! 🚀**

---

*Dernière mise à jour : Mai 2026*  
*Version : 1.0*  
*Basé sur : Getting Started with IBM Bob v1.2.0 par Markus Eisele*