---
layout: post
title: "10-mn tuto : installer un LLM local sur Windows avec Ollama"
image: "/content/images/ollama-tuto.jpg"
ref: localllmtuto
lang: fr
date:   2025-07-11 00:30:00 -0400
categories:
  - Artificial Intelligence
  - Tutorials
tags:
  - Intelligence Artificielle
  - IA
  - Grand Modèle de Langage
  - LLM
  - Tutoriel
  - Ollama
excerpt_separator: <!--more-->
---
![10-mn tuto - LLM local sur Windows avec Ollama](/content/images/ollama-tuto.jpg){: style="display: block; margin: 0 auto;"}

Dans le post précédent, j’ai proposé des angles d’approche pour permettre au plus grand nombre d’appréhender les dernières innovations en termes d’IA. Maintenant, il est somme toute logique que je donne le bon exemple sous l’angle de la vulgarisation techno 🙂

Comme le suggère le titre du post, je vous propose un tutoriel rapide, simple et efficace pour installer votre propre instance de grand modèle de langage, ou LLM, localement sur un PC sous Windows en utilisant [Ollama](https://ollama.com/).
<!--more-->

---
***Avant-propos***: *Cet article, augmenté d'améliorations générées avec des IA ([Napkin](https://www.napkin.ia) , [Google AI](https://ai.google/), [Perplexity](https://www.perplexity.ai/)), est mis à disposition au travers de la license* <span xmlns:cc="http://creativecommons.org/ns#" ><i><a href="https://creativecommons.org/licenses/by-nd/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-ND 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nd.svg?ref=chooser-v1" alt=""></a></i></span>

---
# C'est quoi un LLM ?
Très bonne question, merci de l'avoir posée 😀
Un LLM (Large Language Model) est un modèle d'intelligence artificielle entraîné sur d'énormes quantités de données textuelles pour comprendre et générer du langage humain, apprenant ainsi à prédire les mots suivants dans une séquence.

Parmi les modèles les plus connus du grand public :

* Disponibles au travers de [ChatGPT](https://chatgpt.com/), les modèles GPT de OpenAI ([GPT-4o](https://openai.com/fr-FR/index/gpt-4o-system-card/), [o3 et o4-mini](https://openai.com/index/introducing-o3-and-o4-mini/)).
* [Grok](https://x.ai/grok), par xAI, qui est pleinement intégré à X.
* [Google Gemini](https://deepmind.google/models/gemini/), mis en avant au travers des outils Google tels que Gmail,Google Drive, Google Docs, etc…
* Les modèles [LLama](https://www.llama.com/) de Meta, qui sont pleinement intégrés à Facebook, Instagram et WhatsApp, sont rendus Open Source depuis la sortie de LLama 2 en juillet 2023 ([Dépôt GitHub](https://github.com/meta-llama/llama)).

À partir de cette capacité fondamentale, les applications de ces modèles IA sont nombreuses :
<picture>
  <source srcset="/content/images/llm_apps_d.svg" media="(prefers-color-scheme: dark)">
  <source srcset="/content/images/llm_apps.svg" media="(prefers-color-scheme: light)">
  <img src="/content/images/llm_apps.svg" alt="Applications polyvalentes des LLM" style="display: block; margin: 0 auto;">
</picture>

* **Chatbots avancés**
  * support client automatisé,
  * FAQ interactive.
* **Traitement de données à grand volume**
  * Résumés,
  * Extraction, raffinage puis classification.
* **Traduction automatique**
  * Pour mon article précédent, j’étais bien content d’avoir accès à des LLM pour traduire des articles universitaires chinois \!
* **Génération de code informatique**,
  * Beaucoup utilisé pour l’aide au codage, j’utilise [GitHub Copilot](https://github.com/features/copilot) pour harmoniser [le code Markdown de ce blog](https://github.com/RFC2784/rfc2784.github.io/blob/main/_posts/) \!
* **Simulation de raisonnement**
  * Les dernières évolutions dans ce domaine sont vraiment intéressantes. Outre le modèle [DeepSeek-R1](https://github.com/deepseek-ai/DeepSeek-R1), j’expérimente beaucoup avec l’option de [Recherche Profonde de Gemini Pro 2.5](https://support.google.com/gemini/answer/15719111?hl=fr&sjid=8249538743889943279-NA).

# 10 minutes chrono pour installer un LLM sur un PC Windows, c’est possible !

## Vraiment ?

OK, c’est sûr que vous n’allez pas faire tourner des inférences avec des centaines de milliards de paramètres sur votre laptop, et encore moins des modèles commerciaux, mais pas de souci pour faire tourner des LLM plus modestes mais suffisamment performants pour s'amuser \!

## C’est quoi l’intérêt d’un LLM local ?

Personnellement, je n’y vois que des avantages
<picture>
  <source srcset="/content/images/llm_perks_d.svg" media="(prefers-color-scheme: dark)">
  <source srcset="/content/images/llm_perks.svg" media="(prefers-color-scheme: light)">
  <img src="/content/images/llm_perks.svg" alt="Les avantages d'un LLM local" style="display: block; margin: 0 auto;">
</picture>

* Accès à une **multitude de LLM Open Source récents**, y compris des modèles de raisonnement comme [DeepSeek-R1](https://github.com/deepseek-ai/DeepSeek-R1) ou [Qwen 3](https://github.com/QwenLM/Qwen3).
* **Confidentialité garantie** : une fois le modèle sur le PC, aucune donnée ne quitte l’ordinateur, protégeant ainsi les données échangées avec le modèle (textes, images).
* **Pas d'abonnement** pour les fonctionnalités disponibles.
* **Possibilité de redonner un second souffle à des PC un peu moins récents**. Pour exemple, j’ai reconditionné un vieux laptop avec un Core-I5 et 16 GB de RAM en serveur perso avec une distri Ubuntu, et je fais tourner un petit modèle dessus \!

## C’est quoi les composants ?

### Ollama

Disponible sur Linux, MacOs, WIndows et Docker, cette plateforme logicielle Open Source permet la gestion et l’exécution locale de modèles de langage.

* Site web : [https://ollama.com](https://ollama.com)
* Discord : [https://discord.com/invite/ollama](https://discord.com/invite/ollama)
* Liste des modèles disponibles : [https://ollama.com/library](https://ollama.com/library)
  * Il est possible de s'inscrire [ici](https://ollama.com/signup) pour publier et partager ses propres modèles.
* Dépot GitHub : [https://github.com/ollama/ollama](https://github.com/ollama/ollama)

### Hollama - Client Webchat pour Ollama

Disponible également sur Linux, MacOs, WIndows et Docker, cette application est un client Webchat compatible Ollama et OpenAI.

* Dépot GitHub : [https://github.com/fmaclen/hollama](https://github.com/fmaclen/hollama)
* Live demo : [https://hollama.fernando.is/](https://hollama.fernando.is/)

J’ai choisi Hollama pour sa simplicité d’utilisation, notamment pour charger de nouveaux modèles directement au travers de l’interface graphique.

### Prérequis système

Pas besoin d’une carte graphique dédiée ou d’un PC Copilot \+, la config suivante vous permet de faire vos premières armes \!

| Composant | Configuration minimale |
| :---- | :---- |
| Système d’exploitation | Microsoft Windows 10 ou Windows 11, édition Famille ou Professionnel, maintenu à jour avec les derniers correctifs |
| CPU | 4 coeurs, Intel/AMD, x86-64 |
| RAM | 8GB |
| Stockage | 10GB disponibles |
| Connectivité Internet | Requise pour l’installation des composants et le téléchargement des modèles de langage. |

J’ai validé ce tutoriel sur des machines virtuelles qui utilisent cette configuration minimale, vous pouvez y aller les yeux fermés 😉

### Modèle de langage utilisé dans le tutoriel - gemma3:1b-it-qat
**gemma3:1b-it-qat** désigne un version légère et efficace du modèle Open Source [Gemma 3](https://deepmind.google/models/gemma/gemma-3/) de Google:

* <u>1 milliard de paramètres (“1b”)</u>.
* <u>Instruction-tuned ("it")</u> : Optimisée pour suivre des instructions et répondre de manière conversationnelle, **ce modèle est idéal pour la génération de texte, le résumé et la traduction**.
* <u>Quantization-Aware Trained ("qat")</u> : Entraîné pour supporter la quantification (par exemple en 4 bits), ce qui **réduit considérablement la mémoire nécessaire tout en maintenant une qualité proche des modèles plus lourds**.

## C’est comment qu’on fait ? (Guide étape par étape)
### Ouvrez PowerShell en mode administrateur
   * Clic-droit sur le menu Démarrer et sélectionnez « Terminal (Administrateur) » ou «Windows  PowerShell (Admin) ».
<img src="/content/images/pshell_adm.jpg" alt="" style="display: block; margin: 0 auto;">

   * Cliquez sur \[Oui\] pour accepter l’élévation de privilèges.
   
<img src="/content/images/pshell_adm_uac.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

### Installez un instance locale Ollama, installez l’interface graphique et récupérez le modèle gemma3:1b-it-qat en une seule ligne de commande
   
* Exécutez cette commande :
{% highlight powershell %}
winget install --id=Ollama.Ollama --accept-source-agreements -e; winget install --id=FernandoMaclen.Hollama -e; ollama pull gemma3:1b-it-qat; shutdown -r -t 0
{% endhighlight %}<br/>

   * Une fois le paquet téléchargé et vérifié, le processus d’installation de l’instance Ollama commence, et l’interface graphique d’installation Ollama s’affiche.

<img src="/content/images/ollama_installer_ui.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

  * Durant l’une dernières étapes de ce premier processus d’installation, l’installation du Redistribuable Microsoft C++ 2015/2022 peut s’effectuer de manière automatique s’il n’est pas présent sur le système.

<img src="/content/images/cpp_install.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

  * À la fin du processus d’installation de l’instance Ollama, une fenêtre de bienvenue s'affiche. Vous pouvez cliquer sur \[Finish\] pour la fermer.

<img src="/content/images/ollama_welcome.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* L’instance locale Ollama étant installée, l’installation de l’interface graphique Hollama s’effectue de manière automatique.

<img src="/content/images/hollama_installer.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* Une fois ce processus d’installation terminé, le téléchargement du modèle **gemma3:1b-it-qat** sur l’instance locale Ollama se lance de manière automatique.

<img src="/content/images/gemma3_dl.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* Une fois le modèle téléchargé, le système redémarre automatiquement. Une fois redémarré, vous pouvez alors constater que l’icône de l’application Hollama est disponible sur le Bureau.

<img src="/content/images/hollama_icon.jpg" alt="" style="display: block; margin: 0 auto;">
### Finalisez l’installation
* Double-cliquez sur l’icône Hollama présent sur le bureau pour lancer l’interface graphique. Une notification du pare-feu Windows s’affiche, cliquez sur \[Annuler\] pour bloquer les flux entrants.

<img src="/content/images/hollama_fw.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* Une fois l’application démarrée, celle-ci s'ouvre directement dans les paramètres de l’interface.

<img src="/content/images/hollama_ui.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* Dans la section Serveurs, sélectionnez “Ollama” dans la liste déroulante “Type de connexion” puis cliquez sur \[Ajouter une connexion\].

<img src="/content/images/ollama_server.gif" alt="" style="display: block; margin: 0 auto;"><br/>

* Cliquez sur \[Vérifier\]. Si tout va bien le message “La connexion a été vérifiée et est prête à être utilisée.” s’affiche dans un encart vert en haut de la fenêtre, et la case “Utiiser les modèles de ce serveur” se coche automatiquement.

<img src="/content/images/ollama_verified.gif" alt="" style="display: block; margin: 0 auto;"><br/>

### Testez un premier prompt
* Dans le menu de gauche, cliquez sur \[Nouvelle session\].

<img src="/content/images/hollama_new_session.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* Validez que le modèle est présent dans la liste déroulante, écrivez votre prompt, cliquez sur \[Exécuter\]. Patientez quelques secondes, et voilà, magie 😀

<img src="/content/images/hollama_chat.gif" alt="" style="display: block; margin: 0 auto;"><br/>

### Comment télécharger d'autres modèles avec l'interface graphique ?
* Retournez dans les paramètres de l'application Hollama.
* Sous les paramètres de la connexion "Ollama", cliquez sur le lien "Bibliothèque d'Ollama". Dans la nouvelle fenêtre qui s'affiche, parcourez le catalogue de modèles disponible, copiez l'identifiant du modèle que vous souhaitez télécharger (exemple : **qwen3:0.6b**), puis fermez cette fenêtre.

<img src="/content/images/ollama_library.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* De retour dans les paramètres de la connexion "Ollama", collez l'identifiant du modèle dans la boite de texte "Tirer le modèle", puis cliquez sur le bouton rouge pour lancer le téléchargement.

<img src="/content/images/ollama_pull_model.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* Un message d'information s'affiche en haut de la fenètre pour montrer la progression. Le nouveau modèle est téléchargé et prêt à être utilisé quand le message passera au vert.

<img src="/content/images/ollama_model_ok.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

* Vous pouvez désormais choisir et utiliser ce nouveau modèle dans les sessions de conversation.

<img src="/content/images/ollama_model_list.jpg" alt="" style="display: block; margin: 0 auto;"><br/>

### Supprimer entièrement les composants installés
* Ouvrez PowerShell en mode administrateur \([cf. 1ère étape](#ouvrez-powershell-en-mode-administrateur)\),
* Exécutez la commande suivante pour supprimer tous les composants installés (applications et modèles) :
{% highlight powershell %}
winget uninstall --id=Ollama.Ollama ; winget uninstall --id=FernandoMaclen.Hollama; winget source reset --force; rm $env:USERPROFILE\*ollama* -R; rm $env:USERPROFILE\AppData\Local\*ollama* -R; rm $env:USERPROFILE\AppData\Local\Temp -R; rm $env:USERPROFILE\AppData\Roaming\*ollama* -R; shutdown -r -t 0
{% endhighlight %}
* Une fois les composants désinstallés, le poste va redémarrer automatiquement.

---

# Conclusion

En quelques minutes, vous pouvez désormais expérimenter la puissance des LLM locaux sur votre PC Windows, sans abonnement ni dépendance au cloud. Que ce soit pour apprendre, obtenir de l’aide à la rédaction ou au codage, ou simplement explorer les dernières avancées de l’intelligence artificielle, Ollama et Hollama offrent une solution simple et accessible.

N’hésitez pas à tester différents modèles, à partager vos retours ou vos découvertes, et à contribuer à la communauté open source !