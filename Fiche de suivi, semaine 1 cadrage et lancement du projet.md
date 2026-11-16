# Fiche de suivi, semaine 1 : cadrage et lancement du projet

Nov 16, 2026 · @Larhlimi

## Mode d'emploi

Cette fiche fixe votre projet et prouve que le groupe a démarré : elle compte pour 5 points sur 100. Les fiches des semaines 2 et 3 comptent chacune pour 10 points.

- Une seule fiche par groupe, remplie ensemble et relue par chaque membre.
- Dépôt de la fiche : `docs/suivi/fiche-semaine-1.md` dans le dépôt GitHub du groupe (push S1-6 de la liste des push).
- Date limite : fin de la semaine 1 du projet, à la date annoncée en séance.
- Réponses courtes et vérifiables : un chiffre, un lien ou un nom de fichier valent mieux qu'une phrase générale.
- Si un point n'est pas encore tranché, écrivez « à décider » et la date de décision, plutôt que de laisser la case vide.

Rappel du barème du projet, sur 100 : application finale 20, dépôt GitHub 20, fiches hebdomadaires 25 (5 + 10 + 10), soutenance 20, compte rendu 15.

## 1. Identification du groupe

| Élément | Votre réponse |
| --- | --- |
| Nom du groupe |  |
| Titre du projet |  |
| Sujet : numéro du catalogue, ou « hors catalogue » |  |
| Adresse du dépôt GitHub |  |
| Enseignant ajouté au dépôt (oui ou non) |  |
| Date de remise de la fiche |  |

Membres du groupe (2 à 4 lignes) :

| Nom et prénom | Compte GitHub | Rôle principal dans le projet |
| --- | --- | --- |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

## 2. Sujet et besoin

| Question | Votre réponse |
| --- | --- |
| Besoin en une phrase |  |
| Utilisateur final : qui se sert de l'application |  |
| Ce que fait l'application, vu par l'utilisateur (3 lignes au plus) |  |
| Approche retenue (règles, apprentissage, RAG, agent) et raison du choix |  |
| Conséquence d'une erreur de l'application, et validation humaine prévue |  |
| Sujet hors catalogue : projet du catalogue auquel il est comparable |  |

## 3. Périmètre

La version minimale est le parcours complet le plus simple, de la demande de l'utilisateur jusqu'à la réponse affichée. Elle doit fonctionner à la fin de la semaine 2.

| Rubrique | Votre réponse |
| --- | --- |
| Version minimale : le parcours que vous montrerez en semaine 2 |  |
| Fonction 1, indispensable |  |
| Fonction 2, indispensable |  |
| Fonction 3, si le temps le permet |  |
| Hors périmètre : ce que vous ne ferez pas |  |

## 4. Architecture et technologies

| Composant | Choix prévu | Dossier ou fichier dans le dépôt |
| --- | --- | --- |
| Cœur : modèle, agent ou chaîne RAG |  |  |
| API |  |  |
| Interface |  |  |
| Données et stockage |  |  |
| Tests |  |  |
| Services externes et clés nécessaires |  |  |

Joignez un schéma d'architecture au dépôt (`docs/architecture.png`, ou un diagramme Mermaid dans le README) et indiquez son lien ici :

## 5. Données

Règle du cours : uniquement des données publiques, fictives ou anonymisées.

| Question | Votre réponse |
| --- | --- |
| Origine des données (source, licence) |  |
| Volume disponible aujourd'hui |  |
| Format |  |
| Données personnelles : non, ou oui avec la méthode d'anonymisation |  |
| Jeu d'essai versionné dans le dépôt : chemin du fichier ou du script |  |

### Description du jeu de données

Décrivez le jeu de données tel qu'il est aujourd'hui, chiffres à l'appui. Chaque chiffre doit pouvoir être recalculé par un script du dépôt. Si votre projet n'utilise pas de tableau de données (agent, questions sur des documents), décrivez de la même façon votre corpus de documents ou votre jeu de cas d'évaluation.

Vue d'ensemble :

| Caractéristique | Votre réponse |
| --- | --- |
| Ce que représente une ligne (ou un document) |  |
| Nombre de lignes ou de documents |  |
| Nombre de variables (colonnes) |  |
| Période couverte et langue |  |
| Variable cible ou réponse attendue, s'il y en a une |  |
| Répartition de la cible : effectif par classe, ou minimum, moyenne et maximum |  |
| Pour un corpus de textes : longueur moyenne d'un document, en mots |  |
| Valeurs manquantes et doublons : nombre et traitement prévu |  |
| Découpage prévu : entraînement, test, évaluation |  |
| Script qui recalcule ces chiffres : chemin dans le dépôt |  |

Dictionnaire des variables (une ligne par colonne utilisée) :

| Variable | Type (texte, nombre, catégorie, date) | Signification | Exemple de valeur | Valeurs manquantes (%) |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |

Trois exemples tirés du jeu de données :

| Exemple (entrée) | Réponse ou étiquette attendue | Nature de l'exemple : cas simple, cas difficile, cas limite |
| --- | --- | --- |
|  |  |  |
|  |  |  |
|  |  |  |

Limites connues du jeu de données (taille, déséquilibre entre classes, biais, données générées) :

## 6. Critères de réussite

Un critère est mesurable s'il a une valeur cible et une façon de la vérifier. Donnez-en trois ; la première ligne est un exemple à remplacer.

| Critère | Mesure | Valeur cible | Comment vous le vérifierez |
| --- | --- | --- | --- |
| Exemple : réponses correctes | Part de réponses justes sur 20 questions de test | 16 sur 20 | Script `tests/evaluation.py` |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

## 7. Répartition et planning sur 3 semaines

Un livrable par semaine, repéré par un tag Git. Précisez ce que chaque livrable veut dire pour votre projet.

| Semaine | Livrable attendu | Pour votre projet, concrètement | Responsable | Tag |
| --- | --- | --- | --- | --- |
| 1 | Cadrage, dépôt initialisé, squelette exécutable |  |  | `s1` |
| 2 | Version minimale qui fonctionne de bout en bout |  |  | `s2` |
| 3 | Application finale, documentation, compte rendu |  |  | `v1.0.0` |

Répartition des responsabilités :

| Membre | Responsabilités sur les 3 semaines | Remplaçant en cas d'absence |
| --- | --- | --- |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

## 8. Travail réalisé en semaine 1

Chaque membre remplit sa ligne lui-même. Le lien pointe vers ses commits ou sa pull request sur GitHub.

| Membre | Ce que j'ai fait cette semaine | Lien vers mes commits | Temps passé (heures) |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

État du dépôt à la remise de la fiche :

- [ ] Dépôt créé, enseignant et tous les membres ajoutés
- [ ] README avec le titre, les membres, le sujet et les commandes d'installation (S1-1)
- [ ] Au moins un commit de chaque membre, depuis son propre compte (S1-2)
- [ ] `requirements.txt` installable sur un clone neuf, `.env.example` présent, aucun secret poussé (S1-3)
- [ ] Squelette exécutable et au moins un test qui passe (S1-4)
- [ ] Jeu d'essai et schéma d'architecture dans le dépôt (S1-5)
- [ ] Cette fiche poussée dans `docs/suivi/` et tag `s1` posé (S1-6)

## 9. Risques et points de blocage

| Risque ou blocage | Probabilité (faible, moyenne, forte) | Ce que vous ferez si cela arrive | Qui surveille |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

Question à poser à l'enseignant, s'il y en a une :

## 10. Engagements pour la semaine 2

Trois engagements au plus, chacun vérifiable dans le dépôt. Ils seront relus dans la fiche de la semaine 2.

| Engagement | Responsable | Comment on saura que c'est fait |
| --- | --- | --- |
|  |  |  |
|  |  |  |
|  |  |  |

## Cadre réservé à l'enseignant

| Rubrique | Barème | Note |
| --- | --- | --- |
| Cadrage : sujet, périmètre, critères mesurables (rubriques 2, 3 et 6) | 2 |  |
| Organisation : architecture, données, rôles, planning (rubriques 4, 5 et 7) | 1 |  |
| Preuves GitHub de la semaine 1, contribution de chaque membre (rubrique 8) | 1,5 |  |
| Risques et engagements pour la semaine 2 (rubriques 9 et 10) | 0,5 |  |
| **Total** | **5** |  |

Décision : sujet validé, ou fiche à reprendre avant le :

Commentaire :
