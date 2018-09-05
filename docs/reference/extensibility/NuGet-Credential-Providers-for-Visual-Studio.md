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
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>L'autenticazione di feed di Visual Studio con i provider di credenziali NuGet

L'estensione di NuGet di Visual Studio 3.6 + supporta i provider di credenziali, che consentono di NuGet lavorare con i feed autenticati.
Dopo aver installato un provider di credenziali NuGet per Visual Studio, l'estensione NuGet di Visual Studio verrà automaticamente acquisire e aggiornare le credenziali per i feed autenticati, se necessario.

Un'implementazione di esempio sono disponibili nel [dell'esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

A partire da 4.8 NuGet in Visual Studio supporta i nuovi cross-platform autenticazione plug-in anche, ma non sono l'approccio consigliato per motivi di prestazioni.

> [!Note]
> I provider di credenziali NuGet per Visual Studio deve essere installati come un'estensione di Visual Studio regolare e richiederà [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) o versione successiva.
>
> I provider di credenziali NuGet per Visual Studio funzionano solo in Visual Studio (non in dotnet-restore o nuget.exe). Per i provider di credenziali con nuget.exe, vedere [nuget.exe i provider di credenziali](nuget-exe-Credential-providers.md).
> Per credential provider in msbuild e dotnet vedere [NuGet cross-platform i plug-in](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Disponibili provider di credenziali NuGet per Visual Studio

È disponibile un provider di credenziali creato nell'estensione NuGet di Visual Studio per supportare Visual Studio Team Services.

L'estensione NuGet di Visual Studio Usa interna `VsCredentialProviderImporter` che esegue l'analisi anche per i provider di credenziali plug-in. Questi provider di credenziali plug-in devono essere individuati come un'esportazione MEF di tipo `IVsCredentialProvider`.

I provider di credenziali plug-in disponibili includono:

- [Provider di credenziali MyGet per Visual Studio 2017](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Creazione di un provider di credenziali NuGet per Visual Studio

L'estensione di NuGet di Visual Studio 3.6 + implementa un CredentialService interna che viene usato per acquisire le credenziali. Il CredentialService include un elenco di provider di credenziali incorporati e plug-in. Ogni provider viene provata in sequenza fino a quando non vengono acquisite le credenziali.

Durante l'acquisizione delle credenziali, il servizio di credenziale prova i provider di credenziali nell'ordine seguente, l'arresto, non appena vengono acquisite le credenziali:

1. Le credenziali verranno recuperate dai file di configurazione NuGet (usando l'elemento predefinito `SettingsCredentialProvider`).
1. Se l'origine del pacchetto si trova in Visual Studio Team Services, il `VisualStudioAccountProvider` verrà utilizzato.
1. Tutti gli altri plug-in Visual Studio i provider di credenziali verranno tentati in modo sequenziale.
1. Provare a usare NuGet tutti cross-platform i provider di credenziali in modo sequenziale.
1. Se le credenziali non sono state acquisite, l'utente verrà richiesto per le credenziali utilizzando una finestra di dialogo di autenticazione di base standard.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementazione IVsCredentialProvider.GetCredentialsAsync

Per creare un provider di credenziali NuGet per Visual Studio, creare un'estensione di Visual Studio che espone un pubblico esportazione MEF che implementa il `IVsCredentialProvider` digitare ed è conforme ai principi descritti di seguito.

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

Un'implementazione di esempio sono disponibili nel [dell'esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Ogni provider di credenziali NuGet per Visual Studio deve:

1. Determinare se è possibile fornire le credenziali per l'URI di destinazione prima di iniziare l'acquisizione delle credenziali. Se il provider non è possibile specificare le credenziali per l'origine di destinazione, quindi il metodo deve restituire `null`.
1. Se il provider di gestione delle richieste per l'URI di destinazione, ma non è possibile specificare le credenziali, deve essere generata un'eccezione.

Deve implementare un provider di credenziali NuGet personalizzato per Visual Studio il `IVsCredentialProvider` disponibile nell'interfaccia di [pacchetto NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parametro di input |Descrizione|
| ----------------|-----------|
| Uri di URI | L'Uri di origine pacchetto per il quale le credenziali richieste.|
| Proxy IWebProxy | Proxy Web da utilizzare durante la comunicazione in rete. Null se non esiste alcuna autenticazione proxy configurata. |
| isProxyRequest bool | True se la richiesta è per ottenere le credenziali di autenticazione proxy. Se l'implementazione non è valido per l'acquisizione delle credenziali del proxy, quindi deve essere restituito null. |
| isRetry bool | True se le credenziali sono stati richiesti in precedenza per questo Uri, ma le credenziali fornite non consentiva l'accesso autorizzato. |
| bool non interattive | Se true, il provider di credenziali è necessario eliminare tutti i prompt utente e usare invece i valori predefiniti. |
| Elemento CancellationToken determina l'oggetto CancellationToken | Questo token di annullamento deve essere controllato per determinare se le credenziali di richiesta di operazione è stata annullata. |

**Valore restituito**: un oggetto credenziali che implementa le [ `System.Net.ICredentials` interfaccia](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
