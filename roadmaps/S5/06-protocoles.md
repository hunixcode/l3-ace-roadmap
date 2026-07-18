# Roadmap — Protocoles Réseau

> **Matière** : TCP/IP / ARP / Routage / NAT / DNS  
> **Objectif** : Maîtriser l'architecture protocolaire d'Internet et la configuration réseau

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **Modèle OSI** | 7 couches : Physique, Liaison, Réseau, Transport, Session, Présentation, Application |
| **Modèle TCP/IP** | 4 couches : Accès Réseau, Internet, Transport, Application |
| **Encapsulation** | Chaque couche ajoute son en-tête au paquet de la couche supérieure |
| **PDU (Protocol Data Unit)** | Unité de données à chaque couche : trame (L2), paquet (L3), segment (L4) |
| **MTU (Maximum Transmission Unit)** | Taille maximale d'une trame au niveau liaison (ex: Ethernet = 1500 octets) |

### 🟢 IP (Internet Protocol)

| Concept | Définition |
|---------|-----------|
| **Adresse IPv4** | 32 bits — 4 octets en notation décimale pointée (ex: `192.168.1.1`) |
| **Masque de sous-réseau** | Détermine la partie réseau vs hôte d'une adresse IP |
| **CIDR** | Notation `/24` au lieu de `255.255.255.0` |
| **Sous-réseau** | Division logique d'un réseau IP |
| **Fragmentation** | Découpage d'un paquet IP trop grand par rapport au MTU |
| **TTL (Time To Live)** | Compteur qui évite les boucles de routage |
| **NAT (Network Address Translation)** | Traduction d'adresses privées en adresse publique |

### 🟢 ARP (Address Resolution Protocol)

| Concept | Définition |
|---------|-----------|
| **ARP Request** | Requête broadcast : "Qui a l'IP X ?" |
| **ARP Reply** | Réponse unicast : "Moi, mon MAC est Y" |
| **Cache ARP** | Table qui associe IP ↔ MAC pour éviter des requêtes répétées |
| **Gratuitous ARP** | ARP envoyé sans sollicitation pour annoncer/mettre à jour une correspondance |
| **ARP Spoofing** | Attaque où un attaquant répond avec sa propre MAC pour intercepter le trafic |

### 🟡 TCP (Transmission Control Protocol)

| Concept | Définition |
|---------|-----------|
| **Connexion orientée** | Établissement de connexion avant transfert (3-way handshake) |
| **3-Way Handshake** | SYN → SYN-ACK → ACK |
| **Numéro de séquence** | Identifie l'ordre des octets dans le flux |
| **Numéro d'acquittement** | Prochain octet attendu (ACK cumulatif) |
| **Fenêtre (Window)** | Tampon disponible chez le récepteur — contrôle de flux |
| **Flags TCP** | SYN, ACK, FIN, RST, PSH, URG |
| **Contrôle de congestion** | Slow start, congestion avoidance, fast retransmit |

### 🟡 UDP (User Datagram Protocol)

| Concept | Définition |
|---------|-----------|
| **Sans connexion** | Pas d'établissement de connexion préalable |
| **Non fiable** | Pas de garantie de livraison, pas de réordonnancement |
| **Léger** | En-tête de 8 octets seulement (vs 20+ pour TCP) |
| **Cas d'usage** | Streaming, VoIP, DNS, DHCP, jeux temps réel |

### 🟢 Routage

| Concept | Définition |
|---------|-----------|
| **Table de routage** | Liste des réseaux destination → interface / next hop |
| **Route par défaut** | `0.0.0.0/0` → tout ce qui n'est pas dans la table |
| **Routage statique** | Routes configurées manuellement |
| **Routage dynamique** | Protocoles (RIP, OSPF, BGP) qui échangent des routes automatiquement |

### 🟢 DNS (Domain Name System)

| Concept | Définition |
|---------|-----------|
| **Résolution DNS** | Traduction nom de domaine ↔ adresse IP |
| **Serveur récursif** | Effectue les requêtes à la place du client |
| **Serveur faisant autorité** | Connaît la réponse définitive pour une zone |
| **NSLOOKUP** | Outil en ligne de commande pour interroger les serveurs DNS |
| **Enregistrements DNS** | A (IPv4), AAAA (IPv6), MX (mail), CNAME (alias), NS (name server) |

---

## Projets Concrets

### Projet 1 : Analyseur de Paquets (Mini Wireshark) 🟢

**Objectif :** Programme en Python/C qui capture et analyse les trames réseau

**Fonctionnalités :**
- [ ] Capture de trames Ethernet (raw socket)
- [ ] Parse : trame Ethernet → en-tête IP → TCP/UDP
- [ ] Affichage des informations clés (IP src/dst, ports, flags TCP)
- [ ] Filtres simples (par IP, protocole, port)
- [ ] Export au format PCAP

**Stack technique :** Python (scapy ou socket brute) ou C (libpcap)

**Structure GitHub :**
```
packet-analyzer/
├── README.md
├── capture.py
├── protocols/
│   ├── ethernet.py
│   ├── ip.py
│   ├── tcp.py
│   ├── udp.py
│   └── arp.py
├── filters.py
├── pcap_writer.py
├── tests/
│   └── test_protocols.py
└── samples/
    └── capture.pcap
```

---

### Projet 2 : Simulateur de Routage 🟡

**Objectif :** Simuler le routage IP dans un réseau de routeurs virtuels

**Fonctionnalités :**
- [ ] Topologie configurable (routeurs, liens, coûts)
- [ ] Implémentation de l'algorithme de Dijkstra (OSPF)
- [ ] Tables de routage générées automatiquement
- [ ] Simulation de l'envoi de paquets avec sauts
- [ ] Visualisation du chemin emprunté

**Dépôt GitHub :** `routing-simulator`

---

### Projet 3 : Mini-Serveur Web & DNS 🔴

**Objectif :** Implémenter un serveur HTTP et un résolveur DNS simplifiés

**Fonctionnalités serveur HTTP :**
- [ ] Écoute sur un port configurable
- [ ] Servir des fichiers statiques (HTML, CSS, images)
- [ ] Gestion des méthodes GET, HEAD
- [ ] Gestion de la concurrence (threads/async)
- [ ] Codes de statut (200, 404, 500)

**Fonctionnalités DNS :**
- [ ] Résolution simplifiée (interrogation d'un fichier hosts local)
- [ ] Cache DNS avec expiration TTL

**Dépôt GitHub :** `mini-http-dns-server`

---

## Ressources

- [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/)
- [Wireshark Documentation](https://www.wireshark.org/docs/)
- [TCP/IP Illustrated — Stevens](https://en.wikipedia.org/wiki/TCP/IP_Illustrated)
- [Subnetting Practice](https://subnettingpractice.com/)

---

## Checklist de maîtrise

- [ ] Calculer un sous-réseau à partir d'une adresse IP et d'un masque
- [ ] Expliquer le 3-way handshake TCP
- [ ] Expliquer la différence TCP vs UDP
- [ ] Lire une table de routage
- [ ] Configurer une interface réseau (ip addr, route)
- [ ] Utiliser nslookup, ping, traceroute, tcpdump
- [ ] Expliquer le principe de NAT/PAT
- [ ] Analyser une trame Ethernet avec Wireshark
