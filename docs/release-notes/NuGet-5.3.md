---
title: Note sulla versione di NuGet 5,3
description: Note sulla versione per NuGet 5,3, incluse nuove funzionalità, correzioni di bug e DCR.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: e77219d355f73f3bf01f68283ffb2759813af563
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611317"
---
# <a name="nuget-53-release-notes"></a>Note sulla versione di NuGet 5,3

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.3.6](https://visualstudio.microsoft.com/downloads/) | [Versione futura: 3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-53"></a>Riepilogo: novità di 5,3

* [L'icona del pacchetto può essere incorporata nel pacchetto](../reference/msbuild-targets.md#packing-an-icon-image-file), anziché richiedere un URL esterno. - [#352](https://github.com/NuGet/Home/issues/352)

* Sicurezza migliorata con il rilevamento e l'imposizione di SHA per Packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)

* Abilitare la deprecazione di pacchetti NuGet obsoleti o legacy [#2867](https://github.com/NuGet/Home/issues/2867) | [post di Blog](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](https://docs.microsoft.com/nuget/nuget-org/deprecate-packages)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* I pacchetti NuGet prodotti con 3.0.100-preview9 SDK non possono essere usati dagli utenti di 2,2 SDK... a seconda del fuso orario [#8603](https://github.com/NuGet/Home/issues/8603)

* La virgoletta "caratteri nel percorso provoca un errore di caratteri non validi nel percorso" in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)

* Visual Studio: gli assembly sono completamente NGen-ed non parzialmente NGen-ed- [#8513](https://github.com/NuGet/Home/issues/8513)

* Ridurre l'utilizzo della memoria (annullare la sottoscrizione agli eventi)- [#8471](https://github.com/NuGet/Home/issues/8471)

* Il messaggio "Error_UnableToFindProjectInfo" non è grammaticalmente corretto- [#8441](https://github.com/NuGet/Home/issues/8441)

* Miglioramenti di NU1403: convalida di tutti i pacchetti, inclusi i valori Sha previsti/effettivi [#8424](https://github.com/NuGet/Home/issues/8424)

* Enumerazione multipla in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)

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

* La regressione in `Nuget sources add` causa l'errore "il carattere ':', valore esadecimale 0x3A, non può essere incluso in un nome" Errors- [#7948](https://github.com/NuGet/Home/issues/7948)

* Provider di credenziali del plug-in NuGet: nascondere la finestra del processo [#7511](https://github.com/NuGet/Home/issues/7511)

* Imponi PackagePathResolver è un percorso assoluto [#7349](https://github.com/NuGet/Home/issues/7349)

* Ridurre gli aggiornamenti dell'interfaccia utente nelle schede installa e aggiorna dell'interfaccia utente di gestione pacchetti- [#6570](https://github.com/NuGet/Home/issues/6570)

**DCR:**

* Aggiornare i Framework Novell per eseguire il mapping a NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Abilitare la copia del contenuto di gestione pacchetti "finestra di anteprima" per l'installazione/aggiornamento [#8324](https://github.com/NuGet/Home/issues/8324)

* Abilita ripristino nei file con estensione proj- [#8212](https://github.com/NuGet/Home/issues/8212)

* Introdurre `NUGET_NETFX_PLUGIN_PATHS` e `NUGET_NETCORE_PLUGIN_PATHS` per supportare la configurazione di entrambi allo stesso tempo: [#8151](https://github.com/NuGet/Home/issues/8151)

* Abilitare più versioni per un PackageDownload tramite l'attributo Version [#8074](https://github.com/NuGet/Home/issues/8074)

* Opzioni Add-SolutionDirectory e-PackageDirectory per NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)

**[Elenco di tutti i problemi risolti in questa versione-5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>Riepilogo: novità di 5.3.1

* Plug-in: un'attività è stata annullata. non lasciare che gli annullamenti influiscano sulla creazione di [#8648](https://github.com/NuGet/Home/issues/8648) istanze

* Non è possibile eseguire in modo sicuro l'attività di ripristino due volte in un processo (quando si usano i provider di credenziali)- [#8688](https://github.com/NuGet/Home/issues/8688)
