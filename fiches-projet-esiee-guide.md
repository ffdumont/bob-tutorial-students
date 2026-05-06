# Fiches Projet ESIEE - Guide d'Utilisation de Bob
## Approche Pédagogique Intégrée

**Version :** 1.0  
**Date :** Mai 2026  
**Basé sur :** Analyse de 6 projets ESIEE en Deep Learning & Reinforcement Learning

---

## 🎯 Objectif des Fiches Projet

Ces fiches projet constituent un **pont entre le parcours pédagogique Bob générique et les projets concrets des étudiants ESIEE**. Chaque fiche :

1. **Mappe le parcours pédagogique** aux besoins spécifiques du projet
2. **Pose des questions contextualisées** à chaque étape
3. **Fournit des prompts Bob prêts à l'emploi** adaptés au projet
4. **Guide progressivement** les étudiants à travers les modules

---

## 📚 Structure d'une Fiche Projet

Chaque fiche suit la structure du parcours pédagogique existant :

### 1. Vue d'Ensemble du Projet
- Objectif et composants principaux
- Technologies utilisées
- Attentes vis-à-vis de Bob

### 2. Module 1 : Fondamentaux (2-3h)
Pour chaque tutoriel (1.1 à 1.4) :
- **Questions spécifiques** au projet
- **Prompts Bob suggérés** contextualisés
- **Exercices pratiques** adaptés

### 3. Module 2 : Prise en Main (3-4h)
Pour chaque tutoriel (2.1 à 2.4) :
- **Configuration Bob** pour le projet
- **Context management** spécifique
- **Contrats types** pour les composants du projet
- **Première tâche guidée** sur le projet réel

### 4. Module 3 : Changements Sécurisés (2-3h)
- **Code review** adapté au domaine
- **Modernisation** des composants
- **Sécurité** spécifique au projet

### 5. Module 4 : Limites (1h)
- **Décisions critiques** que l'étudiant doit prendre
- **Anti-patterns** spécifiques au domaine

### 6. Module 5 : Travail en Équipe (2-3h)
- **Workflow d'équipe** pour le projet
- **Répartition des tâches** suggérée
- **Skills personnalisés** pour le projet

### 7. Module 6 : Mindset (1-2h)
- **Shift mental** pour le projet
- **Workflows "boring"** mais efficaces

### 8. Ressources et Checklist
- **Checklist finale** spécifique au projet
- **Prompts prêts à l'emploi**
- **Ressources complémentaires**

---

## 📋 Les 6 Fiches Projet

### ✅ Fiche 1 : Prédiction S&P 500 (CRÉÉE)
**Fichier :** [`fiche-projet-1-prediction-sp500.md`](fiche-projet-1-prediction-sp500.md)  
**Équipe :** DELEHELLE, KENZOUA, SAAD-EDDINE, CODDEVILLE  
**Domaine :** Finance quantitative  
**Focus :** LSTM + Autoencoders + RL pour prédiction financière

**Points clés :**
- Gestion du data leakage (critique en finance)
- Métriques financières (Sharpe ratio, drawdown)
- Disclaimer éducatif obligatoire
- Trois paradigmes d'apprentissage à intégrer

---

### 📝 Fiche 2 : Emotion-IA (À CRÉER)
**Fichier :** `fiche-projet-2-emotion-ia.md`  
**Équipe :** DIOP, WANDAOGO, DIALLO  
**Domaine :** Vision par ordinateur + RL  
**Focus :** CNN pour émotions + DQN pour ajustement vidéo temps réel

**Points clés spécifiques :**
- Optimisation temps réel (< 100ms)
- Gestion du flux vidéo webcam
- Ajustement dynamique des paramètres
- Interface Streamlit temps réel
- Détection de biais démographiques

**Questions spécifiques à intégrer :**
- Comment optimiser l'inférence CNN pour le temps réel ?
- Comment l'agent DQN doit-il ajuster contraste/exposition ?
- Comment détecter et corriger les biais dans les émotions ?
- Comment gérer la latence du pipeline complet ?

---

### 📝 Fiche 3 : CurioRL (À CRÉER)
**Fichier :** `fiche-projet-3-curiorl.md`  
**Équipe :** DOMONQ  
**Domaine :** Recherche en RL  
**Focus :** VAE + Clustering + PPO pour exploration par curiosité

**Points clés spécifiques :**
- Architecture complexe (3 composants interdépendants)
- Récompenses intrinsèques (curiosité)
- Clustering dynamique sur espace latent
- Environnement MiniGrid
- Debugging avancé (collapse de politique, clusters dégénérés)

**Questions spécifiques à intégrer :**
- Comment structurer les 3 modules avec faible couplage ?
- Comment calculer les récompenses de curiosité ?
- Comment détecter le collapse de politique ?
- Comment visualiser l'espace latent et les clusters ?
- Comment Bob peut aider au debugging de comportements émergents ?

---

### 📝 Fiche 4 : SmartFlow (À CRÉER)
**Fichier :** `fiche-projet-4-smartflow.md`  
**Équipe :** VOLCY, GUIRAUDEN  
**Domaine :** Vision + RL pour trafic urbain  
**Focus :** YOLO/Faster R-CNN + PPO + Simulation SUMO

**Points clés spécifiques :**
- Intégration DL (détection) → RL (décision)
- Simulation SUMO (environnement complexe)
- Métriques urbaines (temps d'attente, émissions CO2)
- Dashboard de visualisation temps réel
- Cas d'usage : véhicules d'urgence

**Questions spécifiques à intégrer :**
- Comment connecter YOLO à l'environnement Gymnasium ?
- Comment définir la fonction de récompense (multi-objectifs) ?
- Comment gérer les événements aléatoires (accidents, urgences) ?
- Comment visualiser la simulation et les décisions de l'agent ?
- Comment Bob peut aider à l'intégration SUMO ?

---

### 📝 Fiche 5 : Détection de Fraude (À CRÉER)
**Fichier :** `fiche-projet-5-detection-fraude.md`  
**Équipe :** DEBBAGH, JABRY, GUEDIRI  
**Domaine :** Sécurité financière  
**Focus :** DL pour classification + RL + Dataset déséquilibré

**Points clés spécifiques :**
- Dataset massivement déséquilibré (0.17% de fraudes)
- Temps réel (inférence rapide)
- Métriques adaptées (F1-score, AUC-ROC, pas accuracy)
- Interface Streamlit pour test
- Gestion des faux positifs/négatifs

**Questions spécifiques à intégrer :**
- Comment gérer le déséquilibre extrême des classes ?
- Quelles techniques de sampling utiliser ?
- Comment optimiser pour le temps réel ?
- Comment expliquer les prédictions (SHAP, LIME) ?
- Quelles métriques suivre en production ?

---

### 📝 Fiche 6 : Système de Recommandation (À CRÉER)
**Fichier :** `fiche-projet-6-recommandation.md`  
**Équipe :** PRAT, AÏSSAOUI, GUILLERMET-LAOUAD, JMAL  
**Domaine :** Recommandation adaptative  
**Focus :** Filtrage collaboratif + RL simplifié + Interface web

**Points clés spécifiques :**
- Dataset MovieLens (simple et connu)
- RL simplifié (apprentissage des likes/dislikes)
- Interface utilisateur intuitive
- Adaptation progressive aux préférences
- IA explicable (pourquoi cette recommandation ?)

**Questions spécifiques à intégrer :**
- Comment implémenter le filtrage collaboratif efficacement ?
- Comment l'agent RL doit-il apprendre des feedbacks ?
- Comment créer une interface Streamlit engageante ?
- Comment expliquer les recommandations à l'utilisateur ?
- Comment gérer le cold start (nouveaux utilisateurs) ?

---

## 🎓 Comment Utiliser les Fiches Projet

### Pour les Étudiants

**Étape 1 : Identifier votre projet**
- Trouvez la fiche correspondant à votre projet
- Lisez la vue d'ensemble pour comprendre le mapping

**Étape 2 : Suivre le parcours progressivement**
- Commencez par le Module 1 (Fondamentaux)
- Pour chaque tutoriel du parcours pédagogique :
  1. Lisez le tutoriel générique
  2. Consultez la section correspondante dans votre fiche projet
  3. Répondez aux questions spécifiques
  4. Utilisez les prompts Bob suggérés
  5. Faites les exercices adaptés

**Étape 3 : Itérer et documenter**
- Documentez vos réponses aux questions
- Notez les prompts Bob qui fonctionnent bien
- Partagez vos learnings avec l'équipe

**Exemple de workflow :**
```
1. Lire tutoriel-2.2-gestion-contexte.md (générique)
2. Consulter fiche-projet-X.md → Section "Module 2.2"
3. Répondre aux questions spécifiques à mon projet
4. Créer mon Context Pack avec les suggestions
5. Tester avec Bob sur une tâche réelle
6. Documenter ce qui fonctionne
```

---

### Pour les Enseignants

**Utilisation en cours :**
1. Présentez le parcours pédagogique générique
2. Montrez comment les fiches projet s'y intègrent
3. Guidez les étudiants vers leur fiche spécifique
4. Encouragez la documentation des learnings

**Suivi des étudiants :**
- Vérifiez qu'ils utilisent les questions comme guide
- Demandez-leur de partager leurs prompts Bob efficaces
- Collectez les cas d'usage réussis
- Enrichissez les fiches avec les retours

**Évaluation :**
- Utilisez les checklists finales de chaque fiche
- Évaluez la qualité des contrats définis
- Vérifiez la compréhension du contexte management
- Mesurez l'autonomie progressive

---

## 🔄 Évolution des Fiches

### Version Actuelle (1.0)
- ✅ Fiche 1 : Prédiction S&P 500 (complète)
- 📝 Fiches 2-6 : À créer

### Améliorations Futures
- [ ] Ajouter des vidéos de démonstration
- [ ] Créer des templates de code réutilisables
- [ ] Ajouter des cas d'usage documentés par les étudiants
- [ ] Créer des FAQ par projet
- [ ] Développer des exercices interactifs

---

## 📊 Comparaison des Projets

### Par Complexité Technique

**Haute complexité :**
- CurioRL (3 paradigmes interdépendants, recherche)
- SmartFlow (intégration SUMO, multi-objectifs)

**Complexité moyenne :**
- Prédiction S&P 500 (3 composants mais indépendants)
- Emotion-IA (temps réel, optimisation)

**Complexité accessible :**
- Détection de Fraude (focus sur déséquilibre)
- Recommandation (RL simplifié)

### Par Focus Bob

**Architecture et structuration :**
- CurioRL (modularité critique)
- Prédiction S&P 500 (3 composants)

**Optimisation performance :**
- Emotion-IA (temps réel)
- Détection de Fraude (inférence rapide)

**Intégration et visualisation :**
- SmartFlow (SUMO + dashboard)
- Recommandation (interface utilisateur)

### Par Besoins Spécifiques Bob

**Génération de code complexe :**
- CurioRL, SmartFlow

**Review et debugging :**
- Tous les projets

**Optimisation :**
- Emotion-IA, Détection de Fraude

**Documentation et explicabilité :**
- Recommandation, Détection de Fraude

---

## 💡 Conseils Transversaux

### Tous les Projets DL+RL

**Gestion du contexte :**
- Toujours exclure les données brutes volumineuses
- Inclure les fichiers de configuration
- Prioriser les fichiers de modèles

**Contrats types :**
- Intent clair avec métriques de succès
- Contraintes techniques explicites
- Vérification sur données de test

**Anti-patterns communs :**
- ❌ Optimiser sans validation croisée
- ❌ Ignorer le data leakage
- ❌ Copier-coller sans adaptation
- ❌ Négliger la reproductibilité

**Bonnes pratiques :**
- ✅ Définir des seeds aléatoires
- ✅ Séparer train/val/test proprement
- ✅ Documenter les choix d'architecture
- ✅ Tester sur données out-of-sample

---

## 🎯 Objectifs d'Apprentissage Communs

À la fin de leur projet, tous les étudiants devraient :

### Compétences Bob
- [ ] Formuler des prompts précis et contextuels
- [ ] Gérer efficacement le contexte (Context Pack)
- [ ] Définir des contrats clairs avant le code
- [ ] Utiliser Bob pour la review de code
- [ ] Itérer sur les suggestions de Bob

### Compétences Techniques DL+RL
- [ ] Intégrer plusieurs paradigmes d'apprentissage
- [ ] Gérer les données (preprocessing, splits)
- [ ] Optimiser les performances (GPU, inférence)
- [ ] Créer des interfaces de visualisation
- [ ] Tester et valider rigoureusement

### Compétences Transversales
- [ ] Travailler en équipe avec des outils IA
- [ ] Documenter son travail
- [ ] Débugger efficacement
- [ ] Évaluer et améliorer continuellement

---

## 📞 Support et Ressources

### Documentation
- [Parcours Pédagogique Bob](parcours-pedagogique-bob.md)
- [Tutoriels Disponibles](TUTORIELS-DISPONIBLES.md)
- [Synthèse des Projets ESIEE](synthese-projets-esiee.md)

### Fiches Projet
- [Fiche 1 : Prédiction S&P 500](fiche-projet-1-prediction-sp500.md) ✅
- Fiche 2 : Emotion-IA (à créer)
- Fiche 3 : CurioRL (à créer)
- Fiche 4 : SmartFlow (à créer)
- Fiche 5 : Détection de Fraude (à créer)
- Fiche 6 : Recommandation (à créer)

### Communauté
- Forums IBM Bob
- Partage entre étudiants ESIEE
- Retours d'expérience

---

## 🚀 Prochaines Étapes

### Priorité Immédiate
1. ✅ Valider l'approche avec Fiche 1
2. 📝 Créer les Fiches 2-6
3. 📝 Enrichir les tutoriels existants avec sections DL+RL
4. 📝 Mettre à jour le parcours pédagogique

### Priorité Moyenne
5. Collecter les retours des étudiants
6. Enrichir avec des cas d'usage réels
7. Créer des vidéos de démonstration
8. Développer des templates réutilisables

### Priorité Basse
9. Créer des exercices interactifs
10. Traduire en d'autres langues
11. Développer une certification

---

## 📝 Template pour Nouvelles Fiches

Si vous souhaitez créer une fiche pour un nouveau projet :

```markdown
# Fiche Projet : [Nom du Projet]
## Guide d'Utilisation de Bob pour Votre Projet

**Équipe :** [Noms]
**Domaine :** [Domaine]
**Technologies :** [Liste]

---

## 🎯 Vue d'Ensemble du Projet
[Description, objectifs, composants]

---

## 📚 Parcours Pédagogique Adapté

### Module 1 : Fondamentaux
[Pour chaque tutoriel 1.1-1.4]

### Module 2 : Prise en Main
[Pour chaque tutoriel 2.1-2.4]

### Module 3 : Changements Sécurisés
[Tutoriels 3.1-3.3]

### Module 4 : Limites
[Tutoriels 4.1-4.2]

### Module 5 : Travail en Équipe
[Tutoriels 5.1-5.4]

### Module 6 : Mindset
[Tutoriels 6.1-6.3]

---

## 🎯 Checklist Finale
[Checklist spécifique au projet]

---

## 💡 Prompts Bob Prêts à l'Emploi
[Liste de prompts contextualisés]
```

---

**Version :** 1.0  
**Dernière mise à jour :** Mai 2026  
**Statut :** Fiche 1 créée, Fiches 2-6 à créer