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

**Histoire :**  C'est en 1940 que Stephen Stephen Cole Kleene qui travaillait sur ensembles réguliers de langages rationnels, l'a développé.
La notion a été réintroduite plus tard en tant que langage formel en informatique.
On les utilise aujourd'hui pour programmer des logiciels avec des fonctionnalités de lecture, contrôle, modification, analyse de texte.  C'est lors de l'apparition de commandes comme grep, que regexp à pris tout son sens ,et est devenu une norme pour tout les langages.

Ce sont des patterns pouvant décrire un contenu de texte.

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
	* \\!/ egrep ne prends pas les raccourcis sous terminal sauf si on met des guillemets
	* Les guillements permettent d'empêcher l'utilisation des \
	* [:alnum:] == \w en bash (plus d'infos : http://web.mit.edu/gnu/doc/html/regex_3.html)


**Points importants**

![](https://github.com/TL72X211/UE2-Prosit5/blob/Emilien/expr_reg_emilien.PNG)


### **Les redirections de flux :**

Il est possible de rediriger les résultats de commandes, au lieu qu'il s'affiche dans la console, il peut s'afficher dans un fichier texte, ou en entrée d'une autre commande (chaîne de commandes).

**Rediriger les sorties**

* **>** = rediriger vers un nouveau fichier
*  **>>** = rediriger à la fin d'un fichier (très utiles pour les logs)
* \\!/ pour les deux commandes ci dessus, les erreurs sont quand même affichés dans la console.
	* Pour enregistrer les erreurs dans un fichier à part, on utilise l'opérateur **2>**
	*  EX: cut -d , -f 1 fichier_inexistant.csv > eleves.txt 2> erreurs.log
	*  On peut aussi utiliser **2>>** sur le même principe.
*  On peut fusionner les sorties à l'aide de **2>$1**
	*  Tout ira (les erreurs comprises) dans le fichier nominé, c'est le désigner comme la sortie standart
	*  **2>>$1** NE MARCHE PAS.
	*  Très utile pour les fichiers d'erreurs

**Rediriger les entrées**

* **<** Permet de lire depuis un fichier, c'est à dire qu'on va modifier l'entrée.
	* cat < notes.csv => Va afficher le contenu du fichier envoyé en entrée, cat va recevoir les entrées de notes.csv

* **<<** permet d'envoyer un contenu à une commande avec notre clavier.
	* Exemple : sort -n << FIN : La console va nous demander de taper du texte, on pourra y rentrer le nombre de valeurs que l'on souhaite jusqu'à ce qu'on écrive "FIN". 
	* Exemple 2 : wc -m << FIN : On rentre une chaîne de caractères, puis on appui sur Entrée pour revenir à la ligne, on tape FIN. Le résultat va être le nombre de caractères de la chaîne que l'on vient de rentrer.
	* Le mot "FIN" n'est pas obligatoire ,on peut le remplasser par ce que l'on veut.
	
**Chaîne de commandes**

* On utilise le pipe **|** pour chaîner plusieurs commandes, c'est à dire que tout ce qui va sortir de la commande 1 sera immédiatement envoyé dans la commande 2.
	* **Exemple** : Si on veut récupérer les noms, et les trier :
		* $ _cut -d , -f 1 notes.csv | sort_
	* **Exemple 2** : Trier par taille :
		* $ _du | sort -nr_
	* **Exemple 3** : Chaîne de trois commandes, avec head (filtrer les premières lignes) :
		* $ _du | sort -nr | head_
	* **Exemple 4** : Lister tous les fichiers contenant le mot "log" dans /var/log ( -I permet d'exclure les fichiers binaires), y extraire les noms de fichiers, trier les noms de fichier, supprimer les doublons  :
		* _$ sudo grep log -Ir /var/log  | cut -d : -f 1  | sort | uniq_
	

### **Corbeille d'exercice :**

Trouver une expression régulière qui correspond à un nombre présent à la fin
d'une ligne : 

 *  root@emilien-LAMP:/# egrep -o --color [0-9]\$ trace.txt

Trouver une expression régulière qui correspond à des noms de fichiers avec une extension"jpg" :

*  root@emilien-LAMP:/# ls | egrep .jpg 

Trouver une expression régulière qui trouve tous les mots de 4 caractères :

*  egrep  --color ^[a-z]\{4\}[^a-z] trace.txt 
Trouver une expression régulière permettant de reconnaitre une adresse IPV4 :

![](https://github.com/TL72X211/UE2-Prosit5/blob/Emilien/Screens_Prosit/ipv4.PNG)

**nb :** On peut factoriser [0-1][0-9][0-9] => 1[0-9]{2}

Trouver une expression régulière permettant de reconnaître toutes les dates suivantes {...} :

* root@emilien-LAMP:/# egrep --color '([0-9][0-9]?(/|-| |\.)){2}[0-9]{4}' trace.txt
01/08/1993
2-09-2022
06 2 1965
15.02.1985

Trouver une expression régulière permettant de reconnaître une @email :

* root@emilien-LAMP:/# egrep --color '[[:alnum:]\._-]+@\w+.[a-z]{2,}' trace.txt

**GREP**

Créer un fichier passwd_numéro qui va contenir le contenu de /etc/passwd avec son numéro de ligne :

* grep -n '\w' /etc/passwd > passwd_numero

N'afficher que les lignes contenant la chaîne bash dans /etc/passwd :

* root@emilien-LAMP:/# grep bash /etc/passwd

N'afficher que les lignes où un chemin vers /home apparaît dans le champ destiné à définir le répertoire principal de l'utilisateur dans /etc/passwd :

* root@emilien-LAMP:/# grep '/home' /etc/passwd

N'afficher que les lignes du fichier /etc/passwd pour lesquelles l'interpréteur de commandes n'est pas bash :

* root@emilien-LAMP:/# grep -v /bash /etc/passwd | egrep /bin

**SED**

Remplacer HTTP par HTTPS dans les lignes 4 à 12 dans le fichier.log
1) sed -i 's/http/https/g' fichier.log [incomplète, il manque 4 à 12]












