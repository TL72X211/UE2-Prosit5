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

**Histoire :** Issus de théories mathématiques des langages formels[informatique] (Stephen Cole Kleene [ensembles réguliers, de langages rationnels]) dans les années 1940, on les utilise aujourd'hui pour programmer des logiciels avec des fonctionnalités de lecture, contrôle, modification, analyse de texte.  C'est lors de l'aparition de commandes comme grep, que regexp à pris tout son sens ,et est devenu une norme pour tout les langages.

Ce sont des pattern décrivant un certain montant de texte, leur nom viens d'une théorie mathématique sur laquelle elles sont basées. 
"regex" (contraction de regular expression), et "regexp" sont des diminutifs.
ça constitue un système très puissant et très rapide pour faire des recherches dans des chaînes de caractères (comme des phrases). Ça permet ainsi de faire des rechercher/remplacer très poussée.

Il existe deux types d'expressions régulières :

* POSIX : Mis en avant par le PHP, plus lent que le PCRE.
* PCRE : Vient du PERL, considéré comme plus complexe, mais plus rapide et performant.

On les retrouves dans de nombreux langages comme du PHP, MySQL, Javascript...

* Un regex est toujours entouré par un délimiteur **'#'** en vue que l'on peut mettre des options juste après.
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
* On a également des quantificateurs : ma [a-z] [a-z] == ma [a-z] {2} == ma suivit de deux lettres
	* {min,max}
	* {min,}
	* {max,}
	* {nombre}
	* '*' == {0,}
	* '+' == {1,}
	* '?' == {,1}
* On peut échapper les caractères spéciaux à l'aide du **'\'**

* En PHP, on retrouve la fonction preg_match qui prends deux paramètres, et renvois un booléen. Dans le premier paramètre, on y met notre regexp, et dans le second notre chaîne.

### **Commandes sed/grep :**

https://doc.ubuntu-fr.org/sed

**sed et cut** (Stream Editor ou éditeur de flux) permettent de modifier ou de supprimer une partie d'une chaîne de caractère, par exemple, remplacer un caractère par un autre dans un fichier, ou de supprimer des chaînes de caractère inutile. 
La commande sed peut utiliser des regexp.

**Synthaxe globale :**

* Synthaxe pour remplacer : 

 "s/[occurrence_cherchée]/[occurrence_de_substitution]/[comportement]" 
	 *par défaut, elle s’effectue sur la première occurrence du motif sauf si dans commande, on lui ajoute un comportement (exemple : 2 pour deuxième occurrence).

* Méthode classique : un flux d'entrée, et un flux de sortie (on récupère sur un fichier, et on le met sur un autre)
* Méthode directe : sed -i : applique directement sur le fichier passé en entrée
* sed ' ' [nomfichier.txt] => Renvois le contenu du fichier
* d pour delete
* sed -e '4d; 7d' test.txt => va effacer toutes les lignes entre la ligne 4 et 7, le e pour plusieurs arguments.
* sed '/^#/ d' test.txt => Supprimera toutes les lignes commençant une un '#'*
* sed -n '/Ici/p' test.txt => N'affichera que les lignes qui contiennent 'Ici'


**La commande grep**

Son point fort : La recherche plein texte.

* grep texte nomfichier : Va afficher toutes les lignes qui comportent le mot "texte" dans le fichier nomfichier.
* grep tient compte de la casse, on peut utiliser -i pour ignorer la casse
*  On peut utiliser -n pour connaitre les numéros de lignes
* -v permet de connaître toutes les lignes qui ne contiennent pas un mot donné.
*  -r , on l'utilise dans un répertoire, et il va aller chercher dans tout les fichiers.
*  On utilise -E pour utiliser une expression régulière ou egrep
	* $ grep -E ^Alias .bashrc
	* $egrep ^Alias .bashrc



