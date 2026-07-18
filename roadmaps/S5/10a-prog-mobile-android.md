# Roadmap — Programmation Mobile Android

> **Matière** : Android SDK / Java / Layouts / Intents / Fragments / Bases de données  
> **Objectif** : Développer des applications Android natives avec UI variée, persistance et web

---

## Concepts Clés

### 🟢 Fondamentaux Android

| Concept | Définition |
|---------|-----------|
| **Activity** | Écran unique avec une interface utilisateur — cycle de vie `onCreate`, `onStart`, `onResume`, `onPause`, `onStop`, `onDestroy` |
| **Layout** | Fichier XML définissant la structure d'une interface utilisateur |
| **Intent** | Message asynchrone qui déclenche une Activity, un Service ou un Broadcast |
| **Manifest** | Fichier `AndroidManifest.xml` — déclare les composants, permissions et caractéristiques de l'app |
| **Ressources** | Fichiers `res/` — layouts, valeurs (strings, colors), drawables, mipmaps |
| **Gradle** | Système de build — `build.gradle` pour les dépendances et la configuration |

### 🟢 Layouts

| Layout | Description | Balise XML |
|--------|-------------|------------|
| **LinearLayout** | Aligne les vues horizontalement ou verticalement — `android:orientation` | `<LinearLayout>` |
| **TableLayout** | Grille de lignes et colonnes — chaque `<TableRow>` est une ligne | `<TableLayout>` |
| **RelativeLayout** | Position relative entre vues ou par rapport au parent (`layout_below`, `toRightOf`) | `<RelativeLayout>` |
| **ScrollView** | Conteneur défilant — ne peut contenir qu'un seul enfant (souvent un LinearLayout) | `<ScrollView>` |

### 🟡 Composants d'Interface

| Composant | Usage |
|-----------|-------|
| **TextView** | Affichage de texte |
| **EditText** | Saisie de texte |
| **Button / ImageButton** | Bouton cliquable |
| **ImageView** | Affichage d'image |
| **CheckBox / RadioButton** | Sélection multiple / unique |
| **Spinner** | Liste déroulante |
| **ListView / RecyclerView** | Liste défilante d'éléments |
| **ProgressBar** | Indicateur de progression |
| **SeekBar** | Curseur de réglage |
| **WebView** | Affichage d'une page web intégrée |
| **ViewPager** | Glissement entre pages (swipe) |
| **TabLayout** | Onglets de navigation |

### 🟡 Navigation & Actions

| Concept | Description |
|---------|-------------|
| **Intent explicite** | Lance une Activity spécifique : `new Intent(this, TargetActivity.class)` |
| **Intent implicite** | Déclenche une action sans cibler une Activity : `ACTION_VIEW`, `ACTION_DIAL` |
| **Extra** | Données passées dans un Intent : `putExtra("key", value)` |
| **ActionBar / Toolbar** | Barre d'action en haut — menu, navigation, titre |
| **Options Menu** | Menu accessible via les 3 points ou la touche Menu |
| **Fragments** | Portion d'interface réutilisable dans une Activity — cycle de vie propre |

### 🟡 Fragments

| Concept | Définition |
|---------|-----------|
| **Fragment** | Module d'UI autonome, peut être combiné dans une Activity |
| **FragmentManager** | Gère les transactions de fragments (ajout, remplacement, suppression) |
| **DialogFragment** | Fragment pour afficher une boîte de dialogue |
| **ListFragment** | Fragment avec une liste intégrée |
| **PreferenceFragment** | Fragment pour les écrans de préférences/paramètres |
| **Cycle de vie** | `onAttach` → `onCreate` → `onCreateView` → `onActivityCreated` → `onStart` → ... |

### 🟡 Persistance

| Concept | Description |
|---------|-------------|
| **SharedPreferences** | Stockage clé-valeur simple pour les préférences utilisateur |
| **SQLite** | Base de données relationnelle locale — utilisée via `SQLiteOpenHelper` |
| **Room** | Couche d'abstraction au-dessus de SQLite (Jetpack) |
| **Fichiers internes** | Stockage privé à l'application : `openFileInput()`, `openFileOutput()` |
| **Fichiers externes** | Stockage partagé (photos, téléchargements) — `Environment.getExternalStorageDirectory()` |

### 🟡 Sujets Avancés

| Concept | Description |
|---------|-------------|
| **Orientation** | Gestion du changement d'orientation — `onSaveInstanceState` / `onRestoreInstanceState` |
| **Material Design** | Thème Material, CoordinatorLayout, FloatingActionButton, Snackbar |
| **WebView** | Affiche une page web — configuration de JavaScript, cache |
| **Gallery / ImageSwitcher** | Galerie d'images avec animation de transition |
| **Notifications** | `NotificationManager`, `NotificationChannel` (API 26+) |
| **Permissions** | Demande de permissions à l'exécution (API 23+) |
| **AsyncTask / Threads** | Opérations longues en arrière-plan (remplacé par Coroutines/Kotlin depuis) |

---

## Projets Concrets

### Projet 1 : Application de Notes 🟢

**Objectif :** Application de prise de notes avec titre, contenu et date

**Fonctionnalités :**
- [ ] Liste des notes (ListView/RecyclerView)
- [ ] Ajout / édition / suppression (via Intent et Activity séparée)
- [ ] Persistance SQLite (Room ou SQLiteOpenHelper)
- [ ] Recherche dans les notes
- [ ] Tri par date ou par titre
- [ ] Choix du thème (clair/sombre) via SharedPreferences

**Concepts mis en œuvre :**
- LinearLayout, RelativeLayout
- Intents explicites avec extras
- RecyclerView + Adapter
- SQLiteOpenHelper / Room
- SharedPreferences

**Structure GitHub :**
```
note-app/
├── README.md
├── app/
│   ├── src/main/
│   │   ├── java/com/notes/
│   │   │   ├── MainActivity.java
│   │   │   ├── NoteDetailActivity.java
│   │   │   ├── data/
│   │   │   │   ├── NoteDbHelper.java
│   │   │   │   └── Note.java
│   │   │   └── adapter/
│   │   │       └── NoteAdapter.java
│   │   ├── res/layout/
│   │   │   ├── activity_main.xml
│   │   │   ├── activity_note_detail.xml
│   │   │   └── note_item.xml
│   │   └── AndroidManifest.xml
│   └── build.gradle
└── screenshots/
```

---

### Projet 2 : Application Météo avec WebView + API 🟡

**Objectif :** Application qui affiche la météo en utilisant une API REST + WebView

**Fonctionnalités :**
- [ ] Saisie d'une ville (EditText + AutoCompleteTextView)
- [ ] Appel à une API météo (OpenWeatherMap) via HTTP
- [ ] Affichage des résultats (température, humidité, icône)
- [ ] WebView pour afficher des prévisions détaillées
- [ ] TabLayout + ViewPager pour switcher entre les vues
- [ ] Sauvegarde des villes favorites (SharedPreferences)

**Concepts mis en œuvre :**
- Intent implicite (ACTION_VIEW)
- WebView + WebViewClient
- HttpURLConnection / Volley / Retrofit
- TabLayout + ViewPager
- Spinner, ImageView
- Material Design (FloatingActionButton)

**Dépôt GitHub :** `weather-app-android`

---

### Projet 3 : Lecteur de Flux RSS avec Fragments 🔴

**Objectif :** Application de lecture de flux RSS avec Fragments et base de données

**Fonctionnalités :**
- [ ] Liste des articles (ListFragment)
- [ ] Détail d'un article (Fragment + WebView)
- [ ] Mode tablette : deux fragments côte à côte (master-detail)
- [ ] Ajout de flux RSS personnalisés
- [ ] Synchronisation périodique (AlarmManager / WorkManager)
- [ ] Notifications pour les nouveaux articles
- [ ] Gestion des orientations (paysage/portrait)

**Concepts mis en œuvre :**
- Fragments (ListFragment, FragmentTransaction)
- DialogFragment (ajout de flux)
- PreferenceFragment (paramètres)
- SQLite (articles lus, favoris)
- WebView
- XML Parser (SAX/DOM)
- Gestion de la configuration (onSaveInstanceState)

**Dépôt GitHub :** `rss-reader-android`

---

## Ressources

- [Android Developers Documentation](https://developer.android.com/docs)
- [Android Training — Udacity](https://www.udacity.com/course/android-basics-nanodegree-by-google--nd803)
- [Vogella Android Tutorials](https://www.vogella.com/tutorials/android.html)
- [Material Design Guidelines](https://material.io/design)
- [CodeLabs Android](https://codelabs.developers.google.com/?cat=Android)

---

## Checklist de maîtrise

- [ ] Créer un projet Android avec plusieurs Activity et Layouts
- [ ] Utiliser LinearLayout, TableLayout, RelativeLayout, ScrollView
- [ ] Passer des données entre Activity via Intent
- [ ] Utiliser RecyclerView avec un Adapter personnalisé
- [ ] Implémenter un formulaire avec validation
- [ ] Utiliser SharedPreferences et SQLite
- [ ] Créer un Fragment et gérer ses transactions
- [ ] Utiliser TabLayout + ViewPager
- [ ] Afficher du contenu web avec WebView
- [ ] Gérer les changements d'orientation
- [ ] Utiliser Material Design (Toolbar, FAB, Snackbar)
