# Installation d'Exchange Server SE

*LES OUTILS PRÉQUIS NE SONT PAS PRÉSENT EN LIGNE*  
*ExchangeServerSE-x64.iso*  
*rewrite_amd64_fr-FR.msi*  
*UcmaRuntimeSetup.exe*  
*vcredist_x64.exe*  
  
## Prérequis

### Serveur Active Directory (Windows Server 2025)

Configuration requise :

- Nom du serveur défini
- Adresse IP fixe configurée
- Carte réseau en **NAT**
- Rôles **AD DS** et **DNS** installés
- Contrôleur de domaine promu
- Zone de recherche inversée créée

---

# I - Préparation de l'Active Directory

## 1. Désactiver les mises à jour Windows

Ouvrir **SCONFIG** et bloquer toutes les mises à jour provenant de Windows Update.

---

## 2. Installer les outils ADDS

Ouvrir une console **PowerShell** en administrateur et exécuter :

```powershell
Install-WindowsFeature RSAT-ADDS
```

---

## 3. Installer Microsoft Visual C++ Redistributable

Installer :

- `vcredist_x64.exe`

---

## 4. Monter l'ISO Exchange Server SE

Télécharger l'image ISO :

- `ExchangeServerSE-x64.iso`

Monter l'ISO dans :

```text
E:\exchange
```

---

## 5. Ouvrir l'invite de commandes

Lancer **CMD en tant qu'administrateur** puis se placer dans le dossier :

```cmd
E:\exchange
```

---

## 6. Préparer Active Directory pour Exchange

Exécuter les commandes suivantes dans l'ordre :

### Préparation du schéma

```cmd
Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms_DiagnosticDataON
```

### Préparation de l'organisation

```cmd
Setup.exe /PrepareAD /OrganizationName:"TSSRDavid" /IAcceptExchangeServerLicenseTerms_DiagnosticDataON
```

### Préparation des domaines

```cmd
Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms_DiagnosticDataON
```

---

# II - Installation du serveur Exchange

## Configuration initiale

Vérifier les éléments suivants :

- Nom du serveur défini
- Adresse IP fixe configurée
- Serveur joint au domaine
- Carte réseau en **NAT**

---

## 1. Désactiver les mises à jour Windows

Ouvrir **SCONFIG** et bloquer toutes les mises à jour provenant de Windows Update.

---

## 2. Installer les prérequis

Installer :

- `vcredist_x64.exe`
- `UcmaRuntimeSetup.exe`

---

## 3. Monter l'ISO Exchange SE

Monter l'image ISO dans :

```text
C:\exchange
```

---

## 4. Installation en ligne de commande

Lancer la commande suivante :

```cmd
Setup.exe /Mode:Install /Roles:Mailbox /InstallWindowsComponents /IAcceptExchangeServerLicenseTerms_DiagnosticDataON
```

---

## 5. En cas d'échec

Installer le composant :

- **IIS URL Rewrite**
- Fichier : `rewrite_amd64.msi`

Puis relancer la commande :

```cmd
Setup.exe /Mode:Install /Roles:Mailbox /InstallWindowsComponents /IAcceptExchangeServerLicenseTerms_DiagnosticDataON
```

---

## 6. Alternative : installation graphique (GUI)

Au lieu de l'installation CLI :

- Monter l'ISO Exchange SE
- Exécuter `Setup.exe`
- Suivre l'assistant graphique d'installation

---

## 7. Redémarrage

➡️ Redémarrer le serveur Exchange après l'installation.

---

# Vérification d'accès

## Centre d'administration Exchange (ECP)

Remplacer `xxx.xxx.xxx.xxx` par l'adresse IP fixe du serveur Exchange :

```text
https://xxx.xxx.xxx.xxx/ecp
```

---

## Outlook Web App (OWA)

Remplacer `xxx.xxx.xxx.xxx` par l'adresse IP fixe du serveur Exchange :

```text
https://xxx.xxx.xxx.xxx/owa
```

---

# Checklist finale

- [ ] AD DS installé
- [ ] DNS installé
- [ ] Zone inversée créée
- [ ] Contrôleur de domaine promu
- [ ] Serveur Exchange joint au domaine
- [ ] RSAT-ADDS installé
- [ ] vcredist_x64 installé
- [ ] UCMA Runtime installé
- [ ] Schéma Active Directory préparé
- [ ] Organisation Exchange créée
- [ ] Domaines préparés
- [ ] IIS URL Rewrite installé (si nécessaire)
- [ ] Installation Exchange terminée
- [ ] Serveur redémarré
- [ ] Accès ECP fonctionnel
- [ ] Accès OWA fonctionnel
