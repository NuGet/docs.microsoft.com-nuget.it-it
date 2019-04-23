---
title: Variabili di ambiente NuGet CLI
description: Informazioni di riferimento per le variabili di ambiente nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: ac1bf2b65ab6ec4e8cf864810181fc661236262a
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931982"
---
# <a name="nuget-cli-environment-variables"></a>Variabili di ambiente NuGet CLI

Il comportamento di nuget.exe CLI può essere configurato tramite un numero di variabili di ambiente, che interessano nuget.exe a livello di computer, utente o elaborare i livelli. Le variabili di ambiente è sempre eseguire l'override di tutte le impostazioni in `NuGet.Config` file, consentendo di server per modificare le impostazioni appropriate senza modificare i file di compilazione.

In generale, le opzioni specificate direttamente nella riga di comando o nei file di configurazione NuGet hanno la precedenza, ma esistono alcune eccezioni, ad esempio *FORCE_NUGET_EXE_INTERACTIVE*. Se si ritiene che nuget.exe si comporta in modo diverso tra computer diversi, la causa potrebbe essere una variabile di ambiente. Ad esempio, Kudu di App Web di Azure (usato durante la distribuzione) ha *NUGET_XMLDOC_MODE* impostata su *ignorare* per velocizzare le prestazioni di ripristino del pacchetto e risparmiare spazio su disco.

NuGet CLI usa MSBuild per leggere i file di progetto. Tutte le variabili di ambiente sono disponibili come [proprietà](/visualstudio/msbuild/msbuild-command-line-reference) durante la valutazione di MSBuild.
L'elenco di proprietà documentate nel [NuGet pack e restore come destinazioni MSBuild](../reference/msbuild-targets.md#restore-properties) possono essere impostate anche come variabili di ambiente.

| Variabile | Descrizione | Note |
| --- | --- | --- |
| http_proxy | Proxy HTTP utilizzato per operazioni NuGet HTTP. | Questo potrebbe essere specificato come `http://<username>:<password>@proxy.com`. |
| no_proxy | Consente di configurare i domini da ignorare dalla mediante il proxy. | Specificato come domini separati da virgola (,). |
| EnableNuGetPackageRestore | Flag per se NuGet deve in modo implicito di concedere il consenso se richiesto dal pacchetto durante il ripristino. | Flag specificato viene considerato *true* oppure *1*, qualsiasi altro valore considerato come flag non impostato. |
| NUGET_EXE_NO_PROMPT | Impedisce che il file exe per richiedere le credenziali. | Qualsiasi valore con la differenza viene considerata una stringa vuota o null come questo flag true/set. |
| FORCE_NUGET_EXE_INTERACTIVE | Variabile di ambiente globale per forzare la modalità interattiva. | Qualsiasi valore con la differenza viene considerata una stringa vuota o null come questo flag true/set. |
| NUGET_PACKAGES | Percorso da usare per la *global-packages* cartella come descritto in [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Specificato come percorso assoluto. |
| NUGET_FALLBACK_PACKAGES | Cartelle dei pacchetti globale di fallback. | Percorsi di cartella assoluto separati da punto e virgola (;). |
| NUGET_HTTP_CACHE_PATH | Percorso da usare per la *http-cache* cartella come descritto in [gestione dei pacchetti globali e le cartelle cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Specificato come percorso assoluto. |
| NUGET_PERSIST_DG | Flag che indica se devono essere mantenuti i file di gruppo di distribuzione (i dati raccolti da MSBuild). | Specificato come *true* oppure *false* (impostazione predefinita), se non impostato NUGET_PERSIST_DG_PATH verrà archiviato in una directory temporanea (NuGetScratch cartella nella directory temp di ambiente corrente). |
| NUGET_PERSIST_DG_PATH | Percorso per rendere persistenti i file di gruppo di distribuzione. | Specificato come percorso assoluto, questa opzione viene usata solo quando *NUGET_PERSIST_DG* è impostato su true. |
| NUGET_RESTORE_MSBUILD_ARGS | Imposta gli argomenti MSBuild aggiuntivi. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Imposta il livello di dettaglio del log di MSBuild. | Il valore predefinito è *quiet* ("/ v: q"). I valori possibili *q [uiet]*, *m [inimal]*, *n [ormal]*, *1!d [etailed]*, e *diag [nostic]*. |
| NUGET_SHOW_STACK | Determina se l'eccezione completa (tra cui analisi dello stack) deve essere visualizzato all'utente. | Specificato come *true* oppure *false* (impostazione predefinita). |
| NUGET_XMLDOC_MODE | Determina la modalità di gestione dell'estrazione di file di documentazione XML degli assembly. | Sono supportate le modalità *ignorare* (non estrarre i file di documentazione XML), *comprimere* (memorizzare i file con estensione doc XML come archivio zip) o *none* (valore predefinito, considerare i file con estensione doc XML come normale file). |
| NUGET_CERT_REVOCATION_MODE | Determina la modalità di controllare lo stato di revoca del certificato utilizzato per firmare un pacchetto, viene eseguita quando un pacchetto firmato viene installato o ripristinato. Se non impostato, per impostazione predefinita `online`.| I valori possibili *online* (impostazione predefinita), *offline*.  Correlate a [NU3028](../reference/errors-and-warnings/NU3028.md) |

