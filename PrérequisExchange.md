# Prérequis Exchange

## Infrastructure

Installation de deux serveurs :

- **WS2025 DC-Exchange**
- **WS2025 Exchange**

---

# I - WS2025 DC-Exchange

### Configuration initiale

- Installation complète des **VMware Tools**
- Configuration réseau :
  - Type : **NAT**
  - Adresse IP : **x.x.x.250/24**
- Nom du serveur : **DC-Exchange**

➡️ Redémarrer le serveur

### Installation des rôles

- **Active Directory Domain Services (AD DS)**
- **DNS**

#### Configuration AD DS

- Domaine : **tssrdavid.lan**
- Promotion en contrôleur de domaine

➡️ Redémarrer le serveur

#### Configuration DNS

- Création de la **zone de recherche inversée**

➡️ Redémarrer le serveur

### Comptes utilisateurs

- Création des utilisateurs nécessaires

---

# II - WS2025 Exchange

### Configuration initiale

- Installation complète des **VMware Tools**
- Configuration réseau :
  - Type : **NAT**
  - Adresse IP : **x.x.x.251/24**
- Nom du serveur : **Exchange**

➡️ Redémarrer le serveur

### Intégration au domaine

- Joindre le serveur au domaine **tssrdavid.lan**
- Vérifier la communication avec le contrôleur de domaine (**DC-Exchange**)

➡️ Redémarrer le serveur

---

# Vérifications avant l'installation d'Exchange

- [ ] Résolution DNS fonctionnelle
- [ ] Ping entre les deux serveurs
- [ ] Serveur Exchange joint au domaine
- [ ] Compte administrateur de domaine disponible
- [ ] Date et heure synchronisées
- [ ] Accès Internet fonctionnel (si téléchargement de prérequis)
- [ ] VMware Tools installés sur les deux VM
