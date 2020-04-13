---
title: Utilizzo di pacchetti da feed autenticatiConsuming packages from authenticated feeds
description: Utilizzo di pacchetti da feed autenticati in tutti gli scenari client NuGetConsuming packages from authenticated feeds in all NuGet client scenarios
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231791"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="ed743-103">Utilizzo di pacchetti da feed autenticatiConsuming packages from authenticated feeds</span><span class="sxs-lookup"><span data-stu-id="ed743-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="ed743-104">Oltre ai nuget.org [feed pubblico,](https://api.nuget.org/v3/index.json)i client NuGet hanno la possibilità di interagire con feed di file e feed http privati.</span><span class="sxs-lookup"><span data-stu-id="ed743-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="ed743-105">Per eseguire l'autenticazione con feed http privati, i due approcci sono:</span><span class="sxs-lookup"><span data-stu-id="ed743-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="ed743-106">Aggiungere le credenziali nel file [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="ed743-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="ed743-107">Eseguire l'autenticazione utilizzando uno dei numerosi modelli di estensibilità a seconda del client utilizzato.</span><span class="sxs-lookup"><span data-stu-id="ed743-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="ed743-108">Estendibilità dell'autenticazione dei client NuGetNuGet clients' authentication extensibility</span><span class="sxs-lookup"><span data-stu-id="ed743-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="ed743-109">Per i vari client NuGet, il provider di feed privato stesso è responsabile dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ed743-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="ed743-110">Tutti i client NuGet dispongono di metodi di estendibilità per supportare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="ed743-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="ed743-111">Si tratta di un'estensione di Visual Studio o di un plug-in in grado di comunicare con NuGet per recuperare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="ed743-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="ed743-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ed743-112">Visual Studio</span></span>

<span data-ttu-id="ed743-113">In Visual Studio, NuGet espone un'interfaccia che i provider di feed possono implementare e fornire ai clienti.</span><span class="sxs-lookup"><span data-stu-id="ed743-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="ed743-114">Per ulteriori informazioni, fare riferimento alla documentazione su [come creare un provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)di credenziali di Visual Studio .</span><span class="sxs-lookup"><span data-stu-id="ed743-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="ed743-115">Provider di credenziali NuGet disponibili per Visual StudioAvailable NuGet credential providers for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ed743-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="ed743-116">È disponibile un provider di credenziali integrato in Visual Studio per supportare DevOps di Azure.There is a credential provider built into Visual Studio to support Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="ed743-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="ed743-117">I provider di credenziali plug-in disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="ed743-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="ed743-118">Provider di credenziali MyGet per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ed743-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="ed743-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ed743-119">nuget.exe</span></span>

<span data-ttu-id="ed743-120">Quando `nuget.exe` è necessario disporre delle credenziali per l'autenticazione con un feed, le cerca nel modo seguente:When needs credentials to authenticate with a feed, it looks for the following manner:</span><span class="sxs-lookup"><span data-stu-id="ed743-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ed743-121">Cercare le credenziali `NuGet.config` nei file.</span><span class="sxs-lookup"><span data-stu-id="ed743-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="ed743-122">Usare i provider di credenziali del plug-in V2Use V2 plug-in credential providers</span><span class="sxs-lookup"><span data-stu-id="ed743-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="ed743-123">Usare i provider di credenziali del plug-in V1Use V1 plug-in credential providers</span><span class="sxs-lookup"><span data-stu-id="ed743-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="ed743-124">NuGet richiede quindi all'utente le credenziali nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="ed743-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="ed743-125">Provider di credenziali nuget.exe e V2</span><span class="sxs-lookup"><span data-stu-id="ed743-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="ed743-126">Nella `4.8` versione NuGet definito un nuovo meccanismo di plug-in di autenticazione, qui di seguito indicato come provider di credenziali V2.</span><span class="sxs-lookup"><span data-stu-id="ed743-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="ed743-127">Per l'installazione e la scoperta di tali provider, fare riferimento a [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ed743-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="ed743-128">Provider di credenziali nuget.exe e V1</span><span class="sxs-lookup"><span data-stu-id="ed743-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="ed743-129">Nella `3.3` versione NuGet ha introdotto la prima versione dei plugin di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ed743-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="ed743-130">Per l'installazione e l'individuazione di tali provider fare riferimento ai provider di [credenziali nuget.exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="ed743-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="ed743-131">Provider di credenziali disponibili per nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ed743-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="ed743-132">Provider di credenziali V2 di Azure DevOps o provider di credenziali degli elementi di [AzureAzure](https://github.com/microsoft/artifacts-credprovider) [DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or Azure Artifacts Credential Provider</span><span class="sxs-lookup"><span data-stu-id="ed743-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="ed743-133">Con Visual Studio 2017 versione 15.9 e successive, il provider di credenziali DevOps di Azure viene incluso in Visual Studio.With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed743-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="ed743-134">Se `nuget.exe` utilizza MSBuild da quello specifico set di strumenti di Visual Studio, il plug-in verrà individuato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed743-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="ed743-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="ed743-135">dotnet.exe</span></span>

<span data-ttu-id="ed743-136">Quando `dotnet.exe` è necessario disporre delle credenziali per l'autenticazione con un feed, le cerca nel modo seguente:When needs credentials to authenticate with a feed, it looks for the following manner:</span><span class="sxs-lookup"><span data-stu-id="ed743-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ed743-137">Cercare le credenziali `NuGet.config` nei file.</span><span class="sxs-lookup"><span data-stu-id="ed743-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="ed743-138">Usare i provider di credenziali del plug-in V2Use V2 plug-in credential providers</span><span class="sxs-lookup"><span data-stu-id="ed743-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="ed743-139">Per `dotnet.exe` impostazione predefinita non è interattivo, pertanto potrebbe essere necessario passare un `--interactive` flag per ottenere lo strumento da bloccare per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ed743-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="ed743-140">provider di credenziali dotnet.exe e V2</span><span class="sxs-lookup"><span data-stu-id="ed743-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="ed743-141">Nella `2.2.100` versione dell'SDK, NuGet ha definito un meccanismo di plug-in di autenticazione che funziona in tutti i client.</span><span class="sxs-lookup"><span data-stu-id="ed743-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="ed743-142">Per l'installazione e la scoperta di tali provider, fare riferimento a [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ed743-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="ed743-143">Provider di credenziali disponibili per dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="ed743-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="ed743-144">Provider di credenziali degli elementi di AzureAzure Artifacts Credential Provider</span><span class="sxs-lookup"><span data-stu-id="ed743-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="ed743-145">FILE MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="ed743-145">MSBuild.exe</span></span>

<span data-ttu-id="ed743-146">Quando `MSBuild.exe` è necessario disporre delle credenziali per l'autenticazione con un feed, le cerca nel modo seguente:When needs credentials to authenticate with a feed, it looks for the following manner:</span><span class="sxs-lookup"><span data-stu-id="ed743-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ed743-147">Cercare le credenziali `NuGet.config` nei file</span><span class="sxs-lookup"><span data-stu-id="ed743-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="ed743-148">Usare i provider di credenziali del plug-in V2Use V2 plug-in credential providers</span><span class="sxs-lookup"><span data-stu-id="ed743-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="ed743-149">Per `MSBuild.exe` impostazione predefinita non è interattivo, pertanto potrebbe essere necessario impostare la `/p:NuGetInteractive=true` proprietà per ottenere lo strumento da bloccare per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="ed743-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="ed743-150">Provider di credenziali MSBuild.exe e V2</span><span class="sxs-lookup"><span data-stu-id="ed743-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="ed743-151">In Visual Studio 2019 Update 9, NuGet ha definito un meccanismo di plug-in di autenticazione che funziona in tutti i client.</span><span class="sxs-lookup"><span data-stu-id="ed743-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="ed743-152">Per l'installazione e la scoperta di tali provider, fare riferimento a [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ed743-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="ed743-153">Provider di credenziali disponibili per MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="ed743-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="ed743-154">Provider di credenziali degli elementi di AzureAzure Artifacts Credential Provider</span><span class="sxs-lookup"><span data-stu-id="ed743-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="ed743-155">Con Visual Studio 2017 Update 9 e versioni successive, il provider di credenziali DevOps di Azure viene incluso in Visual Studio.With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed743-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="ed743-156">Non sono necessari ulteriori passaggi.</span><span class="sxs-lookup"><span data-stu-id="ed743-156">No additional steps are required.</span></span>
