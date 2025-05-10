---
layout: post
title:  "Sécurité des systèmes informatiques : de l’émergence du Zero Trust"
ref: itsecztrust
lang: fr
date:   2024-12-16 11:45:00 -0400
categories:
  - IT Network
  - Network Design
  - IT Security
tags:
  - Network Design
  - IT Security
  - Network
  - Security
  - Design  
---
🔒*Face à l'évolution des cybermenaces qui mettent à terre l'approche classique des zones de sécurité, découvrez comment le modèle Zero Trust peut transformer votre infrastructure et protéger vos données sensibles, même contre les hackers les plus rusés.*<br/><br/>🕵️‍♂️*Découvrez également comment l'approche Zero Trust aurait pu éviter le pire Honda Civic de Kévin😅*

---
***Avant-propos**: Cet article, augmenté pour moitié d'améliorations générées avec des IA ([Napkin](https://www.napkin.ia) , [Microsoft Copilot](https://copilot.microsoft.com/) ), est mis à disposition au travers de la license* <span xmlns:cc="http://creativecommons.org/ns#" ><i><a href="https://creativecommons.org/licenses/by-nd/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-ND 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nd.svg?ref=chooser-v1" alt=""></a></i></span>

---
# Niveaux de confiance et maitrises du risque informatique
Inspirée du domaine militaire, les premières itérations de gestion des zones de sécurité reposent sur une organisation claire et structurée des flux. On distingue principalement trois types de zones :

![Zones de sécurité réseau](/content/images/sec_zones.jpg){: style="display: block; margin: 0 auto;"}

## Les zones de confiance (Trust)
Ces zones regroupent tout ce dont l’origine est connue et maîtrisée, comme les réseaux privés des utilisateurs ou les serveurs internes.

## Les zones de non-confiance (Untrust)
Cette catégorie inclut tout ce qui n’est pas sous contrôle, comme Internet, où les risques sont imprévisibles.

## Les zones démilitarisées (DMZ)
Ces zones accueillent les services qui, bien que gérés depuis une zone de confiance, doivent être accessibles depuis des zones de non-confiance.

# Règles de Circulation entre zones de confiance
Les flux circulant au sein d’une même zone ne rencontrent aucune restriction. Cependant, pour assurer la sécurité des systèmes, la communication entre ces zones passe par des contrôles stricts, respectant les principes de base suivants

![Règles de Circulation entre zones de confiance](/content/images/sec_zones_2.jpg){: style="display: block; margin: 0 auto;"}
- On laisse passer les flux initiés depuis une zone de confiance vers les zones démilitarisées et celles de non-confiance. Cependant on va bloquer systématiquement les flux initiés en dehors de la zone de confiance pour éviter toute compromission.
- La zone démilitarisée est par définition plus exposée au risque, et de ce fait est accessible à la fois depuis les zones de confiances et celles de non-confiance.

# Évolution des cybermenaces
Dans un monde où les interactions humaines et commerciales dépendent grandement du monde numérique, la robustesse des contrôles de sécurité des réseaux informatiques est mise à mal en permanence, mettant à mal les principes de base de circulation des flux.
En moins d’un demi-siècle, les individus les moins scrupuleux se sont armés d’outils divers et variés pour porter leurs menaces à un niveau supérieur.

## Les logiciels malveillants
Conçus pour infiltrer, endommager ou perturber les systèmes informatiques. On en retrouve de plusieurs types dont:
- **Les chevaux de Troie**, programmes malveillants distribués sous la forme de logiciels légitimes pour tromper les utilisateurs,
- **Les virus**, qui s’attachent à des fichiers et se propagent lorsque le fichier hôte est ouvert/exécuté,
- **Les vers**, qui s’exécutent et se propagent sans intervention utilisateur,
- **Les rançongiciels**, qui une fois infiltérs dans les systèmes vont chiffrer l’ensemble des données pour permettre aux attaquant d’exiger un paiement contre leur déchiffrement.

![Types de logiciels malveillants](/content/images/malware_types.jpg){: style="display: block; margin: 0 auto;"}

## L’hameçonnage
Cette technique consiste à tromper les utilisateurs pour qu'ils divulguent des informations sensibles, telles que des mots de passe ou des numéros de carte de crédit, en se faisant passer pour une entité de confiance. Les variantes les plus connues sont :
- **Le phishing**, par courriel, qui vise à tromper les utilisateurs pour leur faire cliquer sur des liens frauduleux (faux sites internet, téléchargement de logiciel malveillant,…)
- **Le smishing**, la variante SMS du phising,
- **Le vishing**, par téléphone, qui vise à tromper les personnes pour leur faire révéler verbalement des informations sensibles.

![Techniques communes menant à la divulgation d'informations](/content/images/phish_techs.jpg){: style="display: block; margin: 0 auto;"}

## L’exploitation des failles de sécurité
Bien que les attaques par force brute soient toujours d’actualité, celles-ci sont de moins en moins efficaces au fur et à mesure de l’évolution des systèmes de sécurité. 

En revanche, les cybercriminels se tournent vers des techniques plus sophistiquées pour exploiter les vulnérabilités des systèmes. Les failles de sécurité peuvent résider dans les logiciels, les systèmes d'exploitation, ou même dans les configurations réseau. Une fois qu'une faille est découverte, elle peut être exploitée pour exécuter du code malveillant, accéder à des données sensibles, ou perturber les opérations normales du système. Les attaques ciblées, telles que les exploits zero-day, sont particulièrement dangereuses car elles exploitent des vulnérabilités inconnues des développeurs et des utilisateurs, laissant peu de temps pour réagir et corriger les failles.

![Comprendre les vulnérabilités des systèmes et les cybermenaces](/content/images/understand_vuln.jpg){: style="display: block; margin: 0 auto;"}

## Les attaques par déni de service
Vous savez, quand le site internet marchand que vous consultez affiche une erreur 503 durant le Vendredi Fou ? C’est un déni de service provoqué par un surcroit de traffic, car vous n’êtes pas seul(e) à vouloir profiter des aubaines ;-)

Cet effet de bord indésirable a fait des émules auprès des cyber vilains, qui ont trouvé le moyen de coordonner des attaques de forte amplitude afin de rendre inopérants des services et réseaux entiers en les surchargeant de requêtes inutiles.

![Attaques par déni de service](/content/images/DDoS.jpg){: style="display: block; margin: 0 auto;"}

# Modèle Zero Trust : "Y’a pu personne pantoute à qui tu peux faire confiance asteur..."
En examinant les principaux vecteurs d'attaque, c'est rendu évident que les cybermenaces cherchent à perturber les schémas normaux de circulation des données dans un système. Autrement dit, les attaquants tentent de manipuler ou de détourner les flux de données habituels pour accéder à des informations confidentielles et compromettre la sécurité du système ciblé.

Le concept de **Zero Trust Network Access** (confiance zéro sur les accès réseau) a émergé comme une remédiation effective à ce décloisonnement de fait.
## C'est-tu quoi c't'affaire-là, le Zero Trust ?

Contrairement aux modèles traditionnels de sécurité qui se basent sur des périmètres de confiance, le modèle Zero Trust part du principe que toute entité, qu'elle soit à l'intérieur ou à l'extérieur du réseau, ne doit pas pantoute être automatiquement digne de confiance.

![Cadre de sécurité Zero Trust](/content/images/0trust_framework.jpg){: style="display: block; margin: 0 auto;"}

Le Zero Trust repose sur plusieurs principes clés :
- **Vérification continue** : Chaque tentative d'accès aux ressources doit être authentifiée et autorisée, indépendamment de l'origine de la demande.
- **Moindre privilège** : Les utilisateurs et les systèmes ne reçoivent que les permissions nécessaires pour accomplir leurs tâches, minimisant ainsi les risques en cas de compromission.
- **Micro-segmentation** : Le réseau est divisé en segments plus petits et sécurisés, limitant la propagation des menaces en cas de brèche.
- **Surveillance et analyse** : Une surveillance constante et une analyse des comportements permettent de détecter et de répondre rapidement aux activités suspectes.

## Ça prend quoi pour mettre en place du Zero Trust ?
![Mise en œuvre d'une stratégie Zero Trust](/content/images/0trust_strat.jpg){: style="display: block; margin: 0 auto;"}

La mise en œuvre d'une stratégie Zero Trust nécessite une approche globale et intégrée. Voici quelques étapes essentielles pour adopter ce modèle :
1. **Évaluation des actifs et des risques** : Identifier les actifs critiques et évaluer les risques associés à leur accès et à leur utilisation.
2. **Renforcement de l'authentification** : Mettre en place des mécanismes d'authentification multi-facteurs (MFA) pour renforcer la vérification des identités.
3. **Contrôle des accès** : Utiliser des politiques de contrôle d'accès basées sur des attributs (ABAC, ou RBAC en anglais) pour gérer les permissions de manière dynamique et contextuelle.
4. **Segmentation du réseau** : Implémenter la micro-segmentation pour isoler les différentes parties du réseau et limiter les mouvements latéraux des attaquants.
5. **Surveillance continue** : Déployer des outils de surveillance et d'analyse pour détecter les anomalies et réagir rapidement aux incidents de sécurité.

## C'est bin beau c'te patente de Zero Trust, mais c'est-tu avantageux ?
![Avantages de la mise en œuvre du modèle Zero Trust](/content/images/0trust_perks.jpg){: style="display: block; margin: 0 auto;"}

Bin là oui :) Principalement ça va apporter les avantages suivants
- **Réduction des surfaces d'attaque** : En limitant les accès pis en segmentant le réseau, y'a moins de chances pour les hackers de trouver une brèche.
- **Amélioration de la résilience** : Les systèmes deviennent plus toughs face aux attaques, parce que les brèches potentielles sont contenues pis isolées.
- **Conformité réglementaire** : Le Zero Trust aide à respecter les lois pis les règlements en matière de protection des données et de sécurité.
- **Flexibilité pis adaptabilité** : Le modèle s'adapte aux nouveaux environnements de travail, comme le télétravail ou les infrastructures cloud.

## Ouin, c'est rendu dispendieux de moderniser... Et si je laissais ça comme avant?
Malgré des progrès significatifs dans les mentalités depuis une dizaine d'année, j'entends encore parfois du "il n'est jamais rien arrivé avec le système actuel, et vous me proposer du top notch qui va coûter so fucking cher... Pourquoi je transformerai quoi que ce soit ?".


C'est un peu comme l'histoire de Kévin qui, après avoir économisé durant plusieurs années, vient de s'acheter le char de ses rêves, mais il n'a pas de parking couvert ni de garage pour le parker, et pas le budget pour financer une assurance tous risques. Il s'en câlisse, il habite dans une banlieue sans histoire, y'a jamais rien eu qui s'est passé. Et pis y'a le chien de la famille, Pitou, qui veille sur la maison depuis que Kevin a appris à marcher, c'est chill!

Bien sûr, tu t'en doutes, toute une histoire qui se passe:
- Des voleurs se sont introduits dans le jardin, ont profité que Pitou était en train de dormir pour piller et saccager le précieux véhicule, ne laissant qu'une épave bonne à scrapper.
- Pire encore, ils ont volé le backpack de Kévin qui était dedans, et qui contenait ce que Kévin chérissait encore plus que son char: sa collection de cartes Pokémon!
- Dès le lendemain, les voleurs contactent notre jeune ami pour lui soutirer une rançon d'un montant si indécent qu'il finira par laisser passer cette seule chance de revoir un jour son MewTwo shiny état mint...

L'assurance ne couvrant rien, mais bien décidé à retrouver ses plaisirs d'antan, Kévin va travailler dur et économiser longtemps pour enfin pouvoir se payer à nouveau son Honda Civic et se refaire une collection à faire palir toute la gang au centre d’achat. Par contre on ne l'y reprendra plus :
- Il a fait contruire un garage digne des plus imprenables des chateaux forts, avec trois niveaux de serrures multi-points dont lui seul sait comment des débarrer, et un système de surveillance 24h premium.
- Son classeur de cartes est désormais en sûreté dans un coffre à la caisse Desjardins du village voisin.
- Tout ça est définitivement assuré tout risque!

# En conclusion
*L'histoire de Kevin illustre parfaitement pourquoi il est crucial de moderniser la sécurité des systèmes informatiques, même si cela peut sembler coûteux et inutile à première vue. Voici la conclusion qu'on peut en tirer.*

Kevin pensait que son quartier tranquille et son chien fidèle suffisaient à protéger son précieux char et sa collection de cartes Pokémon. Mais quand les voleurs ont frappé, il a perdu bien plus que ce qu'il avait économisé pendant des années. C'est seulement après cette expérience douloureuse qu'il a compris l'importance d'investir dans des mesures de sécurité robustes, comme un garage sécurisé et un système de surveillance.

De la même manière, les entreprises peuvent penser que leurs systèmes actuels sont suffisants parce qu'ils n'ont jamais été attaqués. Mais les cybermenaces évoluent constamment, et ce qui était sûr hier ne l'est plus aujourd'hui. **Attendre qu'une attaque se produise pour agir peut coûter bien plus cher que de moderniser la sécurité dès maintenant**. En investissant dans des solutions de sécurité avancées comme le Zero Trust, les entreprises peuvent prévenir les pertes catastrophiques et protéger leurs actifs les plus précieux, tout comme Kevin a finalement protégé son nouveau char et sa collection de cartes Pokémon.

![Investir dans la sécurité prévient les pertes](/content/images/0trust_invest.jpg){: style="display: block; margin: 0 auto;"}