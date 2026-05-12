Bonjour Borel,

Je souhaite cadrer avec toi une démarche de capitalisation et de partage de connaissances autour de Keycloak, qui est aujourd'hui l'une des briques les plus critiques d’EasyPRO.
Tu en es le référent depuis le début, et l'objectif de ce mail est de poser le cadre d'un travail commun : documenter, partager et structurer la connaissance autour de cette brique, afin que l'équipe Ops puisse s'en saisir pleinement et que le projet dispose d'une vision claire et durable du sujet.

1. Contexte et raisons de la démarche

Plusieurs éléments rendent ce cadrage nécessaire et urgent :
•	Criticité métier : Keycloak conditionne directement la connexion des clients EasyPRO et notre conformité DSP2. Toute indisponibilité ou erreur de configuration a un impact immédiat sur la production et sur nos engagements réglementaires.
•	Continuité de service : à date, l'équipe Ops n'est pas encore en mesure d'assurer pleinement le relais sur les activités courantes (exploitation, déploiement de plugins, configuration, incidents). C'est précisément ce que cette démarche doit nous permettre de construire ensemble.
•	Mutualisation de la connaissance : nous sommes aujourd'hui en single point of knowledge sur un composant critique. Pour l'équipe comme du point de vue audit et sécurité, nous avons besoin d'élargir cette base de connaissances et de la rendre partagée.
•	Gouvernance et traçabilité : nous avons besoin que l'historique, l'état actuel et les chantiers en cours soient documentés au même niveau que les autres briques de la plateforme.

2. Outils mis à disposition

Pour faciliter ton travail, j'ai préparé deux espaces dédiés :
•	Page Wiki Keycloak (rédaction de la documentation) : [lien wiki]
•	SharePoint Keycloak (dépôt des documents bruts : exports, diagrammes, CR, fichiers de conf, captures, archives) : [lien SharePoint]
Merci d'utiliser exclusivement ces deux espaces, afin que tout soit centralisé et accessible à l’équipe.

3. Arborescence documentaire proposée (Wiki)

Pour qu'on parte sur une base commune, voici la structure que je te propose pour la page Wiki. Tu peux l'adapter à la marge, mais merci de conserver les grandes sections :

A.	Architecture générale et diagrammes
a.	Schéma global d'architecture
b.	Diagrammes de séquence (login, DSP2)
c.	ADR (décisions d'architecture)
d.	Cartographie des intégrations amont / aval : applications consommatrices internes, TPP DSP2, IdP fédérés (LCL SSO…), services back-end appelants. Cette cartographie est indispensable pour évaluer l'impact de tout changement sur Keycloak.
B.	État des lieux technique - inventaire des versions et des composants en production
a.	Versions déployées par environnement (dev-recette / pprd / prod) : Keycloak (tag + digest), Java, base de données...
b.	Plugins / providers / thèmes chargés au runtime
c.	Drift IaC ↔ réel (overrides manuels, hotfix hors GitOps, s'il y'en a)
C.	Configuration & exploitation
a.	Configuration logique : realms, clients, rôles, groupes, politiques (MdP, MFA, sessions), fédération / brokering
b.	Instances Keycloak : URLs des consoles admin et endpoints publics par environnement.
c.	Build et déploiement : 
•	Repos GitLab : lien direct vers le(s) repo(s) Terraform Keycloak, le(s) repo(s) des plugins / providers / thèmes, et le(s) repo(s) des manifests / charts ArgoCD
	Instances ArgoCD : URL des consoles ArgoCD utilisées par environnement, et nom des applications ArgoCD qui pilotent Keycloak
	Pipelines CI/CD : où ils sont définis, ce qu'ils font, ce qu'ils ne font pas (étapes manuelles éventuelles)
	Procédure spécifique de build et de déploiement d'un plugin / provider / thème (étapes, dépendances, contrôle qualité).
d.	Inventaire des runbooks existants et des opérations courantes les plus fréquentes...
e.	Gestion d'incident Keycloak / savoir réagir et diagnostiquer : un arbre de décision clair indiquant par où démarrer l'investigation face à un incident d'authentification, et les premiers réflexes à avoir.
f.	Sauvegarde & restauration :
•	Stratégie de backup : ce qui est sauvegardé (BDD, configuration realm, secrets), où, à quelle fréquence, avec quelle rétention
•	Procédure de restauration testée : étapes, durée constatée, dernière date de test réussi
•	Scénarios de bascule : entre instances, bascule lecture-seule...
D.	Sécurité & observabilité
a.	Comptes admin (humains et techniques) : inventaire, propriétaire, rotation
b.	Secrets : inventaire, localisation, mode d'injection, rotation
c.	Certificats : inventaire, échéances, procédure de renouvellement
d.	Logs & SIEM : événements applicatifs remontés, branchement
e.	Observabilité : métriques exposées, dashboards (Dynatrace, CloudWatch…), Alertes configurées (seuils, destinataires, règles de routage)
E.	Roadmap et plan d'actions 
a.	Plan d'upgrade Keycloak : version cible, prérequis, fenêtres, jalons
b.	Montée de version des composants associés (Java, BDD, images de base...)
c.	Plan de remédiation des CVEs identifiées
d.	Améliorations identifiées : durcissement sécurité, observabilité, automatisation

4. Centralisation documentaire (SharePoint)

Pour la centralisation et le dépôt de tous les documents Keycloak, nous pouvons utiliser ce dossier. J’ai déjà ajouté les documents suivants :
•	KEYCLOAK-Action-Items-V1
•	Cas_usage_securite_Keycloak_SOC_Complet 
•	Keycloak-infos.csv
•	PELICAN_Cahier_Recette_Securite_CAGIP_ Service Keycloak
•	TI-CAGIP-KEYCLOAK-102025

5. Demandes précises et livrables attendus

Pour avancer concrètement, voici les demandes regroupées par priorité, avec les livrables associés. Merci de répondre à ce mail en confirmant la prise en compte de chacune.

•	Plan d'actions & risques résiduels (priorité haute)
•	Ce fichier Excel recense l'ensemble des actions et des risques résiduels Keycloak. Peux-tu le mettre à jour comme suit ?
	Onglet 3 : Risques résiduels : les 6 risques identifiés sont tous en statut « En cours ». Merci de confirmer leur statut actuel et l'état d'avancement du plan de traitement de chacun.
	Onglet 1 : Sur les 73 actions listées, uniquement 28 sont en statut terminé. Merci de revoir et mettre à jour le statut des actions restantes.

•	Transfert de connaissances
o	Organiser 1 à 2 sessions d'1 h avec les membres de l'équipe Ops pour qu'ils puissent assurer, en autonomie :
	Les opérations courantes (configuration, déploiement, exploitation au quotidien),
	Le déploiement d'un changement standard (plugin, provider, configuration realm),
	Le traitement d'un incident P1 / P2 sur Keycloak,
	l'onboarding d'un nouveau client OAuth ou TPP DSP2,
	La procédure de debug d'un problème d'authentification en prod (par où commencer, quels logs regarder).

•	Etat des lieux techniques des composants Keycloak en production 
o	L'IaC nous donne l'état cible, mais pas l'état réellement déployé. J'ai besoin d'une photographie technique à date de Keycloak et de ses composants, par environnement, à publier dans la section État des lieux technique du Wiki :
	Tableau d'inventaire des versions (Keycloak : tag d'image et digest, Java / Quarkus, base de données...)
	Liste des plugins / providers / thèmes réellement chargés au runtime, avec versions et origine ;
	Drift IaC ↔ réel : tout écart entre le code (GitLab / Terraform / ArgoCD) et l'état réellement en cours d'exécution (overrides manuels, hotfix hors GitOps, plugins compilés localement…).
o	Ce livrable est le prérequis à toute décision d'upgrade, de durcissement ou de bascule, et il sera demandé en cas d'audit sécurité ou de revue de risque.

•	Sécurité : comptes admin, secrets et certificats 
o	Produire et publier dans la section Sécurité & observabilité du Wiki :
	L'inventaire des comptes admin Keycloak (humains et techniques), avec usage, propriétaire, et politique de rotation associée
	L'inventaire des secrets utilisés par Keycloak (DB, clients confidentiels, clés de signature, secrets d'intégration), avec leur localisation, leur mode d'injection et leur politique de rotation
	L'inventaire des certificats (front, back-channel, signature des tokens), avec dates d'échéance et procédure de renouvellement documentée
	L'inventaire des clés de signature des realms (JWKS), avec date de dernière rotation et procédure de rotation documentée 

•	Documentation technique complète
o	Rédiger les sections du Wiki selon l'arborescence proposée, avec en particulier :
	Les diagrammes à jour (architecture globale, séquence de login, séquence DSP2) ;
	La cartographie des intégrations amont / aval (applications consommatrices, TPP DSP2, IdP fédérés)

•	Centralisation des documents 
o	Déposer sur le SharePoint tous les documents Keycloak existants : diagrammes d'architecture, schémas de séquence, CR de réunions internes et avec CAGIP / SNI, exports de configuration, etc.

•	Observabilité / monitoring / alerting 
o	Documenter dans le Wiki :
	Les métriques Keycloak exposées et leur source,
	Les dashboards en place avec leurs liens,
	Les alertes configurées (seuils, destinataires, règles de routage),
	La stratégie de logs (collecte, rétention…)

•	État des lieux des actions en cours
o	Rédiger dans Jira les tickets nécessaires pour recenser l'ensemble des actions en cours sur Keycloak, afin qu'elles soient suivies dans l'outil de l'équipe au même titre que les autres chantiers.

•	Roadmap d'upgrade Keycloak (priorité haute)
o	Nous sommes actuellement en Keycloak 26.4.7, qui présente plusieurs CVEs HIGH connues ( 5 versions de patch sont sorties sur la branche 26.4 (26.4.8 → 26.4.11), plus deux mineures complètes : 26.5 et 26.6) Sur la base de l'état des lieux technique, j'ai besoin que tu construises et que tu documentes une roadmap d'upgrade vers les versions les plus récentes de Keycloak, à publier dans la section Roadmap et plan d'actions du Wiki.

J'estime ce plan à environ deux semaines de charge, et je propose de fixer le mercredi 26 mai 2026 comme deadline globale pour l'ensemble des actions ci-dessus. 

Pour te permettre de t'y consacrer pleinement, je prends deux engagements de mon côté :

•	Concentration exclusive sur Keycloak : sur cette période, je te dégage de toute autre sollicitation côté EasyPRO ; seul le périmètre décrit dans ce mail, et les sujets en cours sur Keycloak sont à traiter. Toute demande qui te parviendrait par ailleurs devra m'être remontée pour arbitrage, afin de préserver ton plan de charge.
•	Ordre de bataille : on démarre par les ateliers de transfert de connaissances avec l'équipe Ops. C'est le levier le plus rapide pour sécuriser la continuité de service, embarquer l'équipe, et alimenter le Wiki au fil des sessions. Dans ce contexte, j’ai planifié une première session à cet effet le 20 mai avec le reste de l’équipe. 

Peux-tu, en retour de ce mail, 

•	Me confirmer la prise en compte de chaque point,
•	Me proposer ou valider les dates de réalisation,
•	Me remonter la liste explicite des points que tu identifies comme bloquants ou nécessitant un arbitrage, pour qu'on puisse les traiter en amont, et non en fin de parcours.

Je te remercie d'avance pour ton implication, et reste à ta disposition pour échanger sur l'un ou l'autre de ces points. On fera vivre ce plan ensemble lors du point hebdo, et on ajustera ce qu'il faudra ajuster en chemin.
