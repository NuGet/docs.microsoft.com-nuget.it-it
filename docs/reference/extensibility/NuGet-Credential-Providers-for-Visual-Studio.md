---
title: Provider di credenziali NuGet per Visual Studio
description: I provider di credenziali NuGet eseguono l'autenticazione con i feed implementando l'interfaccia IVsCredentialProvider in un'estensione di Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 906d07eb22599eb423b00300954ff2601dd33369
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383551"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="80072-103">Autenticazione dei feed in Visual Studio con i provider di credenziali NuGet</span><span class="sxs-lookup"><span data-stu-id="80072-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="80072-104">L'estensione di Visual Studio NuGet 3.6 + supporta i provider di credenziali che consentono a NuGet di usare i feed autenticati.</span><span class="sxs-lookup"><span data-stu-id="80072-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="80072-105">Dopo aver installato un provider di credenziali NuGet per Visual Studio, l'estensione NuGet di Visual Studio acquisisce e aggiorna automaticamente le credenziali per i feed autenticati, se necessario.</span><span class="sxs-lookup"><span data-stu-id="80072-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="80072-106">È possibile trovare un'implementazione di esempio nell' [esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="80072-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="80072-107">A partire da 4.8 + NuGet in Visual Studio supporta anche i nuovi plug-in di autenticazione multipiattaforma, ma non è l'approccio consigliato per motivi di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="80072-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="80072-108">I provider di credenziali NuGet per Visual Studio devono essere installati come un'estensione di Visual Studio normale e richiedono [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="80072-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="80072-109">I provider di credenziali NuGet per Visual Studio funzionano solo in Visual Studio (non in dotnet restore o NuGet. exe).</span><span class="sxs-lookup"><span data-stu-id="80072-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="80072-110">Per i provider di credenziali con NuGet. exe, vedere [provider di credenziali NuGet. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="80072-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="80072-111">Per i provider di credenziali in dotnet e MSBuild vedere plug-in [NuGet multipiattaforma](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="80072-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="80072-112">Provider di credenziali NuGet disponibili per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="80072-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="80072-113">È disponibile un provider di credenziali incorporato nell'estensione NuGet di Visual Studio per supportare Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="80072-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="80072-114">L'estensione NuGet di Visual Studio usa una `VsCredentialProviderImporter` interna che analizza anche i provider di credenziali plug-in.</span><span class="sxs-lookup"><span data-stu-id="80072-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="80072-115">Questi provider di credenziali plug-in devono essere individuabili come esportazione MEF di tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="80072-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="80072-116">I provider di credenziali plug-in disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="80072-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="80072-117">Provider di credenziali MyGet per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="80072-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="80072-118">Creazione di un provider di credenziali NuGet per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="80072-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="80072-119">L'estensione di Visual Studio NuGet 3.6 + implementa un CredentialService interno usato per acquisire le credenziali.</span><span class="sxs-lookup"><span data-stu-id="80072-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="80072-120">Il CredentialService include un elenco di provider di credenziali plug-in e incorporati.</span><span class="sxs-lookup"><span data-stu-id="80072-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="80072-121">Ogni provider viene eseguito in modo sequenziale fino a quando le credenziali non vengono acquisite.</span><span class="sxs-lookup"><span data-stu-id="80072-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="80072-122">Durante l'acquisizione delle credenziali, il servizio credenziali tenterà i provider di credenziali nell'ordine seguente e verrà arrestato non appena vengono acquisite le credenziali:</span><span class="sxs-lookup"><span data-stu-id="80072-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="80072-123">Le credenziali verranno recuperate dai file di configurazione NuGet (usando la `SettingsCredentialProvider`incorporata).</span><span class="sxs-lookup"><span data-stu-id="80072-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="80072-124">Se l'origine del pacchetto si trova in Visual Studio Team Services, verrà utilizzato il `VisualStudioAccountProvider`.</span><span class="sxs-lookup"><span data-stu-id="80072-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="80072-125">Tutti gli altri provider di credenziali di Visual Studio plug-in verranno tentati in sequenza.</span><span class="sxs-lookup"><span data-stu-id="80072-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="80072-126">Provare a usare tutti i provider di credenziali multipiattaforma NuGet in sequenza.</span><span class="sxs-lookup"><span data-stu-id="80072-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="80072-127">Se non è stata ancora acquisita alcuna credenziale, all'utente verranno richieste le credenziali utilizzando una finestra di dialogo di autenticazione di base standard.</span><span class="sxs-lookup"><span data-stu-id="80072-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="80072-128">Implementazione di IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="80072-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="80072-129">Per creare un provider di credenziali NuGet per Visual Studio, creare un'estensione di Visual Studio che espone un'esportazione MEF pubblica implementando il tipo di `IVsCredentialProvider` e aderisca ai principi descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="80072-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="80072-130">È possibile trovare un'implementazione di esempio nell' [esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="80072-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="80072-131">Ogni provider di credenziali NuGet per Visual Studio deve:</span><span class="sxs-lookup"><span data-stu-id="80072-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="80072-132">Determinare se può fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="80072-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="80072-133">Se il provider non è in grado di fornire le credenziali per l'origine di destinazione, deve restituire `null`.</span><span class="sxs-lookup"><span data-stu-id="80072-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="80072-134">Se il provider gestisce le richieste per l'URI di destinazione, ma non può fornire le credenziali, verrà generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="80072-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="80072-135">Un provider di credenziali NuGet personalizzato per Visual Studio deve implementare l'interfaccia `IVsCredentialProvider` disponibile nel [pacchetto NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="80072-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="80072-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="80072-136">GetCredentialAsync</span></span>

| <span data-ttu-id="80072-137">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="80072-137">Input Parameter</span></span> |<span data-ttu-id="80072-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="80072-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="80072-139">Uri URI</span><span class="sxs-lookup"><span data-stu-id="80072-139">Uri uri</span></span> | <span data-ttu-id="80072-140">URI di origine del pacchetto per il quale vengono richieste le credenziali.</span><span class="sxs-lookup"><span data-stu-id="80072-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="80072-141">Proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="80072-141">IWebProxy proxy</span></span> | <span data-ttu-id="80072-142">Proxy Web da usare durante la comunicazione sulla rete.</span><span class="sxs-lookup"><span data-stu-id="80072-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="80072-143">Null se non è stata configurata l'autenticazione proxy.</span><span class="sxs-lookup"><span data-stu-id="80072-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="80072-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="80072-144">bool isProxyRequest</span></span> | <span data-ttu-id="80072-145">True se la richiesta deve ottenere le credenziali di autenticazione del proxy.</span><span class="sxs-lookup"><span data-stu-id="80072-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="80072-146">Se l'implementazione non è valida per l'acquisizione delle credenziali proxy, deve essere restituito null.</span><span class="sxs-lookup"><span data-stu-id="80072-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="80072-147">numero di tentativi bool</span><span class="sxs-lookup"><span data-stu-id="80072-147">bool isRetry</span></span> | <span data-ttu-id="80072-148">True se le credenziali sono state richieste in precedenza per questo URI, ma le credenziali fornite non consentono l'accesso autorizzato.</span><span class="sxs-lookup"><span data-stu-id="80072-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="80072-149">bool non interattivo</span><span class="sxs-lookup"><span data-stu-id="80072-149">bool nonInteractive</span></span> | <span data-ttu-id="80072-150">Se true, il provider di credenziali deve ignorare tutti i prompt utente e usare i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="80072-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="80072-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="80072-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="80072-152">Questo token di annullamento deve essere controllato per determinare se l'operazione che richiede le credenziali è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="80072-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="80072-153">**Valore restituito**: oggetto credentials che implementa l' [interfaccia`System.Net.ICredentials`](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="80072-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
