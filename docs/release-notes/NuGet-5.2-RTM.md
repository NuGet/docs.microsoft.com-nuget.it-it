---
title: Note sulla versione di NuGet 5,2 RTM
description: Note sulla versione per NuGet 5,2, incluse nuove funzionalità, correzioni di bug e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776204"
---
# <a name="nuget-52-release-notes"></a>Note sulla versione di NuGet 5,2

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core 

<sup>2</sup> Disponibile come installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-52"></a>Riepilogo: novità di 5,2

* Correzione di un bug critico che ha causato errori di operazioni NuGet occasionali a causa di problemi di percorso in Linux & Mac- [#7341](https://github.com/NuGet/Home/issues/7341)

* Velocità di risposta dell'interfaccia utente migliorata quando si esplorano i pacchetti usando l'interfaccia utente di gestione pacchetti NuGet in Visual Studio particolarmente evidente per le origini lente- [#8039](https://github.com/NuGet/Home/issues/8039)

* Tonnellate di correzioni di affidabilità per il file di blocco ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) e il plug-in di autenticazione ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271)[, #8269,](https://github.com/NuGet/Home/issues/8269)[#8210](https://github.com/NuGet/Home/issues/8210)[, #8198](https://github.com/NuGet/Home/issues/8198)[#7845)](https://github.com/NuGet/Home/issues/7845)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Prestazioni: console di gestione pacchetti: aggiornamento ritardato dell'interfaccia utente "progetto predefinito" valore selezionato ComboBox- [#8235](https://github.com/NuGet/Home/issues/8235)

* Prestazioni: miglioramenti delle prestazioni nell'interfaccia utente di PM- [#8039](https://github.com/NuGet/Home/issues/8039)

* Prestazioni: ritardo dell'interfaccia utente durante la lettura del progetto predefinito in PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Prestazioni: [vsfeedback] la scheda aggiornamento NuGet si blocca per un'origine pacchetto locale- [#6470](https://github.com/NuGet/Home/issues/6470)

* Plug-in: NuGet attende il timeout di handshake completo se il plug-in non viene avviato o termina in anticipo [#8300](https://github.com/NuGet/Home/issues/8300)

* Plug-in: migliorare la diagnostica dell'errore di avvio del plug- [#8271](https://github.com/NuGet/Home/issues/8271)

* Plug-in: problema con nuget.exe individuazione di plug-in predefiniti- [#8269](https://github.com/NuGet/Home/issues/8269)

* Plug-in: il file di cache non è mai letto [#8210](https://github.com/NuGet/Home/issues/8210)

* Plug-in: "un'attività è stata annullata". errori con il plug-in di autenticazione durante il ripristino- [#8198](https://github.com/NuGet/Home/issues/8198)

* Cache di plug-in non individuabile in modo intermittente nelle piattaforme Linux: [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile: con ATF, ha false NU1004 a causa di un controllo di uguaglianza del Framework di destinazione non valido. [#8187](https://github.com/NuGet/Home/issues/8187)

* LockFile: il flag di ripristino "--Locked-Mode" non è rispettato se il file di blocco è vuoto o non valido [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile: non i progetti minuscoli con nomi di assembly personalizzati nei pacchetti bloccano i file [#8114](https://github.com/NuGet/Home/issues/8114)

* LockFile: creare un riferimento al progetto in minuscolo nel file di blocco [#7840](https://github.com/NuGet/Home/issues/7840)

* Ripristino: l'installazione di un pacchetto con firma manomessa comporta più tentativi di installazione non riusciti (con output ripetuto)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: le opzioni utente della soluzione non vengono deserializzate dopo l'aggiornamento di NuGet- [#8166](https://github.com/NuGet/Home/issues/8166)

* DotNet-list-package in un progetto UnitTest restituisce un errore [#8154](https://github.com/NuGet/Home/issues/8154)

* Creare un gruppo di pacchetti NuGet per Visual Studio Installer-correzione di alcuni problemi di configurazione VSIX- [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild non deve impostare nobuild. - [#7801](https://github.com/NuGet/Home/issues/7801)

* La nuova opzione "-SymbolPackageFormat snupkg" genera un errore quando il file con estensione NuSpec contiene un elemento di riferimento esplicito all'assembly [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet. targets (498, 5): errore: Impossibile trovare una parte del percorso '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)

**DCR:**

* Aggiungere una proprietà di MSBuild che indica che PackageDownload è supportato- [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference disattivare il flusso delle dipendenze tramite FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Meccanismo per fornire runtime.jsall'esterno di un pacchetto- [#7351](https://github.com/NuGet/Home/issues/7351)

**[Elenco di tutti i problemi risolti in questa versione-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


