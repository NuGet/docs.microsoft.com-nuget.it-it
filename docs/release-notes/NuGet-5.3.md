---
title: Note sulla versione di NuGet 5,3
description: Note sulla versione per NuGet 5,3, incluse nuove funzionalità, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774101"
---
# <a name="nuget-53-release-notes"></a>Note sulla versione di NuGet 5,3

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.3.0-preview3**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,3 Preview 3](https://visualstudio.microsoft.com/vs/preview/) | [3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup> |

<sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-53-preview-3"></a>Riepilogo: Novità di 5,3 Preview 3

* [L'icona del pacchetto può essere incorporata nel pacchetto](../reference/msbuild-targets.md#packing-an-icon-image-file), anziché richiedere un URL esterno. - [#352](https://github.com/NuGet/Home/issues/352)

* Sicurezza migliorata con il rilevamento e l'imposizione di SHA per Packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Visual Studio: gli assembly sono completamente NGen-ed non parzialmente NGen-ed- [#8513](https://github.com/NuGet/Home/issues/8513)

* Ridurre l'utilizzo della memoria (annullare la sottoscrizione agli eventi)- [#8471](https://github.com/NuGet/Home/issues/8471)

* Il messaggio "Error_UnableToFindProjectInfo" non è grammaticalmente corretto- [#8441](https://github.com/NuGet/Home/issues/8441)

* Miglioramenti di NU1403: convalida di tutti i pacchetti, inclusi i valori Sha previsti/effettivi [#8424](https://github.com/NuGet/Home/issues/8424)

* Enumerazione multipla in NuGetPackageManager. PreviewUpdatePackagesAsync- [#8401](https://github.com/NuGet/Home/issues/8401)

* Annulla la modifica "Public-> Internal" in PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)

* IVsPackageSourceProvider. GetSources (...) ha un comportamento di eccezione definito in modo non corretto- [#8383](https://github.com/NuGet/Home/issues/8383)

* Rendere pubblico il costruttore PluginManager- [#8379](https://github.com/NuGet/Home/issues/8379)

* Metriche per tenere traccia della frequenza di aggiornamento dell'interfaccia utente di PM- [#8369](https://github.com/NuGet/Home/issues/8369)

* Ridurre il numero di aggiornamenti dell'interfaccia utente durante l'installazione tramite l'interfaccia utente di gestione pacchetti- [#8358](https://github.com/NuGet/Home/issues/8358)

* Telemetria: i valori DateTime usano formati specifici delle impostazioni cultura- [#8351](https://github.com/NuGet/Home/issues/8351)

* Ridurre gli aggiornamenti dell'interfaccia utente nella scheda Sfoglia dell'interfaccia utente di gestione pacchetti #6570- [#8339](https://github.com/NuGet/Home/issues/8339)

* [Errore test] "Impossibile analizzare il file di configurazione" richiede due volte [#8320](https://github.com/NuGet/Home/issues/8320)

* Genera un errore NU5037 con una pagina del documento corretta che illustra le correzioni dei clienti (nel pacchetto manca il file nuspec necessario)- [#8291](https://github.com/NuGet/Home/issues/8291)

* Il ripristino in modalità bloccata non riesce quando viene modificato il RuntimeIdentifier di un progetto [#8260](https://github.com/NuGet/Home/issues/8260)

* Eseguire la lettura delle impostazioni in VS Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)

* La regressione nell'"origine NuGet Add" causa "il carattere": ", valore esadecimale 0x3A, non può essere incluso in un nome" Errors- [#7948](https://github.com/NuGet/Home/issues/7948)

* Provider di credenziali del plug-in NuGet: nascondere la finestra del processo [#7511](https://github.com/NuGet/Home/issues/7511)

* Imponi PackagePathResolver è un percorso assoluto [#7349](https://github.com/NuGet/Home/issues/7349)

* Ridurre gli aggiornamenti dell'interfaccia utente nelle schede installa e aggiorna dell'interfaccia utente di gestione pacchetti- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR:**

* Aggiornare i Framework Novell per eseguire il mapping a NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Abilitare la copia del contenuto di gestione pacchetti "finestra di anteprima" per l'installazione/aggiornamento [#8324](https://github.com/NuGet/Home/issues/8324)

* Abilita ripristino nei file con estensione proj- [#8212](https://github.com/NuGet/Home/issues/8212)

* Introdurre `NUGET_NETFX_PLUGIN_PATHS` e`NUGET_NETCORE_PLUGIN_PATHS` per supportare la configurazione di entrambi allo stesso tempo- [#8151](https://github.com/NuGet/Home/issues/8151)

* Abilitare più versioni per un PackageDownload tramite l'attributo Version [#8074](https://github.com/NuGet/Home/issues/8074)

* Opzioni Add-SolutionDirectory e-PackageDirectory per NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)

* Abilitare il pacchetto NuGet come deterministico- [#6229](https://github.com/NuGet/Home/issues/6229)

**[Elenco di tutti i problemi risolti in questa versione-5,3 Preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**
