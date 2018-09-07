---
title: Panoramica dell'ecosistema NuGet
description: Risorse complete dell'ecosistema NuGet che includono origini NuGet, progetti NuGet non Microsoft, utilità e materiali per la formazione.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548144"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Panoramica dell'ecosistema NuGet

Dalla sua introduzione nel 2010, NuGet ha costituito una notevole opportunità per migliorare e automatizzare diversi aspetti dei processi di sviluppo.

Poiché NuGet è open source in base a una [licenza Apache v2](http://choosealicense.com/licenses/apache/) permissiva, altri progetti possono sfruttare i vantaggi offerti da NuGet e le aziende possono introdurre il supporto per NuGet nei loro prodotti. Indipendentemente dal fatto che siano destinati a progetti open source o allo sviluppo di applicazioni aziendali, NuGet e altre applicazioni basate su NuGet forniscono un ampio ecosistema di strumenti mirati al miglioramento del processo di sviluppo software.

Tutti questi progetti risultano innovativi grazie al contributo degli sviluppatori. Proprio come si contribuisce a NuGet, è possibile offrire il proprio contributo anche a questi progetti segnalando difetti e idee per nuove funzionalità, fornendo commenti e suggerimenti, scrivendo la documentazione e offrendo contributi al codice dove possibile.

## <a name="net-foundation-projects"></a>Progetti .NET Foundation

NuGet fornisce un sistema di gestione pacchetti open source gratuito per la piattaforma di sviluppo Microsoft, costituito da alcuni strumenti client e dal set di servizi che formano la [raccolta NuGet ufficiale](http://www.nuget.org). In combinazione, costituiscono il progetto NuGet gestito da [.NET Foundation](http://www.dotnetfoundation.org/).

L'organizzazione NuGet include vari repository su GitHub. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) offre una panoramica di tutti i repository e specifica dove trovare i vari componenti di NuGet.

## <a name="microsoft-projects"></a>Progetti Microsoft

Microsoft ha contribuito ampiamente allo sviluppo di NuGet. Anche tutti i contributi dei collaboratori Microsoft sono open source e sono stati donati (copyright inclusi) a .NET Foundation.

## <a name="non-microsoft-projects"></a>Progetti non Microsoft

Molte altre persone e aziende hanno apportato contributi significativi all'ecosistema NuGet. Ogni progetto elencato di seguito potrebbe disporre di una licenza diversa rispetto ai componenti base di NuGet, pertanto verificare che le condizioni di licenza siano accettabili prima di procedere all'uso:

- [AppVeyor (soluzione CI)](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (o NuGet come servizio)](http://www.myget.org/)
- [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin e MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Altre utilità basate su NuGet

Di seguito sono elencati gli strumenti e le utilità basati su NuGet:

- [Estensioni di Glimpse](http://getglimpse.com/Packages) (i plug-in sono pacchetti)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (i moduli CMS vengono recuperati da un feed NuGet v1 ospitato nella raccolta Orchard)
- [Implementazione Java di NuGet Server](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (bot su Twitter sulle pubblicazioni di nuovi pacchetti)
- [DefinitelyTyped](http://definitelytyped.org/) (definizioni [automatiche](https://github.com/DefinitelyTyped/NugetAutomation/) di tipi TypeScript [pubblicate su NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Riferimenti e materiali per la formazione

L'uso di un nuovo strumento o di una nuova tecnologia in genere implica una curva di apprendimento, ma fortunatamente quella di NuGet non è affatto ripida. In realtà, chiunque può [iniziare a utilizzare i pacchetti](../quickstart/use-a-package.md) rapidamente.

Detto questo, per poter creare pacchetti validi e adottare NuGet nell'ambito di processi di compilazione e distribuzione automatizzati è consigliabile dedicare un po' di tempo alle risorse seguenti:

- [Blog di NuGet](http://blog.nuget.org/)
- [Team di NuGet su Twitter, @nuget](http://twitter.com/nuget)
- Pubblicazioni:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Documentazione per i singoli pacchetti

[NuDoq](http://nudoq.org) fornisce un accesso diretto e aggiornamenti e documentazione per i pacchetti NuGet.

NuDoq esegue regolarmente operazioni di polling nel server della raccolta nuget.org per trovare gli ultimi aggiornamenti pacchetto, decomprime ed elabora i file di documentazione della libreria e aggiorna il sito di conseguenza.

## <a name="adding-your-project"></a>Aggiunta di un progetto

Se si dispone di un progetto per l'ecosistema NuGet che potrebbe rappresentare un valido contributo a questa pagina, inviare una richiesta pull con una modifica a questa pagina.
