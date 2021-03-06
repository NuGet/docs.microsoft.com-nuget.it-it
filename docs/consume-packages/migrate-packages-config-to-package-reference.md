---
title: Migrazione da packages.config a formati PackageReference
description: Informazioni dettagliate su come eseguire la migrazione di un progetto dal formato di gestione packages.config a PackageReference come supportato da NuGet 4.0 + e VS2017 e .NET Core 2,0
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: fabfd76a46a38ff26acbc6439406d99eb3f85bf4
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859161"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Eseguire la migrazione da packages.config a PackageReference

Visual Studio 2017 versione 15.7 e successive supporta la migrazione di un progetto dal formato di gestione [packages.config](../reference/packages-config.md) al formato [PackageReference](../consume-packages/Package-References-in-Project-Files.md).

## <a name="benefits-of-using-packagereference"></a>Vantaggi dell'uso di PackageReference

* **Gestire tutte le dipendenze del progetto in un'unica posizione**: come i riferimenti da progetto a progetto e i riferimenti ad assembly, i riferimenti ai pacchetti NuGet (usando il `PackageReference` nodo) vengono gestiti direttamente all'interno di file di progetto anziché usare un file di packages.config separato.
* **Visualizzazione disordinata delle dipendenze di primo livello**: a differenza packages.config, PackageReference elenca solo i pacchetti NuGet installati direttamente nel progetto. Di conseguenza, l'interfaccia utente di Gestione pacchetti NuGet e il file di progetto non sono ingombri a causa delle dipendenze di livello inferiore.
* **Miglioramenti delle prestazioni**: quando si usa PackageReference, i pacchetti vengono conservati nella cartella *Global-Packages* , come descritto in [gestione dei pacchetti globali e delle cartelle della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) anziché in una `packages` cartella all'interno della soluzione. Di conseguenza, PackageReference offre prestazioni migliori e utilizza meno spazio su disco.
* **Controllo accurato delle dipendenze e del flusso del contenuto**: usando le funzionalità esistenti di MSBuild, è possibile [fare riferimento a un pacchetto NuGet in modo condizionale](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) e scegliere i riferimenti ai pacchetti per Framework di destinazione, configurazione, piattaforma o altri pivot.
* **PackageReference è in fase di sviluppo attivo**: vedere [problemi PackageReference su GitHub](https://aka.ms/nuget-pr-improvements). Il file packages.config non è più in fase di sviluppo attivo.

### <a name="limitations"></a>Limitazioni

* NuGet PackageReference non è disponibile in Visual Studio 2015 e versioni precedenti. I progetti migrati possono essere aperti solo in Visual Studio 2017 e versioni successive.
* La migrazione non è attualmente disponibile per i progetti C++ e ASP.NET.
* Alcuni pacchetti potrebbero non essere del tutto compatibili con PackageReference. Per altre informazioni, vedere i [problemi di compatibilità dei pacchetti](#package-compatibility-issues).

Esistono inoltre alcune differenze nel modo in cui il lavoro di PackageReferences viene confrontato con packages.config. Ad esempio, la [limitazione delle versioni di aggiornamento](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) non è supprted da PackageReference ma aggiunge il supporto per le versioni a [virgola mobile](../consume-packages/package-references-in-project-files.md#floating-versions).

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
> Prima dell'inizio della migrazione, Visual Studio crea un backup del progetto per consentire di [eseguire il rollback a packages.config](#how-to-roll-back-to-packagesconfig) se necessario.

1. Aprire una soluzione contenente il progetto con `packages.config`.

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo **Riferimenti** o sul file `packages.config` e scegliere **Esegui la migrazione da packages.config a PackageReference**.

1. L'utilità di migrazione analizza i riferimenti ai pacchetti NuGet del progetto e tenta di categorizzarli in **Dipendenze di primo livello** (pacchetti NuGet installati direttamente) e **Dipendenze transitive** (pacchetti installati come dipendenze dei pacchetti di primo livello).

   > [!Note]
   > PackageReference supporta il ripristino transitivo dei pacchetti e risolve le dipendenze in modo dinamico, vale a dire che non è necessario installare in modo esplicito le dipendenze transitive.

1. (Facoltativo) È possibile scegliere di considerare un pacchetto NuGet classificato come dipendenza transitiva come dipendenza di primo livello selezionando l'opzione **Primo livello** per il pacchetto. Questa opzione viene impostata automaticamente per i pacchetti contenenti asset che non vengono trasferiti in modo transitivo (ovvero quelli nelle cartelle `build`, `buildCrossTargeting`, `contentFiles` o `analyzers`) e quelli contrassegnati come dipendenza di sviluppo (`developmentDependency = "true"`).

1. Esaminare eventuali [problemi di compatibilità dei pacchetti](#package-compatibility-issues).

1. Selezionare **OK** per avviare la migrazione.

1. Al termine della migrazione, Visual Studio fornisce un report con un percorso del backup, l'elenco dei pacchetti installati (dipendenze di primo livello), un elenco di pacchetti a cui si fa riferimento come dipendenze transitive e un elenco dei problemi di compatibilità identificati all'inizio della migrazione. Il report viene salvato nella cartella di backup.

1. Verificare che la soluzione venga compilata ed eseguita. Se si verificano problemi, [registrare un problema in GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Come eseguire il rollback a packages.config

1. Chiudere il progetto migrato.

1. Copiare il file di progetto e `packages.config` dal backup (in genere `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) nella cartella del progetto. Eliminare la cartella obj se è presente nella directory radice del progetto.

1. Aprire il progetto.

1. Aprire la console di Gestione pacchetti dal menu **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**.

1. Eseguire il comando seguente nella console:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>Creare un pacchetto dopo la migrazione

Al termine della migrazione, è consigliabile aggiungere un riferimento al pacchetto NuGet [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) e quindi usare [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) per creare il pacchetto. Sebbene in alcuni scenari sia possibile usare `dotnet.exe pack` invece di `msbuild -t:pack`, non è consigliabile.

## <a name="package-compatibility-issues"></a>Problemi di compatibilità dei pacchetti

Alcuni aspetti supportati in packages.config non sono supportati in PackageReference. L'utilità di migrazione analizza e rileva tali problemi. I pacchetti che presentano uno o più dei problemi seguenti potrebbero presentare comportamenti imprevisti dopo la migrazione.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>Gli script "install.ps1" vengono ignorati quando il pacchetto viene installato dopo la migrazione

* **Descrizione**: con PackageReference, install.ps1 e uninstall.ps1 script di PowerShell non vengono eseguiti durante l'installazione o la disinstallazione di un pacchetto.

* **Impatto potenziale**: i pacchetti che dipendono da questi script per configurare un comportamento nel progetto di destinazione potrebbero non funzionare come previsto.

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Gli asset "content" non sono disponibili quando il pacchetto viene installato dopo la migrazione

* **Descrizione**: gli asset nella cartella di un pacchetto `content` non sono supportati con PackageReference e vengono ignorati. PackageReference aggiunge il supporto per `contentFiles` per ottenere supporto transitivo e contenuto condiviso migliori.

* **Impatto potenziale**: gli asset in `content` non vengono copiati nel progetto e il codice del progetto che dipende dalla presenza di tali asset richiede il refactoring.

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Le trasformazioni XDT non vengono applicate quando il pacchetto viene installato dopo l'aggiornamento

* **Descrizione**: le trasformazioni xdt non sono supportate con PackageReference e `.xdt` i file vengono ignorati durante l'installazione o la disinstallazione di un pacchetto.

* **Impatto potenziale**: le trasformazioni xdt non vengono applicate ai file XML del progetto, in genere `web.config.install.xdt` e `web.config.uninstall.xdt` , il che significa che il ` web.config` file del progetto non viene aggiornato quando il pacchetto viene installato o disinstallato.

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Gli assembly nella radice lib vengono ignorati quando il pacchetto viene installato dopo la migrazione

* **Descrizione**: con PackageReference, gli assembly presenti nella radice della `lib` cartella senza una sottocartella specifica del Framework di destinazione vengono ignorati. NuGet cerca una sottocartella corrispondente al moniker framework di destinazione (TFM) corrispondente al framework di destinazione del progetto e installa gli assembly corrispondenti nel progetto.

* **Impatto potenziale**: i pacchetti che non dispongono di una sottocartella corrispondente al moniker del Framework di destinazione (TFM) corrispondente al Framework di destinazione del progetto potrebbero non comportarsi come previsto dopo l'installazione della transizione o non riuscita durante la migrazione.

## <a name="found-an-issue-report-it"></a>Segnalare i problemi riscontrati.

Se si verifica un problema con l'esperienza di migrazione, [registrare un problema nel repository GitHub di NuGet](https://github.com/NuGet/Home/issues/).
