# Roadmap — Système d'Exploitation Niveau 3 (IPC)

> **Matière** : Inter-Process Communication / Signaux / Tubes / Sockets / OpenSSL  
> **Objectif** : Maîtriser la communication entre processus sous Unix/Linux et Windows

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **Processus** | Programme en cours d'exécution — possède son propre espace d'adressage |
| **Thread** | Unité d'exécution légère au sein d'un processus — partage la mémoire |
| **IPC (Inter-Process Communication)** | Mécanismes permettant à des processus d'échanger des données |
| **Mutex** | Verrou binaire pour l'exclusion mutuelle entre threads/processus |
| **Sémaphore** | Compteur synchronisant l'accès à une ressource partagée |
| **Deadlock** | Blocage mutuel : deux processus attendent chacun une ressource détenue par l'autre |

### 🟢 IPC Unix/Linux

| Concept | Définition |
|---------|-----------|
| **Signal** | Notification asynchrone envoyée à un processus (SIGINT, SIGTERM, SIGKILL, SIGUSR1) |
| **Signal masquable** | SIGINT, SIGTERM — peuvent être ignorés ou capturés |
| **Signal non-masquable** | SIGKILL, SIGSTOP — ne peuvent pas être ignorés |
| **Tube anonyme (pipe)** | Canal de communication unidirectionnel entre processus parents/enfants — `pipe()` |
| **Tube nommé (FIFO)** | Tube accessible via un fichier spécial — `mkfifo()` — communication entre processus quelconques |
| **Mémoire partagée** | Segment mémoire accessible par plusieurs processus — `shmget()`, `shmat()` |
| **mmap** | Projection d'un fichier ou d'un segment anonyme en mémoire |
| **Socket locale** | Socket Unix (`AF_UNIX`) pour communication locale |

### 🟡 IPC Windows

| Concept | Définition |
|---------|-----------|
| **Presse-papiers (Clipboard)** | Partage de données via le presse-papier système |
| **Tubes nommés Windows** | `\\.\pipe\PipeName` — communication entre processus Windows |
| **File Mapping** | Projection d'un fichier en mémoire partagée |
| **COM** | Component Object Model — standard d'interopérabilité Microsoft |
| **Messages Windows** | Système de messagerie asynchrone (WM_COPYDATA pour IPC) |
| **Mailslot** | Communication unidirectionnelle en broadcast local |

### 🟡 Synchronisation

| Concept | Définition |
|---------|-----------|
| **Section critique** | Zone de code qui ne doit être exécutée que par un seul thread à la fois |
| **Mutex** | Verrou binaire (C) — `pthread_mutex_lock / unlock` |
| **Sémaphore** | Compteur de ressources (C) — `sem_wait / sem_post` |
| **Variable condition** | Permet à un thread d'attendre une condition — `pthread_cond_wait` |

### 🔴 OpenSSL & Cryptographie

| Concept | Définition |
|---------|-----------|
| **RSA** | Cryptographie asymétrique — paire de clés publique/privée |
| **Génération de clés** | `openssl genrsa`, `openssl rsa`, `openssl req` |
| **Chiffrement symétrique** | AES, DES — même clé pour chiffrer/déchiffrer |
| **Certificat X.509** | Document numérique liant une identité à une clé publique |
| **Signature numérique** | Garantit l'authenticité et l'intégrité d'un message |

---

## Projets Concrets

### Projet 1 : Terminal Multi-Processus avec Tubes 🟢

**Objectif :** Simuler un shell Unix avec tubes et redirections

**Fonctionnalités :**
- [ ] `fork()` + `exec()` pour lancer des commandes
- [ ] `pipe()` pour connecter la sortie d'une commande à l'entrée de la suivante (`ls | grep .c`)
- [ ] Redirection `>` / `<` avec `dup2()`
- [ ] Gestion des signaux (Ctrl+C, Ctrl+Z)
- [ ] Jobs background (`&`)

**Stack technique :** C (POSIX)

**Structure GitHub :**
```
mini-shell/
├── README.md
├── src/
│   ├── shell.c
│   ├── parser.c / parser.h    # Parse la ligne de commande
│   ├── executor.c / executor.h # Fork, exec, pipe
│   └── signals.c / signals.h   # Gestion des signaux
├── Makefile
└── tests/
    └── test_commands.txt
```

---

### Projet 2 : Chat Local FIFO & Sockets 🟡

**Objectif :** Application de chat entre processus locaux utilisant FIFOs et sockets Unix

**Fonctionnalités :**
- [ ] Serveur de chat avec tubes nommés (FIFO)
- [ ] Connexion de clients via `AF_UNIX` sockets
- [ ] Diffusion de messages à tous les clients
- [ ] Gestion des pseudonymes
- [ ] Arrêt propre (gestion SIGINT)

**Concepts mis en œuvre :**
- `mkfifo()`, `open()`, `read()` / `write()`
- `socket(AF_UNIX, SOCK_STREAM, 0)`
- `select()` ou `epoll()` pour l'I/O multiplexé
- Gestion de SIGPIPE

**Dépôt GitHub :** `local-chat-ipc`

---

### Projet 3 : Tunnel Chiffré avec OpenSSL 🔴

**Objectif :** Créer un tunnel de communication chiffré entre deux machines

**Fonctionnalités :**
- [ ] Génération de certificats auto-signés (`openssl req -x509`)
- [ ] Handshake TLS (SSL_accept / SSL_connect)
- [ ] Chiffrement asymétrique pour l'échange de clé, symétrique pour les données
- [ ] Tunnel proxy : redirection du trafic local vers un serveur distant
- [ ] Gestion des erreurs et reconnexion

**Stack technique :** C + OpenSSL/LibreSSL

**Dépôt GitHub :** `tls-tunnel`

---

### Bonus : Comparatif Windows vs Linux

Créer une table de correspondance des IPC :

| Fonctionnalité | Unix/Linux | Windows |
|---------------|-----------|---------|
| Tube anonyme | `pipe()` | `CreatePipe()` |
| Tube nommé | `mkfifo()` | `\\.\pipe\name` |
| Mémoire partagée | `shmget / shmat` | `CreateFileMapping / MapViewOfFile` |
| Signal | `signal() / sigaction()` | `SetConsoleCtrlHandler()` |
| Socket local | `AF_UNIX` | Named Pipe / Socket |

**Dépôt GitHub :** `ipc-comparison`

---

## Ressources

- [Advanced Programming in the Unix Environment — Stevens](https://en.wikipedia.org/wiki/Advanced_Programming_in_the_Unix_Environment)
- [OpenSSL Cookbook](https://www.feistyduck.com/library/openssl-cookbook/)
- [Beej's Guide to Unix IPC](https://beej.us/guide/bgipc/)
- [pthreads Tutorial](https://computing.llnl.gov/tutorials/pthreads/)

---

## Checklist de maîtrise

- [ ] Créer et utiliser un tube anonyme entre parent/enfant
- [ ] Créer un tube nommé et l'utiliser entre processus indépendants
- [ ] Capturer et gérer un signal (SIGINT, SIGUSR1)
- [ ] Écrire un programme multi-thread avec mutex
- [ ] Utiliser `mmap` pour la mémoire partagée
- [ ] Générer des clés RSA avec OpenSSL
- [ ] Chiffrer/déchiffrer un fichier avec OpenSSL
- [ ] Expliquer la différence entre tube anonyme et tube nommé
- [ ] Expliquer comment éviter un deadlock
