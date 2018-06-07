---
title: Variabili di ambiente NuGet CLI
description: Riferimento per le variabili di ambiente nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 50bf8b469eda423db7665323823a2daf3f3aa41d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817073"
---
# <a name="nuget-cli-environment-variables"></a>Variabili di ambiente NuGet CLI

Il comportamento di nuget.exe CLI può essere configurato tramite un numero di variabili di ambiente, che influiscono sulla nuget.exe a livello di computer, utente o elaborazione dei livelli. Le variabili di ambiente sempre l'override delle impostazioni in `NuGet.Config` file, consentendo di server per modificare le impostazioni appropriate senza modificare i file di compilazione.

In generale, le opzioni specificate direttamente nella riga di comando o nei file di configurazione NuGet hanno la precedenza, ma esistono alcune eccezioni, ad esempio *FORCE_NUGET_EXE_INTERACTIVE*. Se si ritiene che nuget.exe si comporta in modo diverso tra computer diversi, la causa potrebbe essere una variabile di ambiente. Ad esempio, Kudu App Web di Azure (utilizzato durante la distribuzione) ha *NUGET_XMLDOC_MODE* impostato su *ignorare* per velocizzare le prestazioni di ripristino del pacchetto e risparmiare spazio su disco.

| Variabile | Descrizione | Note |
| --- | --- | --- |
| http_proxy | Proxy HTTP utilizzato per le operazioni HTTP NuGet. | Questo potrebbe essere specificato come `http://<username>:<password>@proxy.com`. |
| no_proxy | Configura i domini da ignorare da tramite proxy. | Specificare come domini separati da virgola (,). |
| EnableNuGetPackageRestore | Flag per se NuGet in modo implicito concedere il consenso se richiesto dal pacchetto durante il ripristino. | Flag specificato viene considerato *true* oppure *1*, qualsiasi altro valore considerato come flag non è impostata. |
| NUGET_EXE_NO_PROMPT | Impedisce il file exe per richiedere le credenziali. | Qualsiasi valore ad eccezione del fatto verrà considerata come una stringa vuota o null, questo flag set/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Variabile di ambiente globali per forzare la modalità interattiva. | Qualsiasi valore ad eccezione del fatto verrà considerata come una stringa vuota o null, questo flag set/true. |
| NUGET_PACKAGES | Percorso da usare per il *globale pacchetti* cartella come descritto in [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Specificato come percorso assoluto. |
| NUGET_FALLBACK_PACKAGES | Cartelle di pacchetti di fallback globale. | Percorsi di cartella assoluto separati da punto e virgola (;). |
| NUGET_HTTP_CACHE_PATH | Percorso da usare per il *cache http* cartella come descritto in [gestione dei pacchetti globali e alla cartella della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Specificato come percorso assoluto. |
| NUGET_PERSIST_DG | Flag che indica se il file dg (dati raccolti da MSBuild) devono essere mantenuto. | Specificato come *true* o *false* (impostazione predefinita), se non impostato NUGET_PERSIST_DG_PATH verrà archiviato in directory temporanea (cartella NuGetScratch nella directory temp di ambiente corrente). |
| NUGET_PERSIST_DG_PATH | Percorso per mantenere i file dg. | Specificato come percorso assoluto, questa opzione viene utilizzato solo quando *NUGET_PERSIST_DG* è impostata su true. |
| NUGET_RESTORE_MSBUILD_ARGS | Imposta gli argomenti MSBuild aggiuntivi. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Imposta il livello di dettaglio del Registro di MSBuild. | Valore predefinito è *quiet* ("/ v: q"). I valori possibili *q [uiet]*, *m [inimal]*, *n [ormal]*, *d [etailed]*, e *diag [nostic]*. |
| NUGET_SHOW_STACK | Determina se l'eccezione completo, inclusa analisi dello stack, deve essere visualizzato all'utente. | Specificato come *true* o *false* (impostazione predefinita). |
| NUGET_XMLDOC_MODE | Determina la modalità di gestione di estrazione di file di documentazione XML assembly. | Le modalità supportate sono *ignorare* (non estrarre i file di documentazione XML), *comprimere* (archiviare file di documento XML come archivio zip) o *Nessuno* (valore predefinito, considerare i file di documento XML come normale file). |
