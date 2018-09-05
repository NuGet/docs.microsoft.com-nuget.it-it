---
title: Provider di credenziali NuGet per Visual Studio
description: Provider di credenziali NuGet eseguire l'autenticazione con i feed implementando l'interfaccia IVsCredentialProvider in un'estensione di Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547954"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="9d49f-103">L'autenticazione di feed di Visual Studio con i provider di credenziali NuGet</span><span class="sxs-lookup"><span data-stu-id="9d49f-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="9d49f-104">L'estensione di NuGet di Visual Studio 3.6 + supporta i provider di credenziali, che consentono di NuGet lavorare con i feed autenticati.</span><span class="sxs-lookup"><span data-stu-id="9d49f-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="9d49f-105">Dopo aver installato un provider di credenziali NuGet per Visual Studio, l'estensione NuGet di Visual Studio verrà automaticamente acquisire e aggiornare le credenziali per i feed autenticati, se necessario.</span><span class="sxs-lookup"><span data-stu-id="9d49f-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="9d49f-106">Un'implementazione di esempio sono disponibili nel [dell'esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="9d49f-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="9d49f-107">A partire da 4.8 NuGet in Visual Studio supporta i nuovi cross-platform autenticazione plug-in anche, ma non sono l'approccio consigliato per motivi di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9d49f-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="9d49f-108">I provider di credenziali NuGet per Visual Studio deve essere installati come un'estensione di Visual Studio regolare e richiederà [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9d49f-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="9d49f-109">I provider di credenziali NuGet per Visual Studio funzionano solo in Visual Studio (non in dotnet-restore o nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="9d49f-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="9d49f-110">Per i provider di credenziali con nuget.exe, vedere [nuget.exe i provider di credenziali](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="9d49f-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="9d49f-111">Per credential provider in msbuild e dotnet vedere [NuGet cross-platform i plug-in](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="9d49f-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="9d49f-112">Disponibili provider di credenziali NuGet per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d49f-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="9d49f-113">È disponibile un provider di credenziali creato nell'estensione NuGet di Visual Studio per supportare Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9d49f-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="9d49f-114">L'estensione NuGet di Visual Studio Usa interna `VsCredentialProviderImporter` che esegue l'analisi anche per i provider di credenziali plug-in.</span><span class="sxs-lookup"><span data-stu-id="9d49f-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="9d49f-115">Questi provider di credenziali plug-in devono essere individuati come un'esportazione MEF di tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="9d49f-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="9d49f-116">I provider di credenziali plug-in disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="9d49f-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="9d49f-117">Provider di credenziali MyGet per Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9d49f-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="9d49f-118">Creazione di un provider di credenziali NuGet per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d49f-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="9d49f-119">L'estensione di NuGet di Visual Studio 3.6 + implementa un CredentialService interna che viene usato per acquisire le credenziali.</span><span class="sxs-lookup"><span data-stu-id="9d49f-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="9d49f-120">Il CredentialService include un elenco di provider di credenziali incorporati e plug-in.</span><span class="sxs-lookup"><span data-stu-id="9d49f-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="9d49f-121">Ogni provider viene provata in sequenza fino a quando non vengono acquisite le credenziali.</span><span class="sxs-lookup"><span data-stu-id="9d49f-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="9d49f-122">Durante l'acquisizione delle credenziali, il servizio di credenziale prova i provider di credenziali nell'ordine seguente, l'arresto, non appena vengono acquisite le credenziali:</span><span class="sxs-lookup"><span data-stu-id="9d49f-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="9d49f-123">Le credenziali verranno recuperate dai file di configurazione NuGet (usando l'elemento predefinito `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="9d49f-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="9d49f-124">Se l'origine del pacchetto si trova in Visual Studio Team Services, il `VisualStudioAccountProvider` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="9d49f-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="9d49f-125">Tutti gli altri plug-in Visual Studio i provider di credenziali verranno tentati in modo sequenziale.</span><span class="sxs-lookup"><span data-stu-id="9d49f-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="9d49f-126">Provare a usare NuGet tutti cross-platform i provider di credenziali in modo sequenziale.</span><span class="sxs-lookup"><span data-stu-id="9d49f-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="9d49f-127">Se le credenziali non sono state acquisite, l'utente verrà richiesto per le credenziali utilizzando una finestra di dialogo di autenticazione di base standard.</span><span class="sxs-lookup"><span data-stu-id="9d49f-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="9d49f-128">Implementazione IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="9d49f-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="9d49f-129">Per creare un provider di credenziali NuGet per Visual Studio, creare un'estensione di Visual Studio che espone un pubblico esportazione MEF che implementa il `IVsCredentialProvider` digitare ed è conforme ai principi descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="9d49f-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="9d49f-130">Un'implementazione di esempio sono disponibili nel [dell'esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="9d49f-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="9d49f-131">Ogni provider di credenziali NuGet per Visual Studio deve:</span><span class="sxs-lookup"><span data-stu-id="9d49f-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="9d49f-132">Determinare se è possibile fornire le credenziali per l'URI di destinazione prima di iniziare l'acquisizione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="9d49f-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="9d49f-133">Se il provider non è possibile specificare le credenziali per l'origine di destinazione, quindi il metodo deve restituire `null`.</span><span class="sxs-lookup"><span data-stu-id="9d49f-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="9d49f-134">Se il provider di gestione delle richieste per l'URI di destinazione, ma non è possibile specificare le credenziali, deve essere generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="9d49f-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="9d49f-135">Deve implementare un provider di credenziali NuGet personalizzato per Visual Studio il `IVsCredentialProvider` disponibile nell'interfaccia di [pacchetto NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="9d49f-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="9d49f-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="9d49f-136">GetCredentialAsync</span></span>

| <span data-ttu-id="9d49f-137">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="9d49f-137">Input Parameter</span></span> |<span data-ttu-id="9d49f-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9d49f-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="9d49f-139">Uri di URI</span><span class="sxs-lookup"><span data-stu-id="9d49f-139">Uri uri</span></span> | <span data-ttu-id="9d49f-140">L'Uri di origine pacchetto per il quale le credenziali richieste.</span><span class="sxs-lookup"><span data-stu-id="9d49f-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="9d49f-141">Proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="9d49f-141">IWebProxy proxy</span></span> | <span data-ttu-id="9d49f-142">Proxy Web da utilizzare durante la comunicazione in rete.</span><span class="sxs-lookup"><span data-stu-id="9d49f-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="9d49f-143">Null se non esiste alcuna autenticazione proxy configurata.</span><span class="sxs-lookup"><span data-stu-id="9d49f-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="9d49f-144">isProxyRequest bool</span><span class="sxs-lookup"><span data-stu-id="9d49f-144">bool isProxyRequest</span></span> | <span data-ttu-id="9d49f-145">True se la richiesta è per ottenere le credenziali di autenticazione proxy.</span><span class="sxs-lookup"><span data-stu-id="9d49f-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="9d49f-146">Se l'implementazione non è valido per l'acquisizione delle credenziali del proxy, quindi deve essere restituito null.</span><span class="sxs-lookup"><span data-stu-id="9d49f-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="9d49f-147">isRetry bool</span><span class="sxs-lookup"><span data-stu-id="9d49f-147">bool isRetry</span></span> | <span data-ttu-id="9d49f-148">True se le credenziali sono stati richiesti in precedenza per questo Uri, ma le credenziali fornite non consentiva l'accesso autorizzato.</span><span class="sxs-lookup"><span data-stu-id="9d49f-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="9d49f-149">bool non interattive</span><span class="sxs-lookup"><span data-stu-id="9d49f-149">bool nonInteractive</span></span> | <span data-ttu-id="9d49f-150">Se true, il provider di credenziali è necessario eliminare tutti i prompt utente e usare invece i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="9d49f-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="9d49f-151">Elemento CancellationToken determina l'oggetto CancellationToken</span><span class="sxs-lookup"><span data-stu-id="9d49f-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="9d49f-152">Questo token di annullamento deve essere controllato per determinare se le credenziali di richiesta di operazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="9d49f-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="9d49f-153">**Valore restituito**: un oggetto credenziali che implementa le [ `System.Net.ICredentials` interfaccia](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="9d49f-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
