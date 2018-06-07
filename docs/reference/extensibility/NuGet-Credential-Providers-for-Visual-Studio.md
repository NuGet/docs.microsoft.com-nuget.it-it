---
title: Provider di credenziali di NuGet per Visual Studio
description: Il provider di credenziali di NuGet l'autenticazione con il feed implementando l'interfaccia IVsCredentialProvider in un'estensione di Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: d4dbcab7c4005efcdc7efe96df3a70e666c558cc
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817844"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>L'autenticazione di feed in Visual Studio con il provider di credenziali di NuGet

L'estensione di NuGet di Visual Studio 3.6 + supporta i provider di credenziali, che consentono a utilizzare i feed autenticato NuGet.
Dopo aver installato un provider di credenziali di NuGet per Visual Studio, l'estensione NuGet di Visual Studio automaticamente acquisisce e aggiorna le credenziali per i feed autenticati in base alle esigenze.

Un'implementazione di esempio è reperibile [l'esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> Provider di credenziali di NuGet per Visual Studio deve essere installato come un'estensione di Visual Studio regolari e richiederà [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (attualmente in anteprima) o versione successiva.
>
> Provider di credenziali di NuGet per Visual Studio funziona solo in Visual Studio (non in ripristino dotnet o nuget.exe). Per i provider di credenziali con nuget.exe, vedere [nuget.exe provider di credenziali](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Provider di credenziali disponibili NuGet per Visual Studio

È un provider di credenziali incorporato l'estensione NuGet di Visual Studio per il supporto di Visual Studio Team Services.

L'estensione NuGet di Visual Studio utilizza un oggetto interno `VsCredentialProviderImporter` che esegue l'analisi anche per i provider di credenziali di plug-in. Questi provider di credenziali di plug-in deve essere individuabile come un'esportazione MEF di tipo `IVsCredentialProvider`.

Provider di credenziali di plug-in disponibili includono:

- [Provider di credenziali MyGet per Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Creazione di un provider di credenziali di NuGet per Visual Studio

L'estensione di NuGet di Visual Studio 3.6 + implementa un CredentialService interna che viene usato per acquisire le credenziali. Il CredentialService include un elenco di provider di credenziali predefinite e plug-in. Ogni provider è tentati in ordine sequenziale fino a quando non vengono acquisite le credenziali.

Durante l'acquisizione delle credenziali, il servizio di credenziali tenterà di provider di credenziali nell'ordine seguente, l'arresto, non appena vengono acquisite le credenziali:

1. Le credenziali verranno recuperate dai file di configurazione NuGet (utilizzando l'elemento predefinito `SettingsCredentialProvider`).
1. Se l'origine del pacchetto si trova in Visual Studio Team Services, il `VisualStudioAccountProvider` verrà utilizzato.
1. Tutti gli altri provider di credenziali di plug-in verrà tentata in sequenza.
1. Se non sono state acquisite senza credenziali, verrà richiesto all'utente le credenziali utilizzando una finestra di dialogo di autenticazione standard.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementazione IVsCredentialProvider.GetCredentialsAsync

Per creare un provider di credenziali di NuGet per Visual Studio, creare un'estensione di Visual Studio che espone un pubblico esportazione MEF che implementa il `IVsCredentialProvider` tipo ed è conforme ai principi descritti di seguito.

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

Un'implementazione di esempio è reperibile [l'esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Ogni provider di credenziali di NuGet per Visual Studio è necessario:

1. Determinare se è possibile fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali. Se il provider non può fornire le credenziali per l'origine di destinazione, quindi deve essere restituito `null`.
1. Se il provider di gestire le richieste per l'URI di destinazione, ma non è possibile fornire le credenziali, deve essere generata un'eccezione.

Deve implementare un provider di credenziali personalizzato di NuGet per Visual Studio il `IVsCredentialProvider` disponibile nell'interfaccia di [pacchetto NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parametro di input |Descrizione|
| ----------------|-----------|
| Uri di URI | L'Uri di origine pacchetto per cui le credenziali vengono richiesti.|
| Interfaccia IWebProxy proxy | Proxy Web da utilizzare durante la comunicazione in rete. Null se non esiste alcuna autenticazione proxy configurata. |
| bool isProxyRequest | True se è richiesta per ottenere le credenziali di autenticazione di proxy. Se l'implementazione non è valido per l'acquisizione delle credenziali del proxy, quindi deve essere restituito null. |
| bool isRetry | True se le credenziali sono stati richiesti in precedenza per questo Uri, ma le credenziali fornite non consentiva l'accesso autorizzato. |
| bool non interattivi | Se true, il provider di credenziali necessario eliminare tutti i prompt utente e utilizzare invece i valori predefiniti. |
| CancellationToken cancellationToken | Questo token di annullamento deve essere controllato per determinare se le credenziali di richiesta di operazione è stata annullata. |

**Valore restituito**: un oggetto credenziali che implementa le [ `System.Net.ICredentials` interfaccia](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
