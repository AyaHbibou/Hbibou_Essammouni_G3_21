# Livrable 2 : jeu de données

**Rédacteur :** Essammouni  |  **Relecteur :** Hbibou
**Fichiers :** `docs/semaine1/2-dataset.md` + `data/sample/`

## 2.1 Description

| Rubrique | Réponse |
|---|---|
| Nom et source (lien) | NASA C-MAPSS (Turbofan Engine Degradation Simulation), sous-ensemble **FD001**. Copie utilisée : https://huggingface.co/datasets/SoyVitou/NASA-C-MAPSS-Turbofan-Engine (configuration `FD001`). Dépôt d'origine : https://www.nasa.gov/content/prognostics-center-of-excellence-data-set-repository |
| Producteur ou propriétaire | NASA, Prognostics Center of Excellence (Saxena et Goebel, 2008). La version Hugging Face est une copie nettoyée publiée par un tiers (SoyVitou). |
| Volume | 1 fichier parquet (`cmapss_fd001_train.parquet`, environ 0,5 Mo), **20 631 lignes**, **29 colonnes**, **100 moteurs** menés jusqu'à la panne (de 128 à 362 cycles selon le moteur). |
| Format et structure | Parquet (échantillon livré en CSV). Série temporelle par moteur : `unit_id`, `cycle`, 3 réglages (`setting_1` à `setting_3`), 21 capteurs (`T24`, `T30`, `T50`, `P30`, `Nf`, `Nc`, `Ps30`, `phi`, `BPR`, `htBleed`, `W31`, `W32`, etc.), cible `RUL` (cycles restants), plus `dataset` et `split`. |
| Langue et période couverte | Données numériques, sans langue. Simulation sans calendrier : l'axe du temps est le numéro de cycle. |
| Licence et droits d'usage |  la page Hugging Face n'indique aucune |
| Données personnelles ou sensibles | Aucune (données simulées de moteurs). |
| Emplacement des données complètes | récupérées par `python src/agent/load_data.py` (Hugging Face) |

## 2.2 Qualité constatée sur l'échantillon

- **Valeurs manquantes :** aucune (0 sur 20 631 lignes).
- **Colonnes constantes :** 7 colonnes sans variation (`setting_3`, `T2`, `P2`, `epr`, `farB`, `Nf_dmd`, `PCNfR_dmd`), retirées au nettoyage.
- **Bruit :** capteurs bruités par construction ; les valeurs extrêmes sont signalées mais **pas supprimées**, car elles font partie de la dégradation simulée.
- **Doublons et cycles manquants :** contrôlés par `check_quality` dans `data.py` (reporter ici le résultat affiché).


## 2.3 Justification

| Fonctionnalité | Données utilisées | En quoi elles suffisent |
|---|---|---|
| F1 : détection des dérives, RUL avec intervalle et explication | C-MAPSS FD001 : capteurs, colonne `RUL`, 50 premiers cycles de chaque moteur comme comportement normal | 100 trajectoires complètes jusqu'à la panne : le profil normal est appris sur les premiers cycles, la RUL exacte sert à entraîner et à mesurer, l'intervalle se calibre sur le jeu de validation (découpage **par moteur**), et SHAP s'applique directement à ces variables tabulaires. |
| F2 : fenêtre d'intervention et ordre de travail | RUL estimée (F1), criticité et planning de production simulés, **corpus de fiches de maintenance et catalogue de pièces** rédigés par le binôme | La fenêtre ne demande que la RUL, la criticité et le planning. Les pièces et la procédure viennent des fiches. C-MAPSS ne contient aucune donnée de maintenance : ce corpus est écrit par l'équipe (5 à 10 fiches). |
| F3 : tableau de bord et validation par le technicien | Capteurs de C-MAPSS rejoués cycle par cycle comme un flux, scores et RUL de F1, décisions enregistrées dans SQLite | Le rejeu d'un moteur simule le temps réel. L'historique des validations et refus est produit par l'application, sans donnée externe. Le courant (simulé) s'affiche à côté des capteurs. |



## 2.4 Alternative de réponse

- **Si le dépôt Hugging Face disparaît :** télécharger C-MAPSS depuis le dépôt NASA PCoE (lien ci-dessus), même contenu d'origine ; il faut seulement reconstruire la colonne `RUL` (cycle maximum du moteur moins le cycle courant).
- **Si C-MAPSS devient inutilisable :** utiliser FEMTO / PRONOSTIA (roulements réels, vibration et température, run-to-failure) ou générer des données simulées (dégradation progressive avec bruit).
- **Ce que l'on perd :** avec FEMTO, moins de moteurs et des données brutes à traiter ; avec des données simulées, aucune validité sur du réel et un risque de modèle trop facile.


## 2.5 Jeu de test

- **Taille :** au moins 45 cas : chaque moteur du jeu de test (environ 15, à confirmer avec la sortie de `data.py`) est coupé à 3 moments de sa vie (RUL réelle proche de 100, 50 et 10 cycles).
- **Origine :** moteurs mis de côté dès le découpage par moteur, jamais vus à l'entraînement.
- **Réponses attendues :** RUL réelle (fournie par le jeu) et alerte attendue ou non ; pour la détection, étiquette « dégradé » (RUL ≤ 30).
- **Scénarios d'ordre de travail :** 20 cas rédigés par l'équipe (équipement, RUL, criticité, planning, pièces attendues).
- **Métriques :** RMSE de la RUL, taux de fausses alarmes, délai moyen entre l'alerte et la panne, complétude de l'ordre de travail.

## Critères d'acceptation (à vérifier par le récepteur)

- [ ] L'échantillon est dans `data/sample/` et s'ouvre sans erreur.
- [x] La licence autorise l'utilisation dans un projet de cours.
- [x] Aucune donnée personnelle.
- [x] Chaque fonctionnalité du MVP est couverte par la justification.
- [x] L'alternative de réponse est accessible (liens vérifiés).
- [x] Le jeu de test est défini.
