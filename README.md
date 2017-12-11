# UE2-Prosit5-Expression-Régulière 

* Mots clés:
- Expression régulière :  Pattern décrivant un certain montant de texte.
- Reconnaissance de motifs
- Serveur de pré-prod
- Référence
- Première maquette
- Imbriqué
- Occurence
- Accès au serveur
- Ctrl + h
- Ctrl + f
- Mise à jour contenue

* Contexte:
  * Quoi ?
    - Trouver les occurences des mots à modifier/changer
  * Comment ?
    - En utilisant les expressions régulière
  * Pourquoi ?
    - Mettre à jour le contenu du fichier
    - Refonte graphique
    - Gagner du temps
    - Limiter les erreurs
    
* Contraintes:
  - Utilisation d'une distribution Linux

* Problématique:
  - Comment utiliser les expressions régulières pour rechercher/remplacer des informations ?

* Généralisation:
  - Automatisation

* Hypothèse:
  - Commande sed permet de remplacer une chaîne de caractère par une autre dans un fichier
  - RegEx est un langage qui permet de "matcher" des chaînes de caractères
  - On peut imbriquer les expressions régulières
  - Ctrl + F permet de rechercher
  - Ctrl + H permet de remplacer
  - Il existe plusieurs types d'expressions régulières (simples et étendues)
 
* Plan d'action:

Etude:
  - Expressions régulières(fonctionnement, histoire, syntaxe, construction)
  - commande sed/grep
  - Redirection de flux (">", "<", ...)
  - Utilisation dans les différents langages
  
Réalisation
  - Corbeille
  - Script

### **Les expressions régulières :**

Ce sont des pattern décrivant un certain montant de texte, leur nom viens d'une théorie mathématique sur laquelle elles sont basées. 
"regex" (contraction de regular expression), et "regexp" sont des diminutifs.
ça constitue un système très puissant et très rapide pour faire des recherches dans des chaînes de caractères (comme des phrases). Ça permet ainsi de faire des rechercher/remplacer très poussée.

Il existe deux types d'expressions régulières :

* POSIX : Mis en avant par le PHP, plus lent que le PCRE.
* PCRE : Vient du PERL, considéré comme plus complexe, mais plus rapide et performant.

On les retrouves dans de nombreux langages comme du PHP, MySQL, Javascript...

Un regex est toujours entouré par un délimiteur **'#'** en vue que l'on peut mettre des options juste après.

* Pour rechercher un mot depuis le début, on utilise **'^'** au début de notre mot
* Pour rechercher un mot depuis la fin, on utilise **'$'** à la fin de notre mot
* Pour rechercher l'un ou l'autre, on rajoute un pipe **'|'**
* Le crochet permet de laisser un où exclusif : m[oai]ts => sélectionne les parties du texte où il y a un m, suivis d'un o **ou** d'un a **ou** d'un i, puis un t et un s. Si on met un **^** dans les crochets, ça inverse le tout (non 'ou'), c'est à dire qui ne contiendra ni o, ni a, ni i.
* On a un système d'intervalle : [a-z] == [abcdefg{...}z]
* Dans le même principe : [0-9] == [0123{...}9]
* On retrouve des raccourcis de raccourcis, il ne faudra pas les mettre entre crochets.
	* . = n'importe quel caractère
	* \w = [a-zA-Z0-9_]
	* \d = [0-9]
	* \n = retour à la ligne
	* \t = tabulation



