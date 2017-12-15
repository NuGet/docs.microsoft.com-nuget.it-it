---
title: Note sulla versione di NuGet 2.8 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 77ba98d8-3d66-4126-b2b6-813ddd8ef192
description: "Note sulla versione per NuGet 2.8 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "NuGet 2.8 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0bb35e9d6ef6f3dde7919cd502b32ba5a550c689
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-28-release-notes"></a>Note sulla versione 2.8 di NuGet

[Note sulla versione di NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [note sulla versione di NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 è stato rilasciato il 29 gennaio 2014.

## <a name="acknowledgements"></a>Riconoscimenti

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) : quando i pacchetti, verifica dell'Id di pacchetti di dipendenza di compressione.
1. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -rimuovere il suffisso $metadata quando persistening feed credenziali.
1. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - supporto specificando i file di progetto per il comando di aggiornamento di nuget.exe.
1. [Alessandro Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -token di sostituzione non è stato superato con - IncludeReferencedProjects.
1. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -correggere nuget.push generando OutOfMemoryException quando l'inserimento di grandi dimensioni.
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -percorso di destinazione non corretto di correzione quando progetto fa riferimento a un altro progetto CLI/C++.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -Consenti pacchetti da installare come dipendenze di sviluppo per impostazione predefinita
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -rimuovere gli aggiornamenti impliciti per la versione più recente di patch
1. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Alcune correzioni di bug e miglioramenti per NuGet.Server, il comando di nuget.exe mirror e di altri utenti.
    - Questa attività sono state eseguite alcuni mesi, con Gregory lavorando con noi la temporizzazione di destra per integrare dati master per 2.8.

## <a name="patch-resolution-for-dependencies"></a>Patch di risoluzione delle dipendenze

Durante la risoluzione delle dipendenze del pacchetto, NuGet è sempre implementata una strategia di selezionando la versione del pacchetto principale e secondario più bassa che soddisfa le dipendenze del pacchetto. A differenza delle versioni principale e secondaria, tuttavia, la versione di patch è stato risolto sempre la versione più recente. Il comportamento è stato malintenzionato, creata una mancanza di determinismo per l'installazione di pacchetti con dipendenze. Si consideri l'esempio seguente:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

In questo esempio, anche se Developer1 e Developer2 installati PackageA@1.0.0, ogni backup terminata con una versione diversa di PackageB. NuGet 2.8 modifica questo comportamento predefinito in modo che il comportamento di risoluzione delle dipendenze per le versioni di patch sia consistente con il comportamento per le versioni principale e secondarie. Nell'esempio precedente, quindi, PackageB@1.0.0 verrà installato in seguito all'installazione PackageA@1.0.0, indipendentemente dalla versione di patch più recente.

## <a name="-dependencyversion-switch"></a>DependencyVersion - opzione

Anche se cambia NuGet 2.8 il _predefinito_ comportamento per la risoluzione delle dipendenze, aggiunge anche un controllo più preciso il processo di risoluzione dipendenza tramite l'opzione - DependencyVersion nella console di gestione di pacchetto. L'opzione consente di risolvere le dipendenze per la versione minima di possibili (comportamento predefinito), la versione più recente, o il minore più alto o la versione di patch.  Questa opzione funziona solo per il pacchetto di installazione del comando di powershell.

![Opzione DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Attributo DependencyVersion

Oltre all'opzione - DependencyVersion sopra descritti, NuGet è inoltre consentito per la possibilità di impostare un nuovo attributo nel file config che definisce che cos'è il valore predefinito, se il parametro - DependencyVersion non viene specificato in una chiamata di pacchetto di installazione. Questo valore verrà rispettato anche dalla finestra di dialogo Gestione pacchetti NuGet per tutte le operazioni di pacchetto di installazione. Per impostare questo valore, aggiungere l'attributo di sotto del file NuGet. config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Operazioni di NuGet anteprima con - whatif

Alcuni pacchetti NuGet possono avere grafici delle dipendenze complete e di conseguenza, può essere utile durante un'installazione, disinstallare o operazione visualizzare prima di tutto ciò che accadrà di aggiornamento. NuGet 2.8 aggiunge l'opzione - whatif di PowerShell di standard per il pacchetto di installazione, disinstallare-package e comandi di pacchetto di aggiornamento per abilitare la chiusura di pacchetti a cui applicare il comando intera visualizzazione. Ad esempio, in esecuzione `install-package Microsoft.AspNet.WebApi -whatif` in un Web ASP.NET vuoto applicazione produce il seguente.

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

## <a name="downgrade-package"></a>Pacchetto di downgrade

Non è insolito per installare una versione non definitiva di un pacchetto per analizzare nuove funzionalità e si decide di ripristinare l'ultima versione stabile. Prima di NuGet 2.8, questo è un processo in più passaggi di disinstallare il pacchetto non definitiva e le relative dipendenze e quindi installare la versione precedente. Con NuGet 2.8, tuttavia, il pacchetto di aggiornamento verrà ora eseguito il rollback della chiusura dell'intero pacchetto (ad esempio struttura delle dipendenze del pacchetto) alla versione precedente.

## <a name="development-dependencies"></a>Dipendenze di sviluppo

Molti tipi diversi di funzionalità possono essere recapitati come pacchetti NuGet - tra cui gli strumenti utilizzati per ottimizzare il processo di sviluppo. Questi componenti, anche se possono essere strumentale lo sviluppo di un nuovo pacchetto, non devono essere considerati una dipendenza del nuovo pacchetto quando più recente pubblicata. NuGet 2.8 consente a un pacchetto identificare se stessa nella `.nuspec` file come un developmentDependency. Durante l'installazione, verranno inoltre aggiunto i metadati per il `packages.config` file del progetto in cui è stato installato il pacchetto. Quando che `packages.config` file viene analizzato in un secondo momento le dipendenze di NuGet durante `nuget.exe pack`, verrà escluso tali dipendenze contrassegnati come dipendenze di sviluppo.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>File di singoli file Packages. config per le diverse piattaforme

Quando si sviluppano applicazioni per più piattaforme di destinazione, è comune disporre di file di progetto diversi per ognuno degli ambienti di compilazione corrispondente. È inoltre comune per utilizzare i pacchetti NuGet diversi nei file di progetto diverso, come pacchetti con vari livelli di supporto per le diverse piattaforme. NuGet 2.8 fornisce un supporto migliorato per questo scenario tramite la creazione di diversi `packages.config` file per file di progetto specifico della piattaforma diversi.

![Più file package.config](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback alla Cache locale

Anche se i pacchetti NuGet vengono in genere utilizzati da una raccolta remota, ad esempio [raccolta NuGet](http://www.nuget.org/) utilizzando una connessione di rete, esistono molti scenari in cui il client non è connesso. Senza una connessione di rete, il client NuGet non è in grado di installare correttamente i pacchetti, anche quando i pacchetti sono stati già nel computer client nella cache locale NuGet. NuGet 2.8 aggiunge automatica della cache fallback nella console di gestione del pacchetto. Ad esempio, quando la scheda di rete di disconnessione e l'installazione di jQuery, la console mostra quanto segue:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

La funzionalità di fallback della cache non richiedono alcun argomento di comando specifico. Inoltre, cache fallback attualmente funziona solo nella console di gestione di pacchetti: il comportamento non funziona nella finestra di dialogo Gestione pacchetti.

## <a name="webmatrix-nuget-client-updates"></a>Gli aggiornamenti del Client NuGet WebMatrix

Insieme a NuGet 2.8, l'estensione NuGet di WebMatrix è stato inoltre aggiornato per includere molte delle principali funzionalità offerte da [NuGet 2.5](../release-notes/nuget-2.5.md). Nuove funzionalità includono quelle, ad esempio 'Update ' al, ' minimo NuGet alla versione' e consentendo la sovrascrittura dei file di contenuto.

Per aggiornare l'estensione Gestione pacchetti NuGet in WebMatrix 3:

1. Aprire WebMatrix 3
1. Fare clic sull'icona di estensioni della barra multifunzione
1. Selezionare la scheda di aggiornamenti
1. Fare clic per aggiornare Gestione pacchetti NuGet per 2.5.0
1. Chiudere e riavviare WebMatrix 3

Questo è primo rilascio del team NuGet dell'estensione Gestione pacchetti NuGet per WebMatrix.  Il codice è stato recentemente fornito da Microsoft in NuGet progetto open source. In precedenza, l'integrazione di NuGet è stato compilato in WebMatrix, e non è possibile aggiornare fuori banda da WebMatrix.  È ora disponibile la funzionalità per aggiornare ulteriormente insieme il resto degli strumenti client di NuGet.

## <a name="bug-fixes"></a>Correzioni di bug

Una delle principali correzioni di bug apportate stato miglioramento delle prestazioni nel pacchetto di aggiornamento-comando.

Oltre a queste funzionalità e risolvere il problema di prestazioni menzionati in precedenza, questa versione di NuGet include anche molte altre correzioni di bug. Si sono verificati problemi di totali 181 risolti nella versione. Per un elenco completo delle operazioni elementi fissa NuGet 2.8,. visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
