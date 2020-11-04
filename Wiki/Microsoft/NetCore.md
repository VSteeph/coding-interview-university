# .NET CORE

## Présentation

Il y a plusieurs modeles d'applications en .NET :
- MVC application (Model View Controller)
- Razor Pages Application

### Evolution de Asp.Net
(1996) Active Server Pages (ASP), cela a permis d'avoir du scripting server side pour des pages dynamiques.

(2002) création des forms avec .NET webforms, mais cela avait le défaut d'avoir beaucoup de données trasnferés entre le server et le site.

(2009) ASP.NET MVC, ils ont essayé de régler la probleme de .Webform, il est opensource, mais il avait ses propres défauts car il était basé sur .Net webforms

(2016) ASP.NET CORE, elle a été crée sur .NET Core, qui est la premiere plateforme de .NET et donc n'est pas lié à windows.

Le développement d'ASP NET CORE a été tres active ASP.NET CORE 2 en 2017 et CORE 3 en 2019 (donc *Visual Studio 2019* mais pas obligé d'avoir SQL-server 2019 même si c'est mieux)

La version 3.0 inclut "meta package" comme une partie de NET core. Entity framework a été enlevé du meta package et a son propre nuget pacckage maintenant.

## Intro

### Création d'un projet
- Type de projet (classic) puis custom
- Stack à choisir (.NET Framework / .NET CORE)
- .NET CORE version
- Template à choisir (Empty, MVC, Razor, Angular, Web App)
- Authentication pour l'appli (Systeme de Login ou autre)
- Docker Support & HTTPS

### Razor Pages
Introduit en 2.0, elles sont devenus la façon par défaut
https://docs.microsoft.com/en-us/aspnet/core/razor-pages/?view=aspnetcore-3.1&tabs=visual-studio

Elles permettent de mieux organiser son code en ayant la logique implenté et le view modele proche.

Elles ont les mêmes fonctions que le MVC (Routing, Models, ActionResult, Tags, Helpers, ...)

Les Razor Pages ont 2 parties :
- Razor PAge (UI/View)
- Page Model (Contains Handlers)

Comme pour le XAML, une page est divisé en C# et en UI (HTML au lieu de XAMl pour les Razor pages), le @model doit avoir la même nomenclature que la classe C#.

### Specific files

#### .Csproj
il a un peu changé avec .NET core. La façon principal d'ajouter d'est références comme pour la librairie standard est le Nugget Package.

Il n'y a plus certains fichiers comme le project json.

#### LaunchSettings.json

Ce sont les informations nécessaires pour Run le projet, il est possible d'avoir plusieurs profils (c'est le cas par défaut).

Le premier profil est IIS Express (localHost) et met l'environnement variables à developpement.
