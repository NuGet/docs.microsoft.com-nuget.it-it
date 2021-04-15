---
title: Note sulla versione di NuGet 5.7
description: Note sulla versione per NuGet 5.7, tra cui nuove funzionalità, correzioni di bug e controller di dominio.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508787"
---
# <a name="nuget-57-release-notes"></a>Note sulla versione di NuGet 5.7

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |
| [**5.7.1**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.7](https://visualstudio.microsoft.com/downloads/) | [3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1 Installato</sup> con il carico di lavoro Visual Studio 2019 con .NET Core

## <a name="summary-whats-new-in-57"></a>Riepilogo: Novità della versione 5.7

### <a name="features-added-in-this-release"></a>Funzionalità aggiunte in questa versione

* Aggiunta del supporto degli alias extern per i riferimenti ai pacchetti NuGet - [#4989](https://github.com/NuGet/Home/issues/4989)

* Il passaggio tra le schede Installato e Aggiornamenti è stato reso più rapido consentendo loro di condividere un'origine dati e riducendo il rifreshing [- #8294](https://github.com/NuGet/Home/issues/8294)

* Velocizzare il ripristino: velocizzare le valutazioni chiamando le API di msBuild Static Graph (dotnet.exe) - [#9644](https://github.com/NuGet/Home/issues/9644)

* Aggiunta Visual Studio ripristino parziale per i progetti PackageReference (no-op++) - [#9513](https://github.com/NuGet/Home/issues/9513)

* Visual Studio Gestione pacchetti'interfaccia utente si arresta meno spesso durante la ricerca di origini di pacchetti non corretti che restituiscono un numero maggiore del numero richiesto di risultati per ogni richiesta HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Aggiunta dell'integrazione delle informazioni PackageVersion per i progetti in stile non SDK nel ripristino di Visual Studio - [#9236](https://github.com/NuGet/Home/issues/9236)

* Aggiunta del supporto per nuget.exe aggiornamento `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Aggiunta del supporto per più file di configurazione nella directory %APPDATA%\NuGet - [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths prende ora in considerazione i pacchetti di origine NuGet [#9431](https://github.com/NuGet/Home/issues/9431)

* Aggiunta dell'API di estendibilità INuGetProjectService.GetInstalledPackagesAsync - [#9702](https://github.com/NuGet/Home/issues/9702)

* Aggiunta dell'API di interoperabilità per enumerare le cartelle di fallback senza richiedere una soluzione o un [progetto - #9395](https://github.com/NuGet/Home/issues/9395)

* Aggiunta `latest` dell'opzione `-MSBuildVersion`  -  [per #8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug:**

* In un ripristino dell'interfaccia della riga di comando dotnet, quando si avviano i plug-in delle credenziali, provare l'interfaccia della riga di comando dotnet nel percorso di sistema se la variabile di ambiente `DOTNET_HOST_PATH`  non è definita. - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe specifica genera un tag di copyright con testo hard-coded di Copyright YYYY anziché `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe genera l'eccezione 'authors required' durante il pacchetto di un file csproj ignorando i segnaposto e gli attributi assemblyinfo se il nome dell'assembly viene modificato [- #4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage viene riutilizzato più volte, operazione non supportata con SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet.Indexing 5.6.0 Preview 3 e versioni successive usano un token di chiave pubblica diverso: [#9481](https://github.com/NuGet/Home/issues/9481)

* Rispettare TreatWarningsAsErrors durante la creazione del pacchetto NuGet - [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Downgrade dei pacchetti non valido per più progetti p2p - [#9549](https://github.com/NuGet/Home/issues/9549)

* La scheda "Sfoglia" non è allineata a sinistra con la casella di ricerca [#9559](https://github.com/NuGet/Home/issues/9559)

* La versione installata non è coerente con l'icona incorporata nell'interfaccia utente di Gestione pacchetti a livello di soluzione per un ID pacchetto con più versioni installate [#9321](https://github.com/NuGet/Home/issues/9321)

* Perdita: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger - [#9595](https://github.com/NuGet/Home/issues/9595)

* Evitare di leggere il file di asset in ripristini senza operazioni - [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet.Protocol non supporta il recupero del numero di download di una versione dalla ricerca [- #9086](https://github.com/NuGet/Home/issues/9086)

* Migliorare le prestazioni della memoria di PackageMetadataResourceV3 riducendo le dipendenze JObject - [#9719](https://github.com/NuGet/Home/issues/9719)

**Progettare le richieste di modifica:**

* L'elemento `<owners>` è stato eliminato quando è ridondante- [#5134](https://github.com/NuGet/Home/issues/5134)

* Log IntervalTrackers come eventi ETW - [#9593](https://github.com/NuGet/Home/issues/9593)

* Aggiunta di un messaggio informativo al ripristino per informare gli utenti cpvm che la funzionalità è in anteprima [- #9340](https://github.com/NuGet/Home/issues/9340)

* Popolare le Esplora soluzioni transitive di pacchetto/progetto dal file di asset - [#9580](https://github.com/NuGet/Home/issues/9580)

* La scheda Pacchetti installati non deve impaginare l'elenco dei [pacchetti- #6995](https://github.com/NuGet/Home/issues/6995)

**[Elenco di tutti i problemi risolti in questa versione - 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Contributi della community

Grazie a tutti i collaboratori che hanno contribuito a rendere straordinaria questa versione di NuGet.

|Chi|Prs|Problemi|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet.Protocol non supporta il recupero del numero di download di una versione dalla ricerca [- #9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage viene riutilizzato più volte che non è supportato con SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|L'elemento `<owners>` è stato eliminato quando è ridondante- [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet non può eseguire il ripristino da origini HTTPS che richiedono certificati client [- #5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|Strumenti di correzione futuri di HttpSourceAuthenticationHandler SemaphoreSlim - [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe specifica genera un tag di copyright con testo hard-coded di Copyright YYYY `$copyright$`  -  [anziché #8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (olivier-spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|In un ripristino dell'interfaccia della riga di comando dotnet, quando si avviano i plug-in delle credenziali, provare l'interfaccia della riga di comando dotnet nel percorso di sistema se la variabile di ambiente `DOTNET_HOST_PATH`  non è definita. - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Aggiunta `latest` dell'opzione per `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|

## <a name="summary-whats-new-in-571"></a>Riepilogo: Novità della versione 5.7.1

* Estendere il file con estensione nupkg.metadata per includere l'origine di installazione [- #10354](https://github.com/NuGet/Home/issues/10354)

* Registrare il contenuto del pacchetto durante la registrazione del ripristino (durante [l'estrazione)](https://github.com/NuGet/Home/issues/10384) - #10384

* Quando si esegue il ripristino al livello di dettaglio normale, registrare l'origine da cui viene ripristinato un pacchetto [#10461](https://github.com/NuGet/Home/issues/10461)

**[Elenco di tutti i problemi risolti in questa versione - 5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**

**[Elenco dei commit in questa versione - 5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**
