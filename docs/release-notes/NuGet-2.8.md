---
title: Note sulla versione 2.8 di NuGet
description: Note sulla versione per NuGet 2.8, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547459"
---
# <a name="nuget-28-release-notes"></a>Note sulla versione 2.8 di NuGet

[Note sulla versione di NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [note sulla versione di NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 è stato rilasciato entro il 29 gennaio 2014.

## <a name="acknowledgements"></a>Riconoscimenti

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) : la creazione di pacchetti, verifica dell'Id dei pacchetti con dipendenze.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -rimuovere il suffisso $metadata quando persistening feed le credenziali.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - supporto tecnico specificando i file di progetto per il comando update nuget.exe.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -token di sostituzione non superato con - IncludeReferencedProjects.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -correggere nuget.push generando un'eccezione OutOfMemoryException durante il push dei pacchetti di grandi dimensioni.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -percorso di destinazione non corretta di correzione quando progetto fa riferimento a un altro progetto CLI/C++.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -consentire ai pacchetti installati come dipendenze per lo sviluppo per impostazione predefinita
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -rimuovere aggiornamenti impliciti per la versione patch più recente
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Diverse correzioni di bug e miglioramenti di NuGet. Server, il comando mirror nuget.exe e altri.
    - Questa operazione è stata eseguita per diversi mesi, con Gregory lavorando con noi il momento giusto per integrare dati master per 2.8.

## <a name="patch-resolution-for-dependencies"></a>Risoluzione delle patch per le dipendenze

Durante la risoluzione delle dipendenze dei pacchetti, NuGet in passato ha implementato una strategia di selezionando la versione principale e secondaria del pacchetto più bassa che soddisfa le dipendenze del pacchetto. A differenza delle versioni principale e secondaria, tuttavia, la versione di patch è stato risolto sempre per la versione più recente. Il comportamento è stato malintenzionato, creata una mancanza di determinismo per l'installazione di pacchetti con dipendenze. Si consideri l'esempio seguente:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

In questo esempio, anche se Developer1 Developer2 installati e PackageA@1.0.0, ogni backup terminata con una versione diversa di PackageB. NuGet 2.8 modifica questo comportamento predefinito in modo che il comportamento di risoluzione delle dipendenze per le versioni di patch sia consistenti con il comportamento per le versioni principali e secondarie. Nell'esempio precedente, quindi PackageB@1.0.0 verrà installata la versione in seguito all'installazione PackageA@1.0.0, indipendentemente dalla versione patch più recente.

## <a name="-dependencyversion-switch"></a>Opzione DependencyVersion-

Anche se NuGet 2.8 viene modificato il _predefinito_ comportamento per la risoluzione delle dipendenze, aggiunge anche maggiore controllo sul processo di risoluzione delle dipendenze mediante l'opzione DependencyVersion - nella console di gestione pacchetti. L'opzione Abilita la risoluzione delle dipendenze per la versione più bassa possibile (comportamento predefinito), la versione più recente, o il minore più alto o versione patch.  Questa opzione funziona solo per install-package nel comando di powershell.

![Opzione DependencyVersion](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Attributo DependencyVersion

Oltre all'opzione DependencyVersion - come indicato in precedenza, NuGet ha anche consentito per la possibilità di impostare un nuovo attributo nel file NuGet. config che definisce ciò che è il valore predefinito, se l'opzione DependencyVersion - non è specificato in una chiamata di Install-package. Questo valore verrà rispettato anche dalla finestra di dialogo Gestione pacchetti NuGet per qualsiasi operazione di installazione del pacchetto. Per impostare questo valore, aggiungere l'attributo seguente nel file NuGet. config:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Operazioni con - whatif NuGet di anteprima

Alcuni pacchetti NuGet possono avere grafici di dipendenza completa e di conseguenza, possono risultare utili durante un'installazione, disinstallare o aggiornare innanzitutto vedere cosa succede dell'operazione. NuGet 2.8 aggiunge l'opzione - whatif PowerShell standard per i comandi di pacchetto di aggiornamento per abilitare l'intera closure di pacchetti a cui il comando verrà applicato la visualizzazione, disinstallare-package e install-package. Ad esempio, l'esecuzione `install-package Microsoft.AspNet.WebApi -whatif` in un Web ASP.NET vuota applicazione produce quanto segue.

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

Non è insolito per installare una versione preliminare di un pacchetto e per studiare le nuove funzionalità e quindi decidere se eseguire il rollback all'ultima versione stabile. Prima di NuGet 2.8, questo era un processo in più passaggi di disinstallazione il pacchetto versione non definitivo e le relative dipendenze e quindi installare la versione precedente. Con NuGet 2.8, tuttavia, il pacchetto di aggiornamento verrà ora eseguito il rollback alla chiusura dell'intero pacchetto (ad esempio, l'albero delle dipendenze del pacchetto) alla versione precedente.

## <a name="development-dependencies"></a>Dipendenze dello sviluppo

Molti tipi diversi di funzionalità possono essere distribuiti come pacchetti NuGet - tra cui strumenti utilizzati per ottimizzare il processo di sviluppo. Questi componenti, anche se possono essere strumentale nello sviluppo di un nuovo pacchetto, non devono essere considerati una dipendenza del nuovo pacchetto quando viene pubblicato in un secondo momento. NuGet 2.8 consente a un pacchetto per identificarsi nel `.nuspec` file come un developmentDependency. Quando è installato, questi metadati verranno aggiunti per il `packages.config` file del progetto in cui è stato installato il pacchetto. Quando che `packages.config` file viene analizzato in un secondo momento le dipendenze di NuGet durante `nuget.exe pack`, vengono escluse tali dipendenze contrassegnati come dipendenze di sviluppo.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>File Packages. config singoli per piattaforme diverse

Quando si sviluppano applicazioni per più piattaforme di destinazione, è comune disporre di file di progetto diversi per ognuno degli ambienti di compilazione corrispondente. È anche comune per utilizzare diversi pacchetti NuGet nei file di progetto diverso, come i pacchetti hanno vari livelli di supporto per piattaforme diverse. NuGet 2.8 offre un supporto migliorato per questo scenario mediante la creazione di diversi `packages.config` file per i file di progetto specifico della piattaforma differente.

![Più file di package](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback alla Cache locale

Anche se i pacchetti NuGet vengono in genere utilizzati da una raccolta remota, ad esempio [NuGet gallery](http://www.nuget.org/) Usa una connessione di rete, sono disponibili molti scenari in cui il client non è connesso. Senza una connessione di rete, il client di NuGet non è in grado di installare correttamente i pacchetti, anche quando tali pacchetti erano già presenti nel computer del client nella cache NuGet locale. NuGet 2.8 aggiunge fallback automatico nella cache alla console di gestione pacchetti. Ad esempio, quando disconnessione della scheda di rete e si installa jQuery, la console mostra quanto segue:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

La funzionalità di fallback della cache non richiedono alcun argomento di comando specifico. Inoltre, fallback nella cache attualmente funziona solo nella console di gestione pacchetti: il comportamento non funziona nella finestra di dialogo Gestione pacchetti.

## <a name="webmatrix-nuget-client-updates"></a>Gli aggiornamenti del Client NuGet WebMatrix

Con NuGet 2.8, l'estensione NuGet per WebMatrix è stato inoltre aggiornato per includere molte delle funzionalità principali fornite con [NuGet 2.5](../release-notes/nuget-2.5.md). Le nuove funzionalità includono quelle, ad esempio 'Update ' al, 'Versione di NuGet minima' e consentendo la sovrascrittura dei file di contenuto.

Per aggiornare l'estensione Gestione pacchetti NuGet in WebMatrix 3:

1. Aprire WebMatrix 3
1. Fare clic sull'icona delle estensioni nella barra multifunzione
1. Selezionare la scheda aggiornamenti
1. Fare clic per aggiornare i pacchetti NuGet per 2.5.0
1. Chiudere e riavviare WebMatrix 3

Questo è primo rilascio del team di NuGet dell'estensione Gestione pacchetti NuGet per WebMatrix.  Il codice è stato recentemente fornito da Microsoft nel progetto NuGet open source. In precedenza, l'integrazione di NuGet è stato compilato in WebMatrix, e non è stato possibile aggiornare fuori da WebMatrix.  È ora disponibile la possibilità di aggiornare ulteriormente insieme al resto degli strumenti client di NuGet.

## <a name="bug-fixes"></a>Correzioni di bug

Uno delle principali correzioni di bug apportate era il miglioramento delle prestazioni nel pacchetto di aggiornamento-reinstallare comando.

Oltre a queste funzionalità e la correzione delle prestazioni indicati in precedenza, questa versione di NuGet include anche molte altre correzioni di bug. Si sono verificati 181 totali problemi risolti nella versione. Per un elenco completo delle operazioni elementi risolti in NuGet 2.8, vista la [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
