---
title: Note sulla versione di NuGet 2,8
description: Note sulla versione per NuGet 2,8, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cb77cf0f049b5b3cfe1039d83ab58e33457674bf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776721"
---
# <a name="nuget-28-release-notes"></a>Note sulla versione di NuGet 2,8

Note sulla versione di [NuGet 2.7.2](../release-notes/nuget-2.7.2.md)  |  [Note sulla versione di NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2,8 è stato rilasciato il 29 gennaio 2014.

## <a name="acknowledgements"></a>Riconoscimenti

1. Stinto [Pritchard](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )
    - [#3466](https://nuget.codeplex.com/workitem/3466) -durante la compressione dei pacchetti, verificando l'ID dei pacchetti di dipendenze.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )
    - [#2379](https://nuget.codeplex.com/workitem/2379) : rimuovere il suffisso di $Metadata quando le credenziali del feed persistening.
3. [Filip de vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )
    - [#3538](http://nuget.codeplex.com/workitem/3538) : supporto che specifica il file di progetto per il comando nuget.exe Update.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - token di sostituzione [#3536](http://nuget.codeplex.com/workitem/3536) non passati con-IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )
    - [#3677](http://nuget.codeplex.com/workitem/3677) -correggere NuGet. push generando OutOfMemoryException quando si esegue il push di un pacchetto di grandi dimensioni.
6. [Ouwens di stato](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -correggere un percorso di destinazione non corretto quando il progetto fa riferimento a un altro progetto CLI/C++.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#3639](https://nuget.codeplex.com/workitem/3639) -Consenti l'installazione dei pacchetti come dipendenze di sviluppo per impostazione predefinita
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - [#3717](https://nuget.codeplex.com/workitem/3717) rimuovere gli aggiornamenti impliciti alla versione più recente della patch
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Diverse correzioni di bug e miglioramenti per NuGet. Server, il nuget.exe comando mirror e altro ancora.
    - Questo lavoro è stato eseguito per diversi mesi, con Gregory collaborando con Microsoft alla tempistica corretta per l'integrazione nel master per 2,8.

## <a name="patch-resolution-for-dependencies"></a>Risoluzione delle patch per le dipendenze

Quando si risolvono le dipendenze dei pacchetti, NuGet ha implementato in passato una strategia di selezione della versione più bassa del pacchetto principale e secondaria che soddisfa le dipendenze del pacchetto. A differenza della versione principale e secondaria, tuttavia, la versione della patch è stata sempre risolta con la versione più recente. Anche se il comportamento era ben intenzionale, ha creato un'assenza di determinismo per l'installazione dei pacchetti con dipendenze. Si consideri l'esempio seguente:

```
PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

PackageB@1.0.1 is published

Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1
```

In questo esempio, anche se Developer1 e Developer2 sono installati PackageA@1.0.0 , ognuno è finito con una versione diversa di PackageB. NuGet 2,8 modifica questo comportamento predefinito in modo che il comportamento di risoluzione delle dipendenze per le versioni delle patch sia coerente con il comportamento per le versioni principali e secondarie. Nell'esempio precedente, quindi, PackageB@1.0.0 verrebbe installato in seguito all'installazione di PackageA@1.0.0 , indipendentemente dalla versione più recente della patch.

## <a name="-dependencyversion-switch"></a>-DependencyVersion-opzione

Sebbene NuGet 2,8 modifichi il comportamento _predefinito_ per la risoluzione delle dipendenze, aggiunge anche un controllo più preciso sul processo di risoluzione delle dipendenze tramite l'opzione-DependencyVersion nella console di gestione pacchetti. Il commutatore consente la risoluzione delle dipendenze con la versione più bassa possibile (comportamento predefinito), la versione più alta possibile o la versione minore o patch più recente.  Questa opzione funziona solo per Install-Package nel comando di PowerShell.

![Opzione DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Attributo DependencyVersion

Oltre all'opzione-DependencyVersion descritta in precedenza, NuGet ha anche la possibilità di impostare un nuovo attributo nel file Nuget.Config che definisce il valore predefinito, se l'opzione-DependencyVersion non è specificata in una chiamata di Install-Package. Questo valore verrà rispettato anche dalla finestra di dialogo Gestione pacchetti NuGet per tutte le operazioni di installazione dei pacchetti. Per impostare questo valore, aggiungere l'attributo seguente al file di Nuget.Config:

```xml
<config>
    <add key="dependencyversion" value="Highest" />
</config>
```

## <a name="preview-nuget-operations-with--whatif"></a>Anteprima delle operazioni NuGet con-WhatIf

Alcuni pacchetti NuGet possono avere grafici delle dipendenze profonde e, di conseguenza, possono essere utili durante un'operazione di installazione, disinstallazione o aggiornamento per vedere prima cosa accadrà. NuGet 2,8 aggiunge l'opzione PowerShell-WhatIf standard ai comandi install-package, Uninstall-Package e Update-Package per consentire la visualizzazione dell'intera chiusura dei pacchetti a cui verrà applicato il comando. Ad esempio, `install-package Microsoft.AspNet.WebApi -whatif` l'esecuzione di in un'applicazione Web ASP.NET vuota produce quanto segue.

```
PM> install-package Microsoft.AspNet.WebApi -whatif
Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
Install Newtonsoft.Json 4.5.11
Install Microsoft.AspNet.WebApi.Client 5.0.0
Install Microsoft.AspNet.WebApi.Core 5.0.0
Install Microsoft.AspNet.WebApi.WebHost 5.0.0
Install Microsoft.AspNet.WebApi 5.0.0
```

## <a name="downgrade-package"></a>Esegui il downgrade del pacchetto

Non è insolito installare una versione provvisoria di un pacchetto per esaminare le nuove funzionalità e quindi decidere di eseguire il rollback all'ultima versione stabile. Prima di NuGet 2,8, si trattava di un processo costituito da più passaggi per la disinstallazione del pacchetto di versioni non definitive e delle relative dipendenze, quindi l'installazione della versione precedente. Con NuGet 2,8, tuttavia, il pacchetto di aggiornamento eseguirà il rollback dell'intera chiusura del pacchetto, ad esempio l'albero delle dipendenze del pacchetto, alla versione precedente.

## <a name="development-dependencies"></a>Dipendenze di sviluppo

Molti tipi diversi di funzionalità possono essere forniti come pacchetti NuGet, inclusi gli strumenti usati per ottimizzare il processo di sviluppo. Questi componenti, sebbene possano essere strumentali nello sviluppo di un nuovo pacchetto, non devono essere considerati una dipendenza del nuovo pacchetto dopo la pubblicazione. NuGet 2,8 consente a un pacchetto di identificarsi nel `.nuspec` file come developmentDependency. Quando è installato, questi metadati verranno aggiunti anche al `packages.config` file del progetto in cui è stato installato il pacchetto. Quando il `packages.config` file viene analizzato in un secondo momento per le dipendenze NuGet durante `nuget.exe pack` , le dipendenze contrassegnate come dipendenze di sviluppo verranno escluse.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Singoli file di packages.config per piattaforme diverse

Quando si sviluppano applicazioni per più piattaforme di destinazione, è comune avere file di progetto diversi per ognuno dei rispettivi ambienti di compilazione. È anche comune usare pacchetti NuGet diversi in file di progetto diversi, poiché i pacchetti hanno livelli di supporto diversi per le diverse piattaforme. NuGet 2,8 fornisce un supporto migliorato per questo scenario creando `packages.config` file diversi per i diversi file di progetto specifici della piattaforma.

![Più file di package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback alla cache locale

Anche se i pacchetti NuGet vengono in genere usati da una raccolta remota, ad esempio [la raccolta NuGet](http://www.nuget.org/) che usa una connessione di rete, esistono molti scenari in cui il client non è connesso. Senza una connessione di rete, il client NuGet non è stato in grado di installare correttamente i pacchetti, anche quando tali pacchetti erano già presenti nel computer del client nella cache NuGet locale. NuGet 2,8 aggiunge il fallback della cache automatica alla console di gestione pacchetti. Ad esempio, quando si disconnette la scheda di rete e si installa jQuery, nella console viene visualizzato quanto segue:

```
PM> Install-Package jquery
The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
Installing 'jQuery 2.0.3'.
Successfully installed 'jQuery 2.0.3'.
Adding 'jQuery 2.0.3' to WebApplication18.
Successfully added 'jQuery 2.0.3' to WebApplication18.
```

La funzionalità di fallback della cache non richiede argomenti di comando specifici. Inoltre, il fallback della cache attualmente funziona solo nella console di gestione pacchetti. il comportamento attualmente non funziona nella finestra di dialogo Gestione pacchetti.

## <a name="webmatrix-nuget-client-updates"></a>Aggiornamenti del client NuGet per WebMatrix

Insieme a NuGet 2,8, è stata aggiornata anche l'estensione NuGet per WebMatrix per includere molte delle funzionalità principali fornite con [nuget 2,5](../release-notes/nuget-2.5.md). Le nuove funzionalità includono quelle, ad esempio "Aggiorna tutto", "versione minima di NuGet" e consentono la sovrascrittura dei file di contenuto.

Per aggiornare l'estensione di gestione pacchetti NuGet in WebMatrix 3:

1. Apri WebMatrix 3
1. Fare clic sull'icona estensioni sulla barra multifunzione
1. Selezionare la scheda aggiornamenti
1. Fare clic per aggiornare Gestione pacchetti NuGet a 2.5.0
1. Chiudere e riavviare WebMatrix 3

Questa è la prima versione del team NuGet dell'estensione Gestione pacchetti NuGet per WebMatrix.  Il codice è stato recentemente fornito da Microsoft nel progetto NuGet open source. In precedenza, l'integrazione di NuGet è stata compilata in WebMatrix e non è stato possibile aggiornarla fuori banda da WebMatrix.  Ora è possibile aggiornarla ulteriormente insieme al resto degli strumenti client di NuGet.

## <a name="bug-fixes"></a>Correzioni di bug

Una delle principali correzioni di bug apportate è stato il miglioramento delle prestazioni nel comando Update-Package-REINSTALL.

Oltre a queste funzionalità e alla precedente correzione delle prestazioni, questa versione di NuGet include anche molte altre correzioni di bug. Nella versione sono stati rilevati 181 problemi totali. Per un elenco completo degli elementi di lavoro corretti in NuGet 2,8, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
