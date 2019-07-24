---
title: Migrazione da Package. config a formati PackageReference
description: Informazioni dettagliate su come eseguire la migrazione di un progetto dal formato di gestione package. config a PackageReference come supportato da NuGet 4.0 + e VS2017 e .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433285"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Eseguire la migrazione da Packages. config a PackageReference

Visual Studio 2017 versione 15,7 e successive supporta la migrazione di un progetto dal formato di gestione [packages. config](./packages-config.md) al formato [PackageReference](../consume-packages/Package-References-in-Project-Files.md) .

## <a name="benefits-of-using-packagereference"></a>Vantaggi dell'uso di PackageReference

* **Gestire tutte le dipendenze del progetto in un'unica posizione**: Analogamente ai riferimenti da progetto a progetto e riferimenti ad assembly, i riferimenti ai `PackageReference` pacchetti NuGet (usando il nodo) vengono gestiti direttamente all'interno di file di progetto anziché usare un file Packages. config separato.
* **Visualizzazione disordinata delle dipendenze di primo livello**: Diversamente da Packages. config, PackageReference elenca solo i pacchetti NuGet installati direttamente nel progetto. Di conseguenza, l'interfaccia utente di gestione pacchetti NuGet e il file di progetto non sono in disordine con le dipendenze di livello inferiore.
* **Miglioramenti delle prestazioni**: Quando si usa PackageReference, i pacchetti vengono conservati nella cartella *Global-Packages* , come descritto in [gestione dei pacchetti globali e delle cartelle della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) anziché in una `packages` cartella all'interno della soluzione. Di conseguenza, PackageReference viene eseguito più velocemente e utilizza meno spazio su disco.
* **Controllo accurato delle dipendenze e del flusso del contenuto**: Usando le funzionalità di MSBuild esistenti, è possibile [fare riferimento a un pacchetto NuGet in modo condizionale](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) e scegliere i riferimenti ai pacchetti per Framework di destinazione, configurazione, piattaforma o altri pivot.
* **PackageReference è in fase di sviluppo attivo**: Vedere [problemi di PackageReference su GitHub](https://aka.ms/nuget-pr-improvements). Packages. config non è più in fase di sviluppo attivo.

### <a name="limitations"></a>Limitazioni

* NuGet PackageReference non è disponibile in Visual Studio 2015 e versioni precedenti. I progetti migrati possono essere aperti solo in Visual Studio 2017 e versioni successive.
* La migrazione non è attualmente disponibile per i progetti C++ e ASP.NET.
* Alcuni pacchetti potrebbero non essere completamente compatibili con PackageReference. Per ulteriori informazioni, vedere [problemi di compatibilità dei pacchetti](#package-compatibility-issues).

### <a name="known-issues"></a>Problemi noti

1. L'opzione `Migrate packages.config to PackageReference...` non è disponibile nel menu di scelta rapida 

#### <a name="issue"></a>Problema 
 
Alla prima apertura di un progetto, NuGet potrebbe non essere inizializzato fino all'esecuzione di un'operazione NuGet. Per questo motivo, l'opzione di migrazione non viene visualizzata nel menu di scelta rapida per `packages.config` o `References`. 

#### <a name="workaround"></a>Soluzione alternativa 

Eseguire una delle azioni NuGet seguenti: 
* Aprire l'interfaccia utente di Gestione pacchetti - fare clic con il pulsante destro del mouse su `References` e scegliere `Manage NuGet Packages...` 
* Aprire la console di Gestione pacchetti - Da `Tools > NuGet Package Manager` selezionare `Package Manager Console` 
* Eseguire un ripristino NuGet - Fare clic con il pulsante destro del mouse sul nodo della soluzione in Esplora soluzioni e scegliere `Restore NuGet Packages` 
* Compilare il progetto, ovvero un altro modo per attivare un ripristino NuGet 

A questo punto, l'opzione di migrazione dovrebbe essere visibile. Si noti che questa opzione non è supportata e non verrà visualizzata per i tipi di progetto ASP.NET e C++. 

## <a name="migration-steps"></a>Passaggi della migrazione

> [!Note]
> Prima dell'inizio della migrazione, Visual Studio crea un backup del progetto per consentire di eseguire il [rollback a Packages. config](#how-to-roll-back-to-packagesconfig) , se necessario.

1. Aprire una soluzione contenente il progetto `packages.config`utilizzando.

1. In **Esplora soluzioni**fare clic con il pulsante destro  del mouse sul `packages.config` nodo riferimenti o sul file e selezionare migrate **packages. config to PackageReference...** .

1. Migrator analizza i riferimenti ai pacchetti NuGet del progetto e tenta di categorizzarli in dipendenze di **primo livello** (pacchetti NuGet installati direttamente) e **dipendenze transitive** (pacchetti installati come dipendenze dei pacchetti di primo livello.

   > [!Note]
   > PackageReference supporta il ripristino transitivo dei pacchetti e risolve le dipendenze in modo dinamico, vale a dire che non è necessario installare in modo esplicito le dipendenze transitive.

1. Opzionale È possibile scegliere di considerare un pacchetto NuGet Classificato come dipendenza transitiva come dipendenza di primo livello selezionando l'opzione di **primo livello** per il pacchetto. Questa opzione viene impostata automaticamente per i pacchetti contenenti asset che non vengono trasferiti in modo transitivo ( `build`quelli `buildCrossTargeting`nelle `contentFiles`cartelle, `analyzers` , o) e quelli contrassegnati come dipendenza di sviluppo`developmentDependency = "true"`().

1. Esaminare eventuali [problemi di compatibilità dei pacchetti](#package-compatibility-issues).

1. Selezionare **OK** per avviare la migrazione.

1. Al termine della migrazione, Visual Studio fornisce un report con un percorso al backup, l'elenco dei pacchetti installati (dipendenze di livello superiore), un elenco di pacchetti a cui si fa riferimento come dipendenze transitive e un elenco di problemi di compatibilità identificati all'inizio di migrazione. Il report viene salvato nella cartella di backup.

1. Verificare che la soluzione venga compilata ed eseguita. Se si verificano problemi, [archiviare un problema in GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Come eseguire il rollback a Packages. config

1. Chiudere il progetto migrato.

1. Copiare il file di progetto `packages.config` e dal backup, in `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`genere, nella cartella del progetto. Eliminare la cartella obj se è presente nella directory radice del progetto.

1. Aprire il progetto.

1. Aprire la console di gestione pacchetti usando il comando di menu **strumenti > gestione pacchetti NuGet > console di gestione pacchetti** .

1. Eseguire il comando seguente nella console:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Creazione di un pacchetto dopo la migrazione

Al termine della migrazione, è consigliabile aggiungere un riferimento al pacchetto NuGet [NuGet. Build. Tasks. Pack](https://www.nuget.org/packages/nuget.build.tasks.pack) e quindi usare [msbuild-t:Pack](../reference/msbuild-targets.md#pack-target) per creare il pacchetto. Sebbene in alcuni scenari sia possibile usare `dotnet.exe pack` `msbuild -t:pack`anziché, non è consigliabile.

## <a name="package-compatibility-issues"></a>Problemi di compatibilità dei pacchetti

Alcuni aspetti supportati in Packages. config non sono supportati in PackageReference. Il Migrator analizza e rileva tali problemi. I pacchetti che presentano uno o più dei seguenti problemi potrebbero non comportarsi come previsto dopo la migrazione.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>gli script "Install. ps1" vengono ignorati quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Con PackageReference, gli script Install. ps1 e Uninstall. ps1 di PowerShell non vengono eseguiti durante l'installazione o la disinstallazione di un pacchetto. |
| **Impatto potenziale** | I pacchetti che dipendono da questi script per configurare un comportamento nel progetto di destinazione potrebbero non funzionare come previsto. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>gli asset "Content" non sono disponibili quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Gli `content` asset nella cartella di un pacchetto non sono supportati con PackageReference e vengono ignorati. PackageReference aggiunge il supporto `contentFiles` per per ottenere supporto transitivo e contenuto condiviso migliori.  |
| **Impatto potenziale** | Gli asset `content` in non vengono copiati nel progetto e il codice del progetto che dipende dalla presenza di tali asset richiede il refactoring.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Le trasformazioni XDT non vengono applicate quando il pacchetto viene installato dopo l'aggiornamento

| | |
| --- | --- |
| **Descrizione** | Le trasformazioni xdt non sono supportate con PackageReference `.xdt` e i file vengono ignorati durante l'installazione o la disinstallazione di un pacchetto.   |
| **Impatto potenziale** | Le trasformazioni xdt non vengono applicate ai file XML del progetto, in genere `web.config.install.xdt` e `web.config.uninstall.xdt`, il` web.config` che significa che il file del progetto non viene aggiornato quando il pacchetto viene installato o disinstallato. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Gli assembly nella radice lib vengono ignorati quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Con PackageReference, gli assembly presenti nella radice della `lib` cartella senza una sottocartella specifica del Framework di destinazione vengono ignorati. NuGet cerca una sottocartella corrispondente al moniker del Framework di destinazione (TFM) corrispondente al Framework di destinazione del progetto e installa gli assembly corrispondenti nel progetto. |
| **Impatto potenziale** | I pacchetti che non dispongono di una sottocartella corrispondente al moniker del Framework di destinazione (TFM) corrispondente al Framework di destinazione del progetto potrebbero non comportarsi come previsto dopo l'installazione della transizione o non riuscita durante la migrazione |

## <a name="found-an-issue-report-it"></a>Si è riscontrato un problema? Segnala!

Se si verifica un problema con l'esperienza di migrazione, inviare [un problema nel repository GitHub di NuGet](https://github.com/NuGet/Home/issues/).
