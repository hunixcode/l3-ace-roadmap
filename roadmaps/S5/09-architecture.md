# Roadmap — Architecture Réseau

> **Matière** : OSI / Ethernet / HDLC / Performances  
> **Objectif** : Maîtriser les fondamentaux de l'architecture réseau, de la couche physique à la couche liaison

---

## Concepts Clés

### 🟢 Fondamentaux

| Concept | Définition |
|---------|-----------|
| **OSI (Open Systems Interconnection)** | Modèle en 7 couches normalisé par l'ISO pour standardiser les communications réseau |
| **Couche Physique (L1)** | Transmission brute de bits sur le support (câble, fibre, air) |
| **Couche Liaison (L2)** | Accès au support, adressage MAC, détection/correction d'erreurs |
| **Couche Réseau (L3)** | Routage des paquets, adressage logique (IP) |
| **Topologie réseau** | Structure du réseau : bus, étoile, anneau, maillée |
| **Bande passante** | Débit maximal théorique (généralement en Mbps ou Gbps) |
| **Débit utile (throughput)** | Débit réel après déduction des overheads |
| **RTT (Round Trip Time)** | Temps aller-retour d'un paquet entre deux points |
| **Taux d'erreur (BER)** | Bit Error Rate — nombre de bits erronés / nombre total de bits |

### 🟢 Supports de Transmission

| Support | Bande passante | Portée | Usage typique |
|---------|---------------|--------|--------------|
| **Paire torsadée** | Jusqu'à 10 Gbps (Cat 6a) | 100m | Ethernet local |
| **Coaxial** | Jusqu'à 1 Gbps | 500m | Câble TV, anciens réseaux |
| **Fibre optique** | Jusqu'à 400 Gbps+ | 40km+ | Backbone Internet |
| **Ondes radio (WiFi)** | Jusqu'à 9.6 Gbps (WiFi 7) | Variable | Réseaux sans fil |

### 🟢 Ethernet (IEEE 802.3)

| Concept | Définition |
|---------|-----------|
| **CSMA/CD** | Carrier Sense Multiple Access with Collision Detection — écoute avant d'émettre, détecte les collisions |
| **Trame Ethernet** | Préambule (8B) + MAC dst (6B) + MAC src (6B) + Type/Longueur (2B) + Données (46-1500B) + CRC (4B) |
| **MAC Address** | Adresse physique unique de 48 bits attribuée par le fabricant |
| **Auto-négociation** | Négociation automatique de la vitesse et du duplex entre deux équipements |
| **Half-duplex vs Full-duplex** | Half = émission ou réception (pas les deux) / Full = simultané |
| **10BASE-T, 100BASE-TX, 1000BASE-T** | Standards Ethernet à 10, 100, 1000 Mbps sur paire torsadée |

### 🟡 HDLC (High-Level Data Link Control)

| Concept | Définition |
|---------|-----------|
| **HDLC** | Protocole de niveau liaison orienté bit — normalisé par l'ISO |
| **Trame HDLC** | Drapeau (01111110) + Adresse + Contrôle + Données + FCS + Drapeau |
| **Transparence (bit stuffing)** | Insertion d'un 0 après 5 "1" consécutifs pour ne pas confondre avec le drapeau |
| **Trame I (Information)** | Transporte des données de l'utilisateur — contient N(S) et N(R) |
| **Trame S (Supervisory)** | Contrôle de flux et d'erreur — RR, RNR, REJ, SREJ |
| **Trame U (Unnumbered)** | Commandes de contrôle (SABM, DISC, UA, DM, FRMR) |
| **Sliding Window** | Fenêtre d'anticipation — W = nombre max de trames non acquittées |
| **Go-back-N (REJ)** | En cas d'erreur, retransmet à partir de la trame erronée |
| **Selective Reject (SREJ)** | Retransmet seulement la trame erronée |

### 🟡 Performance Réseau

| Concept | Définition |
|---------|-----------|
| **Débit effectif** | `(taille de trame) / (temps d'émission + propagation + traitement)` |
| **Efficacité du canal** | `(données utiles) / (données totales transmises)` en tenant compte des overheads |
| **Taille de trame optimale** | Compromis entre overhead (trames petites) et risque d'erreur (trames grandes) |
| **Délai de propagation** | `distance / vitesse de propagation` (c ≈ 2×10⁸ m/s dans un câble) |

### 🔴 Avancés

| Concept | Définition |
|---------|-----------|
| **PPP (Point-to-Point Protocol)** | Protocole liaison pour liaisons point-à-point — successeur de SLIP |
| **SLIP** | Serial Line IP — protocole simple mais sans détection d'erreur |
| **WiFi (IEEE 802.11)** | CSMA/CA (au lieu de CSMA/CD) — évite les collisions au lieu de les détecter |
| **Token Ring (IEEE 802.5)** | Topologie en anneau à jeton — chaque station ne peut émettre que si elle possède le jeton |
| **FDDI** | Fiber Distributed Data Interface — anneau double de fibre optique |

---

## Projets Concrets

### Projet 1 : Calculatrice de Performances Réseau 🟢

**Objectif :** Outil en ligne de commande pour calculer les performances d'une liaison

**Fonctionnalités :**
- [ ] Calcul du débit effectif en fonction du MTU, de la bande passante, du RTT
- [ ] Optimisation de la taille de trame (meilleur compromis overhead/erreurs)
- [ ] Simulation de l'impact du bit stuffing HDLC sur le débit
- [ ] Comparaison HDLC Go-back-N vs Selective Reject
- [ ] Graphiques ASCII ou export CSV

**Stack technique :** Python ou C

**Structure GitHub :**
```
network-calculator/
├── README.md
├── calc.py
├── models/
│   ├── ethernet.py    # Modèle de débit Ethernet
│   ├── hdlc.py        # Modèle HDLC avec bit stuffing
│   ├── wifi.py        # Modèle WiFi
│   └── utils.py
├── tests/
│   └── test_models.py
└── results/
    └── optimisation_mtu.csv
```

---

### Projet 2 : Simulateur HDLC 🟡

**Objectif :** Simuler le protocole HDLC avec gestion d'erreurs

**Fonctionnalités :**
- [ ] Implémentation de trame I, S, U
- [ ] Bit stuffing / bit unstuffing
- [ ] Mode Go-back-N (REJ) — simulateur de pertes
- [ ] Mode Selective Reject (SREJ) — simulateur de pertes
- [ ] Visualisation du sliding window
- [ ] Statistiques : nombre de retransmissions, efficacité

**Stack technique :** Python (simulation avec asyncio) ou C

**Dépôt GitHub :** `hdlc-simulator`

---

### Projet 3 : Capture et Analyse de Trames Ethernet 🟡

**Objectif :** Programme qui capture les trames Ethernet et les affiche

**Fonctionnalités :**
- [ ] Capture raw socket des trames Ethernet
- [ ] Parsing complet de l'en-tête Ethernet (MAC src/dst, type)
- [ ] Parsing ARP
- [ ] Parsing IP + TCP/UDP
- [ ] Parsing ICMP (ping)
- [ ] Statistiques : % de chaque protocole, débit instantané

**Stack technique :** Python (scapy) ou C (libpcap)

**Dépôt GitHub :** `ethernet-analyzer`

---

### Projet 4 : Mini-Switch Ethernet en Logiciel 🔴

**Objectif :** Implémenter un switch Ethernet virtuel (apprentissage MAC + forwarding)

**Fonctionnalités :**
- [ ] Table MAC (apprentissage des adresses)
- [ ] Forwarding / Flooding / Filtering
- [ ] Gestion des boucles (STP simplifié)
- [ ] VLAN simple

**Stack technique :** C ou Python avec raw sockets

**Dépôt GitHub :** `soft-switch`

---

## Ressources

- [IEEE 802.3 Standard](https://standards.ieee.org/standard/802_3-2018.html)
- [HDLC Protocol Overview](https://www.tutorialspoint.com/data_communication_computer_network/hdlc_protocol.htm)
- [Network Performance — Kurose & Ross](https://www.pearson.com/en-us/subject-catalog/p/computer-networking-a-top-down-approach/)
- [Subnetting Practice](https://subnetting.org/)

---

## Checklist de maîtrise

- [ ] Expliquer les 7 couches du modèle OSI
- [ ] Dessiner la structure d'une trame Ethernet
- [ ] Expliquer CSMA/CD (écoute, détection de collision, backoff)
- [ ] Calculer le débit effectif d'une liaison
- [ ] Expliquer le bit stuffing HDLC et pourquoi on l'utilise
- [ ] Comparer Go-back-N vs Selective Reject
- [ ] Convertir des unités : Mbps, Gbps, octets, bits, Gibioctets
- [ ] Expliquer la différence entre un hub, un switch et un routeur
- [ ] Analyser une trame avec Wireshark
