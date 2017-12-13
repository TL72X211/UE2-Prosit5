# UE2-Prosit5-Expression-Régulière

* Mots clés:
- Expression régulière : Une expression régulière, regex ou regexp (parfois appelée expression rationnelle) est, en théorie informatique et théorie du langage formel, une séquence de caractères qui définissent un motif de recherche. Habituellement, ce modèle est ensuite utilisé par les algorithmes de recherche de chaîne pour les opérations "trouver" ou "trouver et remplacer" sur les chaînes.
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
  Fondamentalement, une expression régulière est un motif décrivant une certaine quantité de texte. Leur nom vient de la théorie mathématique sur laquelle ils sont basés. Mais nous ne creuserons pas dans cela. Vous trouverez généralement le nom abrégé en "regex" ou "regexp". Ce tutoriel utilise "regex", car il est facile de prononcer le pluriel "regexes". Sur ce site, les expressions régulières sont surlignées en rouge comme regex.

Ce premier exemple est en fait une regex parfaitement valide. C'est le modèle le plus basique, qui correspond simplement au regex textuel littéral. Une "correspondance" est le morceau de texte, ou la séquence d'octets ou de caractères dont le modèle a été trouvé correspondre par le logiciel de traitement de regex. Les matchs sont surlignés en bleu sur ce site.

`\b[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}\b` est un motif plus complexe. Il décrit une série de lettres, de chiffres, de points, de traits de soulignement, de signes de pourcentage et de tirets, suivis d'un arobas, suivis d'une autre série de lettres, de chiffres et de tirets, suivis d'un point et de deux lettres ou plus. En d'autres termes: ce modèle décrit une adresse e-mail. Cela montre également la coloration syntaxique appliquée aux expressions régulières sur ce site. Les frontières de mots et les quantificateurs sont en bleu, les classes de caractères sont en orange et les littéraux en échappement sont en gris. Vous verrez des couleurs supplémentaires comme le vert pour le regroupement et le violet pour les méta-jetons plus tard dans le didacticiel.

Avec le modèle d'expression régulière ci-dessus, vous pouvez rechercher dans un fichier texte pour trouver des adresses e-mail ou vérifier si une chaîne donnée ressemble à une adresse e-mail. Ce tutoriel utilise le terme "chaîne" pour indiquer le texte auquel l'expression régulière est appliquée. Ce site les met en évidence en vert. Le terme "chaîne" ou "chaîne de caractères" est utilisé par les programmeurs pour indiquer une séquence de caractères. En pratique, vous pouvez utiliser des expressions régulières avec toutes les données auxquelles vous pouvez accéder en utilisant l'application ou le langage de programmation avec lequel vous travaillez.

Il existe deux types d'expressions régulières, qui répondent aux doux noms de :

* POSIX : c'est un langage d'expressions régulières mis en avant par PHP, qui se veut un peu plus simple que PCRE (ça n'en reste pas moins assez complexe). Toutefois, son principal et gros défaut je dirais, c'est que ce « langage » est plus lent que PCRE ;

* PCRE : ces expressions régulières sont issues d'un autre langage (le Perl). Considérées comme un peu plus complexes, elles sont surtout bien plus rapides et performantes.


Syntaxe du regex :
![](https://image.prntscr.com/image/5IhhXUcpQ2aoq-b-P8nnLw.png)

Quantification
![](https://image.prntscr.com/image/tJOrtiRuSz2ISLp89O45GA.png)

![](https://image.prntscr.com/image/bvUbEukQSB2UeArd-7WOWg.png)

![](https://image.prntscr.com/image/ZjFqH2xCSCaIny5Z0NaIGw.png)

![](https://image.prntscr.com/image/m773OovcTqqgXxuaB2wejQ.png)

![](https://image.prntscr.com/image/SfcreMKGSMiHAgDjFxiwiA.png)



  
  - commande sed/grep
  La commande sed (Stream EDitor) à savoir éditeur de flux, est une commande qui permet de gérer les script en mode flux, que ce soit les fichiers en entrée qu'en écriture. Tout ceci garantie une bonne lecture des fichiers en les traitant ligne par ligne.
  Il existe de façon de procéder, une façon normale, sans ajout de paramètre à l'appel de la commande, qui consiste à récupérer le flux d'un fichier et à le sortir sur un autre fichier.
  Une méthode un peu plus direct en rajoutant le paramètre `-i` qui l'applique directement sur le fichier en entrée.
  
  Passage de script à `sed`: 
  
* On peut écrire le script directement dans la ligne de commande, avec l'option sed -e. On séparera les commandes avec des point-virgules.
    C'est la façon "uniligne", souvent très pratique.

* On peut passer à sed un fichier externe (par exemple myscript.sed) contenant le script, avec sed -f script-file. Cela assure une meilleure lisibilité pour les gros scripts, et permet aussi de réutiliser un script.
  Écrire un script pour sed peut devenir assez technique, et c'est seulement en pratiquant que vous arriverez à tirer plein parti de toute la puissance de ce dernier. Aussi, nous allons passer tout de suite à la pratique.
  
  Grep 
  grep recherche dans les FICHIERS d'entrée nommés (ou entrée standard si aucun fichier n'est nommé, ou si un seul trait d'union moins (-) est donné comme nom de fichier) pour les lignes contenant une correspondance avec le MOTIF donné. Par défaut, grep imprime les lignes correspondantes.

De plus, trois programmes variants egrep, fgrep et rgrep sont disponibles. egrep est le même que grep -E. fgrep est le même que grep -F. rgrep est le même que grep -r. L'invocation directe en tant que egrep ou fgrep est déconseillée, mais est fournie pour permettre aux applications historiques qui en dépendent de fonctionner sans modification
  
  
  - Redirection de flux (">", "<", ...)
Chaque commande donne lieu à des réponses, ces réponses peuvent être redirigées vers un fichier ou en entrée d'une autre commande, ce qui peut donc donner lieu à des "commandes chaînées" 
Où ? Dans un fichier, ou en entrée d'une autre commande pour « chaîner des commandes ». Ainsi, le résultat d'une commande peut en déclencher une autre !
Comment ? À l'aide de petits symboles spéciaux, appelés flux de redirection, que vous allez découvrir dans ce chapitre.

`> et >>` permet de redirigé les résultats dans un fichier, le premier redirige dans un nouveau fichier (écrasé si existant), le second à la fin d'un fichier déjà existant
`2>, 2>> et 2>&1` Redirections des erreurs, même si données en paramètres de commandes, elles seront utilisés que si erreur
`< et <<` permet de lire depuis un fichier ou d'un clavier, il s'agit de redirigé des flux d'entrées
`|`(pipe) permet de chaîner les commandes pour en créer plusieurs d'un seul appel



  - Utilisation dans les différents langages
  
  
Réalisation
  - Corbeille
  - Script
