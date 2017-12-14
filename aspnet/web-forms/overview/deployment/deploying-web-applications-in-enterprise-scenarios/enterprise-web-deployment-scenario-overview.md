---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: "Déploiement Web d’entreprise : Vue d’ensemble du scénario | Documents Microsoft"
author: jrjlee
description: "Cet ensemble de didacticiels utilise un exemple de solution avec un niveau réaliste de complexité, ainsi que d’un scénario de déploiement d’une entreprise fictive, pour fournir une référence..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/03/2012
ms.topic: article
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: f90db22bf98456661c530e728e854ce109aec6fd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2017
---
<a name="enterprise-web-deployment-scenario-overview"></a><span data-ttu-id="c12d8-103">Déploiement Web d’entreprise : Vue d’ensemble du scénario</span><span class="sxs-lookup"><span data-stu-id="c12d8-103">Enterprise Web Deployment: Scenario Overview</span></span>
====================
<span data-ttu-id="c12d8-104">par [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c12d8-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c12d8-105">Télécharger le PDF</span><span class="sxs-lookup"><span data-stu-id="c12d8-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c12d8-106">Cet ensemble de didacticiels utilise un exemple de solution avec un niveau réaliste de complexité, ainsi que d’un scénario de déploiement d’une entreprise fictive, pour fournir une implémentation de référence et pour donner les tâches et les procédures pas à pas un contexte commun.</span><span class="sxs-lookup"><span data-stu-id="c12d8-106">This set of tutorials uses a sample solution with a realistic level of complexity, together with a fictional enterprise deployment scenario, to provide a reference implementation and to give the tasks and walkthroughs a common context.</span></span> <span data-ttu-id="c12d8-107">Cette rubrique décrit le scénario du didacticiel et présente l’exemple de solution.</span><span class="sxs-lookup"><span data-stu-id="c12d8-107">This topic describes the tutorial scenario and introduces the sample solution.</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c12d8-108">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c12d8-108">Scenario Description</span></span>

<span data-ttu-id="c12d8-109">Fabrikam, Inc., une société fictive, consiste à créer une solution qui permet aux équipes de ventes à distance de stocker et récupérer des informations de contact à partir d’une interface web.</span><span class="sxs-lookup"><span data-stu-id="c12d8-109">Fabrikam, Inc., a fictitious company, is creating a solution that lets remote sales teams store and retrieve contact information from a web interface.</span></span>

<span data-ttu-id="c12d8-110">Les processus d’Application Lifecycle Management (ALM) chez Fabrikam, Inc. nécessitent la solution pour le déploiement sur trois environnements de serveur à différentes étapes du processus de développement logiciel :</span><span class="sxs-lookup"><span data-stu-id="c12d8-110">The Application Lifecycle Management (ALM) processes at Fabrikam, Inc. require the solution to be deployed to three server environments at various stages of the software development process:</span></span>

- <span data-ttu-id="c12d8-111">Un environnement de test ou de « bac à sable » développeur.</span><span class="sxs-lookup"><span data-stu-id="c12d8-111">A developer test or "sandbox" environment.</span></span>
- <span data-ttu-id="c12d8-112">Un environnement de mise en lots basée sur l’intranet.</span><span class="sxs-lookup"><span data-stu-id="c12d8-112">An intranet-based staging environment.</span></span>
- <span data-ttu-id="c12d8-113">Un environnement de production sur Internet.</span><span class="sxs-lookup"><span data-stu-id="c12d8-113">An Internet-facing production environment.</span></span>

<span data-ttu-id="c12d8-114">Chacun de ces environnements a des exigences de sécurité et de configuration différents, et chaque pose des défis de déploiement unique.</span><span class="sxs-lookup"><span data-stu-id="c12d8-114">Each of these environments has different configuration and security requirements, and each poses unique deployment challenges.</span></span>

### <a name="the-fabrikam-inc-server-infrastructure"></a><span data-ttu-id="c12d8-115">Le Fabrikam, Inc. Infrastructure de serveur</span><span class="sxs-lookup"><span data-stu-id="c12d8-115">The Fabrikam, Inc. Server Infrastructure</span></span>

<span data-ttu-id="c12d8-116">Ceci est l’infrastructure de développement et de déploiement de haut niveau chez Fabrikam, Inc.</span><span class="sxs-lookup"><span data-stu-id="c12d8-116">This is the high-level development and deployment infrastructure at Fabrikam, Inc.</span></span>

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

<span data-ttu-id="c12d8-117">Les stations de travail du développeur, l’infrastructure de contrôle de code source, l’environnement de développement de test et l’environnement intermédiaire que tous résider sur le réseau intranet au sein du domaine Fabrikam.net.</span><span class="sxs-lookup"><span data-stu-id="c12d8-117">The developer workstations, the source control infrastructure, the developer test environment, and the staging environment all reside on the intranet network within the Fabrikam.net domain.</span></span> <span data-ttu-id="c12d8-118">L’environnement de production se trouve sur un réseau de périmètre (également appelé DMZ, zone démilitarisée et sous-réseau filtré), qui est isolé du réseau intranet par un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="c12d8-118">The production environment resides on a perimeter network (also known as DMZ, demilitarized zone, and screened subnet), which is isolated from the intranet network by a firewall.</span></span> <span data-ttu-id="c12d8-119">Il s’agit d’un scénario de déploiement courant : en général, vous isolez vos serveurs de web exposés à Internet à partir de votre infrastructure de serveur interne via l’utilisation de pare-feu ou des serveurs de passerelle.</span><span class="sxs-lookup"><span data-stu-id="c12d8-119">This is a common deployment scenario: you typically isolate your Internet-facing web servers from your internal server infrastructure through the use of firewalls or gateway servers.</span></span>

<span data-ttu-id="c12d8-120">Dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="c12d8-120">In this example:</span></span>

- <span data-ttu-id="c12d8-121">Un serveur Team Foundation Server (TFS) 2010 avec un serveur de builds distincts fournit des fonctionnalités d’intégration continue (CI) et de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="c12d8-121">A Team Foundation Server (TFS) 2010 server with a separate build server provides source control and continuous integration (CI) functionality.</span></span>
- <span data-ttu-id="c12d8-122">L’environnement de test développeur inclut un serveur web d’Internet Information Services (IIS) 7.5 et un serveur de base de données SQL Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="c12d8-122">The developer test environment includes an Internet Information Services (IIS) 7.5 web server and a SQL Server 2008 R2 database server.</span></span>
- <span data-ttu-id="c12d8-123">L’environnement de production comprend plusieurs serveurs web d’IIS 7.5 synchronisées par un serveur de contrôleur de Web Farm Framework (WFF), ainsi que d’un serveur de base de données SQL Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="c12d8-123">The production environment includes multiple IIS 7.5 web servers synchronized by a Web Farm Framework (WFF) controller server, together with a SQL Server 2008 R2 database server.</span></span> <span data-ttu-id="c12d8-124">Dans la pratique, le serveur de base de données peut utiliser le clustering ou la mise en miroir pour améliorer l’évolutivité et la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="c12d8-124">In practice, the database server may use clustering or mirroring to improve scalability and availability.</span></span>
- <span data-ttu-id="c12d8-125">L’environnement intermédiaire est conçu pour répliquer la configuration de l’environnement de production aussi fidèlement que possible.</span><span class="sxs-lookup"><span data-stu-id="c12d8-125">The staging environment is designed to replicate the configuration of the production environment as closely as possible.</span></span>
- <span data-ttu-id="c12d8-126">Les stratégies d’isolation réseau et de pare-feu ne permettent pas de déploiement direct, automatisé à partir de l’intranet pour le réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="c12d8-126">The firewall and network isolation policies do not permit direct, automated deployment from the intranet to the perimeter network.</span></span>

<span data-ttu-id="c12d8-127">La configuration de chacun de ces environnements est décrite plus en détail dans le deuxième didacticiel [configuration des environnements de serveur pour le déploiement Web](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c12d8-127">The configuration of each of these environments is described in more detail in the second tutorial, [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

### <a name="team-roles-for-alm"></a><span data-ttu-id="c12d8-128">Rôles de l’équipe pour ALM</span><span class="sxs-lookup"><span data-stu-id="c12d8-128">Team Roles for ALM</span></span>

<span data-ttu-id="c12d8-129">Ces utilisateurs sont impliqués dans la création, la gestion, la création et la publication de la solution de gestionnaire de contacts :</span><span class="sxs-lookup"><span data-stu-id="c12d8-129">These users are involved in creating, managing, building, and publishing the Contact Manager solution:</span></span>

- <span data-ttu-id="c12d8-130">Matt Hink est un développeur d’applications web Fabrikam, Inc. Il est membre de l’équipe qui a développé une solution de gestionnaire de contacts à l’aide de Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="c12d8-130">Matt Hink is a web application developer at Fabrikam, Inc. He is part of the team who developed the Contact Manager solution by using Visual Studio 2010.</span></span> <span data-ttu-id="c12d8-131">Matt dispose des droits d’administrateur complets sur les serveurs dans l’environnement de test de développeur, ce qui lui permet de configurer l’environnement pour répondre à ses besoins.</span><span class="sxs-lookup"><span data-stu-id="c12d8-131">Matt has full administrator rights on the servers in the developer test environment, which lets him configure the environment to meet his needs.</span></span> <span data-ttu-id="c12d8-132">Il possède également l’accès utilisateur à l’instance de Visual Studio 2010 TFS où il stocke le code source pour la solution de gestionnaire de contacts.</span><span class="sxs-lookup"><span data-stu-id="c12d8-132">He also has user access to the Visual Studio 2010 TFS instance where he stores the source code for the Contact Manager solution.</span></span>
- <span data-ttu-id="c12d8-133">Rob Walters est un administrateur de serveur pour l’équipe de développement de Fabrikam, Inc.</span><span class="sxs-lookup"><span data-stu-id="c12d8-133">Rob Walters is a server administrator for the Fabrikam, Inc. development team.</span></span> <span data-ttu-id="c12d8-134">Rob a un accès administratif sur le serveur TFS pour qu’il peut configurer tous les aspects de TFS et Team Build.</span><span class="sxs-lookup"><span data-stu-id="c12d8-134">Rob has administrative access on the TFS server so that he can configure all aspects of TFS and Team Build.</span></span> <span data-ttu-id="c12d8-135">Rob également avec un accès administratif pour le test et les serveurs web intermédiaires et agit comme l’administrateur de base de données (DBA) pour les serveurs de base de données dans le test et l’environnement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="c12d8-135">Rob also has administrative access to the test and staging web servers and acts as the database administrator (DBA) for the database servers in the test and staging environments.</span></span> <span data-ttu-id="c12d8-136">Rob a configuré Team Build sur le serveur TFS pour effectuer ces tâches :</span><span class="sxs-lookup"><span data-stu-id="c12d8-136">Rob has configured Team Build on the TFS server to carry out these tasks:</span></span>

    - <span data-ttu-id="c12d8-137">Générer et exécuter des tests unitaires sur l’application chaque fois qu’un utilisateur archive un fichier à TFS.</span><span class="sxs-lookup"><span data-stu-id="c12d8-137">Build and run unit tests on the application whenever a user checks in a file to TFS.</span></span> <span data-ttu-id="c12d8-138">Il s’agit de l’élément de configuration.</span><span class="sxs-lookup"><span data-stu-id="c12d8-138">This is called CI.</span></span>
    - <span data-ttu-id="c12d8-139">Déployer l’application Gestionnaire de contacts à l’environnement de test automatiquement une fois que l’application transmet les tests unitaires.</span><span class="sxs-lookup"><span data-stu-id="c12d8-139">Deploy the Contact Manager application to the test environment automatically once the application passes unit tests.</span></span> <span data-ttu-id="c12d8-140">Cela inclut la base de données de publication pour les serveurs de test sur le déploiement initial et les mises à jour la base de données après le déploiement initial.</span><span class="sxs-lookup"><span data-stu-id="c12d8-140">This includes publishing the database to the test servers on initial deployment and any updates to the database after initial deployment.</span></span>
    - <span data-ttu-id="c12d8-141">Déployez l’application Gestionnaire de contacts dans l’environnement intermédiaire dans un processus de la seule étape.</span><span class="sxs-lookup"><span data-stu-id="c12d8-141">Deploy the Contact Manager application to the staging environment in a single-step process.</span></span>
    - <span data-ttu-id="c12d8-142">Créer un package Web un administrateur de serveur Web et un administrateur peuvent utiliser pour publier l’application sur l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c12d8-142">Create a Web package that a Web server administrator and a DBA can use to publish the application to the production environment.</span></span>
- <span data-ttu-id="c12d8-143">Lisa Andrews est responsable du déploiement d’applications sur les serveurs de production de Fabrikam, Inc. un administrateur du serveur.</span><span class="sxs-lookup"><span data-stu-id="c12d8-143">Lisa Andrews is a server administrator responsible for deploying applications to the Fabrikam, Inc. production servers.</span></span> <span data-ttu-id="c12d8-144">Elle dispose d’un accès en lecture au partage où l’équipe TFS Build stocke le package de déploiement web une fois qu’il génère l’application Gestionnaire de contacts.</span><span class="sxs-lookup"><span data-stu-id="c12d8-144">She has read access to the share where the TFS Team Build stores the web deployment package once it builds the Contact Manager application.</span></span> <span data-ttu-id="c12d8-145">Elle a également un accès administratif pour les serveurs web de production afin qu’elle peut déployer l’application en production.</span><span class="sxs-lookup"><span data-stu-id="c12d8-145">She also has administrative access to the production web servers so that she can deploy the application to production.</span></span> <span data-ttu-id="c12d8-146">En outre, elle agit en tant que l’administrateur qui déploie des mises à jour de la base de données et des bases de données sur le serveur de base de données dans l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c12d8-146">Additionally, she acts as the DBA who deploys databases and database updates to the database server in the production environment.</span></span>

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a><span data-ttu-id="c12d8-147">La Solution de gestionnaire de contacts</span><span class="sxs-lookup"><span data-stu-id="c12d8-147">The Contact Manager Solution</span></span>

<span data-ttu-id="c12d8-148">La solution de gestionnaire de contacts est conçue pour permettre aux utilisateurs inscrits, connecté en ajouter et modifier les informations de contact via une interface web.</span><span class="sxs-lookup"><span data-stu-id="c12d8-148">The Contact Manager solution is designed to let registered, logged-in users add and edit contact information through a web interface.</span></span> <span data-ttu-id="c12d8-149">La solution de gestionnaire de contacts se compose de quatre projets individuels :</span><span class="sxs-lookup"><span data-stu-id="c12d8-149">The Contact Manager solution consists of four individual projects:</span></span>

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- <span data-ttu-id="c12d8-150">**ContactManager.Mvc**.</span><span class="sxs-lookup"><span data-stu-id="c12d8-150">**ContactManager.Mvc**.</span></span> <span data-ttu-id="c12d8-151">Il s’agit d’un projet d’application web ASP.NET MVC3 qui représente le point d’entrée pour la solution.</span><span class="sxs-lookup"><span data-stu-id="c12d8-151">This is an ASP.NET MVC3 web application project that represents the entry point for the solution.</span></span> <span data-ttu-id="c12d8-152">Il offre des fonctionnalités d’application web de base, comme en fournissant aux utilisateurs la possibilité de créer et d’afficher les détails du contact.</span><span class="sxs-lookup"><span data-stu-id="c12d8-152">It offers some basic web application functionality, like providing users with the ability to create and view contact details.</span></span> <span data-ttu-id="c12d8-153">L’application s’appuie sur un service Windows Communication Foundation (WCF) pour gérer les contacts et une base de données de services application ASP.NET pour gérer l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="c12d8-153">The application relies on a Windows Communication Foundation (WCF) service to manage contacts and an ASP.NET application services database to manage authentication and authorization.</span></span>
- <span data-ttu-id="c12d8-154">**ContactManager.Database**.</span><span class="sxs-lookup"><span data-stu-id="c12d8-154">**ContactManager.Database**.</span></span> <span data-ttu-id="c12d8-155">Il s’agit d’un projet de base de données Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="c12d8-155">This is a Visual Studio 2010 database project.</span></span> <span data-ttu-id="c12d8-156">Le projet définit le schéma pour une base de données que les magasins de coordonnées.</span><span class="sxs-lookup"><span data-stu-id="c12d8-156">The project defines the schema for a database that stores contact details.</span></span>
- <span data-ttu-id="c12d8-157">**ContactManager.Service**.</span><span class="sxs-lookup"><span data-stu-id="c12d8-157">**ContactManager.Service**.</span></span> <span data-ttu-id="c12d8-158">Il s’agit d’un projet de service web WCF.</span><span class="sxs-lookup"><span data-stu-id="c12d8-158">This is a WCF web service project.</span></span> <span data-ttu-id="c12d8-159">L’expose WCF un point de terminaison qui permet aux appelants à effectuer créer, récupérer, mettre à jour et supprimer (CRUD) des opérations sur la base de données du Gestionnaire de contacts.</span><span class="sxs-lookup"><span data-stu-id="c12d8-159">The WCF exposes an endpoint that allows callers to perform create, retrieve, update, and delete (CRUD) operations on the Contact Manager database.</span></span> <span data-ttu-id="c12d8-160">Le service repose sur la base de données du Gestionnaire de contacts et de l’assembly ContactManager.Common.dll.</span><span class="sxs-lookup"><span data-stu-id="c12d8-160">The service relies on the Contact Manager database and the ContactManager.Common.dll assembly.</span></span>
- <span data-ttu-id="c12d8-161">**ContactManager.Common**.</span><span class="sxs-lookup"><span data-stu-id="c12d8-161">**ContactManager.Common**.</span></span> <span data-ttu-id="c12d8-162">Il s’agit d’un projet de bibliothèque de classes.</span><span class="sxs-lookup"><span data-stu-id="c12d8-162">This is a class library project.</span></span> <span data-ttu-id="c12d8-163">Le service WCF s’appuie sur les types définis dans cet assembly.</span><span class="sxs-lookup"><span data-stu-id="c12d8-163">The WCF service relies on types defined in this assembly.</span></span>

<span data-ttu-id="c12d8-164">Une évaluation complète de la solution et ses exigences de déploiement est fournie dans le premier didacticiel de cette série, [déploiement Web de l’entreprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span><span class="sxs-lookup"><span data-stu-id="c12d8-164">A complete review of the solution and its deployment requirements is provided in the first tutorial in this series, [Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span>

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a><span data-ttu-id="c12d8-165">Tâches de déploiement</span><span class="sxs-lookup"><span data-stu-id="c12d8-165">Deployment Tasks</span></span>

<span data-ttu-id="c12d8-166">Plusieurs tâches distinctes sont impliqués dans le déploiement d’applications sur différents environnements dans une grande entreprise.</span><span class="sxs-lookup"><span data-stu-id="c12d8-166">There are several distinct tasks involved in deploying applications to different environments in a large organization.</span></span> <span data-ttu-id="c12d8-167">Voici les principales tâches que les didacticiels abordent :</span><span class="sxs-lookup"><span data-stu-id="c12d8-167">These are the key tasks that the tutorials cover:</span></span>

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

<span data-ttu-id="c12d8-168">Voici une liste de chaque étape du processus de déploiement du point de vue des utilisateurs décrit plus haut dans ce document :</span><span class="sxs-lookup"><span data-stu-id="c12d8-168">Here is a list of each step in the deployment process from the perspective of the users described earlier in this document:</span></span>

1. <span data-ttu-id="c12d8-169">Tous les membres de l’équipe de révision de la solution de gestionnaire de contacts dans Visual Studio 2010 pour déterminer les problèmes et les exigences de déploiement clés.</span><span class="sxs-lookup"><span data-stu-id="c12d8-169">All members of the team review the Contact Manager solution in Visual Studio 2010 to determine key deployment requirements and issues.</span></span>
2. <span data-ttu-id="c12d8-170">Matt Hink peut déployer la solution de gestionnaire de contacts directement à partir de la station de travail de développement à l’environnement de test de développeur, d’effectuer un test initial de la logique de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c12d8-170">Matt Hink may deploy the Contact Manager solution directly from the developer workstation to the developer test environment, to conduct an initial test of the deployment logic.</span></span>
3. <span data-ttu-id="c12d8-171">Matt Hink ajoute l’application pour le contrôle de code source dans TFS.</span><span class="sxs-lookup"><span data-stu-id="c12d8-171">Matt Hink adds the application to source control in TFS.</span></span>
4. <span data-ttu-id="c12d8-172">Rob Walters crée plusieurs définitions de build pour la solution de gestionnaire de contacts dans Team Build.</span><span class="sxs-lookup"><span data-stu-id="c12d8-172">Rob Walters creates various build definitions for the Contact Manager solution in Team Build.</span></span> <span data-ttu-id="c12d8-173">Une définition de build utilise l’élément de configuration pour déployer la solution à l’environnement de développement de test chaque fois qu’un utilisateur archive du nouveau code.</span><span class="sxs-lookup"><span data-stu-id="c12d8-173">One build definition uses CI to deploy the solution to the developer test environment whenever a user checks in new code.</span></span> <span data-ttu-id="c12d8-174">Une autre définition de build vous permet de déploiements de déclencheur d’utilisateurs dans l’environnement intermédiaire en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="c12d8-174">Another build definition lets users trigger deployments to the staging environment as required.</span></span>
5. <span data-ttu-id="c12d8-175">Chaque fois qu’un utilisateur archive du nouveau code, Team Build automatiquement génère des composants de la solution, exécute les tests unitaires et déploie la solution dans l’environnement de test développeur si la génération a réussi et la passe des tests unitaires.</span><span class="sxs-lookup"><span data-stu-id="c12d8-175">Every time a user checks in new code, Team Build automatically builds the solution components, runs unit tests, and deploys the solution to the developer test environment if the build was successful and the unit tests pass.</span></span>
6. <span data-ttu-id="c12d8-176">Lorsqu’un utilisateur déclenche un déploiement dans l’environnement intermédiaire, la solution empaquetage et du déploiement dans un processus de la seule étape.</span><span class="sxs-lookup"><span data-stu-id="c12d8-176">When a user triggers a deployment to the staging environment, the solution is packaged and deployed in a single-step process.</span></span> <span data-ttu-id="c12d8-177">Ce processus génère également un package pour le déploiement manuel pour l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c12d8-177">This process also generates a package for manual deployment to the production environment.</span></span>
7. <span data-ttu-id="c12d8-178">Lisa Andrews déploie l’application sur l’environnement de production par manuellement l’importation du package web créé à l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="c12d8-178">Lisa Andrews deploys the application to the production environment by manually importing the web package created in step 6.</span></span>

### <a name="key-deployment-issues"></a><span data-ttu-id="c12d8-179">Principaux problèmes de déploiement</span><span class="sxs-lookup"><span data-stu-id="c12d8-179">Key Deployment Issues</span></span>

<span data-ttu-id="c12d8-180">La solution de gestionnaire de contacts et le scénario de Fabrikam, Inc. Mettez en surbrillance les différents problèmes courants et des défis que vous pouvez rencontrer lorsque vous déployez complexes, les solutions d’entreprise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="c12d8-180">The Contact Manager solution and the Fabrikam, Inc. scenario highlight various common issues and challenges that you may encounter when you deploy complex, enterprise-scale solutions.</span></span> <span data-ttu-id="c12d8-181">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c12d8-181">For example:</span></span>

- <span data-ttu-id="c12d8-182">Vous devez être en mesure de déployer des projets pour plusieurs environnements, comme le développeur environnements ou de test, intermédiaire des plates-formes et des serveurs de production.</span><span class="sxs-lookup"><span data-stu-id="c12d8-182">You need to be able to deploy projects to multiple environments, like developer or test environments, staging platforms, and production servers.</span></span> <span data-ttu-id="c12d8-183">La solution doit être déployé avec différents paramètres de configuration pour chaque environnement.</span><span class="sxs-lookup"><span data-stu-id="c12d8-183">The solution needs to be deployed with different configuration settings for each environment.</span></span>
- <span data-ttu-id="c12d8-184">Vous devez déployer plusieurs projets dépendants simultanément dans le cadre d’un processus de génération et de déploiement étape unique ou automatisé.</span><span class="sxs-lookup"><span data-stu-id="c12d8-184">You need to deploy multiple dependent projects simultaneously as part of a single-step or automated build and deployment process.</span></span>
- <span data-ttu-id="c12d8-185">Vous devez être en mesure de déploiement de disque à partir d’un processus automatisé.</span><span class="sxs-lookup"><span data-stu-id="c12d8-185">You need to be able to drive deployment from an automated process.</span></span> <span data-ttu-id="c12d8-186">Par exemple, vous souhaitez utiliser un processus de l’élément de configuration pour déployer des applications web dans un environnement intermédiaire lorsque le nouveau code est archivé.</span><span class="sxs-lookup"><span data-stu-id="c12d8-186">For example, you want to use a CI process to deploy web applications to a staging environment when new code is checked in.</span></span>
- <span data-ttu-id="c12d8-187">Vous devez être en mesure de contrôler le processus de déploiement et de définir des variables de déploiement en dehors de Visual Studio, comme les développeurs ont peu de chances pour que les paramètres de configuration corrects ou les informations d’identification nécessaires pour chaque environnement cible.</span><span class="sxs-lookup"><span data-stu-id="c12d8-187">You need to be able to control the deployment process and set deployment variables from outside Visual Studio, as developers are unlikely to have the correct configuration settings or the necessary credentials for every target environment.</span></span>
- <span data-ttu-id="c12d8-188">Vous devez déployer des projets de base de données basée sur le schéma et conserver les données existantes sur les déploiements suivants.</span><span class="sxs-lookup"><span data-stu-id="c12d8-188">You need to deploy schema-based database projects and preserve existing data on subsequent deployments.</span></span>
- <span data-ttu-id="c12d8-189">Vous devez déployer des bases de données d’appartenance sur une base ad hoc sans déployer des données de compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c12d8-189">You need to deploy membership databases on an ad hoc basis without deploying user account data.</span></span> <span data-ttu-id="c12d8-190">Vous devez également mettre à jour le schéma des bases de données d’appartenance déployé sans perte de données de compte utilisateur existant.</span><span class="sxs-lookup"><span data-stu-id="c12d8-190">You may also need to update the schema of deployed membership databases without losing existing user account data.</span></span>
- <span data-ttu-id="c12d8-191">Vous devez exclure certains fichiers ou dossiers lorsque vous déployez du contenu pour les environnements cibles différents.</span><span class="sxs-lookup"><span data-stu-id="c12d8-191">You need to exclude certain files or folders when you deploy content to various target environments.</span></span>

<span data-ttu-id="c12d8-192">En outre, la gestion du déploiement quand les mises à jour fréquentes et incrémentielle lève des défis supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="c12d8-192">In addition, managing deployment when updates are frequent and incremental throws up some additional challenges.</span></span> <span data-ttu-id="c12d8-193">Exemple :</span><span class="sxs-lookup"><span data-stu-id="c12d8-193">For example:</span></span>

- <span data-ttu-id="c12d8-194">Pour exécuter des tests unitaires chaque fois qu’un développeur vérifie dans le nouveau code.</span><span class="sxs-lookup"><span data-stu-id="c12d8-194">You run unit tests every time a developer checks in new code.</span></span> <span data-ttu-id="c12d8-195">Vous souhaitez déployer la solution si le code réussit les tests unitaires uniquement.</span><span class="sxs-lookup"><span data-stu-id="c12d8-195">You only want to deploy the solution if the code passes the unit tests.</span></span>
- <span data-ttu-id="c12d8-196">Lorsque vous déployez une application web dans un environnement intermédiaire ou de production, vous souhaitez rediriger les utilisateurs vers un *application\_offline.htm* fichier pendant la durée du processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c12d8-196">When you deploy a web application to a staging or production environment, you want to redirect users to an *app\_offline.htm* file for the duration of the deployment process.</span></span>
- <span data-ttu-id="c12d8-197">Vous souhaitez connecter des activités de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c12d8-197">You want to log deployment activities.</span></span> <span data-ttu-id="c12d8-198">Le processus de déploiement doit envoyer des notifications par courrier électronique des déploiements réussies ou échoués pour les destinataires désignés.</span><span class="sxs-lookup"><span data-stu-id="c12d8-198">The deployment process should send email notifications of successful or failed deployments to designated recipients.</span></span>
- <span data-ttu-id="c12d8-199">En cas d’un déploiement automatisé, le processus de déploiement doit réexécuter le déploiement actuel ou déployer le package web précédente à la place.</span><span class="sxs-lookup"><span data-stu-id="c12d8-199">If an automated deployment fails, the deployment process should retry the current deployment or deploy the previous web package instead.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c12d8-200">[Précédent](deploying-web-applications-in-enterprise-scenarios.md)
[Suivant](application-lifecycle-management-from-development-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="c12d8-200">[Previous](deploying-web-applications-in-enterprise-scenarios.md)
[Next](application-lifecycle-management-from-development-to-production.md)</span></span>