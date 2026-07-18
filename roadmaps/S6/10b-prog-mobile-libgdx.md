# Roadmap — Programmation Mobile (LibGDX)

> **Matière** : LibGDX / Box2D / Android / Java / Game Dev  
> **Objectif** : Développer des jeux Android complets avec moteur physique et graphismes avancés

---

## Concepts Clés

### 🟢 Fondamentaux LibGDX

| Concept | Définition |
|---------|-----------|
| **ApplicationListener** | Interface principale du cycle de vie : `create()`, `render()`, `resize()`, `pause()`, `resume()`, `dispose()` |
| **Game + Screen** | Architecture modulaire — `Game` gère les transitions, chaque `Screen` est un état (menu, jeu, game-over) |
| **SpriteBatch** | Classe qui dessine des sprites en lot (batch) de façon optimisée (texture switching minimisé) |
| **Texture / TextureRegion** | Image chargée en GPU / portion d'une texture (pour les sprites dans un atlas) |
| **OrthographicCamera** | Caméra 2D — définit ce qui est visible et comment c'est projeté |
| **Delta time** | Temps écoulé depuis la dernière frame — utilisé pour des mouvements indépendants du framerate |

### 🟡 Asset Management & Graphismes

| Concept | Définition |
|---------|-----------|
| **Texture Atlas** | Grand sprite sheet contenant plusieurs sprites — un fichier `.atlas` décrit les coordonnées |
| **TexturePacker** | Outil qui génère le texture atlas à partir d'images individuelles |
| **TileMap (Tiled)** | Carte composée de tuiles — éditée avec l'outil Tiled, chargée avec `TmxMapLoader` |
| **Animation** | Série de TextureRegion jouée avec `Animation<TextureRegion>` + temps de frame |
| **Parallax Scrolling** | Couches d'arrière-plan qui bougent à des vitesses différentes pour donner la profondeur |
| **Sprite** | Texture avec position, rotation, échelle, couleur |

### 🟡 Box2D Physics

| Concept | Définition |
|---------|-----------|
| **World** | Univers Box2D — contient tous les corps, contraintes, et contacts |
| **Body** | Corps physique — types : `staticBody` (fixe), `dynamicBody` (mobile), `kinematicBody` (animé) |
| **Fixture** | Forme de collision attachée à un body (cercle, polygone, chaîne) |
| **Shape** | Forme géométrique de la fixture — `CircleShape`, `PolygonShape` |
| **Joint** | Contrainte entre deux corps — `RevoluteJoint`, `DistanceJoint`, `PrismaticJoint` |
| **Contact / ContactListener** | Détection et réaction aux collisions |
| **RayCast** | Tracer un rayon dans le monde et détecter ce qu'il touche |
| **Step** | Simulation d'un pas de temps physique — `world.step(delta, velocityIterations, positionIterations)` |

### 🟡 Entrées & Capteurs

| Concept | Définition |
|---------|-----------|
| **Gdx.input** | Accès aux entrées clavier, souris, tactile |
| **Touchpad** | Zone tactile virtuelle pour la direction — `Touchpad` (composant Scene2D) |
| **Accéléromètre / Gyroscope** | Capteurs de mouvement — `Gdx.input.getAccelerometerX/Y/Z()` |
| **Gestionnaires d'entrée** | `InputProcessor` — implémente `touchDown`, `touchUp`, `touchDragged`, `keyDown` |

### 🟡 Persistance

| Concept | Définition |
|---------|-----------|
| **Préférences (Local)** | Stockage clé-valeur simple — `Gdx.app.getPreferences("game").putInteger("highscore", 100).flush()` |
| **Fichiers locaux** | `Gdx.files.local("data.txt")` — lecture/écriture dans le stockage local |
| **SQLite (Android)** | Base de données locale pour des structures plus complexes |

---

## Projets Concrets

### Projet 1 : Space Warrior — Shoot 'em Up 🟢

**Objectif :** Jeu de tir spatial avec vagues d'ennemis et boss

**Fonctionnalités :**
- [ ] Écran titre (splash) avec choix gyroscope/touchpad
- [ ] Vaisseau joueur contrôlé par touchpad (ou gyroscope)
- [ ] Tir de projectiles (pistolet laser)
- [ ] Ennemis : aliens, planètes obstacles, champs d'énergie
- [ ] Missiles ennemis à intervalles aléatoires
- [ ] Collision = mort
- [ ] Score basé sur le temps de survie
- [ ] Sons et musique d'ambiance
- [ ] Parallax scrolling (fond spatial)
- [ ] Écran Game Over avec score et option de redémarrer

**Structure GitHub :**
```
space-warrior/
├── README.md
├── core/
│   ├── src/com/game/
│   │   ├── SpaceWarriorGame.java    # Classe principale Game
│   │   ├── screens/
│   │   │   ├── SplashScreen.java
│   │   │   ├── GameScreen.java
│   │   │   └── GameOverScreen.java
│   │   ├── entities/
│   │   │   ├── Ship.java
│   │   │   ├── Bullet.java
│   │   │   ├── Alien.java
│   │   │   └── Obstacle.java
│   │   ├── systems/
│   │   │   ├── InputSystem.java
│   │   │   ├── CollisionSystem.java
│   │   │   └── SpawnSystem.java
│   │   └── utils/
│   │       └── AssetManager.java
│   └── assets/
│       ├── atlas/          # Textures
│       ├── sounds/         # Sons et musique
│       └── skins/          # UI
└── android/
    └── src/.../AndroidLauncher.java
```

---

### Projet 2 : Super Platformer avec Box2D 🟡

**Objectif :** Jeu de plateforme 2D avec physique réaliste

**Fonctionnalités :**
- [ ] Personnage avec saut, double saut, dash
- [ ] Plateformes avec collisions Box2D
- [ ] Plateformes mobiles (kinematic bodies)
- [ ] Pièges (pics, laves) — contact = mort
- [ ] Items à collecter (clés, pièces, power-ups)
- [ ] Niveaux avec TileMap (Tiled)
- [ ] Caméra qui suit le joueur
- [ ] Animations de personnage (idle, run, jump, die)
- [ ] Barre de vie, score, timer

**Concepts techniques :**
- Box2D World + ContactListener
- TileMap rendering with parallax
- State machine pour le personnage
- Camera smoothing (lerp)

**Dépôt GitHub :** `box2d-platformer`

---

### Projet 3 : Jeu de Labyrinthe Gyroscopique 🔴

**Objectif :** Faire rouler une bille dans un labyrinthe en inclinant le téléphone

**Fonctionnalités :**
- [ ] Gyroscope : incliner = déplacer la bille
- [ ] 3 niveaux de difficulté : Facile, Difficile, Diabolique
- [ ] 2 types de bille : normale et animée (feu)
- [ ] Labyrinthe conçu avec Tiled
- [ ] Box2D pour les collisions bille/mur
- [ ] Chronomètre + meilleur temps persistant
- [ ] Écran de victoire/défaite

**Dépôt GitHub :** `gyro-maze-game`

---

### Projet Bonus : Compilation et Publication sur Google Play 🔴

- [ ] Générer une APK signée
- [ ] Créer une fiche Play Store (icône, screenshots, description)
- [ ] Publier en bêta fermée
- [ ] Intégrer AdMob (publicité) ou des achats in-app

---

## Ressources

- [LibGDX Wiki](https://libgdx.com/wiki/) — documentation officielle
- [LibGDX Info](https://www.libgdx.info/) — tutoriels par Brett W.
- [Box2D Manual](https://box2d.org/documentation/)
- [Tiled Map Editor](https://www.mapeditor.org/)
- [Game From Scratch — LibGDX Tutorials](https://gamefromscratch.com/libgdx-tutorial-series/)

---

## Checklist de maîtrise

- [ ] Configurer un projet LibGDX avec les sous-projets core, android, desktop
- [ ] Créer un Game avec plusieurs Screen et gérer les transitions
- [ ] Utiliser SpriteBatch pour le rendu optimisé
- [ ] Charger et utiliser un Texture Atlas
- [ ] Créer et gérer des animations
- [ ] Intégrer Box2D : World, Body, Fixture, ContactListener
- [ ] Gérer l'entrée utilisateur (touchpad ET gyroscope)
- [ ] Implémenter un parallax scrolling
- [ ] Utiliser Tiled pour les niveaux
- [ ] Persister les scores (Preferences ou SQLite)
- [ ] Générer une APK signée et la tester sur un vrai appareil
