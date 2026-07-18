# Roadmap — Bases de Données

> **Matière** : SQL / PL/SQL / Oracle / Conception  
> **Objectif** : Maîtriser la conception, l'implémentation et l'optimisation de bases de données relationnelles

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **Modèle relationnel** | Modèle où les données sont représentées par des relations (tables) avec des attributs, proposé par E.F. Codd en 1969 |
| **Relation / Table** | Ensemble de tuples, structuré en lignes et colonnes |
| **Attribut** | Colonne d'une relation, définie par un nom et un domaine |
| **Domaine** | Ensemble de valeurs autorisées pour un attribut |
| **Tuple / Enregistrement** | Ligne d'une relation |
| **Clé primaire (PK)** | Attribut ou combinaison qui identifie de façon unique chaque tuple |
| **Clé étrangère (FK)** | Attribut référençant la clé primaire d'une autre table |
| **Schéma** | Structure d'une base (noms des tables, attributs, types, contraintes) |
| **Extension** | Ensemble des tuples d'une relation à un instant donné |

### 🟢 SQL DDL & DML

| Concept | Définition |
|---------|-----------|
| **DDL** | Data Definition Language — `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** | Data Manipulation Language — `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| **SELECT** | Requête d'interrogation avec projection (`SELECT`), sélection (`WHERE`), jointures (`JOIN`) |
| **Jointure (JOIN)** | Combinaison de lignes de deux tables basée sur une condition (`INNER`, `LEFT`, `RIGHT`, `FULL`) |
| **Sous-requête** | Requête imbriquée dans une autre requête |
| **Agrégation** | `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` avec `GROUP BY` et `HAVING` |
| **Vue (VIEW)** | Table virtuelle basée sur une requête stockée |

### 🟡 Conception & Normalisation

| Concept | Définition |
|---------|-----------|
| **MCD (Modèle Conceptuel de Données)** | Représentation entité-association (entités, relations, cardinalités) |
| **MLD (Modèle Logique de Données)** | Traduction du MCD en tables relationnelles |
| **1ère Forme Normale (1NF)** | Chaque attribut contient une valeur atomique |
| **2ème Forme Normale (2NF)** | 1NF + toute dépendance fonctionnelle non-triviale porte sur la totalité de la clé primaire |
| **3ème Forme Normale (3NF)** | 2NF + pas de dépendance transitive d'un attribut non-clé vers un autre attribut non-clé |
| **Dépendance fonctionnelle** | `X → Y` signifie que la valeur de X détermine la valeur de Y |

### 🟡 Transactions & Intégrité

| Concept | Définition |
|---------|-----------|
| **Transaction** | Unité logique de travail (une ou plusieurs opérations SQL) |
| **ACID** | Atomicité, Cohérence, Isolation, Durabilité |
| **COMMIT** | Valide la transaction en cours |
| **ROLLBACK** | Annule la transaction en cours |
| **Contrainte d'intégrité** | Règle qui garantit la cohérence des données (domaine, PK, FK, CHECK, UNIQUE) |

### 🔴 Avancés

| Concept | Définition |
|---------|-----------|
| **PL/SQL** | Langage procédural Oracle — blocs, curseurs, exceptions, procédures stockées, triggers |
| **Trigger** | Procédure déclenchée automatiquement avant/après une opération DML |
| **Curseur** | Pointeur permettant d'itérer ligne par ligne sur une requête |
| **Index** | Structure optimisée (B-tree, Hash) pour accélérer les recherches |
| **Verrouillage** | Mécanisme de contrôle de concurrence (lignes, pages, tables) |

---

## Projets Concrets

### Projet 1 : Gestion de Bibliothèque 🟢

**Objectif :** Concevoir et implémenter une base de données pour une bibliothèque

**Fonctionnalités :**
- [ ] MCD/MLD : Livres, Auteurs, Adhérents, Emprunts
- [ ] CRUD complet (INSERT, UPDATE, DELETE)
- [ ] Requêtes avancées : livres en retard, adhérents les plus actifs
- [ ] Vues : livres disponibles, historique d'un adhérent
- [ ] Contraintes : pas d'emprunt si déjà 3 livres

**Structure GitHub :**
```
library-db/
├── README.md
├── schema/
│   ├── mcd.png            # Modèle Conceptuel de Données
│   ├── mld.png            # Modèle Logique de Données
│   └── create-tables.sql  # DDL
├── data/
│   └── seed.sql           # Données de test
├── queries/
│   ├── basic.sql          # SELECT, WHERE, JOIN
│   ├── advanced.sql       # Agrégations, sous-requêtes
│   └── views.sql          # Création des vues
├── plsql/
│   ├── procedures.sql     # Procédures stockées
│   ├── functions.sql      # Fonctions
│   └── triggers.sql       # Déclencheurs
└── docs/
    └── explications.md    # Justification des choix de conception
```

---

### Projet 2 : AnalyseSI — Clone 🟡

**Objectif :** Reproduire l'outil AnalyseSI utilisé en cours

**Fonctionnalités :**
- [ ] Charger un schéma relationnel
- [ ] Calcul automatique des dépendances fonctionnelles
- [ ] Vérification des formes normales (1NF, 2NF, 3NF, BCNF)
- [ ] Algorithme de normalisation (décomposition en 3NF)
- [ ] Génération de schéma SQL

**Stack technique :** Java (ou Python avec SQLAlchemy)

**Dépôt GitHub :** `analyse-si-clone`

---

### Projet 3 : Petit SGBD en Ligne de Commande 🔴

**Objectif :** Implémenter un mini SGBD avec stockage fichier, index et transactions simples

**Fonctionnalités :**
- [ ] Stockage de tables dans des fichiers CSV
- [ ] Index hash/B-tree en mémoire
- [ ] Support de requêtes simplifiées (`SELECT * FROM t WHERE col=val`)
- [ ] Transactions basiques avec log de journalisation
- [ ] Récupération après crash

**Stack technique :** C ou Python

**Dépôt GitHub :** `tiny-dbms`

---

## Ressources

- [SQL Tutorial — Mode Analytics](https://mode.com/sql-tutorial/)
- [Use The Index, Luke](https://use-the-index-luke.com/) — optimisation des indexes
- [Oracle Live SQL](https://livesql.oracle.com/) — IDE SQL Oracle gratuit
- [Normalisation interactive](https://www.bkent.net/Doc/simple5.htm)

---

## Checklist de maîtrise

- [ ] Concevoir le MCD/MLD d'un problème métier simple
- [ ] Écrire des requêtes SELECT avec jointures, agrégats, sous-requêtes
- [ ] Normaliser une relation jusqu'en 3NF
- [ ] Créer et utiliser des vues
- [ ] Écrire une procédure PL/SQL avec curseur
- [ ] Implémenter un trigger
- [ ] Expliquer le principe ACID et les niveaux d'isolation
- [ ] Optimiser une requête lente avec EXPLAIN PLAN
