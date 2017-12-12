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

* \ permet d'escape les autres caractères ou de faire des racourcis (ex : /d pour 0-9)
* ^
* $
* . 
* |
* ?
* *
* +
* (
* )
* [
* { permet d'exprimer une quantité {3} ou {2,5} ou {2,}

si on veut les utiliser comme vrai caractères on les escape avec le \
  
décris une suite de lettre(s), chiffre(s), point(s),underscore(s), pourcent(s),plus et moin(s) suivi d'un @ d'un autre suite de chiffre/lettre/._%+- , un point et une suite de lettre d'une taille de 2 ou +


fonctionnement interne :

il existe 2 types de moteurs regex: orientés texte et orientés regex, presque tous les moteurs regex modernes sont orientés regex (car les lazy quantifiers et backreferences -to be seen later- ne sont possible que pour les moteurs orientés regex)

moteur orienté regex : parcourt l'expression régulière et essaye de match le token suivant de la regex u caractère suivant, si il trouve une match il continue dans la regex et la string a tester, sinon il backtrack à une position précédente dans la regex et la string où il peut *"try a different path through the regex."* (j traduit pas de suite pour éviter une perte de sens)

une regex retourne toujours le premier résultat qu'il trouve (le plus a gauche dans la string)

ensemble de caractères : [] ex: gr[ea]y fonctionne grey et gray mais pas graay ou graey, l'ordre des caractères dans le set n'est pas important


  - commande sed/grep1
  - Redirection de flux (">", "<", ...)
  - Utilisation dans les différents langages
  
Réalisation
  - Corbeille
  - Script

