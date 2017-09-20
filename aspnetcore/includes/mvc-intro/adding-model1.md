# <a name="adding-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="3db8e-101">Ajout d’un modèle dans une application ASP.NET Core MVC</span><span class="sxs-lookup"><span data-stu-id="3db8e-101">Adding a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="3db8e-102">Par [Rick Anderson](https://twitter.com/RickAndMSFT) et [Ryan Nowak](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="3db8e-102">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="3db8e-103">Dans cette section, vous ajoutez des classes pour la gestion des films d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="3db8e-103">In this section, you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="3db8e-104">Ces classes constituent la partie « **M**odèle » de l’application **M**VC.</span><span class="sxs-lookup"><span data-stu-id="3db8e-104">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="3db8e-105">Vous utilisez ces classes avec [Entity Framework Core](https://docs.microsoft.com/ef/core) (EF Core) pour travailler avec une base de données.</span><span class="sxs-lookup"><span data-stu-id="3db8e-105">You use these classes with [Entity Framework Core](https://docs.microsoft.com/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="3db8e-106">EF Core est un framework de mappage relationnel d’objets qui simplifie le code d’accès aux données à écrire.</span><span class="sxs-lookup"><span data-stu-id="3db8e-106">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span> <span data-ttu-id="3db8e-107">[EF Core prend en charge de nombreux moteurs de base de données](https://docs.microsoft.com/ef/core/providers/).</span><span class="sxs-lookup"><span data-stu-id="3db8e-107">[EF Core supports many database engines](https://docs.microsoft.com/ef/core/providers/).</span></span>

<span data-ttu-id="3db8e-108">Les classes de modèle que vous créez portent le nom de classes OCT (« Objet CLR Traditionnel »), car elles n’ont pas de dépendances envers EF Core.</span><span class="sxs-lookup"><span data-stu-id="3db8e-108">The model classes you'll create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="3db8e-109">Elles définissent simplement les propriétés des données stockées dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="3db8e-109">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="3db8e-110">Dans ce didacticiel, vous écrivez d’abord les classes du modèle, puis EF Core crée la base de données.</span><span class="sxs-lookup"><span data-stu-id="3db8e-110">In this tutorial you'll write the model classes first, and EF Core will create the database.</span></span> <span data-ttu-id="3db8e-111">Une autre approche que nous ne décrivons pas ici consiste à générer les classes du modèle à partir d’une base de données déjà existante.</span><span class="sxs-lookup"><span data-stu-id="3db8e-111">An alternate approach not covered here is to generate model classes from an already-existing database.</span></span> <span data-ttu-id="3db8e-112">Pour plus d’informations sur cette approche, consultez [Getting Started with EF Core on ASP.NET Core with an Existing Database](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db).</span><span class="sxs-lookup"><span data-stu-id="3db8e-112">For information about that approach, see [ASP.NET Core - Existing Database](https://docs.microsoft.com/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="3db8e-113">Ajouter une classe de modèle de données</span><span class="sxs-lookup"><span data-stu-id="3db8e-113">Add a data model class</span></span>