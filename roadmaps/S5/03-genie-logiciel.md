# Roadmap — Génie Logiciel

> **Matière** : UML / Java / Design Patterns / TDD  
> **Objectif** : Maîtriser la modélisation et la conception orientée-objet pour produire un logiciel de qualité

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **Classe** | Modèle définissant les attributs et méthodes communs à un ensemble d'objets |
| **Objet** | Instance d'une classe avec un état (valeurs d'attributs) et un comportement (méthodes) |
| **Encapsulation** | Principe de masquage des données — attributs privés, accès via getters/setters |
| **Héritage** | Relation "est-un" — une classe fille hérite des attributs/méthodes de la classe mère |
| **Polymorphisme** | Capacité d'un objet à se comporter différemment selon son type réel |
| **Abstraction** | Classe abstraite / interface — ne peut pas être instanciée, sert de contrat |
| **Association** | Relation structurelle entre classes (un étudiant suit un cours) |
| **Agrégation** | Association faible — le "tout" peut exister sans les "parties" |
| **Composition** | Association forte — le "tout" possède les "parties", leur cycle de vie est lié |

### 🟢 UML — Diagrammes

| Diagramme | Utilité |
|-----------|---------|
| **Diagramme de classes** | Structure statique : classes, attributs, méthodes, relations |
| **Diagramme de séquence** | Interactions temporelles entre objets : messages, appels, retours |
| **Diagramme d'activités** | Flux de contrôle/Workflow : actions, décisions, parallélisme |
| **Diagramme de cas d'utilisation** | Fonctionnalités du système vues par l'utilisateur |

### 🟡 Design Patterns

| Pattern | Problème résolu | Exemple |
|---------|----------------|---------|
| **Singleton** | Garantir une seule instance d'une classe | Gestionnaire de configuration |
| **Factory** | Déléguer la création d'objets | Création de différents types de personnages |
| **Observer** | Notifier plusieurs objets d'un changement | UI qui se met à jour quand les données changent |
| **Strategy** | Encapsuler des algorithmes interchangeables | Différents modes de calcul de prix |
| **Decorator** | Ajouter dynamiquement des fonctionnalités | Ajout d'options à une commande |
| **Adapter** | Faire collaborer des interfaces incompatibles | Wrapper d'une bibliothèque externe |

### 🟡 TDD (Test-Driven Development)

| Concept | Définition |
|---------|-----------|
| **Cycle Red-Green-Refactor** | Écrire un test qui échoue → faire passer le test → refactoriser |
| **Test unitaire** | Test d'une unité de code (méthode) isolément |
| **Mock** | Objet simulé imitant le comportement d'un vrai objet |
| **Couverture de code** | Pourcentage de code exécuté par les tests |
| **Kata Bowling** | Exercice classique de TDD : compter les points au bowling |

---

## Projets Concrets

### Projet 1 : Système de Gestion de Tournoi 🟢

**Objectif :** Concevoir et implémenter un système de gestion de tournoi sportif (type poker, échecs, etc.)

**Modélisation UML :**
- [ ] Diagramme de classes (Joueur, Tournoi, Match, Score, Classement)
- [ ] Diagramme de séquence (inscription, déroulement d'un match)
- [ ] Diagramme d'activités (déroulement du tournoi)
- [ ] Diagramme de cas d'utilisation

**Implémentation Java :**
- [ ] Classes avec héritage (Match individuel / Match par équipe)
- [ ] Interface `Classable` pour tout objet pouvant être classé
- [ ] Tests unitaires JUnit pour chaque méthode métier
- [ ] Persistance fichier (sauvegarde/chargement)

**Structure GitHub :**
```
tournament-manager/
├── README.md
├── uml/
│   ├── class-diagram.png
│   ├── sequence-diagram.png
│   ├── activity-diagram.png
│   └── usecase-diagram.png
├── src/
│   ├── main/java/
│   │   ├── model/          # Entités métier
│   │   ├── service/        # Logique métier
│   │   └── persistence/    # Sauvegarde/chargement
│   └── test/java/          # Tests JUnit
├── pom.xml
└── docs/
    └── choix-conception.md # Justification des patterns utilisés
```

---

### Projet 2 : Kata Bowling — TDD 🟡

**Objectif :** Implémenter le scoring du bowling en pur TDD

**Fonctionnalités :**
- [ ] Calcul du score pour une partie nulle
- [ ] Gestion des spare (`/`)
- [ ] Gestion des strike (`X`)
- [ ] Gestion du 10ème frame spécial
- [ ] Perfect game (300)

**Stack technique :** Java + JUnit

**Dépôt GitHub :** `kata-bowling-tdd`

---

### Projet 3 : Refactoring d'un Legacy Code 🔴

**Objectif :** Prendre un code spaghetti et le refactoriser proprement

**Étapes :**
- [ ] Analyser le code existant (identifier les antipatterns)
- [ ] Écrire des tests de caractérisation
- [ ] Appliquer des refactorings (Extract Method, Rename, Replace Conditional with Polymorphism)
- [ ] Valider que les tests passent toujours

**Dépôt GitHub :** `legacy-refactoring-kata`

---

## Ressources

- [PlantUML](https://plantuml.com/) — diagrammes UML en texte
- [Refactoring Guru — Design Patterns](https://refactoring.guru/design-patterns)
- [Coding Dojo — Kata Bowling](https://codingdojo.org/kata/Bowling/)
- [Clean Code — Robert C. Martin](https://www.oreilly.com/library/view/clean-code/9780136083238/)

---

## Checklist de maîtrise

- [ ] Dessiner un diagramme de classes UML complet (relations, cardinalités, héritage)
- [ ] Dessiner un diagramme de séquence montrant les interactions
- [ ] Identifier et appliquer le bon design pattern pour un problème donné
- [ ] Écrire les tests AVANT le code (TDD)
- [ ] Convertir un diagramme UML en code Java (et vice-versa)
- [ ] Expliquer la différence agrégation vs composition
- [ ] Refactoriser un code sans en casser les tests
