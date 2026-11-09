# Livrable 3 : maquette globale

**Rédacteur :** Aya Hbibou   **Relecteur :** Khaoula Essammouni  **Fichiers :** docs/semaine1/3-maquette.md + docs/semaine1/img/

## 3.1 Schéma d'architecture

```mermaid
flowchart TD
    U["Technicien"] -->|"1. consulte, valide ou refuse"| UI["Streamlit : tableau de bord"]
    UI -->|"2. requête REST"| API["FastAPI : contrôle d'accès et journalisation"]
    API -->|"3. lance l'analyse"| ORC["Orchestrateur Python"]

    S["Capteurs simulés : vibration, température, courant"] -->|"mesures"| ING
    ORC --> ING["Ingestion et nettoyage"]
    ING --> DER["Détection de dérives : Isolation Forest"]
    DER --> RUL["Estimation de la RUL : Random Forest + SHAP"]
    RUL --> PLAN["Planification : règles RUL, criticité, planning"]
    PLAN --> OT["Création de l'ordre de travail"]

    RAG["Mini-RAG : fiches de maintenance"] -->|"pièces et procédure"| OT
    RUL -.->|"optionnel"| LLM["LLM : rédaction du diagnostic"]
    LLM -.-> OT

    OT --> DB[("SQLite : GMAO simulée")]
    DB -->|"4. ordre de travail proposé"| API
    API -->|"5. réponse"| UI
    UI -->|"6. décision du technicien"| API
    API -->|"journal des décisions"| DB

    ML["MLflow et DVC : modèles et données"] -.-> DER
    ML -.-> RUL
```

**Parcours d'une requête :** le technicien ouvre le tableau de bord, Streamlit interroge l'API FastAPI, qui déclenche l'orchestrateur. Celui-ci enchaîne ingestion, détection de dérives, RUL, planification et création de l'ordre de travail. L'ordre est enregistré dans SQLite et renvoyé au tableau de bord. Le technicien le valide ou le refuse, et la décision est journalisée.

## 3.2 Légende du schéma

| Composant | Rôle | Fonctionnalité |
|-----------|------|----------------|
| Technicien | Utilisateur qui décide (validation obligatoire) | F3 |
| Streamlit | Tableau de bord : courbes, alertes, RUL, validation ou refus | F3 |
| FastAPI | Point d'entrée REST, contrôle d'accès, journalisation des décisions | F1, F2, F3 |
| Orchestrateur Python | Enchaîne les modules de la chaîne de traitement | F1, F2 |
| Capteurs simulés | Mesures de vibration, température et courant (courant simulé) | F1 |
| Ingestion et nettoyage | Valeurs manquantes et aberrantes, synchronisation, fenêtres glissantes | F1 |
| Détection de dérives | Isolation Forest entraîné sur le comportement normal | F1 |
| Estimation de la RUL | Random Forest avec incertitude, explication SHAP | F1 |
| LLM (optionnel) | Rédige le diagnostic en langage clair, sans décider | F1 |
| Planification | Règles selon la RUL, la criticité et le planning de production | F2 |
| Mini-RAG | Retrouve pièces et procédure dans les fiches de maintenance, avec citations | F2 |
| Création de l'ordre de travail | Assemble fenêtre d'intervention, pièces et procédure | F2 |
| SQLite (GMAO simulée) | Équipements, pièces, ordres de travail, journal des décisions | F2, F3 |
| MLflow et DVC | Suivi des expériences et versionnement des données et modèles | Support de F1 |
| Docker Compose et GitHub Actions | Environnement reproductible, tests et construction automatisés | Support de F1 à F3 |

## 3.3 Maquette des écrans