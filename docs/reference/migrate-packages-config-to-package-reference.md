---
title: Migrazione da package.config a formati PackageReference
description: Informazioni dettagliate su come eseguire la migrazione di un progetto dal formato gestione package.config a PackageReference come supportato da NuGet 4.0 + e VS2017 e 2.0 di .NET Core
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: e0a4363a2807874ec8e2693c5b1c1a0eb2e8af0e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818786"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>La migrazione da Packages. config a PackageReference

Visual Studio 2017 versione 15.7 Preview 3 e versioni successive è supportata la migrazione di un progetto dal [Packages](./packages-config.md) formato di gestione per il [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formato.

## <a name="benefits-of-using-packagereference"></a>Vantaggi dell'utilizzo PackageReference

* **Gestire tutte le dipendenze di progetto in un'unica posizione**: come riferimenti da progetto a progetto e riferimenti all'assembly fa riferimento a pacchetto NuGet (usando il `PackageReference` nodo) vengono gestite direttamente all'interno di file di progetto anziché un oggetto separato file Packages. config.
* **Si riempia di elementi di visualizzazione delle dipendenze di primo livello**: a differenza dei file Packages. config, PackageReference Elenca solo i pacchetti di NuGet è installato direttamente nel progetto. Di conseguenza, la UI di gestione pacchetti NuGet e il file di progetto non sono chiara con dipendenze di livello inferiore.
* **Miglioramenti delle prestazioni**: quando si utilizza PackageReference, i pacchetti vengono mantenuti nel *globale pacchetti* cartella (come descritto in [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) piuttosto che in un `packages` cartella all'interno della soluzione. Di conseguenza, PackageReference assicura prestazioni più rapide e utilizza meno spazio su disco.
* **Fine di controllare le dipendenze e il flusso del contenuto**: tramite le funzionalità esistenti di MSBuild consente [in modo condizionale fanno riferimento a un pacchetto NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) scegliere pacchetto fa riferimento al framework di destinazione, configurazione, piattaforma o altri punti.
* **PackageReference è in fase di sviluppo**: vedere [PackageReference problemi su GitHub](https://aka.ms/nuget-pr-improvements). file Packages. config non è più in fase di sviluppo.

### <a name="limitations"></a>Limitazioni

* NuGet PackageReference non è disponibile in Visual Studio 2015 e versioni precedenti. Progetti migrati possono essere aperti solo in Visual Studio 2017.
* Migrazione non è attualmente disponibile per il progetto C++ e ASP.NET.
* Alcuni pacchetti potrebbero non essere completamente compatibili con PackageReference. Per altre informazioni, vedere [problemi di compatibilità del pacchetto](#package-compatibility-issues).

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
> Prima di inizia la migrazione, Visual Studio crea un backup del progetto per poter [ripristinare Packages](#how-to-roll-back-to-packagesconfig) se necessario.

1. Aprire una soluzione contenente progetti tramite `packages.config`.

1. In **Esplora soluzioni**, fare clic sui **riferimenti** nodo o il `packages.config` file e selezionare **migrare PackageReference Packages. config...** .

1. La migrazione Analizza riferimenti del pacchetto NuGet del progetto e tenta di suddividere in categorie **dipendenze di primo livello** (NuGet pacchetti tale directory è stato installato) e **dipendenze Transitive**(pacchetti che sono stati installati come dipendenze dei pacchetti di primo livello).

   > [!Note]
   > PackageReference supporta ripristino del pacchetto transitiva e consente di risolvere le dipendenze in modo dinamico, vale a dire che non è necessario installare le dipendenze transitive in modo esplicito.

1. (Facoltativo) È possibile scegliere di considerare un pacchetto NuGet classificato come una dipendenza transitiva come dipendenza di livello superiore, selezionare il **primo livello** opzione per il pacchetto. Questa opzione viene impostata automaticamente per i pacchetti che contengono risorse che non passano in modo transitivo (quelli presenti il `build`, `buildCrossTargeting`, `contentFiles`, oppure `analyzers` cartelle) e quelli contrassegnati come una dipendenza di sviluppo (`developmentDependency = "true"`).

1. Rivedere le [problemi di compatibilità del pacchetto](#package-compatibility-issues).

1. Selezionare **OK** per avviare la migrazione.

1. Al termine della migrazione, Visual Studio fornisce un report con un percorso per il backup, l'elenco dei pacchetti installati (dipendenze di primo livello), un elenco di pacchetti di cui viene fatto riferimento come dipendenze transitive e un elenco dei problemi di compatibilità identificato all'inizio di migrazione. Il report viene salvato nella cartella di backup.

1. Verificare che la soluzione si basa e viene eseguito. Se si verificano problemi, [file di un problema in GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Come eseguire il rollback a Packages. config

1. Chiudere il progetto migrato.

1. Copiare il file di progetto e `packages.config` dal backup (in genere `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) nella cartella di progetto. Eliminare la cartella obj se è presente nella directory radice del progetto.

1. Aprire il progetto.

1. Aprire la Console di gestione pacchetti utilizzando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando di menu.

1. Eseguire il comando seguente nella Console:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problemi di compatibilità dei pacchetti

Alcuni aspetti di cui sono supportate in Packages. config non sono supportati in PackageReference. La migrazione analizza e rileva tali problemi. I pacchetti che include uno o più dei seguenti problemi potrebbero non comportarsi come previsto dopo la migrazione.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>"install.ps1" script vengono ignorati quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Con PackageReference, gli script di PowerShell install.ps1 e uninstall.ps1 non vengono eseguiti durante l'installazione o disinstallazione di un pacchetto. |
| **Impatto potenziale** | I pacchetti che dipendono da questi script per configurare il comportamento di alcuni nel progetto di destinazione potrebbero non funzionare come previsto. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>Asset "contenuto" non sono disponibili quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Gli asset in un pacchetto `content` cartella non sono supportate con PackageReference e vengono ignorati. PackageReference aggiunge il supporto per `contentFiles` meglio transitivo supporto e contenuto condiviso.  |
| **Impatto potenziale** | Gli asset in `content` non vengono copiati nel progetto e progetto codice che dipende dalla presenza di tali risorse richiede il refactoring.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Le trasformazioni XDT non vengono applicate quando il pacchetto viene installato dopo l'aggiornamento

| | |
| --- | --- |
| **Descrizione** | Le trasformazioni XDT non sono supportate con PackageReference e `.xdt` i file vengono ignorati durante l'installazione o disinstallazione di un pacchetto.   |
| **Impatto potenziale** | Trasformazioni XDT non vengono applicate a qualsiasi file XML di progetto, in genere, `web.config.install.xdt` e `web.config.uninstall.xdt`, ovvero il progetto` web.config` file non viene aggiornato quando il pacchetto viene installato o disinstallato. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Gli assembly nella directory principale lib vengono ignorati quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Con PackageReference, gli assembly presentano nella radice della `lib` cartella senza una destinazione framework specifici sottocartella vengono ignorati. NuGet Cerca una sottocartella moniker del framework di destinazione (TFM) corrispondente al framework di destinazione del progetto di corrispondenza e installa gli assembly corrispondenti nel progetto. |
| **Impatto potenziale** | I pacchetti che non dispongono di una sottocartella corrispondenza moniker del framework di destinazione (TFM) corrispondente al framework di destinazione del progetto non venga si comportano come previsto al termine della transizione o non riuscire durante la migrazione |

## <a name="found-an-issue-report-it"></a>Rilevato un problema? Segnalarlo!

Se si esegue un problema con l'esperienza di migrazione, eseguire [file di un problema nel repository NuGet GitHub](https://github.com/NuGet/Home/issues/).
