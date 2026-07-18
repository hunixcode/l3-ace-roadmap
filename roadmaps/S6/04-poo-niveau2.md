# Roadmap — POO Niveau 2

> **Matière** : Java Swing / AWT / Réseau / Java 2D  
> **Objectif** : Développer des applications desktop Java avec interfaces graphiques, réseau et multimédia

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **AWT** | Abstract Window Toolkit — bibliothèque graphique Java de base (lourde, dépend du système) |
| **Swing** | Bibliothèque graphique légère + riche que AWT, purement Java (JFrame, JButton...) |
| **Conteneur** | Élément pouvant contenir d'autres composants (JPanel, JFrame) |
| **Composant** | Élément graphique (JButton, JLabel, JTextField) |
| **Layout Manager** | Objet qui gère le placement des composants dans un conteneur |
| **Événement** | Action déclenchée par l'utilisateur (clic, saisie...) |
| **Listener** | Interface qui écoute et réagit à un type d'événement |

### 🟢 Layout Managers

| Manager | Description | Quand l'utiliser |
|---------|-------------|------------------|
| **FlowLayout** | Place les composants les uns à la suite des autres, passe à la ligne | Barres d'outils |
| **BorderLayout** | Divise le conteneur en 5 zones : NORTH, SOUTH, EAST, WEST, CENTER | Fenêtre principale |
| **GridLayout** | Grille régulière de cellules (lignes x colonnes) | Calculatrice, pavé numérique |
| **GridBagLayout** | Grille flexible — chaque composant peut occuper plusieurs cellules | Formulaires complexes |
| **BoxLayout** | Aligne les composants en ligne ou en colonne | Panneaux verticaux |

### 🟡 Swing Avancé

| Concept | Définition |
|---------|-----------|
| **JTabbedPane** | Conteneur à onglets |
| **JScrollPane** | Conteneur avec barres de défilement |
| **JSplitPane** | Diviseur redimensionnable entre deux composants |
| **JDesktopPane / JInternalFrame** | MDI (Multiple Document Interface) — fenêtres internes |
| **JPopupMenu** | Menu contextuel (clic droit) |
| **GlassPane** | Calque transparent superposé pour dessiner ou capturer des événements |

### 🟡 Réseau

| Concept | Définition |
|---------|-----------|
| **Socket** | Point de terminaison d'une connexion TCP entre deux machines |
| **ServerSocket** | Socket qui écoute les connexions entrantes sur un port |
| **DatagramSocket / DatagramPacket** | Communication UDP sans connexion |
| **Client-serveur** | Modèle où le serveur fournit un service et le client le consomme |

### 🟡 Entrées/Sorties

| Concept | Définition |
|---------|-----------|
| **FileReader / FileWriter** | Lecture/écriture de fichiers caractères |
| **BufferedReader** | Lecture ligne par ligne avec buffer |
| **PrintWriter** | Écriture formatée |
| **Sérialisation** | Conversion d'un objet en flux d'octets (ObjectOutputStream) |

---

## Projets Concrets

### Projet 1 : Bloc Notes Avancé 🟢

**Objectif :** Créer un éditeur de texte complet avec Swing

**Fonctionnalités :**
- [ ] Barre de menus (Fichier, Édition, Format, Aide)
- [ ] Onglets (JTabbedPane) pour plusieurs fichiers ouverts
- [ ] Rechercher/Remplacer
- [ ] Compteur de mots
- [ ] Sauvegarde automatique
- [ ] Thème clair/sombre

**Concepts mis en œuvre :**
- JMenuBar, JMenu, JMenuItem, JPopupMenu
- JTabbedPane, JScrollPane
- FileReader/FileWriter, BufferedReader/PrintWriter
- ActionListener, KeyListener

**Structure GitHub :**
```
java-notepad/
├── README.md
├── src/
│   ├── main/
│   │   ├── ui/          # Composants Swing
│   │   ├── model/       # Document, Line, Style
│   │   ├── io/          # Lecture/écriture fichiers
│   │   └── search/      # Algorithme de recherche
│   └── test/
├── pom.xml
└── screenshots/
```

---

### Projet 2 : Chat Client-Serveur 🟡

**Objectif :** Application de messagerie instantanée en réseau

**Fonctionnalités :**
- [ ] Serveur multi-clients (threads)
- [ ] Pseudonyme
- [ ] Messages privés (`/w pseudo message`)
- [ ] Liste des utilisateurs connectés
- [ ] Historique des messages
- [ ] Interface Swing séparée pour client

**Concepts mis en œuvre :**
- Socket / ServerSocket
- Threads (ThreadPool)
- BufferedReader / PrintWriter sur flux réseau
- JList pour la liste des utilisateurs
- JTextPane pour le formatage des messages

**Dépôt GitHub :** `java-chat-app`

---

### Projet 3 : Éditeur de Dessin Vectoriel 🔴

**Objectif :** Application de dessin avec Java 2D

**Fonctionnalités :**
- [ ] Formes : rectangle, cercle, ligne, courbe
- [ ] Sélection, déplacement, redimensionnement
- [ ] Propriétés : couleur, épaisseur de trait, remplissage
- [ ] Calques (JLayeredPane)
- [ ] Annuler/Rétablir (pattern Command)
- [ ] Export PNG / SVG

**Concepts mis en œuvre :**
- Graphics2D (dessin vectoriel)
- MouseListener / MouseMotionListener
- Pattern Command pour undo/redo
- JLayeredPane pour les calques
- Sérialisation pour la sauvegarde

**Dépôt GitHub :** `vector-drawing-editor`

---

## Ressources

- [The Java Tutorials — Swing](https://docs.oracle.com/javase/tutorial/uiswing/)
- [Java 2D API](https://docs.oracle.com/javase/tutorial/2d/)
- [Java Socket Programming](https://docs.oracle.com/javase/tutorial/networking/sockets/)
- [Game Programming Patterns](https://gameprogrammingpatterns.com/)

---

## Checklist de maîtrise

- [ ] Créer une interface Swing avec plusieurs Layout Managers
- [ ] Gérer les événements clavier et souris
- [ ] Implémenter une architecture client-serveur TCP
- [ ] Dessiner des formes avec Graphics2D
- [ ] Lire/écrire des fichiers texte et binaires
- [ ] Utiliser JTabbedPane, JDesktopPane, JSplitPane
- [ ] Créer un menu contextuel et une barre de menus
- [ ] Gérer les threads pour ne pas bloquer l'UI
