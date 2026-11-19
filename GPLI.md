# TP - Installation de GLPI 12.0.2 sur Debian 13.7

## Objectif

Mettre en place un serveur GLPI fonctionnel sous Debian 13.7 en mode CLI avec :

- SSH
- Apache2
- MariaDB
- PHP 8.x
- PHP-FPM
- GLPI 12.0.2
- GLPI Agent
- Inventaire automatique

---

# Architecture

```text
Debian 13.7
│
├── SSH (22)
├── Apache2 (80)
├── MariaDB
├── PHP-FPM
├── GLPI 12.0.2
└── GLPI Agent
        │
        └── Remontée d'inventaire automatique
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

Résultat attendu :

```text
Debian GNU/Linux 13.7
```

✅ Système à jour

---

# 2 - Vérification du réseau

Afficher la configuration réseau :

```bash
ip a
```

Tester la connectivité Internet :

```bash
ping 8.8.8.8
```

Tester la résolution DNS :

```bash
ping google.fr
```

✅ Réseau fonctionnel

---

# 3 - Installation du serveur SSH

Installer OpenSSH :

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

Contrôler le port 22 :

```bash
ss -tulpn | grep :22
```

✅ SSH opérationnel

---

# 4 - Installation du serveur Web et de MariaDB

Installer Apache, PHP et MariaDB :

```bash
apt install apache2 php mariadb-server -y
```

Installer les modules PHP requis pour GLPI :

```bash
apt install php-xml php-common php-json php-mysql php-mbstring php-curl php-gd php-intl php-zip php-bz2 php-apcu -y
```

Installer les modules complémentaires :

```bash
apt install php-ldap php-fpm php-bcmath -y
```

Vérifier PHP :

```bash
php -v
```

✅ Apache, MariaDB et PHP installés

---

# 5 - Sécurisation de MariaDB

Lancer l'assistant :

```bash
mariadb-secure-installation
```

Choix recommandés :

```text
Définir le mot de passe root : Oui
Supprimer les utilisateurs anonymes : Oui
Interdire l'accès root distant : Oui
Supprimer la base de test : Oui
Recharger les privilèges : Oui
```

✅ MariaDB sécurisée

---

# 6 - Création de la base GLPI

Connexion à MariaDB :

```bash
mysql -u root -p
```

Créer la base :

```sql
CREATE DATABASE glpi;
```

Créer l'utilisateur :

```sql
GRANT ALL PRIVILEGES ON glpi.* TO 'vincent'@'localhost' IDENTIFIED BY 'Azerty1';
```

Appliquer :

```sql
FLUSH PRIVILEGES;
```

Quitter :

```sql
EXIT;
```

✅ Base de données créée

---

# 7 - Téléchargement de GLPI

Se placer dans le dossier temporaire :

```bash
cd /tmp
```

Télécharger GLPI :

```bash
wget https://github.com/glpi-project/glpi/releases/download/12.0.2/glpi-12.0.2.tgz
```

Extraire directement dans Apache :

```bash
tar -xzvf glpi-12.0.2.tgz -C /var/www/html
```

Vérifier :

```bash
ls /var/www/html
```

✅ GLPI déployé

---

# 8 - Configuration des permissions

Attribuer les permissions :

```bash
chmod -R 755 /var/www/html/
```

Attribuer le propriétaire Apache :

```bash
chown -R www-data:www-data /var/www/html/
```

Redémarrer les services :

```bash
systemctl restart apache2 mariadb.service
```

✅ Permissions configurées

---

# 9 - Configuration du VirtualHost Apache

Créer le fichier :

```bash
nano /etc/apache2/sites-available/glpi.conf
```

Ajouter :

```apache
<VirtualHost *:80*
    ServerName glpi
    ServerAli*s 172.X.X.X

    DocumentRoot /*ar/www/html

    Alias /glpi /*ar/www/html/glpi/public

    <Dire*tory*/var/www/html/glpi/public>
       *Options -Indexes +FollowSymLinks
 *      Require all*granted

        RewriteEngine On
*       RewriteBase /glpi/

       *RewriteCond %{REQUEST_FILENAME* !-f
        RewriteCond %{REQUEST*FILENAME} !-d
        RewriteRule * index.php [QSA,L]
    </Directory*

    <FilesMatch \.php$>
*       SetHandler "proxy:unix:/run*php*php8.4-fpm.sock|fcgi*//localhost"
    </FilesMatch>

  * ErrorLog ${APACHE_LOG_DIR}/glpi_e*ror*log
    CustomLog ${APACHE_LOG_DIR*/glpi_access.log combined
</Virtua*Host*
```

Sauvegarder :

```text
*TRL + O
Entrée
CTRL + X*```

✅ VirtualHost créé*
---

# 10 - Activation des module* Apache*
Activer les modules nécessaires :*
```bash
a2enmod proxy_fcgi setenv*f*```

```bash
a2enmod*rewrite
```

Activer PHP-FPM :

*``bash
a2en*onf php*-fpm
```

Désactiver le site par défaut :

```bash
a2dissite 000-default.conf
```

Activer le site GLPI :

```bash
a2ensite glpi.conf
```

Redémarrer Apache :

```bash
systemctl restart apache2 mariadb.service
```

Vérifier :

```bash
apachectl configtest
```

Résultat attendu :

```text
Syntax OK
```

✅ Configuration Apache validée

---

# 11 - Installation de GLPI

Depuis un navigateur :

```text
http://IP_DU_SERVEUR/glpi
```

Suivre l'assistant :

### Langue

```text
Français
```

### Licence

```text
Accepter
```

### Type d'installation

```text
Nouvelle installation
```

### Connexion à la base

```text
Serveur : localhost
Utilisateur : vincent
Mot de passe : Azerty1
Base : glpi
```

Finaliser l'installation.

✅ GLPI opérationnel

---

# 12 - Première connexion

Comptes par défaut :

| Utilisateur | Mot de passe |
|------------|------------|
| glpi | glpi |
| tech | tech |
| normal | normal |
| post-only | postonly |

⚠️ Modifier immédiatement le mot de passe du compte administrateur.

---

# 13 - Installation de GLPI Agent

Installer l'agent :

```bash
apt install glpi-agent -y
```

Vérifier :

```bash
glpi-agent --version
```

Configurer :

```bash
nano /etc/glpi-agent/agent.cfg
```

Ajouter :

```text
server = http://IP_DU_SERVEUR/glpi/front/inventory.php
```

Enregistrer.

✅ Agent configuré

---

# 14 - Premier inventaire

Lancer manuellement :

```bash
glpi-agent
```

Dans GLPI :

```text
Parc
→ Ordinateurs
```

Le serveur Debian doit apparaître.

✅ Inventaire remonté

---

# 15 - Vérifications finales

Contrôle des services :

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
systemctl status php8.4-fpm
```

```bash
systemctl status glpi-agent
```

Tous les services doivent être :

```text
active (running)
```

---

# Dépannage rapide

## Vérifier Apache

```bash
apachectl configtest
```

## Vérifier les logs GLPI

```bash
tail -f /var/log/apache2/glpi_error.log
```

## Vérifier les ports ouverts

```bash
ss -tulpn
```

## Vérifier PHP

```bash
php -v
```

## Vérifier MariaDB

```bash
mysql -u root -p
```

---

# Résultat attendu

✅ Debian 13.7 installée

✅ SSH opérationnel

✅ Apache fonctionnel

✅ MariaDB sécurisée

✅ PHP-FPM installé

✅ GLPI 12.0.2 accessible

✅ Agent GLPI installé

✅ Inventaire automatique fonctionnel

---

# Mémo à retenir

```text
1. Mise à jour Debian
2. Installation SSH
3. Installation Apache / MariaDB
4. Installation PHP
5. Sécurisation MariaDB
6. Création base GLPI
7. Téléchargement GLPI
8. Permissions
9. VirtualHost Apache
10. Modules Apache
11. Installation GLPI
12. Installation GLPI Agent
13. Premier inventaire
14. Vérifications finales
```
