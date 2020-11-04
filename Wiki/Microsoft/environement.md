# Microsoft

## Organisation général

### Common Language Infrastructure (CLI)
Cela permet d'avoir un code exécutable dans un environnement en runtime qui supporte plusieurs langages de haut niveau et sur différentes plateformes sans avoir à ré-écrire des architectures spécifiques.

![orga](img/orga.png)

Microsoft utilise un intermediate Language (IL) ou (CIL) Common Intermediate Language pour définir les instructions binaires et se rapproche de l'architecture des CPU. C'est à dire que les données sont push dans des stacks plutôt que tirer de registre. Le langage est orienté objet et stack-based

## .Net (.NET Platform)

L'avantage de cet outil est de prendre en compte tout ce qui est commun aux applications pour que les développeurs puissent se concentrer sur leur spécificité et pas le fonctionnement générique.

![diagram](img/diagram_ms.png)

On peut voir qu'il y a 3 couches. La premiere est l'Infrastructure qui est partagé par tout l'éco-systeme, c'est ce qui va permettre de créer le runtime avec le CLR (Common Language Runtime) et le CIL (Common Intermediate language).

Construit sur cette base, on obtient la librairie .NET standard qui permettent d'avoir une vaste collection de code pour s'occuper des taches récurentes comme le networking, file system acces, etc. C'est un code qui est utilisabble sur n'importe quel type d'application.

Enfin, la derniere couche est divisé en plusieurs parties. Ce sont différents stacks / implementation de la platforme .NET. Il y a plusieurs stacks, mais les 3 du diagrame sont les principaux. Ils ont toutes une configuration de .NET particuliere. Certains éléments comme le CLR peuvent être remplacés par des éléments compatibles. Dans certains cas, même la librairie  standard peut être remplacer.

Chacun de ces stacks sont crées avec des utilités spécifiques. Par exemple, .NET Framework est adapté pour les machine windows, c'est le plus vieux et le plus gros, tandis que le .Core est plus récent, plus léger et multiplateforme.

Ces stacks supportent un certain nombre d'app models, c'est à dire une librairie dédié à créer un type d'app  en particulier.

## Terminologie
Le terme .NET Framework peut être confus car il est utilisé dans plusieurs cas :
- L'ecosysteme entier (.NET platform)
- Le stack .NET framework (comme Xamarin ou .NET core)
- Template a quoi doit ressembler un stack

## Specificité
