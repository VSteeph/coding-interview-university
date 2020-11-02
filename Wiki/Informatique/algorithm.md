# Algorithmes

## Measurer l'efficacité/vitesse

Cela ne se mesure déjà pas par rapport à la vitesse en temps car tous les ordinateurs et les utilisations sont variés. Un algorithm se mesure d'une façon uniforme : Big O notation. Cela mesure la complexité Asymptotique d'un programe. C'est à dire déterminer l'augmentation de la vitesse de l'execution d'un programme quand la taille de l'input augmente vers l'infini (augmentation Asymptotique).

Par exemple, trier un array d'une taille de 10, 1000, 1 millions, quel est l'évolution du runtime du programe.

Compter le nombre de lettres dans une string :

- Façon la plus simple, caractere par caractere et ajouter 1 à chaque caractere. Cet algorithm s'execute dans un temps linéaire basé sur le nombre de caracteres "n", donc O(n). L'augmentation du nombre de caractere est linéaire avec l'augmentation du runtime du programe.
- Si on store le nombre de caractere dans une variable Length au moment de la création de la string, savoir le nombre de caractere dans une string, il suffit de regarder la variable. Acceder la valeur d'une variable est considéré comme une opération constante asymptotique, c'est à dire 0(1). c'est à dire que le programme s'executera en constant time par rapport à l'input size.

La 2eme façon ne signifie pas que le code s'execute en 1 étapes, mais peu importe la taille de l'input, il n'y aura pas d'impact.

### Types d'asymptotique complexité
- O(n)², c'est tres lent et comme c'est exponentiel, cela tend à prendre beaucoup de temps. Cela pose problème principalement dans le Big Data mais pour des petites tailles d'input, il y a peu/pas de différence avec O(n) car il y a un build up de la fonction.

- O(log n), c'est illustré par trouver un élément dans un tableau trié (Binary search algorithm qui consiste à diviser un tableau en 2), cela veut dire que pour n = 8, cela donnera 3 itérations et pour n = 16 cela donnera 4 itérations.

- O(2^n) : plus lent algo possible quand on travaille avec la donnée

Ces types sont utilisés pour 2 façons : upper & lower bounds qui permettent de donner le temps minimum et le temps maximum qu'un algorithm peut mettre.

Le plus de temps : Big O => O( log n) => Binary search
Le moins de temps : Omega => Ω(1) => Binary Search
Quand les 2 cas sont équivalent : Theta => θ(1) => 2eme cas pour compter le nombre de caracteres dans une string
