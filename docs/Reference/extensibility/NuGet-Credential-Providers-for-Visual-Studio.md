---
title: Provider di credenziali di NuGet per Visual Studio | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: Il provider di credenziali di NuGet l'autenticazione con il feed implementando l'interfaccia IVsCredentialProvider in un'estensione di Visual Studio.
keywords: Eseguire l'autenticazione con la raccolta, estensione di visual studio NuGet, l'autenticazione con il feed NuGet i provider di credenziali,
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="e05a8-104">L'autenticazione di feed in Visual Studio con il provider di credenziali di NuGet</span><span class="sxs-lookup"><span data-stu-id="e05a8-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="e05a8-105">L'estensione di NuGet di Visual Studio 3.6 + supporta i provider di credenziali, che consentono a utilizzare i feed autenticato NuGet.</span><span class="sxs-lookup"><span data-stu-id="e05a8-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="e05a8-106">Dopo aver installato un provider di credenziali di NuGet per Visual Studio, l'estensione NuGet di Visual Studio automaticamente acquisisce e aggiorna le credenziali per i feed autenticati in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e05a8-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="e05a8-107">Un'implementazione di esempio è reperibile [l'esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="e05a8-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="e05a8-108">Provider di credenziali di NuGet per Visual Studio deve essere installato come un'estensione di Visual Studio regolari e richiederà [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (attualmente in anteprima) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e05a8-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="e05a8-109">Provider di credenziali di NuGet per Visual Studio funziona solo in Visual Studio (non in ripristino dotnet o nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="e05a8-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="e05a8-110">Per i provider di credenziali con nuget.exe, vedere [nuget.exe provider di credenziali](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="e05a8-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="e05a8-111">Provider di credenziali disponibili NuGet per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e05a8-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="e05a8-112">È un provider di credenziali incorporato l'estensione NuGet di Visual Studio per il supporto di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="e05a8-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="e05a8-113">L'estensione NuGet di Visual Studio utilizza un oggetto interno `VsCredentialProviderImporter` che esegue l'analisi anche per i provider di credenziali di plug-in.</span><span class="sxs-lookup"><span data-stu-id="e05a8-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="e05a8-114">Questi provider di credenziali di plug-in deve essere individuabile come un'esportazione MEF di tipo `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="e05a8-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="e05a8-115">Provider di credenziali di plug-in disponibili includono:</span><span class="sxs-lookup"><span data-stu-id="e05a8-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="e05a8-116">Provider di credenziali MyGet per Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e05a8-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="e05a8-117">Creazione di un provider di credenziali di NuGet per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e05a8-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="e05a8-118">L'estensione di NuGet di Visual Studio 3.6 + implementa un CredentialService interna che viene usato per acquisire le credenziali.</span><span class="sxs-lookup"><span data-stu-id="e05a8-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="e05a8-119">Il CredentialService include un elenco di provider di credenziali predefinite e plug-in.</span><span class="sxs-lookup"><span data-stu-id="e05a8-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="e05a8-120">Ogni provider è tentati in ordine sequenziale fino a quando non vengono acquisite le credenziali.</span><span class="sxs-lookup"><span data-stu-id="e05a8-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="e05a8-121">Durante l'acquisizione delle credenziali, il servizio di credenziali tenterà di provider di credenziali nell'ordine seguente, l'arresto, non appena vengono acquisite le credenziali:</span><span class="sxs-lookup"><span data-stu-id="e05a8-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="e05a8-122">Le credenziali verranno recuperate dai file di configurazione NuGet (utilizzando l'elemento predefinito `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="e05a8-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="e05a8-123">Se l'origine del pacchetto si trova in Visual Studio Team Services, il `VisualStudioAccountProvider` verrà utilizzato.</span><span class="sxs-lookup"><span data-stu-id="e05a8-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="e05a8-124">Tutti gli altri provider di credenziali di plug-in verrà tentata in sequenza.</span><span class="sxs-lookup"><span data-stu-id="e05a8-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="e05a8-125">Se non sono state acquisite senza credenziali, verrà richiesto all'utente le credenziali utilizzando una finestra di dialogo di autenticazione standard.</span><span class="sxs-lookup"><span data-stu-id="e05a8-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="e05a8-126">Implementazione IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="e05a8-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="e05a8-127">Per creare un provider di credenziali di NuGet per Visual Studio, creare un'estensione di Visual Studio che espone un pubblico esportazione MEF che implementa il `IVsCredentialProvider` tipo ed è conforme ai principi descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="e05a8-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="e05a8-128">Un'implementazione di esempio è reperibile [l'esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="e05a8-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="e05a8-129">Ogni provider di credenziali di NuGet per Visual Studio è necessario:</span><span class="sxs-lookup"><span data-stu-id="e05a8-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="e05a8-130">Determinare se è possibile fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="e05a8-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="e05a8-131">Se il provider non può fornire le credenziali per l'origine di destinazione, quindi deve essere restituito `null`.</span><span class="sxs-lookup"><span data-stu-id="e05a8-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="e05a8-132">Se il provider di gestire le richieste per l'URI di destinazione, ma non è possibile fornire le credenziali, deve essere generata un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="e05a8-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="e05a8-133">Deve implementare un provider di credenziali personalizzato di NuGet per Visual Studio il `IVsCredentialProvider` disponibile nell'interfaccia di [pacchetto NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="e05a8-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="e05a8-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="e05a8-134">GetCredentialAsync</span></span>

| <span data-ttu-id="e05a8-135">Parametro di input</span><span class="sxs-lookup"><span data-stu-id="e05a8-135">Input Parameter</span></span> |<span data-ttu-id="e05a8-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e05a8-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="e05a8-137">Uri di URI</span><span class="sxs-lookup"><span data-stu-id="e05a8-137">Uri uri</span></span> | <span data-ttu-id="e05a8-138">L'Uri di origine pacchetto per cui le credenziali vengono richiesti.</span><span class="sxs-lookup"><span data-stu-id="e05a8-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="e05a8-139">Interfaccia IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="e05a8-139">IWebProxy proxy</span></span> | <span data-ttu-id="e05a8-140">Proxy Web da utilizzare durante la comunicazione in rete.</span><span class="sxs-lookup"><span data-stu-id="e05a8-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="e05a8-141">Null se non esiste alcuna autenticazione proxy configurata.</span><span class="sxs-lookup"><span data-stu-id="e05a8-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="e05a8-142">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="e05a8-142">bool isProxyRequest</span></span> | <span data-ttu-id="e05a8-143">True se è richiesta per ottenere le credenziali di autenticazione di proxy.</span><span class="sxs-lookup"><span data-stu-id="e05a8-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="e05a8-144">Se l'implementazione non è valido per l'acquisizione delle credenziali del proxy, quindi deve essere restituito null.</span><span class="sxs-lookup"><span data-stu-id="e05a8-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="e05a8-145">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="e05a8-145">bool isRetry</span></span> | <span data-ttu-id="e05a8-146">True se le credenziali sono stati richiesti in precedenza per questo Uri, ma le credenziali fornite non consentiva l'accesso autorizzato.</span><span class="sxs-lookup"><span data-stu-id="e05a8-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="e05a8-147">bool non interattivi</span><span class="sxs-lookup"><span data-stu-id="e05a8-147">bool nonInteractive</span></span> | <span data-ttu-id="e05a8-148">Se true, il provider di credenziali necessario eliminare tutti i prompt utente e utilizzare invece i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="e05a8-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="e05a8-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="e05a8-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="e05a8-150">Questo token di annullamento deve essere controllato per determinare se le credenziali di richiesta di operazione è stata annullata.</span><span class="sxs-lookup"><span data-stu-id="e05a8-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |
  
<span data-ttu-id="e05a8-151">**Valore restituito**: un oggetto credenziali che implementa il [ `System.Net.ICredentials` interfaccia](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span><span class="sxs-lookup"><span data-stu-id="e05a8-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span></span>
