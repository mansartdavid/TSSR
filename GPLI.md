# TP - Installation de GLPI 12.x sur Debian 13.7

## Objectif

Mettre en place un serveur GLPI fonctionnel sous Debian 13.7 avec :

- SSH
- Apache
- MariaDB
- PHP
- GLPI 12.x
- GLPI Agent
- Inventaire automatique du serveur

---

# Schéma

```text
Debian 13.7
│
├── SSH
├── Apache
├── MariaDB
├── PHP
├── GLPI
└── GLPI Agent
        │
        └── Inventaire automatique
```

---

# 1 - Mise à jour du système

Passer en root :

```bash
su -
```

Mettre à jour Debian :

```bash
apt update
apt upgrade -y
```

Vérifier la version :

```bash
cat /etc/os-release
```

Résultat attendu : Debian 13.7

---

# 2 - Vérification du réseau

Afficher l'adresse IP :

```bash
ip a
```

Tester Internet :

```bash
ping 8.8.8.8
```

Tester le DNS :

```bash
ping google.fr
```

✅ Réseau opérationnel

---

# 3 - Installation de SSH

Installer le serveur SSH :

```bash
apt install openssh-server -y
```

Activer le service :

```bash
systemctl enable ssh
systemctl start ssh
```

Vérifier :

```bash
systemctl status ssh
```

Vérifier l'écoute du port 22 :

```bash
ss -tulpn | grep :22
```

✅ SSH opérationnel

---

# 4 - Installation d'Apache

Installer Apache :

```bash
apt install apache2 -y
```

Activer Apache :

```bash
systemctl enable apache2
systemctl start apache2
```

Contrôle :

```bash
systemctl status apache2
```

Tester depuis un navigateur :

```text
http://IP_DU_SERVEUR
```

✅ Apache opérationnel

---

# 5 - Installation de MariaDB

Installer MariaDB :

```bash
apt install mariadb-server -y
```

Activer le service :

```bash
systemctl enable mariadb
systemctl start mariadb
```

Sécuriser l'installation :

```bash
mysql_secure_installation
```

Choix recommandés :

```text
Définir un mot de passe root : Oui
Supprimer les utilisateurs anonymes : Oui
Interdire l'accès root distant : Oui
Supprimer la base de test : Oui
Recharger les privilèges : Oui
```

✅ MariaDB sécurisée

---

# 6 - Installation de PHP

Installer PHP et les modules nécessaires :

```bash
apt install php php-mysql php-curl php-gd php-intl php-mbstring php-xml php-zip php-ldap php-imap php-bcmath -y
```

Vérifier :

```bash
php -v
```

Redémarrer Apache :

```bash
systemctl restart apache2
```

✅ PHP installé

---

# 7 - Création de la base GLPI

Connexion à MariaDB :

```bash
mysql -u root -p
```

Créer la base :

```sql
CREATE DATABASE glpi;

CREATE USER 'glpi'@'localhost' IDENTIFIED BY 'MotDePasse123';

GRANT ALL PRIVILEGES ON glpi.* TO 'glpi'@'localhost';

FLUSH PRIVILEGES;

EXIT;
```

✅ Base GLPI prête

---

# 8 - Téléchargement de GLPI

Se placer dans le dossier temporaire :

```bash
cd /tmp
```

Télécharger GLPI :

```bash
wget https://github.com/glpi-project/glpi/releases/latest/download/glpi.tgz
```

Extraire l'archive :

```bash
tar -xzf glpi.tgz
```

Déplacer GLPI :

```bash
mv glpi /var/www/html/
```

Définir les permissions :

```bash
chown -R www-data:www-data /var/www/html/glpi
chmod -R 755 /var/www/html/glpi
```

✅ Fichiers GLPI installés

---

# 9 - Installation de GLPI

Depuis un navigateur :

```text
http://IP_DU_SERVEUR/glpi
```

Suivre l'assistant :

## Langue

```text
Français
```

## Contrat de licence

```text
Accepter
```

## Type d'installation

```text
Nouvelle installation
```

## Paramètres de base de données

```text
Serveur : localhost
Utilisateur : glpi
Mot de passe : MotDePasse123
Base : glpi
```

Finaliser l'installation.

✅ GLPI opérationnel

---

# 10 - Première connexion

Identifiants par défaut :

| Compte | Mot de passe |
|----------|----------|
| glpi | glpi |
| tech | tech |
| normal | normal |
| post-only | postonly |

⚠️ Changer immédiatement le mot de passe du compte glpi.

---

# 11 - Installation de GLPI Agent

Installer l'agent :

```bash
apt install glpi-agent -y
```

Vérifier :

```bash
glpi-agent --version
```

Configurer l'adresse du serveur :

```bash
nano /etc/glpi-agent/agent.cfg
```

Ajouter :

```text
server = http://IP_DU_SERVEUR/glpi/front/inventory.php
```

Sauvegarder le fichier.

---

# 12 - Envoi du premier inventaire

Lancer un inventaire manuel :

```bash
glpi-agent
```

Contrôler dans GLPI :

```text
Parc
→ Ordinateurs
```

Le serveur Debian doit apparaître.

✅ Inventaire fonctionnel

---

# 13 - Vérifications finales

Contrôler les services :

```bash
systemctl status ssh
```

```bash
systemctl status apache2
```

```bash
systemctl status mariadb
```

```bash
systemctl status glpi-agent
```

Tous les services doivent être :

```text
active (running)
```

---

# Résultat attendu

✅ Debian installée

✅ SSH opérationnel

✅ Apache opérationnel

✅ MariaDB opérationnelle

✅ PHP installé

✅ GLPI accessible via navigateur

✅ GLPI Agent installé

✅ Inventaire du serveur remonté dans GLPI

---

# Mémo à retenir

```text
1. Mise à jour Debian
2. Installation SSH
3. Installation Apache
4. Installation MariaDB
5. Installation PHP
6. Création de la base GLPI
7. Installation GLPI
8. Installation GLPI Agent
9. Premier inventaire
10. Vérifications finales
```
