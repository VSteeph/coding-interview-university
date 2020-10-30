# C# features

## Yield keyword
Tous les IEnumerable peuvent être utiliser dans une foreach loop. En gros, cela permet d'examiner plusieurs valeurs dans un container/collection, une à la fois.

Application du yield keyword

```
class IteratorExemple : IEnumerable<int> {
  public IEnumerator<int> GetEnumerator() {
    for(int index = 0; index <10; idnex++)
      {
        yield return index;
      }
  }

  IEnumerator IEnumerable.GetEnumerator() {
    return GetEnumerator;
  }
}
```

Le yield keyword permet d'utiliser les foreach avec les IEnumerable. c'est à dire que la valeur est envoyé et la fonction est mis en "pause" contrairement à un return classique. La prochaine itération continuera au dernier index afin de parcourir toutes les valeurs du IEnumerable

Yield ne peut être utiliser que dans les méthodes qui return un IEnumerator<T> ou IEnumerable<T> et leur version non-generic

### Named iterators
Il est aussi possible de créer une method qui return un IEnumerable<T> et avoir plusieurs versions avec des comportements differents :

```
public Class Counter
{
  public IEnumerable<int> CountUp(int start, int end)
  {
    int current = start;
    while (current < end)
    {
      yield return current;
      current++;
    }
  }

  public IEnumerable<int> Countdown(int start, int end)
  {
    int current = start;
    while(current > end)
    {
      yield return current;
      current--;
    }
  }
}

Counter counter = new Counter();
foreach(int number in counter.CountUp(5,50))
{
  Console.WriteLine(number)
}

foreach(int number in counter.Countdown(50,10))
{
  Console.WriteLine(number)
}
```

## Constants
Une façon d'avoir une variable qui ne change jamais de valeur est d'utiliesr les keywords :
- Const
- readonly

C'est une sécurité pour être sur que personne ne change la valeur, c'est utile pour le GUID de la verison d'un logiciel (comme Visual Studio) par exemple. On peut donc déclarer ses variables en tant que const car une fois déclaré, ils ne changeront jamais. Une variable const est par défaut static.

La différence entre const et readonly est que readonly peut être assigné par la suite. Ce sont des runtime constants. C'est utile lors de constructors par exemple, si on veut donner un GUID à chaque nouvelle voiture.

## Attributes
Cela permet d'ajoute  de la metaData au code. Ils peuvent être ajoutés au types, paramètres de méthodes et return types. Les attributs peuvent être detectés par le compiler, external code tools, ou même le code en reflection.

Cela prend cette forme

```
[Obsolete]
private void DisplayFlashPlayer()
{  
}

[Obsolete("Utiliser la fonction DisplayNativePlayer", true)]
private void DisplayFlashPlayer(int width, int height)
{
}
```

Le True permet de signifier si le compiler doit considérer le message comme une erreur plutôt qu'un warning. Les attributs peuvent se cumuler
```
[Attribute 1]
[Attribute 2]
[Attribute 3]
public class SomeClass {

}
```

## NameOf operator
Cela permet d'avoir le nom de la proprieté utilisé. C'est en général une bonne pratique d'utiliser nameOf plutôt que d'écrire le nom de la proprieté car cela permet de changer le nom si nécessaire plus simplement.

Par exemple, dans une class "Book", on veut override le toString pour avoir une meilleure division

```
Class Book {
  public string title {get;set;}
  public string Author {get;set;}
  public int Pages {get;set;}

  public override string ToString() {
    // Façon 1 :
    return $"Book Title = {Title}, Author = {Author}, Pages = {Pages}"
    // Façon 2 :
    return $" nameof(Book) nameof(title) = {Title}, nameof(AuthorAuthor) = {Author}, nameof(Pages) = {Pages}"
  }
}
```

## sizeof Operator
Cela permet de récupérer la taille en bytes (8 bits) d'un type. Par exemple, sizeof(int) retourne 4 car c'est la taille d'un int. C'est pratique pour manipuler des bytes, on peut créer des byteArray

```
byte[] byteArray = new byte[sizeof(int) *4];
```
Une bonne pratique est de mettre sizeof(int) plutôt que 4 car cela explique le choix du chiffre 4

## Bit Fields
Il est facile d'oublier que les variables sont avant tout une allocation de mémoire à une valeur en bits. Il est intéressant donc d'utiliser les bits directement pour traduire des données. C'est tres utile dans les data fields.

Par exemple, pour gérer les droits sur un forum, plutôt que d'utiliser un bool qui prend un byte, il est intéressant d'utiliser des bits :

```
Not Used - 0
Account Suspended - 0
Can Create Threads - 1
Can Edit own Post - 1
Can delete other's post - 0
Can edit other's post - 1
Can vote on posts - 1
Can create posts - 1
```

Si on prend les permissions ci-dessus, cela nous donne 00110111 (un byte) avec toutes les permissions de chaque utilisateur. Cela peut aussi être traduit en code hexadecimal, en l'occurence 37. Dans cette situation, c'est le binaire qui nous intéresse car cela symbolise une série de bool representant les droits d'un utilisateurs.

Il est possible de stocker ces variables dans des ints avec des mots clés comme :
```
int binaryNumber = 0b00110111; // 0b
int hexaNumber = 0x37; // 0x
```

### bit shift operators
Il est possible de déplacer les bits d'un certain nombres vers la droite ou vers la gauche grâce aux operators << & >>
```
int result = 0b00110111 >> 2 // decale de 2 vers la droite, ce qui donne 0b00001101
int result = 0b00110111 << 2 // decale de 2 vers la gauche, ce qui donne 0b11011100
```

### Bitwise logical operators
Les operators en bits sont les versions mono de and et or, c'est à dire && => & et || devient |. Ces operators vont parcourir tous les bits un à la fois et vont dire 1 = true, 0 = false.

Par exemple,
```
01010101
11111111
```
avec le "&", cela va regarder chaque série de bits (haut et bas) et s'il y a un 0, cela donnera 0 car, on a pris and. Si, on avait pris or, il suffirait d'avoir 1 pour donner 1.

```
01010101 => Valeur A
11111111 => Valeur B
01010101 => AND
11111111 => OR

// Code
int a = 0b01010101;
int b= 0b11111111;

int combinedWithAnd = a & b // 01010101
int combinedWithOr = a | b // 11111111
```

Le dernier bit operator est XOR. Il retourne vrai si l'un est vrai MAIS pas l'autre, c'est exclusif. Exemple
```
01010101 => Valeur A
11111111 => Valeur B
10101010 => XOR

int combinedWithXor = a ^b;
```

Enfin, le dernier oéprator est ~ qui est le complement, c'est à dire que comme ! il donnne l'inverse, donc il prend les bits et donne leur inverse
```
int a = 0b01010101;
int complementA = ~a; // ce qui donnera 0b10101010
```

Enfin tous les operateurs ont equivalent comme +=, c'est à dire
```
int number = 0b00001101;
number <<=1; // number = number << 1
number >>=1  // number = number >> 1
number &= 16 // number = number & 16
number|= 20  // number = number | 20
number ^= 32 // number = number ^32
```

### Enumeration Flags
> tres bon exemple sur la doc Microsoft

 [Microsoft Doc](https://docs.microsoft.com/en-us/dotnet/api/system.flagsattribute?view=netcore-3.1)

 Cela permet d'utiliser les bits comme Enumerations :
 ```
[flags]
public enum ForumPrivileges
{
  CreatePosts = 1 << 0,    // 1   00000001
  EditOwnPosts = 1 << 1,   // 2   00000010
  VoteOnPosts = 1 << 2,    // 4   00000100
  EditAnyPosts = 1 << 3,   // 8   00001000
  deletePosts = 1 << 4,    // 16  00010000
  CreateThreads = 1 << 5,  // 32  00100000
  Suspended = 1 << 6,      // 64  01000000

  // comme dans la doc microsoft, on peut aller plus vite en faisant, le << sont la pour la démonstration
  None = 0
  BasicUser = CreatePosts | EditOwnPosts | VoteOnPosts,
  // cela permet de créer un basic user avec les valeurs suivantes
  00000001 - CreatePosts
  00000010 - EditOwnPosts
  00000100 - VoteOnPosts
  00000111 - Combinaison des 3 valeurs avec Or

  Administrator = BasicUser | EditAnyPosts | deletePosts | CreateThreads // ce qui donne 00111111
}
 ```
 C'est à dire qu'avec le shift, on peut avoir un seul bits à comparer et facilement savoir si la personne a les droits et on peut aussi attribuer des droits avec le | ou en enlever avec le XOR (XOR permet de toggle plus que d'enlever) :

```
ForumPrivileges privileges = ForumPrivileges.BasicUser;
privileges |= ForumPrivileges.Suspended;

00000111 - basic users
01000000 - suspended
01000111 - nouveau privileges avec OR

// inversement
privileges ^= ForumPrivileges.EditOwnPosts;
01000111 - etat des privileges del 'user'
00000010 - Edit Own post
01000101 - Nouveau privileges avec XOR
```

Enfin, & permet de savoir si un element est activé

```
bool isSuspended = (privileges & ForumPrivileges.Suspended) == forum.Suspended
01000111 - privileges
01000000 - Suspended
01000000 - resultat AND
```

## Reflection
