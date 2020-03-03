---
title: Utilizzo di pacchetti da feed autenticati
description: Utilizzo di pacchetti da feed autenticati in tutti gli scenari client NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231791"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="09080-103">Utilizzo di pacchetti da feed autenticati</span><span class="sxs-lookup"><span data-stu-id="09080-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="09080-104">Oltre al [feed pubblico](https://api.nuget.org/v3/index.json)di NuGet.org, i client NuGet sono in grado di interagire con i feed di file e i feed http privati.</span><span class="sxs-lookup"><span data-stu-id="09080-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="09080-105">Per eseguire l'autenticazione con feed http privati, i 2 approcci sono:</span><span class="sxs-lookup"><span data-stu-id="09080-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="09080-106">Aggiungere le credenziali in [NuGet. config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="09080-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="09080-107">Eseguire l'autenticazione usando uno dei numerosi modelli di estendibilità a seconda del client usato.</span><span class="sxs-lookup"><span data-stu-id="09080-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="09080-108">Estendibilità dell'autenticazione dei client NuGet</span><span class="sxs-lookup"><span data-stu-id="09080-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="09080-109">Per i vari client NuGet, il provider di feed privato è responsabile dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="09080-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="09080-110">Tutti i client NuGet hanno metodi di estendibilità per supportare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="09080-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="09080-111">Si tratta di un'estensione di Visual Studio o un plug-in in grado di comunicare con NuGet per recuperare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="09080-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="09080-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09080-112">Visual Studio</span></span>

<span data-ttu-id="09080-113">In Visual Studio, NuGet espone un'interfaccia che i provider di feed possono implementare e fornire ai propri clienti.</span><span class="sxs-lookup"><span data-stu-id="09080-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="09080-114">Per altri dettagli, vedere la documentazione su [come creare un provider di credenziali di Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="09080-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="09080-115">Provider di credenziali NuGet disponibili per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09080-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="09080-116">Per supportare Azure DevOps è disponibile un provider di credenziali incorporato in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09080-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="09080-117">I provider di credenziali plug-in disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="09080-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="09080-118">Provider di credenziali MyGet per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09080-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="09080-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="09080-119">nuget.exe</span></span>

<span data-ttu-id="09080-120">Quando `nuget.exe` necessita di credenziali per l'autenticazione con un feed, la ricerca viene eseguita nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="09080-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="09080-121">Cercare le credenziali nei file di `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="09080-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="09080-122">Usare i provider di credenziali plug-in V2</span><span class="sxs-lookup"><span data-stu-id="09080-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="09080-123">Usare i provider di credenziali plug-in V1</span><span class="sxs-lookup"><span data-stu-id="09080-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="09080-124">NuGet chiede quindi all'utente le credenziali nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="09080-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="09080-125">provider di credenziali NuGet. exe e V2</span><span class="sxs-lookup"><span data-stu-id="09080-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="09080-126">Nella versione `4.8` NuGet definisce un nuovo meccanismo di plug-in di autenticazione, in seguito denominato provider di credenziali V2.</span><span class="sxs-lookup"><span data-stu-id="09080-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="09080-127">Per l'installazione e l'individuazione di tali provider, vedere [plug-in NuGet multipiattaforma](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="09080-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="09080-128">provider di credenziali NuGet. exe e V1</span><span class="sxs-lookup"><span data-stu-id="09080-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="09080-129">Nella versione `3.3` in NuGet è stata introdotta la prima versione di plug-in di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="09080-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="09080-130">Per l'installazione e l'individuazione di questi provider, vedere [provider di credenziali NuGet. exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="09080-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="09080-131">Provider di credenziali disponibili per NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="09080-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="09080-132">Provider di [credenziali di Azure DevOps V2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) o [provider di credenziali Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="09080-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="09080-133">Con Visual Studio 2017 versione 15,9 e successive, il provider di credenziali di Azure DevOps è incluso in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09080-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="09080-134">Se `nuget.exe` USA MSBuild da quel set di strumenti di Visual Studio specifico, il plug-in verrà individuato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="09080-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="09080-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="09080-135">dotnet.exe</span></span>

<span data-ttu-id="09080-136">Quando `dotnet.exe` necessita di credenziali per l'autenticazione con un feed, la ricerca viene eseguita nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="09080-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="09080-137">Cercare le credenziali nei file di `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="09080-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="09080-138">Usare i provider di credenziali plug-in V2</span><span class="sxs-lookup"><span data-stu-id="09080-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="09080-139">Per impostazione predefinita `dotnet.exe` non è interattivo, quindi potrebbe essere necessario passare un flag `--interactive` per ottenere lo strumento da bloccare per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="09080-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="09080-140">provider di credenziali dotnet. exe e V2</span><span class="sxs-lookup"><span data-stu-id="09080-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="09080-141">Nella versione `2.2.100` dell'SDK, NuGet definisce un meccanismo di plug-in di autenticazione che funziona in tutti i client.</span><span class="sxs-lookup"><span data-stu-id="09080-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="09080-142">Per l'installazione e l'individuazione di tali provider, vedere [plug-in NuGet multipiattaforma](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="09080-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="09080-143">Provider di credenziali disponibili per dotnet. exe</span><span class="sxs-lookup"><span data-stu-id="09080-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="09080-144">Provider di credenziali Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="09080-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="09080-145">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="09080-145">MSBuild.exe</span></span>

<span data-ttu-id="09080-146">Quando `MSBuild.exe` necessita di credenziali per l'autenticazione con un feed, la ricerca viene eseguita nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="09080-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="09080-147">Cerca le credenziali nei file di `NuGet.config`</span><span class="sxs-lookup"><span data-stu-id="09080-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="09080-148">Usare i provider di credenziali plug-in V2</span><span class="sxs-lookup"><span data-stu-id="09080-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="09080-149">Per impostazione predefinita `MSBuild.exe` non è interattivo, quindi potrebbe essere necessario impostare la proprietà `/p:NuGetInteractive=true` per fare in modo che lo strumento si blocchi per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="09080-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="09080-150">Provider di credenziali MSBuild. exe e V2</span><span class="sxs-lookup"><span data-stu-id="09080-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="09080-151">In Visual Studio 2019 Update 9, NuGet definisce un meccanismo di plug-in di autenticazione che funziona in tutti i client.</span><span class="sxs-lookup"><span data-stu-id="09080-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="09080-152">Per l'installazione e l'individuazione di tali provider, vedere [plug-in NuGet multipiattaforma](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="09080-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="09080-153">Provider di credenziali disponibili per MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="09080-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="09080-154">Provider di credenziali Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="09080-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="09080-155">Con Visual Studio 2017 Update 9 e versioni successive, il provider di credenziali di Azure DevOps è incluso in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09080-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="09080-156">Non sono necessari passaggi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="09080-156">No additional steps are required.</span></span>
