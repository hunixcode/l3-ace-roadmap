# Roadmap — Automates & Compilation

> **Matière** : Flex / Bison / C / Théorie des langages  
> **Objectif** : Construire un compilateur ou interpréteur minimal de A à Z

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **Alphabet** | Ensemble fini de symboles (ex: `{a, b, c}`) |
| **Mot** | Suite finie de symboles d'un alphabet |
| **Langage** | Ensemble (fini ou infini) de mots sur un alphabet |
| **Grammaire hors-contexte** | `(V, Σ, R, S)` où V = non-terminaux, Σ = terminaux, R = règles de production, S = axiome |
| **Expression régulière** | Notation pour décrire un langage régulier (`*`, `+`, `?`, `|`) |
| **Automate fini** | Machine à états avec états, transitions, état initial/accepteurs |

### 🟡 Lexical Analysis (Flex)

| Concept | Définition |
|---------|-----------|
| **Token** | Plus petite unité lexicale significative (mot-clé, identifiant, nombre) |
| **Lexème** | Séquence de caractères correspondant à un token |
| **Start condition** | État dans lequel Flex se trouve, permettant une tokenisation contextuelle |
| **Greedy matching** | Flex associe toujours la règle la plus longue possible |
| **Pattern** | Expression régulière associée à une action Flex |

### 🟡 Syntax Analysis (Bison)

| Concept | Définition |
|---------|-----------|
| **Grammaire ambiguë** | Une grammaire qui peut produire le même mot avec deux arbres de dérivation différents |
| **Précédence des opérateurs** | Règles + * (priorité) et associativité gauche/droite pour lever l'ambiguïté |
| **Récursivité gauche** | `A → A α` — Bison la gère nativement |
| **Arbre de Syntaxe Abstraite (AST)** | Arbre où les nœuds internes sont des opérateurs et les feuilles des opérandes |
| **Dérivation** | Série de remplacements de non-terminaux par des parties droites de règles |

### 🔴 Avancés

| Concept | Définition |
|---------|-----------|
| **Théorème de Chomsky-Schützenberger** | Tout langage hors-contexte peut être représenté comme l'intersection d'un langage de Dyck et d'un langage régulier |
| **Langage de Dyck** | Langage des parenthèses bien formées |
| **Lemme de la pompe (pumping lemma)** | Pour les langages réguliers (resp. hors-contexte), il existe une propriété de répétition |
| **Table de symboles** | Structure associant noms (variables, fonctions) à leurs attributs (type, adresse, scope) |

---

## Projets Concrets

### Projet 1 : Mini-Calculatrice Interpréteur 🟢

**Objectif :** Construire un interpréteur pour expressions arithmétiques

**Fonctionnalités :**
- [ ] Variables (`x = 5 + 3`)
- [ ] Opérateurs `+`, `-`, `*`, `/`, `^`
- [ ] Parenthèses et précédence
- [ ] Fonctions intégrées : `sin()`, `cos()`, `sqrt()`, `abs()`
- [ ] Gestion des erreurs (division par zéro, variable non définie)

**Stack technique :** Flex + Bison + C

**Structure GitHub :**
```
mini-calc/
├── README.md
├── Makefile
├── calc.lex          # Analyseur lexical Flex
├── calc.y            # Analyseur syntaxique Bison
├── ast.h / ast.c     # Définition et construction de l'AST
├── eval.h / eval.c   # Évaluateur d'AST
├── symtab.h / symtab.c  # Table des symboles
├── main.c
└── tests/
    ├── test_expressions.txt
    └── test_errors.txt
```

---

### Projet 2 : Analyseur de Langage Naturel Minimal 🟡

**Objectif :** Parser des phrases françaises simples en structures grammaticales

**Fonctionnalités :**
- [ ] Grammaire sujet-verbe-complément
- [ ] Groupes nominaux (déterminant + nom + adjectif)
- [ ] Conjugaison limitée (présent)
- [ ] Arbre syntaxique en sortie

**Stack technique :** Flex + Bison + C + DOT (Graphviz) pour visualiser l'arbre

**Dépôt GitHub :** `natural-language-parser`

---

### Projet 3 : Mini-Compilateur vers P-Code ou ASM 🔴

**Objectif :** Compiler un langage de type C minimal en bytecode

**Fonctionnalités :**
- [ ] Variables typées (int, float)
- [ ] Conditionnelles (`if` / `else`)
- [ ] Boucles (`while`, `for`)
- [ ] Génération de code (P-Code ou assembleur x86 minimal)
- [ ] Exécution via VM ou assemblage

**Stack technique :** Flex + Bison + C

**Dépôt GitHub :** `tiny-compiler`

---

## Ressources

- [Flex Manual](https://westes.github.io/flex/manual/)
- [Bison Manual](https://www.gnu.org/software/bison/manual/)
- [Compiler Construction (Jack Crenshaw)](https://compilers.iecc.com/crenshaw/) — très accessible
- [Dragon Book — Aho, Lam, Sethi, Ullman](https://en.wikipedia.org/wiki/Compilers:_Principles,_Techniques,_and_Tools)

---

## Checklist de maîtrise

- [ ] Écrire une spec Flex pour tokeniser un langage quelconque
- [ ] Écrire une grammaire Bison non-ambiguë pour des expressions
- [ ] Construire et parcourir un AST
- [ ] Gérer les erreurs lexicales et syntaxiques
- [ ] Implémenter une table de symboles
- [ ] Comprendre la différence entre analyse lexicale, syntaxique et sémantique
- [ ] Expliquer le théorème Chomsky-Schützenberger
