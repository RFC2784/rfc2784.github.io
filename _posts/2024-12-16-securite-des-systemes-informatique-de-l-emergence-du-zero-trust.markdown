---
layout: post
title:  "Sécurité des systèmes informatiques : de l’émergence du Zero Trust"
date:   2024-12-16 14:00:00 -0400
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
# Niveaux de confiance et maitrises du risque informatique #
Inspirée du domaine militaire, les premières itérations de gestion des zones de sécurité reposent sur une organisation claire et structurée des flux. On distingue principalement trois types de zones :
<div align="center"><img src ="/content/images/sec_zones.png" alt="Zones de sécurité réseau" width=75%></div>

**Les zones de confiance (Trust)**

Ces zones regroupent tout ce dont l’origine est connue et maîtrisée, comme les réseaux privés des utilisateurs ou les serveurs internes.


**Les zones de non-confiance (Untrust)**

Cette catégorie inclut tout ce qui n’est pas sous contrôle, comme Internet, où les risques sont imprévisibles.


**Les zones démilitarisées (DMZ)**

Ces zones accueillent les services qui, bien que gérés depuis une zone de confiance, doivent être accessibles depuis des zones de non-confiance.

# Règles de Circulation entre zones de confiance #
Les flux circulant au sein d’une même zone ne rencontrent aucune restriction. Cependant, pour assurer la sécurité des systèmes, la communication entre ces zones passe par des contrôles stricts, respectant les principes de base suivants
<div align="center"><img src ="/content/images/sec_zones_2.png" alt="Règles de Circulation entre zones de confiance" width=75%></div>

- On laisse passer les flux initiés depuis une zone de confiance vers les zones démilitarisées et celles de non-confiance. Cependant on va bloquer systématiquement les flux initiés en dehors de la zone de confiance pour éviter toute compromission.
- La zone démilitarisée est par définition plus exposée au risque, et de ce fait est accessible à la fois depuis les zones de confiances et celles de non-confiance.

# Évolution des cybermenaces #

Dans un monde où les interactions humaines et commerciales dépendent grandement du monde numérique, la robustesse des contrôles de sécurité des réseaux informatiques est mise à mal en permanence, mettant à mal les principes de base de circulation des flux.
En moins d’un demi-siècle, les individus les moins scrupuleux se sont armés d’outils divers et variés pour porter leurs menaces à un niveau supérieur.

## Les logiciels malveillants ##
Conçus pour infiltrer, endommager ou perturber les systèmes informatiques. On en retrouve de plusieurs types dont:
- **Les chevaux de Troie**, programmes malveillants distribués sous la forme de logiciels légitimes pour tromper les utilisateurs,
- **Les virus**, qui s’attachent à des fichiers et se propagent lorsque le fichier hôte est ouvert/exécuté,
- **Les vers**, qui s’exécutent et se propagent sans intervention utilisateur,
- **Les rançongiciels**, qui une fois infiltérs dans les systèmes vont chiffrer l’ensemble des données pour permettre aux attaquant d’exiger un paiement contre leur déchiffrement.
<div align="center"><img src ="/content/images/malware_types.png" alt="Types de logiciels malveillants" width=75%></div>

## L’hameçonnage ##
Cette technique consiste à tromper les utilisateurs pour qu'ils divulguent des informations sensibles, telles que des mots de passe ou des numéros de carte de crédit, en se faisant passer pour une entité de confiance. Les variantes les plus connues sont :
- **Le phishing**, par courriel, qui vise à tromper les utilisateurs pour leur faire cliquer sur des liens frauduleux (faux sites internet, téléchargement de logiciel malveillant,…)
- **Le smishing**, la variante SMS du phising,
- **Le vishing**, par téléphone, qui vise à tromper les personnes pour leur faire révéler verbalement des informations sensibles.
<div align="center"><img src ="/content/images/phish_techs.png" alt="Techniques communes menant à la divulgation d'informations" width=75%></div>

## L’exploitation des failles de sécurité ##
Bien que les attaques par force brute soient toujours d’actualité, celles-ci sont de moins en moins efficaces au fur et à mesure de l’évolution des systèmes de sécurité. 

En revanche, les cybercriminels se tournent vers des techniques plus sophistiquées pour exploiter les vulnérabilités des systèmes. Les failles de sécurité peuvent résider dans les logiciels, les systèmes d'exploitation, ou même dans les configurations réseau. Une fois qu'une faille est découverte, elle peut être exploitée pour exécuter du code malveillant, accéder à des données sensibles, ou perturber les opérations normales du système. Les attaques ciblées, telles que les exploits zero-day, sont particulièrement dangereuses car elles exploitent des vulnérabilités inconnues des développeurs et des utilisateurs, laissant peu de temps pour réagir et corriger les failles.
<div align="center"><img src ="/content/images/understand_vuln.png" alt="Comprendre les vulnérabilités des systèmes et les cybermenaces" width=75%></div>

## Les attaques par déni de service ##
Vous savez, quand le site internet marchand que vous consultez affiche une erreur 503 durant le Vendredi Fou ? C’est un déni de service provoqué par un surcroit de traffic, car vous n’êtes pas seul(e) à vouloir profiter des aubaines ;-)

Cet effet de bord indésirable a fait des émules auprès des cyber vilains, qui ont trouvé le moyen de coordonner des attaques de forte amplitude afin de rendre inopérants des services et réseaux entiers en les surchargeant de requêtes inutiles.
<div align="center"><img src ="/content/images/DDoS.png" alt="Attaques par déni de service" width=75%></div>
