---
layout: post
title:  "Le principe de diversité comme levier décisionnel lors de la conception d'une solution technologique"
ref: divprinctech
lang: fr
date:   2022-07-25 14:00:00 -0400
categories:
  - IT Network
  - Network Design
tags:
  - Conception de réseau
  - Réseau
  - Design  
---
***Avertissement :** Ce post contient principalement des concepts de haut niveau et des informations de référence pour une meilleure compréhension par un large public. Il n'entre pas dans les détails des sujets techniques abordés.*

# Pourquoi parler de diversité dans un tel contexte ?  
Si vous vivez au Canada ou suivez l'actualité IT, vous avez certainement entendu parler de la panne majeure qu'a connue **Rogers Communications le 8 juillet 2022**.  
Au début de cet événement, j'étais surpris qu'une telle panne ait entraîné une interruption de service pour des applications critiques comme la **plateforme de paiement Interac** ou plusieurs portails web de services gouvernementaux canadiens.

Pour être honnête, je ne peux pas imaginer que les décideurs concernés n'aient pas pleinement appliqué le principe de diversité lors de la conception de la solution.

# Que signifie le principe de diversité ?  
Parmi toutes les leçons apprises en tant que résolveur de problèmes, puis en tant que concepteur de solutions réseau, l'une des plus importantes est **de ne pas sous-estimer l'importance d'appliquer la diversité comme facteur clé pour la redondance et la sécurité dans la conception d'une solution technologique** :

- Plus l'organisation sous-jacente est grande, plus la solution doit être diversifiée.
- Cela doit prévaloir dans chaque décision prise pour concevoir et initier un projet d'intégration.
- Cela peut s'appliquer à plusieurs cas d'utilisation, tels que :
  - Plusieurs fournisseurs pour le même type d'équipement utilisé sur différents périmètres.
  - Plusieurs prestataires pour le même type de service nécessitant une redondance.
  - Plusieurs chemins pour acheminer un flux d'application critique.
  - Etc.

# Le principe de diversité par exemple : la connectivité réseau d'Interac  

*Comme mentionné précédemment, la plateforme de paiement Interac a été impactée par ce que j'appellerai désormais la "panne Rogers". Il est déjà bien connu qu'Interac a choisi Rogers comme principal fournisseur de services pour la connectivité réseau de ses systèmes opérationnels. Alors examinons ensemble comment cette entreprise applique le principe de diversité à la conception de son réseau !*

## Bon exemple : mes observations sur la connectivité Internet d'Interac  

Une telle organisation gère son propre système autonome Internet pour administrer les préfixes IPv4 publics (**AS399405** détenu sous ARIN). Il est donc assez facile de récupérer des informations utiles concernant les objets de route correspondants et les partenaires de peering :

![BGP Info pour AS399405](/content/images/AS399405_info_20220722.jpg){: style="display: block; margin: 0 auto;"}
***Source : [https://bgp.he.net/AS399405#_asinfo](https://bgp.he.net/AS399405#_asinfo)***
{: style="text-align: center"}

- On peut conclure que **le principe de diversité est correctement appliqué au niveau du transit Internet**, car **le peering BGP est établi avec deux FAI différents** :
  - Rogers Communications (**AS812**),
  - Beanfield Technologies (**AS2199**).
- L'annonce de route du préfixe IPv4 /23 appartenant à Interac capturée le jour de la panne Rogers par un utilisateur Twitter prouve que **tout fonctionnait bien depuis le peering Beanfield** :

![Capture d'écran Twitter](/content/images/bgp-interac-tweet.jpg){: style="display: block; margin: 0 auto;"}
***Source : [https://twitter.com/mattools/status/1545440711981645826](https://twitter.com/mattools/status/1545440711981645826)***
{: style="text-align: center"}

- *Intéressant de noter qu'Interac a envisagé d'avoir plus d'un fournisseur de transit Internet après les périodes de confinement liées au COVID-19.*

## Mauvais exemple : mes hypothèses sur la version initiale de la conception de la connectivité réseau d'Interac  

Comme indiqué par Rogers dans sa [réponse à la demande d'information du Conseil de la radiodiffusion et des télécommunications canadiennes concernant la panne Rogers](https://crtc.gc.ca/public/otf/2022/c12_202203868/4215445.docx) :
- "Un codage spécifique a été introduit dans nos routeurs de distribution, ce qui a déclenché la défaillance du réseau IP central de Rogers" lors d'un changement planifié.
- "Le changement de configuration a supprimé un filtre de routage et a permis à toutes les routes possibles vers Internet de passer par les routeurs. En conséquence, les routeurs ont immédiatement commencé à propager un volume anormalement élevé de routes dans tout le réseau central. <ins>Certaines équipements de routage du réseau ont été submergés, <b>ont dépassé leurs niveaux de capacité et n'ont alors pas pu acheminer le trafic</b></ins>, ce qui a entraîné l'arrêt du traitement du trafic par le réseau central commun."
- "Étant donné que la panne concernait le réseau central de Rogers, **tous les services de Rogers, toutes marques confondues [...] ont été impactés**."

Comme mentionné précédemment, nous savons avec certitude que la configuration de connectivité de transit Internet pour les systèmes opérationnels d'Interac était probablement toujours active via un FAI alternatif malgré la panne Rogers.  
**Alors comment est-il possible qu'une panne globale de Rogers entraîne encore l'indisponibilité des paiements Interac ?**

Une explication possible est que **la connectivité réseau privée entre les différents sites d'hébergement des systèmes opérationnels d'Interac reposait uniquement sur le backbone de Rogers Communications**, comme illustré dans le diagramme suivant (basé sur mes hypothèses) :

![Diagramme logique basé sur les hypothèses de Geoffray REAU](/content/images/interac-logical.png){: style="display: block; margin: 0 auto;"}

- Notez qu'un réseau privé entièrement maillé basé sur une connectivité Ethernet point à point peut reposer sur le backbone d'un fournisseur de services. Dans une telle configuration, le fournisseur propose la connectivité de couche 2 via la couche 3 au milieu, comme Ethernet-over-MPLS.
- L'un des scénarios envisageables implique le composant Internet d'une application critique :
  - il pourrait être hébergé sur un site, mais dépend de services privés back-end hébergés sur un autre site.
  - En rompant la connectivité privée inter-sites, l'application devient donc indisponible...
- **Ce scénario a été en quelque sorte confirmé dans** [la déclaration d'Interac sur la panne Rogers](https://www.interac.ca/fr/contenu/nouvelles/declaration-dinterac-au-sujet-de-la-panne-de-services-de-rogers/) :

   *"Chacune de nos plateformes, Interac Débit et Interac Virement, dispose de <ins>réseaux superflus, <b>notamment en termes de diversité des circuits</b></ins>. Ces réseaux bénéficient des garanties de disponibilité 24 heures sur 24 et 7 jours sur 7 de nos fournisseurs, mais <ins>les événements du 8 juillet ont clairement montré que ces garanties ne pouvaient être respectées. <b>Ces réseaux superflus avec diversité de circuits n'auraient pas dû être aussi vulnérables à l'activité de service de soutien de Rogers</b></ins>."*

## Plan de remédiation : appliquer le principe de diversité pour des améliorations  

Toujours selon la déclaration officielle mentionnée ci-dessus, Interac a indiqué que la remédiation de ce maillon faible sera effectuée notamment par "l'ajout d’une plus grande variété de fournisseurs pour renforcer la fiabilité de notre réseau actuel", et en continuant "à travailler avec nos fournisseurs actuels pour renforcer nos engagements" :
- Nous avons ici une confirmation que le principe de diversité doit être appliqué à chaque couche de la conception d'une solution technologique, et **peut également être appliqué lors de son amélioration**.
- Basé sur les fournisseurs de connectivité identifiés plus haut (Rogers et Beanfield), en supposant que la connectivité réseau privée repose sur des circuits Ethernet-Over-MPLS point à point entièrement fournis par Rogers, une évolution possible de la conception réseau est de détourner l'un de ces circuits point à point de Rogers vers Beanfield, comme illustré dans le diagramme ci-dessous :

![Diagramme logique d'évolution basé sur les hypothèses de Geoffray REAU](/content/images/interac-logical-evolution.png){: style="display: block; margin: 0 auto;"}

# Appel à discussion !  
Comme vous pouvez le voir, ce post reflète mes propres opinions et hypothèses sur ce sujet. Je suis ouvert à des points de vue externes pour approfondir !

Alors <b>n'hésitez pas à me contacter sur les réseaux sociaux (liens en pied de page) et <ins>à réagir à ce post avec votre opinion sur le sujet</ins> !</b>