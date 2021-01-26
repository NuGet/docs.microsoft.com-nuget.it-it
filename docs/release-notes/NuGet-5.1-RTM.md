---
title: Note sulla versione di NuGet 5,1 RTM
description: Note sulla versione per NuGet 5,1, incluse nuove funzionalità, correzioni di bug e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: d6f6bffc6b5fda9ee1b9d9830f6d7d3c0f5be654
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780136"
---
# <a name="nuget-51-release-notes"></a>Note sulla versione di NuGet 5,1

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.1.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,1](https://visualstudio.microsoft.com/downloads/) | [2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core 

<sup>2</sup> Disponibile come installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-51"></a>Riepilogo: novità di 5,1

* Supporto per ignorare un push del pacchetto se esiste già per consentire una migliore integrazione con i flussi di lavoro CI/CD- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)

* Visual Studio offre ora un comodo collegamento alla pagina della raccolta di nuget.org del pacchetto: [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)

* Supporto per le nuove risorse di .NET Core 3,0 come [Targeting Pack](https://github.com/dotnet/cli/issues/10006) e [Runtime Pack](https://github.com/dotnet/cli/issues/10007)
  * Supporto di pacchetti NuGet e ripristino per FrameworkReferences per abilitare i riferimenti ai pacchetti di runtime e di destinazione- [#7342](https://github.com/NuGet/Home/issues/7342)
  * Supporto dello scenario "solo download" del pacchetto con PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)
  * Escludi i pacchetti di runtime e targeting dai risultati della ricerca & Restore Graph con PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Plug-in: Dettagli eccezione persi durante la creazione del plug- [#8057](https://github.com/NuGet/Home/issues/8057)

* L'intervallo di PackageReference con limite inferiore esclusivo non funziona se il limite inferiore è presente in una delle origini. - [#8054](https://github.com/NuGet/Home/issues/8054)

* Migliorare [#8021](https://github.com/NuGet/Home/issues/8021) messaggi di IsPackableFalseError

* Packages lock file-Rigenera file di blocco quando viene modificato il grafico del progetto: [#8019](https://github.com/NuGet/Home/issues/8019)

* Bug ProjectSystem: i pacchetti NuGet vengono rimossi automaticamente- [#8017](https://github.com/NuGet/Home/issues/8017)

* Aggiungere una destinazione per la restituzione di FrameworkReference simile a CollectPackageDownloads e CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)

* Cache HTTP: la risorsa RepositoryResources non viene memorizzata nella cache in modalità [#7997](https://github.com/NuGet/Home/issues/7997)

* Registrazione: l'eccezione stack non viene segnalata con un livello di dettaglio dettagliato- [#7955](https://github.com/NuGet/Home/issues/7955)

* Modificare tutti gli URL di documentazione NuGet per usare HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)

* Miglioramento del messaggio di avviso NU3024- [#7933](https://github.com/NuGet/Home/issues/7933)

* Impossibile aggiornare il file di blocco quando packagereference è stato rimosso- [#7930](https://github.com/NuGet/Home/issues/7930)

* Migliorare la gestione dei casi di errore durante la convalida dell'elemento licenseUrl e License in NuSpec- [#7915](https://github.com/NuGet/Home/issues/7915)

* Interfaccia utente PM: fare clic con il pulsante destro del mouse sull'intestazione della scheda e fare clic su "Apri percorso file" genera un errore [#7913](https://github.com/NuGet/Home/issues/7913)

* Plug-in: registra quando viene chiuso il processo del plug- [#7907](https://github.com/NuGet/Home/issues/7907)

* Plug-in: velocità di collisione elevata nella registrazione dei valori DateTime- [#7899](https://github.com/NuGet/Home/issues/7899)

* Il file manifest. ReadFrom ha esito negativo in qualsiasi NuSpec con LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)

* RestoreLockedMode: NU1004 imprevisto quando ProjectReference fa riferimento a un progetto con AssemblyName personalizzato- [#7889](https://github.com/NuGet/Home/issues/7889)

* Messaggio di errore migliore quando l'avvio del plug-in ha esito negativo con un'eccezione- [#7857](https://github.com/NuGet/Home/issues/7857)

* Quando si esegue un ripristino NoOp, evitare * .dgspec.jsdurante la scrittura nella directory obj- [#7854](https://github.com/NuGet/Home/issues/7854)

* GeneratePathProperty = true non riesce a generare la proprietà in caso di mancata corrispondenza [#7843](https://github.com/NuGet/Home/issues/7843)

* Impostazioni: il carattere non valido nel percorso di origine del pacchetto può arrestarsi in modo anomalo e [#7820](https://github.com/NuGet/Home/issues/7820)

* Se il file di blocco viene eliminato, Restore non genera il file di blocco in NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)

* L'URL di licenza e la licenza causano un errore di lettura con i metadati [#7547](https://github.com/NuGet/Home/issues/7547)

* Eccezioni non gestite in V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)

* nuget.exe restituisce zero del codice di uscita per argomenti non validi- [#7178](https://github.com/NuGet/Home/issues/7178)

* Aggiornare i documenti degli errori e degli avvisi per riflettere gli scenari correlati alla firma: [#6498](https://github.com/NuGet/Home/issues/6498)

* Il file degli asset deve usare percorsi relativi per consentire lo stato di trasferimento dei progetti più facilmente [#4582](https://github.com/NuGet/Home/issues/4582)

**DCR**

* Plug-in: abilitazione della registrazione diagnostica- [#7859](https://github.com/NuGet/Home/issues/7859)

* Eseguire il mapping di Tizen 6 a NetStandard 2,1- [#7773](https://github.com/NuGet/Home/issues/7773)

**[Elenco di tutti i problemi risolti in questa versione-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**
