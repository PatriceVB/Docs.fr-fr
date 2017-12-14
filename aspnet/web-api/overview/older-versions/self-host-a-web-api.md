---
uid: web-api/overview/older-versions/self-host-a-web-api
title: "Auto-hébergement ASP.NET Web API 1 (c#) | Documents Microsoft"
author: MikeWasson
description: "API Web ASP.NET ne requiert pas d’IIS. Vous pouvez auto-hébergement une API web dans votre propre processus d’hébergement. Ce didacticiel montre comment héberger une API web à l’intérieur d’une console applic..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2012
ms.topic: article
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: b308ee9ec209ba8bbb021827655c83443dd149e6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="0d5f1-105">Auto-hébergement ASP.NET Web API 1 (c#)</span><span class="sxs-lookup"><span data-stu-id="0d5f1-105">Self-Host ASP.NET Web API 1 (C#)</span></span>
====================
<span data-ttu-id="0d5f1-106">par [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0d5f1-106">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="0d5f1-107">API Web ASP.NET ne requiert pas d’IIS.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-107">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="0d5f1-108">Vous pouvez auto-hébergement une API web dans votre propre processus d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-108">You can self-host a web API in your own host process.</span></span> <span data-ttu-id="0d5f1-109">Ce didacticiel montre comment héberger une API web à l’intérieur d’une application console.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-109">This tutorial shows how to host a web API inside a console application.</span></span>
> 
> <span data-ttu-id="0d5f1-110">**Nouvelles applications doivent utiliser OWIN pour l’auto-hébergement API Web.**</span><span class="sxs-lookup"><span data-stu-id="0d5f1-110">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="0d5f1-111">Consultez [OWIN permet d’auto-hébergement ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="0d5f1-111">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="0d5f1-112">Versions du logiciel utilisées dans le didacticiel</span><span class="sxs-lookup"><span data-stu-id="0d5f1-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="0d5f1-113">API Web 1</span><span class="sxs-lookup"><span data-stu-id="0d5f1-113">Web API 1</span></span>
> - <span data-ttu-id="0d5f1-114">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="0d5f1-114">Visual Studio 2012</span></span>


## <a name="create-the-console-application-project"></a><span data-ttu-id="0d5f1-115">Créer le projet d’Application Console</span><span class="sxs-lookup"><span data-stu-id="0d5f1-115">Create the Console Application Project</span></span>

<span data-ttu-id="0d5f1-116">Démarrez Visual Studio et sélectionnez **nouveau projet** à partir de la **Démarrer** page.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-116">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="0d5f1-117">Ou, à partir de la **fichier** menu, sélectionnez **nouveau** , puis **projet**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-117">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="0d5f1-118">Dans le **modèles** volet, sélectionnez **modèles installés** et développez le **Visual C#** nœud.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-118">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="0d5f1-119">Sous **Visual C#**, sélectionnez **Windows**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-119">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="0d5f1-120">Dans la liste des modèles de projet, sélectionnez **Application Console**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-120">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="0d5f1-121">Nommez le projet &quot;SelfHost&quot; et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-121">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="0d5f1-122">Définir le Framework cible (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="0d5f1-122">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="0d5f1-123">Si vous utilisez Visual Studio 2010, modifier le framework cible pour le .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-123">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="0d5f1-124">(Par défaut, le modèle de projet cible le [du profil .net Framework Client](https://msdn.microsoft.com/en-us/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span><span class="sxs-lookup"><span data-stu-id="0d5f1-124">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/en-us/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="0d5f1-125">Dans l’Explorateur de solutions, cliquez sur le projet et sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-125">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="0d5f1-126">Dans le **framework cible** déroulante liste, de modifier le framework cible pour le .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-126">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="0d5f1-127">Lorsque vous êtes invité à appliquer la modification, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-127">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="0d5f1-128">Installer le Gestionnaire de Package NuGet</span><span class="sxs-lookup"><span data-stu-id="0d5f1-128">Install NuGet Package Manager</span></span>

<span data-ttu-id="0d5f1-129">Le Gestionnaire de Package NuGet est le moyen le plus simple pour ajouter les assemblys de l’API Web à un projet non-ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-129">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="0d5f1-130">Pour vérifier si le Gestionnaire de Package NuGet est installé, cliquez sur le **outils** menu dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-130">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="0d5f1-131">Si vous voyez un élément de menu appelé **Gestionnaire de Package de bibliothèque**, vous devez le Gestionnaire de Package NuGet.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-131">If you see a menu item called **Library Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="0d5f1-132">Pour installer le Gestionnaire de Package NuGet :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-132">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="0d5f1-133">Démarrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-133">Start Visual Studio.</span></span>
2. <span data-ttu-id="0d5f1-134">À partir de la **outils** menu, sélectionnez **Extensions et mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-134">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="0d5f1-135">Dans le **Extensions et mises à jour** boîte de dialogue, sélectionnez **Online**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-135">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="0d5f1-136">Si vous ne voyez pas « Gestionnaire de Package NuGet », tapez « Gestionnaire de package nuget » dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-136">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="0d5f1-137">Sélectionnez le Gestionnaire de Package NuGet et cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-137">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="0d5f1-138">Une fois le téléchargement terminé, vous devrez installer.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-138">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="0d5f1-139">Une fois l’installation terminée, vous pouvez être invité à redémarrer Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-139">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="0d5f1-140">Ajoutez le Package NuGet de l’API Web</span><span class="sxs-lookup"><span data-stu-id="0d5f1-140">Add the Web API NuGet Package</span></span>

<span data-ttu-id="0d5f1-141">Une fois que le Gestionnaire de Package NuGet est installé, ajoutez le package de Self-Host d’API Web à votre projet.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-141">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="0d5f1-142">À partir de la **outils** menu, sélectionnez **Gestionnaire de Package de bibliothèque**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-142">From the **Tools** menu, select **Library Package Manager**.</span></span> <span data-ttu-id="0d5f1-143">*Remarque*: Si ne vous voyez pas ce menu d’élément, assurez-vous que ce gestionnaire de Package NuGet installé correctement.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-143">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="0d5f1-144">Sélectionnez **gérer les Packages NuGet pour la Solution...**</span><span class="sxs-lookup"><span data-stu-id="0d5f1-144">Select **Manage NuGet Packages for Solution...**</span></span>
3. <span data-ttu-id="0d5f1-145">Dans le **gérer les Packages pépite** boîte de dialogue, sélectionnez **Online**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-145">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="0d5f1-146">Dans la zone de recherche, tapez &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-146">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="0d5f1-147">Sélectionnez le package ASP.NET Web API Self Host et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-147">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="0d5f1-148">Une fois le package installé, cliquez sur **fermer** pour fermer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-148">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="0d5f1-149">Veillez à installer le package nommé Microsoft.AspNet.WebApi.SelfHost, AspNetWebApi.SelfHost pas.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-149">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>


![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="0d5f1-150">Créer le modèle et le contrôleur</span><span class="sxs-lookup"><span data-stu-id="0d5f1-150">Create the Model and Controller</span></span>

<span data-ttu-id="0d5f1-151">Ce didacticiel utilise les mêmes classes de modèle et du contrôleur en tant que le [mise en route](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-151">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="0d5f1-152">Ajoutez une classe publique nommée `Product`.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-152">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="0d5f1-153">Ajoutez une classe publique nommée `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-153">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="0d5f1-154">Dériver de cette classe à partir de **System.Web.Http.ApiController**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-154">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="0d5f1-155">Pour plus d’informations sur le code de ce contrôleur, consultez le [mise en route](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-155">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="0d5f1-156">Ce contrôleur définit trois actions GET :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-156">This controller defines three GET actions:</span></span>

| <span data-ttu-id="0d5f1-157">URI</span><span class="sxs-lookup"><span data-stu-id="0d5f1-157">URI</span></span> | <span data-ttu-id="0d5f1-158">Description</span><span class="sxs-lookup"><span data-stu-id="0d5f1-158">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0d5f1-159">produits/api /</span><span class="sxs-lookup"><span data-stu-id="0d5f1-159">/api/products</span></span> | <span data-ttu-id="0d5f1-160">Obtenir une liste de tous les produits.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-160">Get a list of all products.</span></span> |
| <span data-ttu-id="0d5f1-161">/API/produits/*id*</span><span class="sxs-lookup"><span data-stu-id="0d5f1-161">/api/products/*id*</span></span> | <span data-ttu-id="0d5f1-162">Obtenir un produit par ID.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-162">Get a product by ID.</span></span> |
| <span data-ttu-id="0d5f1-163">/ API/produits / ? catégorie =*catégorie*</span><span class="sxs-lookup"><span data-stu-id="0d5f1-163">/api/products/?category=*category*</span></span> | <span data-ttu-id="0d5f1-164">Obtenir une liste de produits par catégorie.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-164">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="0d5f1-165">Hôte de l’API Web</span><span class="sxs-lookup"><span data-stu-id="0d5f1-165">Host the Web API</span></span>

<span data-ttu-id="0d5f1-166">Ouvrez le fichier Program.cs et ajoutez le code suivant à l’aide des instructions :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-166">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="0d5f1-167">Ajoutez le code suivant à la **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-167">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="0d5f1-168">(Facultatif) Ajouter une réservation Namespace d’URL HTTP</span><span class="sxs-lookup"><span data-stu-id="0d5f1-168">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="0d5f1-169">Cette application écoute `http://localhost:8080/`.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-169">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="0d5f1-170">Par défaut, à l’écoute sur une adresse HTTP particulière nécessite des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-170">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="0d5f1-171">Lorsque vous exécutez le didacticiel, par conséquent, vous obtiendrez cette erreur : « HTTP n’a pas inscrire URL http://+:8080/ » il existe deux façons d’éviter cette erreur :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-171">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="0d5f1-172">Exécuter Visual Studio avec des autorisations d’administrateur élevés, ou</span><span class="sxs-lookup"><span data-stu-id="0d5f1-172">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="0d5f1-173">Utilisation de Netsh.exe pour accorder des autorisations de votre compte pour réserver l’URL.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-173">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="0d5f1-174">Pour utiliser Netsh.exe, ouvrez une invite de commandes avec des privilèges d’administrateur et entrez la commande suivante de la commande : suivantes :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-174">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="0d5f1-175">où *Machine\nom d’utilisateur* est votre compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-175">where *machine\username* is your user account.</span></span>

<span data-ttu-id="0d5f1-176">Lorsque vous avez terminé l’auto-hébergement, veillez à supprimer la réservation :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-176">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="0d5f1-177">Appeler l’API Web à partir d’une Application cliente (c#)</span><span class="sxs-lookup"><span data-stu-id="0d5f1-177">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="0d5f1-178">Nous allons écrire une application console simple qui appelle l’API web.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-178">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="0d5f1-179">Ajouter un nouveau projet d’application console à la solution :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-179">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="0d5f1-180">Dans l’Explorateur de solutions, cliquez sur la solution et sélectionnez **ajouter un nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-180">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="0d5f1-181">Créez une application console nommée &quot;ClientApp&quot;.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-181">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="0d5f1-182">Utilisez le Gestionnaire de Package NuGet pour ajouter le package ASP.NET Web API Core Libraries :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-182">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="0d5f1-183">Dans le menu Outils, sélectionnez **Gestionnaire de Package de bibliothèque**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-183">From the Tools menu, select **Library Package Manager**.</span></span>
- <span data-ttu-id="0d5f1-184">Sélectionnez **gérer les Packages NuGet pour la Solution...**</span><span class="sxs-lookup"><span data-stu-id="0d5f1-184">Select **Manage NuGet Packages for Solution...**</span></span>
- <span data-ttu-id="0d5f1-185">Dans le **gérer les Packages NuGet** boîte de dialogue, sélectionnez **Online**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-185">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="0d5f1-186">Dans la zone de recherche, tapez &quot;Microsoft.AspNet.WebApi.Client&quot;.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-186">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="0d5f1-187">Sélectionnez le package Microsoft ASP.NET Web API Client Libraries et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-187">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="0d5f1-188">Ajoutez une référence dans ClientApp au projet SelfHost :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-188">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="0d5f1-189">Dans l’Explorateur de solutions, cliquez sur le projet ClientApp.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-189">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="0d5f1-190">Sélectionnez **ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-190">Select **Add Reference**.</span></span>
- <span data-ttu-id="0d5f1-191">Dans le **Gestionnaire de références** boîte de dialogue, sous **Solution**, sélectionnez **projets**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-191">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="0d5f1-192">Sélectionnez le projet SelfHost.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-192">Select the SelfHost project.</span></span>
- <span data-ttu-id="0d5f1-193">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-193">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="0d5f1-194">Ouvrez le fichier Client/Program.cs.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-194">Open the Client/Program.cs file.</span></span> <span data-ttu-id="0d5f1-195">Ajoutez le code suivant **à l’aide de** instruction :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-195">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="0d5f1-196">Ajouter un mappage statique **HttpClient** instance :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-196">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="0d5f1-197">Ajoutez les méthodes suivantes pour répertorier tous les produits, un produit par l’ID de liste et répertorient les produits par catégorie.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-197">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="0d5f1-198">Chacune de ces méthodes suit le même modèle :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-198">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="0d5f1-199">Appelez **HttpClient.GetAsync** pour envoyer une requête GET à l’URI approprié.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-199">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="0d5f1-200">Appelez **HttpResponseMessage.EnsureSuccessStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-200">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="0d5f1-201">Cette méthode lève une exception si l’état de réponse HTTP est un code d’erreur.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-201">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="0d5f1-202">Appelez **ReadAsAsync&lt;T&gt;**  pour désérialiser un type CLR de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-202">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="0d5f1-203">Cette méthode est une méthode d’extension, définie dans **System.Net.Http.HttpContentExtensions**.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-203">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="0d5f1-204">Le **GetAsync** et **ReadAsAsync** méthodes sont asynchrones.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-204">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="0d5f1-205">Elles retournent **tâche** objets qui représentent l’opération asynchrone.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-205">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="0d5f1-206">Obtention de la **résultat** propriété bloque le thread jusqu'à ce que l’opération se termine.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-206">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="0d5f1-207">Pour plus d’informations sur l’utilisation du client HTTP, y compris comment effectuer des appels non bloquant, consultez [appeler une Web API d’un Client .NET](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="0d5f1-207">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="0d5f1-208">Avant d’appeler ces méthodes, définissez la propriété BaseAddress sur l’instance de client HTTP pour «`http://localhost:8080`».</span><span class="sxs-lookup"><span data-stu-id="0d5f1-208">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="0d5f1-209">Exemple :</span><span class="sxs-lookup"><span data-stu-id="0d5f1-209">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="0d5f1-210">Il doit le résultat suivant.</span><span class="sxs-lookup"><span data-stu-id="0d5f1-210">This should output the following.</span></span> <span data-ttu-id="0d5f1-211">(N’oubliez pas à exécuter l’application SelfHost en premier).</span><span class="sxs-lookup"><span data-stu-id="0d5f1-211">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)