# Roadmap — Programmation par Contraintes

> **Matière** : Prolog / CSP / Logique  
> **Objectif** : Maîtriser le paradigme logique et la résolution de problèmes par contraintes

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **Paradigme déclaratif** | On décrit **quoi** calculer, pas **comment** le calculer |
| **Fait** | Assertion de base en Prolog : `parent(jean, marie).` |
| **Règle** | Conclusion conditionnelle : `grandparent(X,Y) :- parent(X,Z), parent(Z,Y).` |
| **Interrogation (Query)** | Question posée au moteur Prolog : `?- grandparent(jean, Qui).` |
| **Unification** | Processus de mise en correspondance de deux termes (variables, constantes) |
| **Backtracking** | Mécanisme de retour en arrière quand une branche de recherche échoue |
| **Coupure (!)** | Prédicat qui empêche le backtracking — contrôle l'exploration |

### 🟡 Prolog Intermédiaire

| Concept | Définition |
|---------|-----------|
| **Liste** | Structure de données : `[1, 2, 3]` ou `[T|Q]` (tête + queue) |
| **Récursion** | Technique de base en Prolog (pas de boucles) |
| **Prédicat** | Relation entre termes (l'équivalent d'une fonction) |
| **Variable anonyme** | `_` — variable dont on ne se soucie pas de la valeur |
| **DCG (Definite Clause Grammar)** | Grammaire directement exprimable en Prolog pour le parsing |
| **findall / setof / bagof** | Prédicats de collecte de solutions |

### 🟡 CSP (Constraint Satisfaction Problems)

| Concept | Définition |
|---------|-----------|
| **Variables** | Entités à assigner (ex: les cases d'un Sudoku) |
| **Domaines** | Valeurs possibles pour chaque variable (ex: `1..9`) |
| **Contraintes** | Relations entre variables (ex: `X < Y`, `X ≠ Y`, `X + Y = Z`) |
| **Propagation de contraintes** | Réduction des domaines par élimination des valeurs impossibles |
| **Backtracking avec contraintes** | Recherche qui utilise les contraintes pour élaguer l'arbre |
| **Forward checking** | Après assignation, mise à jour des domaines des variables non assignées |

### 🔴 Avancés

| Concept | Définition |
|---------|-----------|
| **CLP(FD)** | Constraint Logic Programming over Finite Domains — bibliothèque Prolog pour CSP |
| **Optimisation** | Trouver la meilleure solution (minimiser/maximiser) via `labeling` avec options |
| **Algorithme de N-Queens** | Placement de N reines sans qu'elles ne s'attaquent — problème CSP classique |
| **Prédicats méta-logiques** | `var/1`, `nonvar/1`, `ground/1` — testent l'état d'une variable |

---

## Projets Concrets

### Projet 1 : Solveur de Sudoku 🟢

**Objectif :** Résoudre un Sudoku 9x9 avec contraintes

**Fonctionnalités :**
- [ ] Définition des contraintes (lignes, colonnes, blocs 3x3)
- [ ] Chargement d'une grille depuis un fichier texte
- [ ] Affichage formaté de la solution
- [ ] Version interactive (l'utilisateur peut saisir des valeurs)
- [ ] Génération de grilles (sans résolution)

**Stack technique :** Prolog (SWI-Prolog ou GNU Prolog)

**Structure GitHub :**
```
sudoku-solver/
├── README.md
├── sudoku.pl
├── generator.pl
├── grilles/
│   ├── facile.txt
│   ├── moyen.txt
│   ├── difficile.txt
│   └── diabolique.txt
├── tests/
│   └── test_sudoku.pl
└── docs/
    └── contraintes.md
```

---

### Projet 2 : Planificateur d'Emploi du Temps 🟡

**Objectif :** Générer un emploi du temps universitaire sous contraintes

**Contraintes :**
- [ ] Un cours ne peut pas être donné par deux profs en même temps
- [ ] Une salle ne peut accueillir qu'un seul cours à la fois
- [ ] Capacité de salle ≥ nombre d'étudiants
- [ ] Un prof ne peut pas être à deux endroits à la fois
- [ ] Contraintes horaires (pas de cours après 18h)

**Stack technique :** Prolog + CLP(FD)

**Dépôt GitHub :** `timetable-scheduler`

---

### Projet 3 : Moteur de Jeu Textuel 🔴

**Objectif :** Créer un jeu d'aventure textuel où le moteur d'inférence Prolog gère les règles

**Fonctionnalités :**
- [ ] Base de faits : objets, lieux, personnages
- [ ] Règles d'interaction : déplacement, ramassage, utilisation
- [ ] Inférence : si le joueur a une clé et est devant une porte, il peut l'ouvrir
- [ ] Parser DCG pour les commandes naturelles (`prendre la clé rouge`)
- [ ] Générateur de quêtes procédurales

**Stack technique :** SWI-Prolog

**Dépôt GitHub :** `prolog-adventure-game`

---

## Ressources

- [SWI-Prolog Documentation](https://www.swi-prolog.org/pldoc/)
- [Learn Prolog Now!](https://www.learnprolognow.org/) — excellent tutorial
- [CLP(FD) Library](https://www.swi-prolog.org/man/clpfd.html)
- [Prolog Problems — 99 Prolog Problems](https://www.ic.unicamp.br/~meidanis/courses/mc336/2009s2/prolog/problemas/)

---

## Checklist de maîtrise

- [ ] Écrire des faits, règles et requêtes simples
- [ ] Utiliser les listes et la récursion
- [ ] Comprendre l'unification et le backtracking
- [ ] Résoudre un problème avec findall/setof
- [ ] Modéliser un CSP et le résoudre avec CLP(FD)
- [ ] Utiliser la coupure (`!`) à bon escient
- [ ] Expliquer la différence entre paradigme impératif, fonctionnel et logique
