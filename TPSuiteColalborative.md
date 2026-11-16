#Étude de choix d'une suite collaborative

##Contexte

L'entreprise fictive **Atelier ExploreIT** compte 40 salariés et souhaite mettre en place une suite collaborative répondant aux besoins suivants :

###Population 1 : Administration (10 utilisateurs)

- Comptabilité

- Ressources Humaines

- Direction

**Besoins :**

- Utilisation d'Excel avec macros VBA

- Environ 200 Go de données par utilisateur

- Partage externe contrôlé

- Messagerie professionnelle

###Population 2 : Terrain / Commerciaux (30 utilisateurs)

**Besoins :**

- Messagerie professionnelle

- Partage de documents

- Visioconférence

- Environ 20 Go de stockage par utilisateur

###Population 3 : Ensemble des collaborateurs

**Besoins :**

- Adresse mail au nom de domaine de l'entreprise

- Authentification multifacteur (MFA)

- Réunions jusqu'à 100 participants

---

#Solutions étudiées

## Google Workspace

###Avantages

- Coût réduit

- Simplicité d'utilisation

- Stockage généreux

###Inconvénients

- Incompatibilité avec les macros VBA Excel

- Gestion avancée des postes limitée

- Nécessite l'abandon d'Excel pour Google Sheets

## Microsoft 365

###Avantages

- Compatibilité totale avec Excel et les macros VBA

- Gestion centralisée des utilisateurs

- Intégration native avec Windows

- Sécurité renforcée

- Solution unique pour toute l'entreprise

###Inconvénients

- Coût supérieur à Google Workspace

---
##Comparaison rapide des solutions

| Critère | Google Workspace | Microsoft 365 |
|----------|----------|----------|
| Coût | ✅ Généralement moins cher | ❌ Plus coûteux |
| Prise en main | ✅ Simple et intuitive | ✅ Très répandue en entreprise |
| Stockage | ✅ Généreux selon l'offre choisie | ✅ Suffisant pour les besoins de l'entreprise |
| Compatibilité Excel VBA | ❌ Non compatible | ✅ Compatible à 100 % |
| Intégration Windows | ⚠️ Limitée | ✅ Native |
| Administration des utilisateurs | ⚠️ Plus basique | ✅ Plus complète |
| Sécurité avancée | ⚠️ Selon les offres | ✅ Incluse dans Business Premium |
| Adaptation aux besoins d'Atelier ExploreIT | ⚠️ Partielle | ✅ Complète |

###Synthèse

Google Workspace représente une solution intéressante grâce à son coût plus faible et à sa simplicité d'utilisation. En revanche, l'absence de compatibilité avec les macros VBA d'Excel constitue un point bloquant pour les services administratifs de l'entreprise.

Microsoft 365 est plus coûteux, mais il répond à l'ensemble des besoins identifiés, notamment pour la comptabilité, les ressources humaines et la direction. C'est donc la solution retenue pour Atelier ExploreIT.  

  
#Solution retenue

L'analyse montre que les besoins des utilisateurs ne sont pas identiques.

L'utilisation d'Excel avec macros VBA par les services administratifs impose l'utilisation de Microsoft 365.

Afin d'optimiser les coûts tout en répondant aux besoins fonctionnels, deux licences Microsoft 365 sont retenues.

## Répartition des licences

| Population | Nombre | Licence |

| Comptabilité / RH / Direction | 10 | <span style="color:#4472C4">Microsoft 365 Business Premium</span> |

| Commerciaux / Terrain | 30 | <span style="color:#70AD47">Microsoft 365 Business Basic</span> |

---

#Justification du choix

##Microsoft 365 Business Premium (10 licences)

Cette licence apporte :

- Applications Office Desktop complètes

- Excel avec prise en charge des macros VBA

- Outlook

- Teams

- Exchange Online

- OneDrive

- Intune

- Sécurité avancée

- Authentification multifacteur

> Cette offre répond intégralement aux besoins des services administratifs.

##Microsoft 365 Business Basic (30 licences)

Cette licence apporte :

- Outlook Web

- Teams

- OneDrive

- Word, Excel et PowerPoint Online

- Exchange Online

- MFA

Les utilisateurs terrain n'ont pas besoin d'Excel Desktop ni de macros VBA.

> <span style="color:#00B050"><strong>Cette licence est donc suffisante pour leurs usages quotidiens tout en restant économique.</strong></span>

---

#Estimation financière

## Tarifs retenus

| Offre | Quantité | Prix unitaire HT/mois | Prix unitaire TTC/mois |

| Business Premium | 10 | 19,06 € | 22,87 € |

| Business Basic | 30 | 5,60 € | 6,72 € |

## Coût mensuel

| Offre | Quantité | Total HT/mois | Total TTC/mois |

| Business Premium | 10 | 190,60 € | 228,70 € |

| Business Basic | 30 | 168,00 € | 201,60 € |

| **Total** | **40** | **358,60 €** | **430,30 €** |

> Coût mensuel TTC : 430,30 €

## Coût annuel

| Offre | Total HT/an | Total TTC/an |

| Business Premium | 2 287,20 € | 2 744,40 € |

| Business Basic | 2 016,00 € | 2 419,20 € |

| **Total annuel** | **4 303,20 €** | **5 163,60 €** |

  
> Coût annuel TTC : 5 163,60 €

---

##Analyse budgétaire

Le coût total de la solution retenue représente :

- **358,60 € HT par mois** (**430,30 € TTC**)

- **4 303,20 € HT par an** (**5 163,60 € TTC**)

Cette répartition des licences permet de faire des économies tout en répondant aux besoins de chacun. Les équipes administratives disposent des outils avancés dont elles ont besoin, tandis que les commerciaux profitent d'une offre plus légère mais parfaitement adaptée à leur utilisation quotidienne.

---
### Matrice de décision

| Critère | Google Workspace | Microsoft 365 | Avantage |
|----------|----------|----------|----------|
| Prix | ✅ | ❌ | Google Workspace |
| Migration depuis l'existant | ⚠️ Nécessite des adaptations | ✅ Plus simple | Microsoft 365 |
| Accessibilité | ✅ Applications Web performantes | ✅ Applications Web et Desktop | Égalité |
| Compatibilité avec le parc Windows | ⚠️ Correcte | ✅ Native | Microsoft 365 |
| Hébergement des données | ✅ Conforme RGPD | ✅ Conforme RGPD | Égalité |
| Sécurité | ✅ Bonne | ✅ Très complète | Microsoft 365 |
| Administration | ⚠️ Plus limitée | ✅ Plus complète | Microsoft 365 |
| Compatibilité Excel VBA | ❌ Non compatible | ✅ Compatible | Microsoft 365 |

### Recommandation

Bien que Google Workspace soit moins coûteux, Microsoft 365 est la solution la plus adaptée aux besoins de l'entreprise.

La présence d'un parc informatique Windows, l'utilisation d'Excel avec macros VBA et les fonctionnalités d'administration avancées constituent des arguments importants en faveur de Microsoft 365.

La migration sera plus simple, les utilisateurs conserveront leurs outils habituels et l'entreprise bénéficiera d'une gestion centralisée de ses services et de sa sécurité.  

  
##Conclusion  

La solution retenue repose exclusivement sur Microsoft 365 :

- 10 licences Business Premium pour les utilisateurs nécessitant Excel avec macros VBA.

- 30 licences Business Basic pour les utilisateurs terrain.

Cette architecture répond à l'ensemble des besoins fonctionnels, garantit une administration simplifiée, assure la compatibilité avec les outils Microsoft déjà largement utilisés en entreprise et permet d'optimiser les coûts en évitant l'attribution de licences Premium à l'ensemble des salariés.

##**Microsoft 365 est donc la solution recommandée pour Atelier ExploreIT.**  
##**La solution est donc techniquement cohérente, évolutive et économiquement pertinente pour Atelier ExploreIT.**
