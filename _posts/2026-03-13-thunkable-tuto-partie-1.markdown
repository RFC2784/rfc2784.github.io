---
layout: post
title: "Tuto Thunkable (1/2) : Créer une app mobile connectée au Cloud avec Firebase, sans coder"
image: "/content/images/thunkable-tuto-part1.jpg"
ref: thunkablefirebasep1
lang: fr
date:   2026-03-13 12:00:00 -0400
categories:
  - Tutorials
  - No-Code
tags:
  - Thunkable
  - Firebase
  - Développement Mobile
  - Tutoriel
  - Application
  - No-Code
excerpt_separator: <!--more-->
---
![Tuto Thunkable - App mobile connectée avec Firebase](/content/images/thunkable-tuto-part1.jpg){: style="display: block; margin: 0 auto;"}

Depuis cette année, j'ai l'occasion d'agir comme mentor pour le programme Technovation Montréal. Voir des équipes passer d'une simple idée à un prototype mobile fonctionnel en quelques semaines m'a rappelé une chose essentielle : le *no-code* est un levier d'innovation absolument fantastique. 

Même lorsque l'on ambitionne de développer soi-même des applications mobiles de A à Z avec des frameworks avancés comme React Native, passer par ces plateformes visuelles permet de valider une architecture backend et une logique d'interface en un éclair 🙂

Pour joindre le geste à la parole, je vous propose une nouvelle série de deux tutoriels pour créer une application mobile iOS/Android dynamique et connectée au Cloud, sans écrire une seule ligne de code classique.
<!--more-->

---
***Avant-propos***: *Cet article, augmenté d'améliorations générées avec des IA ([Google Gemini](https://gemini.google.com/)), est mis à disposition au travers de la license* <span xmlns:cc="http://creativecommons.org/ns#" ><i><a href="https://creativecommons.org/licenses/by-nd/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-ND 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nd.svg?ref=chooser-v1" alt=""></a></i></span>

---

# C'est quoi le plan de match ?
L'objectif de cette mini-série est de construire une application mobile en y intégrant progressivement des concepts professionnels. Voici notre feuille de route :
1. **Aujourd'hui :** Créer l'interface d'une application de "Citations Motivantes" (MotivApp) avec [Thunkable](https://thunkable.com/), et la connecter à une vraie base de données Cloud en temps réel avec [Firebase](https://firebase.google.com/).
2. **Partie 2 :** Rendre l'application intelligente en remplaçant notre base de données par des requêtes à l'API de Google Gemini pour générer des citations uniques à la volée 🚀

# 15 minutes chrono pour prototyper notre application !

Notre application comportera deux écrans : un écran d'accueil avec un bouton "Inspire-moi !", et un écran d'affichage qui ira piocher aléatoirement une citation stockée dans le Cloud.

## Étape 1 : Préparer le backend avec Firebase
Firebase est la plateforme de Google qui fournit des services backend prêts à l'emploi. Nous allons utiliser sa **Realtime Database**.

1. Connectez-vous à la [Console Firebase](https://console.firebase.google.com/) avec un compte Google et cliquez sur **Créer un projet** (nommez-le *MotivApp*).
2. Dans le menu de gauche, allez dans **Bases de données et stockage d'objets** > **Realtime Database** et cliquez sur **Créer une base de données**. Sélectionner la région la plus proche de vous, puis choisissez le mode test pour commencer facilement.
3. Dans l'onglet **Données**, nous allons structurer notre base avec des identifiants uniques pour que ce soit robuste. Cliquez sur les trois petits points à droite de l'URL de votre base, choisissez **Importer un fichier JSON**, et importez un fichier contenant ceci :

{% highlight json %}
{
  "citations": {
    "quote_001": {
      "texte": "Le succès, c'est tomber sept fois, se relever huit.",
      "auteur": "Proverbe japonais"
    },
    "quote_002": {
      "texte": "Faites que le rêve dévore votre vie...",
      "auteur": "Antoine de Saint-Exupéry"
    },
    "quote_003": {
      "texte": "L'innovation distingue le leader du suiveur.",
      "auteur": "Steve Jobs"
    }
  }
}
{% endhighlight %}

<img src="/content/images/firebase_rtdb_setup.jpg" alt="Structure JSON dans Firebase" style="display: block; margin: 0 auto;"><br/>

*Gardez l'URL de votre base de données et votre clé d'API web sous la main, nous en aurons besoin dans Thunkable !*

La manière la plus simple de trouver votre clé API et l'URL de votre base est de :

1. Se rendre sur la page Vue d'ensemble du projet dans la console Firebase.
2. Cliquer sur le bouton [+ Ajouter une application]
3. Cliquer sur le bouton </> pour ajouter une application web.
4. Mettez *MotivApp* en pseudo d'application, puis cliquer sur [Enregistrer l'application].
5. Une fenêtre contextuelle s'affichera avec toutes les valeurs dont vous avez besoin.
<img src="/content/images/firebase_api_key.jpg" alt="Affichage de la clé API et de l'URL de la base de données dans la console Firebase" style="display: block; margin: 0 auto;"><br/>

## Étape 2 : Le Design (Interface Visuelle)

Créez un compte gratuit sur [Thunkable](https://x.thunkable.com/signup) et démarrez un nouveau projet:
* Sur l'écran principal, vous trouverez une zone de saisie (prompt box).
* Au bas de cette zone, repérez la mention « Prefer to start from scratch? » puis cliquez sur <u>Create Blank Project</u>.

<img src="/content/images/thunkable_pbox.jpg" alt="Thunkable Prompt Box" style="display: block; margin: 0 auto;"><br/>

* Saisissez *MotivApp* comme nom de projet (Project name), sélectionnez *Health & Fitness*, et assurez-vous que l'option *Use the Drag and Drop Builder* est bien cochée.
* Cliquez sur [Create].

<img src="/content/images/thunkable_app_def.jpg" alt="Thunkable App definition" style="display: block; margin: 0 auto;"><br/>

**Sur le Screen1 (Accueil) :**
1. Glissez un composant **Label** au centre de l'écran avec le texte "Bienvenue sur MotivApp !". Centrez le texte et changer la taille de police dans l'arborescence à gauche.
2. Glissez un composant **Button** en dessous. Changez son texte pour "Inspire-moi !". Renommez ce composant `Btn_Inspire` dans l'arborescence à gauche.

<img src="/content/images/thunkable_screen_1.jpg" alt="Écran 1 de l'application MotivApp" style="display: block; margin: 0 auto;"><br/>

**Sur le Screen2 (Citation) :**
1. Ajoutez un deuxième écran (`Screen2`).
2. Glissez deux **Labels** l'un sous l'autre. Le premier (texte principal) sera renommé `Label_Quote`, le second (plus petit, pour l'auteur) sera `Label_Author`.
3. Glissez un **Button** en dessous avec le texte "Retour" (`Btn_Retour`).
4. **Connectez votre Realtime Database** 
  * Dans votre onglet Thunkable, cliquez sur l'icône d'engrenage (Settings) dans la barre latérale.
  * Faites défiler jusqu'à la section Firebase et collez la valeur « apiKey » dans le champ « Firebase API Key ».
  * Toujours dans la section Firebase, collez l'URL « databaseURL » dans le champ « Database URL ».

<img src="/content/images/thunkable_screen_2.jpg" alt="Écran 2 de l'application MotivApp" style="display: block; margin: 0 auto;"><br/>

## Étape 3 : La Logique (Les Blocs)
Passez de l'onglet **Design** à l'onglet **Blocks**. C'est ici que la magie opère !

**Logique du Screen1 :**
* Prenez le bloc `when Btn_Inspire Clicks do` et glissez à l'intérieur le bloc `Navigate to Screen2`.

**Logique du Screen2 (Extraction des données JSON) :**
Ici, nous devons récupérer notre dictionnaire de citations, en choisir une au hasard, puis isoler son texte et son auteur.

1. Allez dans *Variables* et prenez le bloc `initialize cloud variable name`. Nommez-la `"citations"` (cela doit correspondre *exactement* au nom racine de notre JSON dans Firebase pour que Thunkable fasse la synchronisation automatiquement).
2. Prenez le bloc `when Screen2 Opens do`.
3. À l'intérieur, nous allons d'abord lister nos clés. Créez une variable temporaire `cle_aleatoire`. Assignez-lui le bloc `random item of list`. La liste à fournir sera générée par le bloc `get object properties of` (dans la catégorie *Objects*) appliqué à notre variable `cloud citations`.
4. Maintenant que nous avons une clé au hasard (ex: *quote_002*), créons une variable `citation_choisie`. Assignez-lui la propriété (bloc `get property of object`) correspondant à `cle_aleatoire` extraite de notre variable cloud `citations`.
5. Enfin, mettez à jour vos labels ! Attribuez au `Label_Quote` la propriété `"texte"` de l'objet `citation_choisie`, et au `Label_Author` sa propriété `"auteur"`.
6. Prenez le bloc `when Btn_Retour Clicks do` et glissez à l'intérieur le bloc `Navigate to Screen1`.


<img src="/content/images/thunkable_firebase_blocks.jpg" alt="Blocs logiques Thunkable avec Firebase" style="display: block; margin: 0 auto;"><br/>

## Étape 4 : Tester la bête !
Pas besoin de compiler ! 
* Téléchargez l'application **Thunkable Live** sur votre smartphone (iOS ou Android).
* Connectez-vous avec votre compte. Touchez votre projet et testez : vous devriez voir une nouvelle citation tirée directement de votre base de données Cloud à chaque essai 😉

---

# Conclusion

Et voilà ! Vous avez créé une véritable application mobile connectée à un backend professionnel. L'avantage énorme de cette architecture, c'est que vous pouvez maintenant ajouter, modifier ou supprimer des citations directement depuis la console Firebase, et l'application de vos utilisateurs se mettra à jour instantanément, sans qu'ils n'aient à la retélécharger.

Mais pourquoi s'arrêter en si bon chemin ? Dans **la partie 2 de ce tutoriel**, nous allons remplacer notre base Firebase par l'API de l'intelligence artificielle Gemini. Notre application ne se contentera plus de lire des citations, elle les inventera sur mesure ! Restez à l'écoute.