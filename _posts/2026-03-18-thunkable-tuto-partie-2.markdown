---
layout: post
title: "Tuto Thunkable (2/2) : Rendre son application mobile intelligente avec l'API Gemini"
image: "/content/images/thunkable-gemini-tuto.jpg"
ref: thunkablegeminip2
lang: fr
date:   2026-03-18 06:00:00 -0400
categories:
  - Tutorials
  - No-Code
  - Artificial Intelligence
tags:
  - Thunkable
  - Gemini
  - API
  - Développement Mobile
  - Tutoriel
  - No-Code
  - Prompt Engineering
excerpt_separator:
excerpt_separator: <!--more-->
---
![Tuto Thunkable - Intégrer Gemini API](/content/images/thunkable-tuto-part2.jpg){: style="display: block; margin: 0 auto;"}

Dans **[la première partie de ce tutoriel](/2026/03/13/thunkable-tuto-part-1.html)**, nous avons connecté notre prototype mobile à une base de données Firebase. C'est une excellente pratique, particulièrement pertinente si vous envisagez de basculer plus tard sur du développement avec des frameworks comme React Native. Cependant, cette approche nous rend dépendants d'une base de données pré-remplie.

Aujourd'hui, on passe à la vitesse supérieure. Après 20 ans dans l'industrie des TI, je suis toujours fasciné par la façon dont on peut désormais intégrer de l'intelligence artificielle dans une application en quelques clics. Nous allons remplacer notre base statique par l'API de Google Gemini pour générer des citations 100% sur mesure, à la volée !
<!--more-->

---
***Avant-propos***: *Cet article, augmenté d'améliorations générées avec des IA ([Google Gemini](https://gemini.google.com/)), est mis à disposition au travers de la license* <span xmlns:cc="http://creativecommons.org/ns#" ><i><a href="https://creativecommons.org/licenses/by-nd/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-ND 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nd.svg?ref=chooser-v1" alt=""></a></i></span>

---

# Étape 1 : Obtenir les clés du cerveau (Google AI Studio)
Pour parler à Gemini depuis notre application, il nous faut un laissez-passer : une clé d'API.
* Rendez-vous sur [Google AI Studio](https://aistudio.google.com/).
* Connectez-vous avec votre compte Google.
* Dans le menu de gauche, cliquez sur **Get API key** puis sur le bouton **Create API key**.

<img src="/content/images/gemini_api_keygen.jpg" alt="Générer une clé API sur Google AI Studio" style="display: block; margin: 0 auto;"><br/>

* Une fois la clé d'API créée, cliquez dessus pour l'afficher.
* Copiez cette longue suite de caractères et gardez-la précieusement (ne la partagez jamais publiquement).
<img src="/content/images/gemini_api_key.jpg" alt="Afficher une clé API sur Google AI Studio" style="display: block; margin: 0 auto;"><br/>

# Étape 2 : Adapter le Design de MotivApp
Reprenons notre projet Thunkable là où nous l'avons laissé. Nous allons ajouter un peu d'interactivité.
* **Sur le Screen1 (Accueil) :** Ajoutez un composant **Text Input** juste au-dessus du bouton "Inspire-moi !". Modifiez son paramètre *Hint* (indice) pour afficher : "Entrez un thème (ex: Le sport, Le code...)". Renommez ce composant `Input_Theme`.
<img src="/content/images/thunkable_gemini_design.jpg" alt="Design mis à jour avec le champ texte" style="display: block; margin: 0 auto;"><br/>

# Étape 3 : Le Prompt Engineering avec RISEN
C'est le cœur du réacteur. Pour éviter que l'IA ne divague, nous allons structurer notre requête (prompt) avec le framework professionnel **RISEN**. Voici comment nous allons contraindre le modèle `gemini-2.5-flash` :
* **R (Role) :** Agis comme un coach de vie expert en motivation.
* **I (Instruction) :** Écris une citation motivante inédite basée sur le thème suivant : [Thème tapé par l'utilisateur].
* **S (Steps) :** 1. Analyse le thème. 2. Trouve un angle inspirant. 3. Formule la citation. 4. Attribue-la à un auteur fictif ou réel.
* **E (End Goal) :** Le lecteur doit ressentir une envie immédiate de passer à l'action.
* **N (Narrowing) :** La réponse DOIT suivre ce format strict : 'Citation - Auteur'. Ne dépasse pas 20 mots. N'inclus aucune salutation.

Voici exactement le texte final que notre application va assembler, en remplaçant la variable de fin par le thème choisi par l'utilisateur :

{% highlight text %}
Agis comme un coach de vie expert en motivation. 
Écris une citation motivante inédite basée sur le thème suivant : [THÈME DE L'UTILISATEUR]. 
1. Analyse le thème. 2. Trouve un angle inspirant. 3. Formule la citation. 4. Attribue-la à un auteur fictif ou réel. 
Le lecteur doit ressentir une envie immédiate de passer à l'action. 
La réponse DOIT suivre ce format strict : 'Citation - Auteur'. Ne dépasse pas 20 mots. N'inclus aucune salutation.
{% endhighlight %}

# Étape 4 : La Logique et les Blocs

## Sur le Screen1
### Aperçu des blocs
<img src="/content/images/thunkable_gemini_blocks_part1.jpg" alt="Aperçu des blocs du Screen1" style="display: block; margin: 0 auto;"><br/>

### Séquence des blocs

**Initialisation**
* À l'ouverture du `Screen1`, videz le champ `Input_Theme`.
* Lors du clic sur `Btn_Inspire`, nous devons vérifier que le texte `Text` du composant `Input_Theme` n'est pas vide avant d'exécuter les étapes suivantes.

**Construire la requête API :**
* Créez un composant **Web API** : dans la liste de gauche, déroulez "Advanced", puis cliquez sur le [+] à droite de "Web APIs". C'est lui qui remplacera Firebase pour dialoguer avec les serveurs de Google.

  * Renommez-le en `Gemini`.
  * Configurez l'URL de l'API : définissez le champ "URL" à `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent`.
  * Configurez votre clé d'API : 
    * Définissez le champ "Property" à `key`.
    * Collez votre clé d'API dans le champ "Value".
    * Cliquez sur [Add].
  * Configurez l'en-tête (header) :
    * Définissez le champ "Property" à `Content-Type`.
    * Tapez `application/json` dans le champ "Value".
    * Cliquez sur [Add].
  * Cliquez sur [Done].

<img src="/content/images/thunkable_webapi_config.jpg" alt="Configuration de la WebAPI" style="display: block; margin: 0 auto;"><br/>

L'API de Gemini est très stricte sur le format des données qu'elle reçoit. Elle attend un objet JSON contenant une liste `contents`, qui contient elle-même une liste `parts`, qui contient enfin l'attribut `text` avec notre prompt. Dans Thunkable, la façon la plus simple de construire ce corps de requête (le *Body*) est d'utiliser un bloc de texte.

1. D'abord, créez une variable `full_prompt` et utilisez un bloc `join` pour y coller le gros bloc de texte RISEN (vu à l'étape 3) avec le texte `Text` du composant `Input_Theme`.
2. Prenez un autre bloc de texte avancé `join` (qui permet de coller plusieurs morceaux de texte ensemble).
3. Dans la première case, collez exactement ce début de code JSON : `{"contents": [{"parts": [{"text": "`
4. Dans la deuxième case, glissez votre variable `full_prompt`.
5. Dans la troisième case, fermez le code JSON avec : `"}]}]}`
6. Assignez le tout au bloc `set Web_API's Body to`.

<img src="/content/images/thunkable_prompt_building.jpg" alt="Construction du prompt" style="display: block; margin: 0 auto;">

**Extraire la réponse JSON :**
* Lancez l'appel avec le bloc `call Web_API's Post`.
* L'API nous répond avec un gros bloc de données textuelles complexes.
* Dans la section verte `then do` du bloc Post, utilisez le bloc `get object from JSON` pour transformer la réponse (`response`) en une variable nommée `citation`.
* Utilisez les blocs `get property` pour creuser dans cet objet. Le chemin exact pour extraire le texte brut de Gemini est : `candidates[1]` -> `content` -> `parts[1]` -> `text`.
* **Séparer la citation de l'auteur :** Puisque nous avons forcé Gemini (avec notre N de RISEN) à répondre au format "Citation - Auteur", nous allons couper ce texte en deux !
  1. Créez une variable `response_list`.
  2. Assignez-lui le bloc `make list from text` (dans *Lists*), avec le texte extrait de Gemini, et tapez `" - "` dans la case `delimiter`.
  3. Maintenant que nous avons récupéré la citation, nous pouvons naviguer vers le Screen2.
  
<img src="/content/images/thunkable_gemini_json_extract.jpg" alt="Appel Web API et parsing JSON" style="display: block; margin: 0 auto;"><br/>

## Sur le Screen2
  1. Mettez à jour le `Label_Quote` en allant chercher le premier élément de cette liste (bloc `in list get # 1`).
  2. Mettez à jour le `Label_Author` en allant chercher le deuxième élément (bloc `in list get # 2`).

<img src="/content/images/thunkable_gemini_blocks_part2.jpg" alt="Affichage de la citation" style="display: block; margin: 0 auto;"><br/>

# Étape 5 : Essayez !
Le moment de vérité est arrivé.
* Lancez l'application via **Thunkable Live** sur votre téléphone (ou via l'aperçu Web de la plateforme).
* Sur le premier écran, tapez un thème qui vous inspire dans le champ de texte (par exemple : "La gestion du stress", "Le dépassement de soi" ou "L'apprentissage de la guitare").
* Appuyez sur **Inspire-moi !**.
* Après une brève seconde (le temps que le modèle de Google génère sa réponse), vous basculez automatiquement sur le deuxième écran.
* Et voilà ! Une citation unique, parfaitement formatée et taillée sur mesure pour votre thème s'affiche sous vos yeux. Vous n'avez plus qu'à cliquer sur "Retour" pour tester avec une nouvelle idée !

# Conclusion

Félicitations ! Vous venez de créer une application mobile capable de générer du contenu à l'infini grâce à l'intelligence artificielle. Les limites du *no-code* sont repoussées tous les jours, et c'est le moment idéal pour expérimenter. 

N'hésitez pas à modifier le prompt RISEN pour créer un générateur de recettes de cuisine, un créateur de poèmes ou même un quiz interactif. À vous de jouer !