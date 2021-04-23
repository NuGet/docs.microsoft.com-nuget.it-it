---
title: Utilizzo di pacchetti da feed autenticati
description: Utilizzo di pacchetti da feed autenticati in tutti gli scenari client NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901512"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="55e82-103">Utilizzo di pacchetti da feed autenticati</span><span class="sxs-lookup"><span data-stu-id="55e82-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="55e82-104">Oltre al feed [nuget.org,](https://api.nuget.org/v3/index.json)i client NuGet hanno la possibilità di interagire con feed di file e feed HTTP privati.</span><span class="sxs-lookup"><span data-stu-id="55e82-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="55e82-105">Per eseguire l'autenticazione con feed HTTP privati, i due approcci sono:</span><span class="sxs-lookup"><span data-stu-id="55e82-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="55e82-106">Aggiungere le credenziali nel [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="55e82-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="55e82-107">Eseguire l'autenticazione usando uno dei numerosi modelli di estendibilità a seconda del client usato.</span><span class="sxs-lookup"><span data-stu-id="55e82-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="55e82-108">Estendibilità dell'autenticazione dei client NuGet</span><span class="sxs-lookup"><span data-stu-id="55e82-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="55e82-109">Per i vari client NuGet, il provider di feed privato è responsabile dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="55e82-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="55e82-110">Tutti i client NuGet hanno metodi di estendibilità per supportare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="55e82-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="55e82-111">Si tratta di un'estensione Visual Studio o un plug-in in grado di comunicare con NuGet per recuperare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="55e82-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="55e82-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55e82-112">Visual Studio</span></span>

<span data-ttu-id="55e82-113">In Visual Studio NuGet espone un'interfaccia che i provider di feed possono implementare e fornire ai clienti.</span><span class="sxs-lookup"><span data-stu-id="55e82-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="55e82-114">Per altre informazioni, vedere la documentazione su come creare un provider di [Visual Studio credenziali.](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)</span><span class="sxs-lookup"><span data-stu-id="55e82-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="55e82-115">Provider di credenziali NuGet disponibili per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55e82-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="55e82-116">È disponibile un provider di credenziali incorporato in Visual Studio per supportare Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="55e82-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="55e82-117">I provider di credenziali plug-in disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="55e82-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="55e82-118">MyGet Provider di credenziali per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55e82-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="55e82-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="55e82-119">nuget.exe</span></span>

<span data-ttu-id="55e82-120">Quando `nuget.exe` sono necessarie le credenziali per l'autenticazione con un feed, queste vengono cercate nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="55e82-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="55e82-121">Cercare le credenziali nei `NuGet.config` file.</span><span class="sxs-lookup"><span data-stu-id="55e82-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="55e82-122">Usare i provider di credenziali del plug-in V2</span><span class="sxs-lookup"><span data-stu-id="55e82-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="55e82-123">Usare i provider di credenziali del plug-in V1</span><span class="sxs-lookup"><span data-stu-id="55e82-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="55e82-124">NuGet richiede quindi all'utente le credenziali nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="55e82-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="55e82-125">nuget.exe e provider di credenziali V2</span><span class="sxs-lookup"><span data-stu-id="55e82-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="55e82-126">Nella versione NuGet ha definito un nuovo meccanismo del plug-in di autenticazione, denominato successivamente provider di credenziali `4.8` V2.</span><span class="sxs-lookup"><span data-stu-id="55e82-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="55e82-127">Per l'installazione e l'individuazione di tali provider, vedere [Plug-in multipiattaforma NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="55e82-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="55e82-128">nuget.exe e provider di credenziali V1</span><span class="sxs-lookup"><span data-stu-id="55e82-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="55e82-129">Nella versione `3.3` NuGet ha introdotto la prima versione dei plug-in di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="55e82-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="55e82-130">Per l'installazione e l'individuazione di tali provider, fare [ riferimentonuget.exe provider di credenziali](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="55e82-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="55e82-131">Provider di credenziali disponibili per nuget.exe</span><span class="sxs-lookup"><span data-stu-id="55e82-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="55e82-132">[Azure DevOps provider di credenziali V2](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) o [Azure Artifacts Provider di credenziali](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="55e82-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="55e82-133">Con Visual Studio 2017 versione 15.9 e successive, il provider Azure DevOps credenziali è in bundle in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55e82-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="55e82-134">Se `nuget.exe` usa MSBuild da quel set Visual Studio strumenti, il plug-in verrà individuato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="55e82-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="55e82-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="55e82-135">dotnet.exe</span></span>

<span data-ttu-id="55e82-136">Quando `dotnet.exe` sono necessarie credenziali per l'autenticazione con un feed, le cerca nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="55e82-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="55e82-137">Cercare le credenziali nei `NuGet.config` file.</span><span class="sxs-lookup"><span data-stu-id="55e82-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="55e82-138">Usare i provider di credenziali del plug-in V2</span><span class="sxs-lookup"><span data-stu-id="55e82-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="55e82-139">Per impostazione predefinita, non è interattiva, quindi potrebbe essere necessario passare un flag per ottenere `dotnet.exe` lo strumento da bloccare per `--interactive` l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="55e82-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="55e82-140">dotnet.exe e provider di credenziali V2</span><span class="sxs-lookup"><span data-stu-id="55e82-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="55e82-141">Nella versione `2.2.100` dell'SDK NuGet ha definito un meccanismo del plug-in di autenticazione che funziona in tutti i client.</span><span class="sxs-lookup"><span data-stu-id="55e82-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="55e82-142">Per l'installazione e l'individuazione di tali provider, vedere [Plug-in multipiattaforma NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="55e82-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="55e82-143">Provider di credenziali disponibili per dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="55e82-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="55e82-144">Azure Artifacts Provider di credenziali</span><span class="sxs-lookup"><span data-stu-id="55e82-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="55e82-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="55e82-145">MSBuild.exe</span></span>

<span data-ttu-id="55e82-146">Quando `MSBuild.exe` sono necessarie le credenziali per l'autenticazione con un feed, queste vengono cercate nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="55e82-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="55e82-147">Cercare le credenziali nei `NuGet.config` file</span><span class="sxs-lookup"><span data-stu-id="55e82-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="55e82-148">Usare i provider di credenziali del plug-in V2</span><span class="sxs-lookup"><span data-stu-id="55e82-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="55e82-149">Per impostazione predefinita, non è interattiva, quindi potrebbe essere necessario impostare la proprietà per ottenere `MSBuild.exe` lo strumento da bloccare per `/p:NuGetInteractive=true` l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="55e82-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="55e82-150">provider di credenziali MSBuild.exe e V2</span><span class="sxs-lookup"><span data-stu-id="55e82-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="55e82-151">In Visual Studio 2019 Update 9, NuGet ha definito un meccanismo del plug-in di autenticazione che funziona in tutti i client.</span><span class="sxs-lookup"><span data-stu-id="55e82-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="55e82-152">Per l'installazione e l'individuazione di tali provider, vedere [Plug-in multipiattaforma NuGet.](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)</span><span class="sxs-lookup"><span data-stu-id="55e82-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="55e82-153">Provider di credenziali disponibili per MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="55e82-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="55e82-154">Azure Artifacts Provider di credenziali</span><span class="sxs-lookup"><span data-stu-id="55e82-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="55e82-155">Con Visual Studio 2017 Update 9 e versioni successive, il provider Azure DevOps credenziali è in bundle in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55e82-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="55e82-156">Non sono necessari altri passaggi.</span><span class="sxs-lookup"><span data-stu-id="55e82-156">No additional steps are required.</span></span>
