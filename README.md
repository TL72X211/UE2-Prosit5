# UE2-Prosit5-Expression-Régulière

* Mots clés:
- Expression régulière : une chaîne de caractères, qui décrit, selon une syntaxe précise, un ensemble de chaînes de caractères possibles.
- Reconnaissance de motifs : 
- Serveur de pré-prod : 
- Référence : 
- Première maquette :
- Imbriqué : 
- Occurrence : 
- Accès au serveur :
- Ctrl + h : fonction de remplacement
- Ctrl + f : fonction de recherche
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

une expression réguilre est un pattern (motif, format, gabarit) décrivant du texte, le nom viens de la théorie mathématique sur laquelle elles sont basées, on les abrège généralement en regex 
les regex permettent de match du text, un match est un texte, séquence d'octets ou suite de caractères dont le pattern correspond à un autre selon la regex

[A-Z0-9._%+-]+@[A-Z0-9.-]+\\.[A-Z]{2,}

avec les expressions régulières on peut chercher : 

* un caractère ou une suite de caractères précise 'a' ou "Jean" (**a confirmer**: il doit y avoir moyen d'être sensible à la case)
* une suite de lettres quelconque "[A-Z]"
* une suite de chiffre quelconque "[0-9]"
* une combinaison quelconque de lettre et/ou de chiffres [A-Z0-9]
*  n'importe quel caractère d'une liste [azer.;%]

Syntaxe:

il existe 12 caractères spéciaux:

* \ permet d'escape les autres caractères ou de faire des raccourcis (ex : /d pour 0-9)
* ^ permet d’effectuer un ‘non’ dans une classe de caractère ou le début de la string
* $ ‘ancre’ match la fin de la string
* . match un seul caractère
* | permet d’effectuer un ‘ou’
* ? l'item précédent sera match 0 ou 1 fois
* \* l'item précédent sera match 0 ou + fois
* + l'item précédent sera match 1 ou + fois
* ( permet la création d’un groupe 
* [ créé une classe de caractères
* { permet d'exprimer une quantité {3} ou {2,5} ou {2,}
* \- permet la création d’une range

si on veut les utiliser comme vrai caractères on les escape avec le \

en bash :
 
décris une suite de lettre(s), chiffre(s), point(s),underscore(s), pourcent(s),plus et moin(s) suivi d'un @ d'un autre suite de chiffre/lettre/._%+- , un point et une suite de lettre d'une taille de 2 ou +


fonctionnement interne :

il existe 2 types de moteurs regex: orientés texte et orientés regex, presque tous les moteurs regex modernes sont orientés regex (car les lazy quantifiers et backreferences -to be seen later- ne sont possible que pour les moteurs orientés regex)

**fonctionnement moteur regex**
moteur orienté regex : parcourt l'expression régulière et essaye de match le token suivant de la regex au caractère suivant, si il trouve une match il continue dans la regex et la string a tester, sinon il backtrack à une position précédente dans la regex et la string où il peut *"try a different path through the regex."* (j traduit pas de suite pour éviter une perte de sens)

une regex retourne toujours le premier résultat qu'il trouve (le plus a gauche dans la string)

**char class**
classe de caractères : [] ex: gr[ea]y fonctionne grey et gray mais pas graay ou graey, l'ordre des caractères dans le set n'est pas important. Pratique pour trouver des mots même s'ils sont mal orthographiés 

^ permet d'effectuer un 'non' ^[0-9\r\n] match tout ce qui n'est pas un chiffre ou un retour chariot
il est important de noter qu'une negated character class doit match un character q[^u]  ne match pas un q qui n'est pas suivi d'un u main un q suivi d'un caractère qui n'est pas un u (ne fonctionnera pas avec un q en fin de string donc)
répéter une classe de caractères : si on répète une classe de caractères avec ,* ou + on répète la classe entière et non uniquement les caractères qu’elle à match ( [0-9]+ match 856 aussi bien que 222), pour répéter les caractères matchés on utilise les backreferences (  ([0-9])\1+ match 222 mais pas 856 et match 333 dans 83337

**fonctionnement moteur regex**
Classes de caractères : on applique la regex gr[ae]y à “Is his hair grey or gray ? »
Le moteur n’arrive pas a match g pour les 12 premiers caractères, il match ensuite g, passe au r, le match et arrive au troisième token [ae] il doit match un a ou un e, il commence par a et échoue mais puisqu’il s’agit d’un moteur orienté regex il continue d’essayer de match les autres permutations avant de déterminer que la regex ne match pas, il continue donc en essaye de faire match le e au lieu du a  et réussi, il match ensuite le y et a donc trouvé une complete match qu’il retourne et s’arrête

**char class**
On peut soustraire des classes de caractères en XML, XPath, .NET et JGsoft 
backreference : 

  - commande sed/grep
Grep : permet d’obtenir les lignes auxquelles la regex est valide
Options : 
-e MOTIF utilise MOTIF 
-f FICHIER lis les motifs dans le fichier
-c affiche le numéro des lignes auxquelles le motif corresponds
-o affiche uniquement la partie répondant à la regex
--color affiche en couleur ce qui réponds au regex
-n écris ‘numéroLigne :ligne’
-nC affiche le numéro de la gine comme n et les lignes de contexte avec numLigne-ligne
-w n’affiche que le mot exact et pas les variantes
-i ignore la case
-A N affiche les N lignes qui suivent celle contenant le motif
-B N affiche les N lignes qui précèdent celle qui contient le motif
-C N affiche 4 lignes de contexte 
- Redirection de flux (">", "<", ...)
- Utilisation dans les différents langages

Pour éviter d’avoir a escape tous les caractères spéciaux on peut mettre notre regex entre simple quotes
La syntaxe est similaire à celle vu précédement
alnum
letters and digits
alpha
letters
blank
system-dependent; for GNU, a space or tab
cntrl
control characters (in the ASCII encoding, code 0177 and codes less than 040)
digit
digits
graph
same as print except omits space
lower
lowercase letters
print
printable characters (in the ASCII encoding, space tilde--codes 040 through 0176)
punct
neither control nor alphanumeric characters
space
space, carriage return, newline, vertical tab, and form feed
upper
uppercase letters
xdigit
hexadecimal digits: 0--9, a--f, A--F

redirection
  >
Save output to a file.
>>
Append output to a file.
<
Read input from a file.
2>
Redirect error messages.
|
Send the output from one program as input to another program.

**SED**
Stream editor (ctrl+h)

substitution
Sed s/[regex][remplacement] [fichier]
Ou sed -e s/[regex][remplacement] [fichier]

Négation avec !
Supression d
Pour les lignes on les donnent au début  debut,fin
Réalisation
  - Corbeille

Trouver une expression régulière qui correspond à un nombre présent à la fin d'une ligne.
[0-9]$
Trouver une expression régulière qui correspond à des noms de fichiers avec une extension "jpg".
[\w]*\.jpg
Trouver une expression régulière qui trouve tous les mots de 4 caractères.
[^A-z][A-z]{4}[^A-z]
Trouver une expression régulière permettant de reconnaître toutes les dates suivantes : 
• 01/08/1933 
• 2-09-2022 
• 06 2 1965 
• 15.02.1985
[0-9]{1,2}(\/|-| |\.)[0-9]{1,2}(\/|-| |\.)[0-9]{4}[^0-9]

Trouver une expression régulière permettant de reconnaitre une adresse IPv4.
((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)
Prends 250-255, 249-200 0-199 suivi d’un . 3 fois et sans point une 4eme il doit y avoir plus propre mais je n’ai pas trouvé mieux
Trouver une expression régulière permettant de reconnaître une adresse e-mail (pour information, la RFC 822 http://www.w3.org/Protocols/rfc822/ )
[\w.]+@[\w]+\.[A-z]{2,}
  - Script
GREP 
Sous Linux, donnez et testez une ligne de commande utilisant grep permettant : 
• De créer un fichier passwd_numero contenant le contenu de chaque ligne du fichier /etc/passwd précédée de son numéro de ligne. 
grep --color -n '.' /etc/passwd  > pass.txt
• De n’afficher que les lignes contenant la chaîne bash dans /etc/passwd. 
grep bash /etc/passwd
• De n’afficher que les lignes où un chemin vers /home apparaît dans le champ destiné à définir le répertoire principal de l’utilisateur dans /etc/passwd. 
grep  '/home' /etc/passwd
• De n’afficher que les lignes du fichier /etc/passwd pour lesquelles l’interpréteur de commandes n’est pas le bash.
grep -v 'bash' /etc/passwd | grep --color '/bin/' /etc/passwd



Biblio :
http://web.mit.edu/gnu/doc/html/regex_3.html

