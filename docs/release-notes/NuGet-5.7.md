---
title: Note sulla versione di NuGet 5,7
description: Note sulla versione per NuGet 5,7, incluse nuove funzionalità, correzioni di bug e DCR.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 6c821091983ab0b5d59b759e1ee9930cf449fd9d
ms.sourcegitcommit: 6cda91f135e58cf57a2471b0c7c4a2f748f40024
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2020
ms.locfileid: "89364168"
---
# <a name="nuget-57-release-notes"></a>Note sulla versione di NuGet 5,7

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio | Disponibile in .NET SDK |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> installato con Visual Studio 2019 con carico di lavoro .NET Core

## <a name="summary-whats-new-in-57"></a>Riepilogo: novità di 5,7

### <a name="features-added-in-this-release"></a>Funzionalità aggiunte in questa versione

* Aggiunta del supporto alias extern per i riferimenti ai pacchetti NuGet- [#4989](https://github.com/NuGet/Home/issues/4989)

* Si è reso più rapido il cambio tra le schede installato e aggiornamenti consentendo loro di condividere un'origine dati e riducendo Resfreshing- [#8294](https://github.com/NuGet/Home/issues/8294)

* Rendere più rapido il ripristino velocizzare le valutazioni chiamando le API Graph statiche di MSBuild (dotnet.exe)- [#9644](https://github.com/NuGet/Home/issues/9644)

* Aggiunta del ripristino parziale di Visual Studio per progetti PackageReference (no-op + +)- [#9513](https://github.com/NuGet/Home/issues/9513)

* L'interfaccia utente di gestione pacchetti di Visual Studio si arresterà in modo anomalo meno spesso durante la ricerca di origini di pacchetti che restituiscono un numero di risultati maggiore di quello richiesto per ogni richiesta HTTP. - [#8478](https://github.com/NuGet/Home/issues/8478)

* Aggiunta dell'integrazione delle informazioni di PackageVersion per i progetti di tipo non SDK in Visual Studio Restore- [#9236](https://github.com/NuGet/Home/issues/9236)

* Aggiunta del supporto per nuget.exe aggiornamento `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)

* Aggiunta del supporto per più file di configurazione nella directory%APPDATA%\NuGet- [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths ora accetta i pacchetti di origine NuGet in account [#9431](https://github.com/NuGet/Home/issues/9431)

* Aggiunta dell'API di estendibilità INuGetProjectService. GetInstalledPackagesAsync- [#9702](https://github.com/NuGet/Home/issues/9702)

* Aggiunta dell'API di interoperabilità per enumerare le cartelle di fallback senza richiedere una soluzione o un progetto [#9395](https://github.com/NuGet/Home/issues/9395)

* Aggiunta `latest` dell'opzione per `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* In un ripristino dell'interfaccia della riga di comando dotnet, quando si avviano plug-in delle credenziali, provare l'interfaccia della riga di comando DotNet sul percorso di sistema se la `DOTNET_HOST_PATH`  variabile di ambiente - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe spec genera un tag Copyright con un testo hardcoded di aaaa, anziché `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe genera l'eccezione ' authors required ' durante il pacchetto di un csproj ignorando i segnaposto e gli attributi AssemblyInfo se il nome dell'assembly viene modificato- [#4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage viene riutilizzato più volte, che non è supportato con SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)

* NuGet. indexing 5.6.0 Preview 3 e versioni successive usano un token di chiave pubblica diverso- [#9481](https://github.com/NuGet/Home/issues/9481)

* Rispettare TreatWarningsAsErrors durante la creazione del pacchetto NuGet: [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Downgrade di pacchetti non corretti per più progetti P2P- [#9549](https://github.com/NuGet/Home/issues/9549)

* La scheda "Sfoglia" non è allineata a sinistra con la casella di ricerca [#9559](https://github.com/NuGet/Home/issues/9559)

* La versione installata non è coerente con l'icona incorporata nell'interfaccia utente del livello di soluzione per un ID pacchetto con più versioni installate- [#9321](https://github.com/NuGet/Home/issues/9321)

* Perdita: PartCreationPolicy (CreationPolicy. nonshareed) NuGet. SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)

* Evitare di leggere il file degli asset nei ripristini no-op- [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet. Protocol non supporta il recupero del numero di download di una versione dalla ricerca [#9086](https://github.com/NuGet/Home/issues/9086)

* Migliorare le prestazioni di memoria di PackageMetadataResourceV3 riducendo le dipendenze di JObject- [#9719](https://github.com/NuGet/Home/issues/9719)

**Progettazione richieste di modifica:**

* L' `<owners>` elemento è stato eliminato quando è ridondante [#5134](https://github.com/NuGet/Home/issues/5134)

* Log IntervalTrackers come eventi ETW- [#9593](https://github.com/NuGet/Home/issues/9593)

* Aggiunto un messaggio informativo sul ripristino per informare gli utenti di CPVM che la funzionalità è in anteprima [#9340](https://github.com/NuGet/Home/issues/9340)

* Popola Esplora soluzioni dipendenze transitive di pacchetto/progetto dal file di asset- [#9580](https://github.com/NuGet/Home/issues/9580)

* La scheda pacchetti installati non dovrebbe impaginare l'elenco dei pacchetti- [#6995](https://github.com/NuGet/Home/issues/6995)

**[Elenco di tutti i problemi risolti in questa versione-5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Contributi della community

Grazie a tutti i collaboratori che hanno contribuito a rendere questa versione di NuGet eccezionale.

|Chi|Richieste pull|Problemi|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet. Protocol non supporta il recupero del numero di download di una versione dalla ricerca [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage viene riutilizzato più volte, che non è supportato con SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661)|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|L' `<owners>` elemento è stato eliminato quando è ridondante [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (BlackGad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet non è in grado di eseguire il ripristino da origini HTTPS che richiedono certificati client- [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim future proofing- [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunnita (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe spec genera un tag Copyright con un testo hardcoded di aaaa, anziché `$copyright$`  -  [#8696](https://github.com/NuGet/Home/issues/8696)|
|[Olivier Spinelli (Olivier-Spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|In un ripristino dell'interfaccia della riga di comando dotnet, quando si avviano plug-in delle credenziali, provare l'interfaccia della riga di comando DotNet sul percorso di sistema se la `DOTNET_HOST_PATH`  variabile di ambiente - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyzhang](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|Aggiunta `latest` dell'opzione per `-MSBuildVersion`  -  [#8808](https://github.com/NuGet/Home/issues/8808)|
