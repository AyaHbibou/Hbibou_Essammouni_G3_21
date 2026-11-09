# Livrable 1 : descriptif du projet mis à jour

**Rédacteur :** Aya Hbibou   **Relecteur :** Khaoula Essammouni  **Fichier :** docs/semaine1/1-descriptif.md

## 1.1 Contexte et problème

Les pannes non planifiées de pompes et de moteurs électriques causent des arrêts de production, des coûts élevés et des risques de sécurité. Les équipes de maintenance et leurs techniciens travaillent aujourd'hui en maintenance corrective (réparation après la panne) ou préventive à intervalles fixes. Ces deux approches sont coûteuses : la première subit les arrêts, la seconde remplace des pièces encore saines. Il manque un outil qui détecte la dégradation d'un roulement à l'avance et déclenche l'intervention au bon moment.

## 1.2 Objectif en une phrase

Détecter les dérives des capteurs d'un équipement tournant, estimer sa durée de vie restante (RUL) avec une incertitude, puis proposer au technicien un ordre de travail planifié qu'il valide.

## 1.3 Utilisateurs cibles et scénario d'usage principal

**Utilisateurs :** le technicien de maintenance (il décide) et le responsable maintenance (il suit l'état du parc d'équipements).

**Scénario :**
1. L'agent reçoit en continu les mesures des capteurs (vibration, température, courant) de plusieurs équipements simulés.
2. Il nettoie les séries temporelles et les compare au profil normal appris.
3. Lorsqu'une dérive apparaît, il l'affiche avec un niveau de confiance.
4. Il estime la RUL de l'équipement, avec son incertitude, et explique son diagnostic.
5. Il propose une fenêtre d'intervention selon la RUL, la criticité et le planning de production.
6. Il prépare l'ordre de travail dans la GMAO simulée, avec les pièces et la procédure.
7. Le technicien valide ou refuse l'ordre de travail ; la décision est journalisée.

## 1.4 Fonctionnalités du MVP (binôme : 2 à 3)

| N° | Fonctionnalité | Ce que l'utilisateur voit ou obtient | Priorité (indispensable, souhaitable) |
|----|----------------|--------------------------------------|---------------------------------------|
| F1 | Détection des dérives et estimation de la RUL | Pour chaque équipement : un score de dérive, une RUL avec intervalle d'incertitude, et une explication du diagnostic (SHAP, avec texte rédigé par le LLM s'il est retenu) | Indispensable |
| F2 | Planification et ordre de travail | Une fenêtre d'intervention proposée selon la RUL, la criticité et le planning, puis un ordre de travail dans la GMAO simulée avec pièces et procédure issues des fiches de maintenance  | Indispensable |
| F3 | Tableau de bord et validation par le technicien | Courbes des capteurs, alertes, RUL et fenêtre proposée ; boutons pour valider ou refuser l'ordre de travail, avec historique des décisions | Indispensable |


## 1.5 Services et composants techniques

| Service ou composant | Rôle dans le projet | Technologie choisie | Pourquoi ce choix |
|----------------------|---------------------|---------------------|-------------------|
| Modèle (LLM ou ML) | Détection des dérives, estimation de la RUL, rédaction optionnelle du diagnostic | Isolation Forest (ou autoencodeur) ; Random Forest ; LLM optionnel | Modèles simples et explicables avec SHAP ; le LLM ne fait que rédiger, jamais décider |
| Recherche ou mémoire (RAG, base vectorielle, SGBD) | GMAO simulée (équipements, pièces, ordres de travail) et recherche dans les fiches de maintenance | SQLite ; mini-RAG avec index vectoriel (FAISS ou Chroma, à confirmer) | SQLite suffit pour une GMAO simulée ; le RAG fournit pièces et procédure avec sources citées |
| Outils appelés par l'agent | Détection de dérives, estimation de la RUL, planification, création de l'ordre de travail | Orchestrateur Python enchaînant les modules | Chaîne simple et testable, module par module |
| API | Exposer mesures, dérives, RUL, planification et ordres de travail | FastAPI | Validation Pydantic et documentation Swagger automatiques |
| Interface | Tableau de bord et validation humaine | Streamlit | Interface de démonstration rapide en Python |
| Conteneur et intégration continue | Environnement reproductible, tests et construction automatisés | Docker , GitHub Actions | Même environnement pour les deux membres du binôme et vérification à chaque push |
| Suivi des données et des expériences | Reproductibilité des jeux de données et comparaison des essais | DVC, MLflow | Versionner C-MAPSS, CWRU, FEMTO et retrouver le meilleur modèle |

## 1.6 Hors périmètre

- Machines et GMAO réelles (données de bancs d'essai ou simulées uniquement).
- Défauts multiples simultanés : un seul type de dégradation par équipement.
- Optimisation globale du planning de production.
- Pompes et moteurs électriques réels (extension possible).

## 1.7 Écart avec la fiche du catalogue

- **Ajouts :** estimation de la RUL avec incertitude communiquée ; validation obligatoire du technicien pour chaque ordre de travail ; mini-RAG sur des fiches de maintenance pour les pièces et la procédure ; explication et niveau de confiance pour chaque alerte.
- **Modifications :** capteurs IoT et GMAO réels remplacés par des versions simulées, faute d'accès à du matériel industriel ; données issues de jeux publics (C-MAPSS pour la RUL, CWRU et FEMTO pour la vibration), avec le courant simulé.
- **Retraits :** aucun.
- **Pourquoi :** rester réalisable en binôme, avec des données publiques, tout en gardant une chaîne complète de la mesure à l'ordre de travail validé.