# Introduction
Le développement informatique concerne tout ce qui touche à l’étude, à la conception, à la construction, au développement, à la mise au point, à la maintenance et à l’amélioration des logiciels/applications et sites web.

En SIN, pour effectuer du développement informatique nous étudierons plusieurs langages de programmation :

Langages de programmation pour le développement logiciels/applications :
- Arduino (très proche du C et du C++ – pour développer des programmes sur des cartes Arduino ou des microcontrôleurs de type ESP32). Une fiche de synthèse sur les différentes commandes et spécificités du langage Arduino est disponible sur le site du professeur.
- Python (pour développer des programmes sur des cartes Raspberry Pi).
Pour apprendre le langage Python une série de cours/problèmes est proposé sur le site France-ioi.org

#arduino_uno
![[Arduino_uno.png]]
#esp32
![[esp32.png]]
#raspberry3pi
![[Raspberry_pi3.png]]

Langages de programmation pour le développement WEB :
- [HTML](HTML) (HyperText Markup Language – Langage de balisage d’hypertexte – permet de représenter des pages web).
- [CSS](Css) (Cascading Style Sheet – feuille de style en cascade – Langage permettant de mettre en forme une page web). Vous pouvez retrouver l’activité HTML/CSS effectué en classe de première sur le site du professeur.
- [PHP](php) (Hypertext Preprocessor – permet de créer des pages web dynamiques).
Le langage PHP sera étudié en activité.

# Encodage de l’information
## Principe d'une base

La base est le nombre qui sert à définir un système de numération. La base du système décimal est dix alors que celle du système hexadécimal est 16 et la base du système binaire est 2. Quelques soit la base numérique employée, elle suit la relation suivante :
![[Principe_base.png]]
Où `bi` est le chiffre de la base de rang `i` et `ai` est la puissance de la `base a` d'exposant de rang `i`.

*Exemple : base 10*
`1986 = (1 × 103 ) + (9 × 102 ) + (8 × 101 ) + (6 × 100 )`

## Le système décimal
Le système décimal est celui dans lequel nous avons le plus l'habitude d'écrire. Chaque chiffre peut avoir 10 valeurs différentes : 0, 1, 2, 3, 4, 5, 6, 7, 8, 9. De ce fait, le système décimal a pour `base 10`. Tout nombre écrit dans le système décimal vérifie la relation suivante :
745 = 7 × 100 + 4 × 10 + 5 × 1
745 = 7 × 10 × 10 + 4 × 10 + 5 × 1
745 = 7 × 102 + 4 × 101 + 5 × 100

Chaque chiffre du nombre est à multiplier par une puissance de 10 : c'est ce que l'on nomme le `poids du chiffre`.

L'exposant de cette puissance est nul pour le chiffre situé le plus à droite et s'accroît d'une unité pour chaque passage à un chiffre vers la gauche.

12 435 = 1 × 104 + 2 × 103 + 4 × 102 + 3 × 101 + 5 × 100 .

Cette façon d'écrire les nombres est appelée `système de numération de position`. Dans notre système conventionnel, nous utilisons les puissances de 10 pour pondérer la valeur des chiffres selon leur position, cependant il est possible d'imaginer d'autres systèmes de nombres ayant comme base un nombre entier
différent.

## Le système binaire
Dans le système binaire, chaque chiffre peut avoir 2 valeurs différentes : 0, 1. De ce fait, le système a pour base 2. Tout nombre écrit dans ce système vérifie la relation suivante :

(10 110)2 = 1 × 24 + 0 × 23 + 1 × 22 + 1 × 21 + 0 × 20
(10 110)2 = 1 × 16 + 0 × 8 + 1 × 4 + 1 × 2 + 0 × 1
donc `(10110)2 = (22)1 0`

Tous les systèmes de numération de position obéissent aux règles que nous venons de voir.

## Le système hexadécimal
Le système hexadécimal utilise les 16 symboles suivants : 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F. De ce fait, le système a pour `base 16`.
Un nombre exprimé en base 16 pourra se présenter de la manière suivante : (5AF)1 6.

Le nombre (5AF)1 6 peut se décomposer comme suit :
(5AF)1 6 = 5 × 162 + A × 161 + F × 160
En remplaçant A et F par leur équivalent en base 10, on obtient :
(5AF)1 6 = 5 × 162 + 10 × 161 + 15 × 160
(5AF)1 6 = 5 × 256 + 10 × 16 + 15 × 1
donc `(5AF)1 6 = (1455)1 0`

## Le système octal
Le système octal utilise un système de numération ayant comme base 8. Il faut noter que dans ce système nous n'aurons plus 10 symboles mais 8 seulement : 0, 1, 2, 3, 4, 5, 6, 7.

Ainsi, un nombre exprimé en base 8 pourra se présenter de la manière suivante : (745) 8

Lorsque l'on écrit un nombre, il faudra bien préciser la base dans laquelle on l'exprime pour lever les éventuelles indéterminations (745 existe aussi en base 10). Ainsi le nombre sera mis entre parenthèses (745 dans notre exemple) et indicé d'un nombre représentant sa base (8 est mis en indice).

Cette base obéira aux mêmes règles que la base 10, vue précédemment, ainsi on peut décomposer (745)8 de la façon suivante :

(745)8 = 7 × 82 + 4 × 81 + 5 × 80
(745)8 = 7 × 64 + 4 × 8 + 5 × 1
(745)8 = 448 + 32 + 5

Nous venons de voir que : `(745)8 = (485)10`.
![[Base convertion.png]]
## ASCII
Le code ASCII (pour American Standard Code for Information Interchange) est une norme informatique de codage de caractères alphanumériques. ASCII comprend 128 combinaisons de 7 bits historiquement qui définissent 95 caractères imprimables, dont les chiffres arabes de 0 à 9, les lettres de l’alphabet latin non accentuées, minuscules et majuscules, des symboles de ponctuation et quelques caractères mathématiques simples.

Il convient bien pour coder les textes en anglais, mais est insuffisant pour le français, notamment en raison de `l’absence des caractères accentués`. Il est à noter aussi que les 32 premières combinaisons ne sont pas imprimables ainsi que la dernière, 127 : toutes correspondent à des commandes de terminal informatique.
Ainsi, la combinaison 127 correspond à la commande pour effacer.

Le code ASCII a été étendu sur 8 bits pour incorporer certains caractères accentués (notamment les accents français). On voit ci-dessous la deuxième partie du code ASCII dit étendu codé sur 8 bits, la première partie étant le code ASCII historique sur 7 bits qui code en décimal de 0 à 127, en hexadécimal de 00h à 7Fh. L’extension ci-dessous code donc en décimal de 128 à 255 et en hexadécimal de 80h à FFh.
![[ASCII.png]]

## UNICODE
Unicode est un standard informatique qui permet des échanges de textes dans de `très nombreuses langues`, à un niveau mondial. Il est développé par le `Consortium Unicode`, qui vise au codage de texte écrit en donnant à tout caractère de n'importe quel système d'écriture un nom et un identifiant numérique, et ce de manière unifiée, quelle que soit la plateforme informatique ou le logiciel utilisés.

À ce jour, Unicode référence plus de `137 000 caractères` dans une centaine d’écritures.

La principale caractéristique d’UTF-8 (variante d’Unicode) est qu’elle est `rétro compatible` avec la norme ASCII, c’est-à-dire que tout caractère ASCII se code en UTF-8 sous forme d’un unique octet, identique au code ASCII. Par exemple, « `A` » (A majuscule) a pour code ASCII 65 et se code en UTF-8 par l'octet 65.