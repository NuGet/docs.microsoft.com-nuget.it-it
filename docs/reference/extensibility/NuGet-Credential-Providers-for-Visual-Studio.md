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
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Autenticazione dei feed in Visual Studio con i provider di credenziali NuGet

L'estensione di Visual Studio NuGet 3.6 + supporta i provider di credenziali che consentono a NuGet di usare i feed autenticati.
Dopo aver installato un provider di credenziali NuGet per Visual Studio, l'estensione NuGet di Visual Studio acquisisce e aggiorna automaticamente le credenziali per i feed autenticati, se necessario.

È possibile trovare un'implementazione di esempio nell' [esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

A partire da 4.8 + NuGet in Visual Studio supporta anche i nuovi plug-in di autenticazione multipiattaforma, ma non è l'approccio consigliato per motivi di prestazioni.

> [!Note]
> I provider di credenziali NuGet per Visual Studio devono essere installati come un'estensione di Visual Studio normale e richiedono [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) o versione successiva.
>
> I provider di credenziali NuGet per Visual Studio funzionano solo in Visual Studio (non in dotnet restore o NuGet. exe). Per i provider di credenziali con NuGet. exe, vedere [provider di credenziali NuGet. exe](nuget-exe-Credential-providers.md).
> Per i provider di credenziali in dotnet e MSBuild vedere plug-in [NuGet multipiattaforma](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Provider di credenziali NuGet disponibili per Visual Studio

È disponibile un provider di credenziali incorporato nell'estensione NuGet di Visual Studio per supportare Visual Studio Team Services.

L'estensione NuGet di Visual Studio usa una `VsCredentialProviderImporter` interna che analizza anche i provider di credenziali plug-in. Questi provider di credenziali plug-in devono essere individuabili come esportazione MEF di tipo `IVsCredentialProvider`.

I provider di credenziali plug-in disponibili includono:

- [Provider di credenziali MyGet per Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Creazione di un provider di credenziali NuGet per Visual Studio

L'estensione di Visual Studio NuGet 3.6 + implementa un CredentialService interno usato per acquisire le credenziali. Il CredentialService include un elenco di provider di credenziali plug-in e incorporati. Ogni provider viene eseguito in modo sequenziale fino a quando le credenziali non vengono acquisite.

Durante l'acquisizione delle credenziali, il servizio credenziali tenterà i provider di credenziali nell'ordine seguente e verrà arrestato non appena vengono acquisite le credenziali:

1. Le credenziali verranno recuperate dai file di configurazione NuGet (usando la `SettingsCredentialProvider`incorporata).
1. Se l'origine del pacchetto si trova in Visual Studio Team Services, verrà utilizzato il `VisualStudioAccountProvider`.
1. Tutti gli altri provider di credenziali di Visual Studio plug-in verranno tentati in sequenza.
1. Provare a usare tutti i provider di credenziali multipiattaforma NuGet in sequenza.
1. Se non è stata ancora acquisita alcuna credenziale, all'utente verranno richieste le credenziali utilizzando una finestra di dialogo di autenticazione di base standard.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>Implementazione di IVsCredentialProvider. GetCredentialsAsync

Per creare un provider di credenziali NuGet per Visual Studio, creare un'estensione di Visual Studio che espone un'esportazione MEF pubblica implementando il tipo di `IVsCredentialProvider` e aderisca ai principi descritti di seguito.

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

È possibile trovare un'implementazione di esempio nell' [esempio VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Ogni provider di credenziali NuGet per Visual Studio deve:

1. Determinare se può fornire le credenziali per l'URI di destinazione prima di avviare l'acquisizione delle credenziali. Se il provider non è in grado di fornire le credenziali per l'origine di destinazione, deve restituire `null`.
1. Se il provider gestisce le richieste per l'URI di destinazione, ma non può fornire le credenziali, verrà generata un'eccezione.

Un provider di credenziali NuGet personalizzato per Visual Studio deve implementare l'interfaccia `IVsCredentialProvider` disponibile nel [pacchetto NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Parametro di input |Descrizione|
| ----------------|-----------|
| Uri URI | URI di origine del pacchetto per il quale vengono richieste le credenziali.|
| Proxy IWebProxy | Proxy Web da usare durante la comunicazione sulla rete. Null se non è stata configurata l'autenticazione proxy. |
| bool isProxyRequest | True se la richiesta deve ottenere le credenziali di autenticazione del proxy. Se l'implementazione non è valida per l'acquisizione delle credenziali proxy, deve essere restituito null. |
| numero di tentativi bool | True se le credenziali sono state richieste in precedenza per questo URI, ma le credenziali fornite non consentono l'accesso autorizzato. |
| bool non interattivo | Se true, il provider di credenziali deve ignorare tutti i prompt utente e usare i valori predefiniti. |
| CancellationToken cancellationToken | Questo token di annullamento deve essere controllato per determinare se l'operazione che richiede le credenziali è stata annullata. |

**Valore restituito**: oggetto credentials che implementa l' [interfaccia`System.Net.ICredentials`](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
