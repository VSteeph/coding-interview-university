# Data Structured

## Arrays
Un array est un chunk continu de mémoire, qui est divisible en élément de même tailles qui sont referencés par des entiers continus (1 based ou 0 based index, c'est à dire qui commence 0 ou à 1, en général 0)

L'avantage est qu'on peut accéder à tout moment à n'importe quel élément d'un array. C'est possible en calculant la prochaine adresse.

On prend l'adresse de l'array et on ajoute la taille de l'element * l'index, ce qui donne
```
array_addr + elem_size * (i - first_index) // ce qui permet d'avoir une base 1 ou 0
```
C'est pour cela qu'on utilise des éléments à même taille.

### Multi-Dimensional Arrays
Ce sont des tableaux dans des tableaux souvent écrit par int[x][y]. Pour calculer l'adresse, on utilise le même procédé mais à 2 échelles.

| 0,0 | 0,1 | 0,2 | 0,3 |
|-----|-----|-----|-----|
| 1,0 | 1,1 | 1,2 | 1,3 |
| 2,0 | 2,1 | 2,2 | 2,3 |

On selectionne déjà la colonne qu'on va utiliser avec la formule qu'on a vu précdemment et on fait de même avec le 2eme index

```
array_addr + elem_Size1 * (i - first_Index) + elem_Size2 * (y - first_Index);
```

Dans ce cas, on assume que tous les éléments sont après les autres, ça s'appelle le Row-Major order ou Row-major index.

D'autres compiler regroupent tous les index 1 puis tous les index 2, ce qui donnerait:
- 0,0
- 1,0
- 2,0
- 0,1
- 1,1
- 2,1
- 0,2
- 1,2
- 2,2

Cela s'appelle Column-major order

### Times for common Operation
Les opérations de base comme lire ou modier sont de O(1), mais pour ajouter ou enlever, c'est différent.

Pour ajouter un element à la fin, on ajoute le nombre d'éléments donc 0(1) et pareil pour enlever le dernier.

Pour enlever le premier ou ajouter le premier, cela nécessite de tout restructurer, c'est donc 0(n) afin d'éviter les trous

|           | Add    | Remove |
|-----------|--------|--------|
| Beginning | O(n)   | O(n)   |
| Middle    | O(n) ? | O(n) ? |
| End       | O(1)   | O(1)   |
