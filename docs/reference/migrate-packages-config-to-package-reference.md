---
title: Migrazione da package per i formati PackageReference
description: Informazioni dettagliate su come eseguire la migrazione di un progetto dal formato di gestione di package a PackageReference come supportato da NuGet 4.0 + e Visual Studio 2017 e .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 4f42403abbf07c2c48ce13c70c49f7f3c15c40e4
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2018
ms.locfileid: "39072366"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>Eseguire la migrazione da Packages. config a PackageReference

Visual Studio 2017 versione 15.7 e successive supporta la migrazione di un progetto dal [Packages. config](./packages-config.md) formato di gestione per il [PackageReference](../consume-packages/Package-References-in-Project-Files.md) formato.

## <a name="benefits-of-using-packagereference"></a>Vantaggi dell'uso di PackageReference

* **Gestire tutte le dipendenze di progetto in un'unica posizione**: come riferimenti da progetto a progetto e riferimenti ad assembly, fa riferimento a pacchetto NuGet (usando il `PackageReference` nodo) vengono gestiti direttamente nel file di progetto anziché un oggetto separato file Packages. config.
* **Si riempia di elementi di visualizzazione delle dipendenze di primo livello**: a differenza di Packages. config, PackageReference, vengono elencati solo i pacchetti NuGet è installato direttamente nel progetto. Di conseguenza, la UI di gestione pacchetti NuGet e il file di progetto non sono congestionate da dipendenze di livello inferiore.
* **Miglioramenti delle prestazioni**: quando si usa PackageReference, i pacchetti vengono mantenuti nel *global-packages* cartella (come descritto in [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md) piuttosto che in un `packages` cartella all'interno della soluzione. Di conseguenza, PackageReference eseguita più velocemente e richiede meno spazio su disco.
* **Controllo delle dipendenze e il flusso del contenuto dettagliato**: grazie alle funzionalità esistenti di MSBuild consente [in modo condizionale fanno riferimento a un pacchetto NuGet](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) e scegliere i riferimenti ai pacchetti per ogni framework di destinazione, configurazione, piattaforma o altri punti.
* **PackageReference è in fase di sviluppo**: vedere [PackageReference problemi in GitHub](https://aka.ms/nuget-pr-improvements). Packages. config non è più in fase di sviluppo.

### <a name="limitations"></a>Limitazioni

* NuGet PackageReference non è disponibile in Visual Studio 2015 e versioni precedenti. Progetti migrati possono essere aperti solo in Visual Studio 2017.
* Migrazione non è attualmente disponibile per il progetto C++ e ASP.NET.
* Alcuni pacchetti potrebbero non essere completamente compatibili con PackageReference. Per altre informazioni, vedere [problemi di compatibilità pacchetti](#package-compatibility-issues).

### <a name="known-issues"></a>Problemi noti

1. L'opzione `Migrate packages.config to PackageReference...` non è disponibile nel menu di scelta rapida 

#### <a name="issue"></a>Problema 
 
Alla prima apertura di un progetto, NuGet potrebbe non essere inizializzato fino all'esecuzione di un'operazione NuGet. Per questo motivo, l'opzione di migrazione non viene visualizzata nel menu di scelta rapida per `packages.config` o `References`. 

#### <a name="workaround"></a>Soluzione alternativa 

Eseguire una delle operazioni NuGet seguenti: 
* Aprire l'interfaccia utente di Gestione pacchetti - fare clic con il pulsante destro del mouse su `References` e scegliere `Manage NuGet Packages...` 
* Aprire la console di Gestione pacchetti - Da `Tools > NuGet Package Manager` selezionare `Package Manager Console` 
* Eseguire un ripristino NuGet - Fare clic con il pulsante destro del mouse sul nodo della soluzione in Esplora soluzioni e scegliere `Restore NuGet Packages` 
* Compilare il progetto, ovvero un altro modo per attivare un ripristino NuGet 

A questo punto, l'opzione di migrazione dovrebbe essere visibile. Si noti che questa opzione non è supportata e non verrà visualizzata per i tipi di progetto ASP.NET e C++. 

## <a name="migration-steps"></a>Passaggi della migrazione

> [!Note]
> Prima che inizi la migrazione, Visual Studio crea un backup del progetto per consentire [: ripristino di Packages. config](#how-to-roll-back-to-packagesconfig) se necessario.

1. Aprire una soluzione contenente progetti usando `packages.config`.

1. Nella **Esplora soluzioni**, fare clic sul **riferimenti** nodo o la `packages.config` file e selezionare **Migrovat Packages. config a PackageReference...** .

1. Il migrator Analizza riferimenti del pacchetto NuGet del progetto e tenta di suddividere in categorie **dipendenze di livello superiore** (pacchetti NuGet che è stato installato direttamente) e **dipendenze Transitive** (pacchetti installati come dipendenze dei pacchetti di primo livello).

   > [!Note]
   > PackageReference supporta il ripristino dei pacchetti transitiva e risolve le dipendenze in modo dinamico, vale a dire che non è necessario installare le dipendenze transitive in modo esplicito.

1. (Facoltativo) È possibile scegliere di trattare un pacchetto NuGet classificato come dipendenza transitiva come dipendenza di livello superiore, selezionare la **principale** opzione per il pacchetto. Questa opzione viene impostata automaticamente per i pacchetti che contengono gli asset che non passano in modo transitivo (quelli presenti il `build`, `buildCrossTargeting`, `contentFiles`, o `analyzers` cartelle) e quelli contrassegnati come dipendenza di sviluppo (`developmentDependency = "true"`).

1. Rivedere le [problemi di compatibilità pacchetti](#package-compatibility-issues).

1. Selezionare **OK** per avviare la migrazione.

1. Al termine della migrazione, Visual Studio fornisce un report con un percorso per il backup, l'elenco dei pacchetti installati (dipendenze di livello superiore), un elenco di pacchetti di cui viene fatto riferimento come dipendenze transitive e un elenco di problemi di compatibilità identificato all'inizio di migrazione. Il report viene salvato nella cartella di backup.

1. Verificare che la soluzione venga generata ed eseguita. Se si verificano problemi, [segnalare un problema in GitHub](https://github.com/NuGet/Home/issues/).

## <a name="how-to-roll-back-to-packagesconfig"></a>Come eseguire il rollback di Packages. config

1. Chiudere il progetto migrato.

1. Copiare il file di progetto e `packages.config` dalla copia di backup (in genere `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) alla cartella del progetto. Eliminare la cartella obj se è presente nella directory radice del progetto.

1. Aprire il progetto.

1. Aprire la Console di gestione pacchetti usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando di menu.

1. Eseguire il comando seguente nella Console:

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>Problemi di compatibilità dei pacchetti

Alcuni aspetti che sono supportate in Packages. config non sono supportati in PackageReference. La migrazione analizza e rileva questi problemi. Qualsiasi pacchetto che contiene uno o più dei problemi seguenti potrebbe non comportarsi come previsto dopo la migrazione.

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>gli script "install.ps1" vengono ignorati quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Con PackageReference, gli script di PowerShell install.ps1 e uninstall.ps1 non vengono eseguiti durante l'installazione o disinstallazione di un pacchetto. |
| **Impatto potenziale** | I pacchetti che dipendono da tali script per configurare un comportamento nel progetto di destinazione potrebbero non funzionare come previsto. |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>gli asset "content" non sono disponibili quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Risorse in un pacchetto `content` cartella non sono supportate con PackageReference e vengono ignorati. Aggiunge il supporto di PackageReference `contentFiles` transitivo supporto più efficace e contenuto condiviso.  |
| **Impatto potenziale** | Gli asset in `content` non vengono copiati nel progetto e progetto codice che dipende dalla presenza di tali asset richiede il refactoring.  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>Trasformazioni XDT non vengono applicate quando il pacchetto viene installato dopo l'aggiornamento

| | |
| --- | --- |
| **Descrizione** | Trasformazioni XDT non sono supportate con PackageReference e `.xdt` file vengono ignorati durante l'installazione o disinstallazione di un pacchetto.   |
| **Impatto potenziale** | Trasformazioni XDT non vengono applicate a tutti i file XML di progetto, in genere `web.config.install.xdt` e `web.config.uninstall.xdt`, ovvero il progetto` web.config` file non viene aggiornata quando il pacchetto viene installato o disinstallato. |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>Gli assembly nella directory radice lib vengono ignorati quando il pacchetto viene installato dopo la migrazione

| | |
| --- | --- |
| **Descrizione** | Con PackageReference, gli assembly presentano nella radice di `lib` cartella senza una target framework sottocartella specifica vengono ignorati. NuGet Cerca una sottocartella corrispondente il moniker del framework di destinazione (TFM) corrispondente al framework di destinazione del progetto e installa gli assembly corrispondenti nel progetto. |
| **Impatto potenziale** | I pacchetti che non è una sottocartella corrispondente il moniker del framework di destinazione (TFM) corrispondente al framework di destinazione del progetto potrebbero non comportarsi come previsto al termine della transizione o esito negativo di installazione durante la migrazione |

## <a name="found-an-issue-report-it"></a>Stato riscontrato un problema? Segnalarla!

Se si verifica un problema con l'esperienza di migrazione, please [segnalare un problema nel repository GitHub di NuGet](https://github.com/NuGet/Home/issues/).
