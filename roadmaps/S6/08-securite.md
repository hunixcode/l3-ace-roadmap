# Roadmap — Sécurité Informatique

> **Matière** : Cryptographie / 2FA / Passkeys / Burp Suite / Docker / IoT  
> **Objectif** : Comprendre les mécanismes d'attaque et de défense, savoir sécuriser un système

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **CIA Triad** | Confidentialité, Intégrité, Disponibilité — les trois objectifs de sécurité |
| **Authentification** | Vérification de l'identité d'un utilisateur (qqch que vous savez/avez/êtes) |
| **Contrôle d'accès** | Limitation des actions autorisées pour un utilisateur identifié |
| **Confidentialité** | Seules les personnes autorisées peuvent lire l'information |
| **Intégrité** | L'information n'a pas été modifiée de façon non autorisée |
| **Disponibilité** | Le système est accessible quand on en a besoin |
| **Non-répudiation** | Une action ne peut pas être niée par son auteur (signature numérique) |

### 🟡 Cryptographie

| Concept | Définition |
|---------|-----------|
| **Chiffrement symétrique** | Même clé pour chiffrer et déchiffrer (AES, DES, 3DES) — rapide mais partage de clé problématique |
| **Chiffrement asymétrique** | Paire de clés publique/privée (RSA, ECC) — lent mais pas de partage de clé |
| **Hash** | Fonction à sens unique (SHA-256, MD5) — intégrité des données |
| **Signature numérique** | Hash chiffré avec la clé privée — authenticité + intégrité |
| **Certificat X.509** | Document liant une clé publique à une identité, signé par une Autorité de Certification |
| **PKI** | Infrastructure à clé publique — hiérarchie de certificats |

### 🟡 Authentification & 2FA

| Concept | Définition |
|---------|-----------|
| **OTP (One-Time Password)** | Mot de passe valable pour une seule connexion |
| **TOTP (Time-based OTP)** | OTP qui change toutes les 30 secondes (Google Authenticator, Authy) |
| **HOTP (HMAC-based OTP)** | OTP basé sur un compteur |
| **U2F / FIDO2** | Clé physique USB/NFC pour l'authentification forte |
| **Passkey** | Standard FIDO2/WebAuthn — remplace le mot de passe par une paire de clés liée au site |
| **WebAuthn API** | API navigateur permettant l'authentification sans mot de passe |
| **2FA** | Deux facteurs sur trois : connaissance (mot de passe), possession (téléphone), inhérence (empreinte) |
| **ANSSI** | Agence Nationale de la Sécurité des Systèmes d'Information — guide des bonnes pratiques |

### 🟡 Attaques

| Concept | Définition |
|---------|-----------|
| **Zéro Day** | Vulnérabilité non connue du public — pas de correctif disponible |
| **DDoS** | Distributed Denial of Service — submerger un serveur de requêtes pour le rendre indisponible |
| **Botnet** | Réseau de machines infectées contrôlées par un attaquant (Mirai IoT botnet) |
| **ARP Spoofing** | L'attaquant répond aux requêtes ARP avec sa propre MAC |
| **Injection SQL** | Insertion de code SQL malveillant dans une requête |
| **Homme du milieu (MITM)** | Interception et modification de la communication entre deux parties |
| **Side-Channel Attack** | Attaque basée sur l'analyse du comportement physique (temps, consommation, rayonnement) |

### 🟢 Outils

| Outil | Utilité |
|-------|---------|
| **Burp Suite** | Proxy d'interception HTTP/S — analyse et modification de trafic web |
| **Docker** | Conteneurisation — environnement isolé pour tests de sécurité |
| **Nmap** | Scan de ports et découverte de services |
| **Wireshark** | Analyse de paquets réseau |

---

## Projets Concrets

### Projet 1 : Plateforme de Pentest Web 🟢

**Objectif :** Mettre en place un environnement Docker vulnérable et le tester

**Fonctionnalités :**
- [ ] Conteneur Docker avec application web vulnérable (DVWA ou custom)
- [ ] Installation et configuration de Burp Suite
- [ ] Tests : injection SQL, XSS, CSRF, path traversal
- [ ] Rapport de sécurité documentant chaque vulnérabilité trouvée
- [ ] Proposition de correctifs

**Stack technique :** Docker, Docker Compose, Burp Suite, SQLite

**Structure GitHub :**
```
web-pentest-lab/
├── README.md
├── docker-compose.yml
├── vulnerable-app/
│   ├── Dockerfile
│   ├── app.py          # Flask vulnérable
│   └── init.sql
├── reports/
│   ├── sql-injection.md
│   ├── xss.md
│   └── csrf.md
└── fixes/
    └── patched-app/
```

---

### Projet 2 : Implémentation d'un Système d'Authentification 2FA 🟡

**Objectif :** Ajouter l'authentification à deux facteurs à une application web

**Fonctionnalités :**
- [ ] Inscription/connexion avec mot de passe (hashé avec bcrypt)
- [ ] Génération d'un secret TOTP (RFC 6238)
- [ ] QR Code pour l'import dans Google Authenticator/Authy
- [ ] Vérification du code 2FA à la connexion
- [ ] Codes de secours (one-time use)
- [ ] Option : support Passkey (WebAuthn)

**Stack technique :** Python (Flask) + `pyotp` + `qrcode` + `cryptography` ou Java + Spring Boot

**Dépôt GitHub :** `2fa-auth-system`

---

### Projet 3 : Outil de Détection d'Intrusion Réseau (NIDS) 🔴

**Objectif :** Analyser le trafic réseau en temps réel et détecter des patterns suspects

**Fonctionnalités :**
- [ ] Capture en temps réel (pcap / libpcap)
- [ ] Détection de scan de ports (Nmap)
- [ ] Détection d'ARP spoofing
- [ ] Détection de SYN flood
- [ ] Alertes avec seuils configurables
- [ ] Dashboard de visualisation

**Stack technique :** Python (scapy) + Elasticsearch + Kibana (ou simple interface web)

**Dépôt GitHub :** `simple-nids`

---

## Ressources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/) — les 10 vulnérabilités web les plus critiques
- [ANSSI — Guide d'authentification multifacteur](https://www.ssi.gouv.fr/)
- [PortSwigger — Web Security Academy](https://portswigger.net/web-security) — gratuit, excellent
- [TryHackMe](https://tryhackme.com/) — plateforme d'entraînement CTF
- [Have I Been Pwned](https://haveibeenpwned.com/) — vérifier les fuites de données

---

## Checklist de maîtrise

- [ ] Expliquer la CIA Triad avec des exemples concrets
- [ ] Configurer Burp Suite et intercepter/modifier une requête HTTP
- [ ] Expliquer comment fonctionne un TOTP
- [ ] Installer et configurer Docker pour isoler une application
- [ ] Expliquer la différence entre chiffrement symétrique et asymétrique
- [ ] Reconnaître une injection SQL et la corriger (requêtes préparées)
- [ ] Expliquer les 3 types de facteurs d'authentification
- [ ] Décrire le fonctionnement des Passkeys / WebAuthn
- [ ] Expliquer ce qu'est un botnet et comment il fonctionne (Mirai)
