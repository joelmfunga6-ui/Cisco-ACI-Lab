# Cisco-ACI-Lab
Lab – Déploiement du Cisco ACI Simulator sur VMware Workstation &amp; Intégration des premiers nœuds
Voici une **version totalement restructurée en format LAB**, prête à être publiée sur GitHub dans un dépôt *Cisco-ACI-Lab* ou *ACI-Simulator-Lab*.
Le style suit les standards GitHub Labs : sections, étapes, prérequis, screenshots (que tu ajouteras), résultats et concepts clés.

# 🧪 **Lab – Déploiement du Cisco ACI Simulator sur VMware Workstation & Intégration des premiers nœuds**

## 📘 **Overview**

Dans ce lab, je décris les étapes réalisées pour **déployer le Cisco ACI Simulator** sur **VMware Workstation**, initialiser l’APIC et intégrer les premiers **nœuds Leaf** dans le fabric ACI.

Ce projet m’a permis de renforcer ma compréhension de **Cisco ACI (Application Centric Infrastructure)**, une architecture SDN moderne utilisée dans les environnements Datacenter.

---

# 🔵 **1. Introduction à Cisco ACI**

Cisco ACI est une architecture datacenter basée sur le **Software-Defined Networking (SDN)**, permettant :

* l’**automatisation** des configurations,
* la **centralisation** du contrôle réseau,
* la **programmabilité** du fabric.

### 🔧 Comparaison avec d’autres solutions SDN

| Domaine                 | Technologie      |
| ----------------------- | ---------------- |
| WAN                     | **Cisco SD-WAN** |
| LAN                     | **Cisco DNA**    |
| Datacenter              | **Cisco ACI**    |
| Virtualisation (VMware) | **VMware NSX**   |
| Arista                  | **CloudVision**  |

### 🧩 Composants principaux d’un fabric ACI

* **APIC (Application Policy Infrastructure Controller)** → le cerveau
* **Spines** → cœur du réseau, gèrent control plane & data plane
* **Leafs** → switches connectant serveurs, firewalls, endpoints
* **Fabric** → ensemble automatisé grâce au Zero Touch Provisioning (ZTP)

L’APIC orchestre tout :
découverte des nœuds, gestion des politiques, cohérence du fabric et supervision.

---

# 🔵 **2. Objectifs du Lab**

1. Déployer le Cisco ACI Simulator (OVA) sur VMware Workstation
2. Initialiser et configurer le premier APIC
3. Ajouter un premier switch Leaf dans le fabric
4. Comprendre le processus de découverte LLDP et l’enrôlement dans le fabric

---

# 🔵 **3. Environnement & Prérequis**

### 🖥️ **Matériel utilisé**

* VMware Workstation
* 8 vCPU
* 32 Go de RAM
* Stockage suffisant pour l’OVA ACI (~70 Go)

### ⚙️ **Ressources allouées**

Le laboratoire recommande plus, mais j’ai adapté :

| Composant | Ressources Recommandées | Ressources Affectées  |
| --------- | ----------------------- | --------------------- |
| APIC      | 8 CPU / 24–32 Go RAM    | **4 CPU / 16 Go RAM** |
| Leafs     | 4 CPU / 8 Go RAM        | Conforme              |

### 📥 **Fichier utilisé**

* **Cisco ACI Simulator OVA** (fourni par Cisco DevNet)

---

# 🔵 **4. Étapes du Lab**

---

## **Étape 1 – Déploiement de l’OVA ACI Simulator**

1. Importation de l’OVA dans VMware Workstation
2. Modification des ressources CPU / RAM
3. Résolution d'un message bloquant lié à un nombre insuffisant de CPU
4. Démarrage & initialisation complète de la VM APIC
5. Configuration initiale :

   * Adresse IP
   * Gateway
   * Credentials des APICs
   * Fabric Name

📌 *Malgré les ressources limitées, l’APIC a pu s’initialiser correctement.*

---

## **Étape 2 – Mise en place du fabric ACI**

### 🔍 2.1 Découverte automatique des nœuds (LLDP)

Lorsque le simulateur ACI démarre :

* les Leafs se présentent via **LLDP**,
* l’APIC les détecte automatiquement,
* le fabric propose l’intégration avec un ID unique.

### 🧩 2.2 Ajout du premier Leaf

J’ai intégré le premier switch en spécifiant :

* le **Node ID**,
* le **Node Name**,
* le **Role** (Leaf / Spine),
* la **Pod Assignment**.

Cela m’a permis de visualiser :

* le processus de découverte
* la création de la topologie
* l’arrivée du nœud en état *"In Discovery"* puis *"Registered"*
* la cohérence du fabric contrôlée par APIC

# 🔵 **5. Résultats & Compréhensions Acquises**

Ce lab m’a permis de mieux comprendre :

### ✔ **L’architecture interne du fabric ACI**

Spines et Leafs communiquent via un underlay automatisé.

### ✔ **Le rôle central du contrôleur APIC**

Interface unique pour la politique, la découverte, la gestion du fabric.

### ✔ **Le processus de Zero Touch Provisioning (ZTP)**

Les nœuds se configurent eux-mêmes dès leur connexion au fabric.

### ✔ **L’automatisation du datacenter via ACI**

ACI simplifie les opérations réseau en réduisant la configuration manuelle.


# 🔵 **6. Points que j’ajouterai plus tard dans le Lab (Roadmap)**

* Déploiement des **EPGs**, **Bridge Domains**, **VRFs**
* Configuration de contrats (ACI Contracts)
* Intégration d’un hyperviseur (VMware ESXi)
* Automatisation via API REST & Python
* Ajout de Spines dans le fabric

# 🎯 **Conclusion**

Ce lab m’a offert une première immersion complète dans Cisco ACI, depuis l’installation jusqu’à l’intégration d’un premier switch Leaf.
Il m’a permis de consolider mes bases sur :

* la logique du fabric,
* la découverte automatique,
* l’importance de l’APIC,
* et l'automatisation au cœur de l’architecture ACI.

