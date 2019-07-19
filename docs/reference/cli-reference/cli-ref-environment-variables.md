---
title: Variabili di ambiente CLI NuGet
description: Informazioni di riferimento per le variabili di ambiente NuGet. exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b04efaecce1d5bc892dfc48ae3e872d80aad209d
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327828"
---
# <a name="nuget-cli-environment-variables"></a>Variabili di ambiente CLI NuGet

Il comportamento dell'interfaccia della riga di comando di NuGet. exe può essere configurato tramite una serie di variabili di ambiente, che influiscono su NuGet. exe a livello di computer, utente o processo. Le variabili di ambiente eseguono sempre l' `NuGet.Config` override delle impostazioni nei file, consentendo ai server di compilazione di modificare le impostazioni appropriate senza modificare alcun file.

In generale, le opzioni specificate direttamente nella riga di comando o nei file di configurazione NuGet hanno la precedenza, ma esistono alcune eccezioni, ad esempio *FORCE_NUGET_EXE_INTERACTIVE*. Se si rileva che NuGet. exe si comporta in modo diverso tra computer diversi, una variabile di ambiente potrebbe essere la stessa. Ad esempio, per le app Web di Azure Kudu (usato durante la distribuzione) *NUGET_XMLDOC_MODE* è impostato su *Skip* per velocizzare le prestazioni di ripristino del pacchetto e risparmiare spazio su disco.

L'interfaccia della riga di comando di NuGet USA MSBuild per leggere i file di progetto. Tutte le variabili di ambiente sono disponibili come [Proprietà](/visualstudio/msbuild/msbuild-command-line-reference) durante la valutazione di MSBuild.
L'elenco delle proprietà documentate nel [pacchetto e nel ripristino di NuGet come destinazioni MSBuild](../msbuild-targets.md#restore-properties) può essere impostato anche come variabile di ambiente.

| Variabile | Descrizione | Note |
| --- | --- | --- |
| http_proxy | Proxy http usato per le operazioni HTTP NuGet. | Viene specificato come `http://<username>:<password>@proxy.com`. |
| no_proxy | Configura domini per il bypass dall'uso del proxy. | Specificato come domini separati da virgola (,). |
| EnableNuGetPackageRestore | Flag per se NuGet deve concedere in modo implicito il consenso se richiesto dal pacchetto durante il ripristino. | Il flag specificato viene considerato *true* o *1*, qualsiasi altro valore trattato come flag non impostato. |
| NUGET_EXE_NO_PROMPT | Impedisce al file exe di richiedere le credenziali. | Qualsiasi valore, ad eccezione di una stringa vuota o null, verrà considerato come questo flag set/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Variabile di ambiente globale per forzare la modalità interattiva. | Qualsiasi valore, ad eccezione di una stringa vuota o null, verrà considerato come questo flag set/true. |
| NUGET_PACKAGES | Percorso da usare per la cartella *Global-Packages* , come descritto in [gestione delle cartelle dei pacchetti globali e della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Specificato come percorso assoluto. |
| NUGET_FALLBACK_PACKAGES | Cartelle dei pacchetti di fallback globali. | Percorsi di cartella assoluti separati da punto e virgola (;). |
| NUGET_HTTP_CACHE_PATH | Percorso da usare per la cartella *http-cache* come descritto in [gestione delle cartelle dei pacchetti globali e della cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md). | Specificato come percorso assoluto. |
| NUGET_PERSIST_DG | Flag che indica se i file DG (dati raccolti da MSBuild) devono essere resi permanente. | Specificato come *true* o *false* (impostazione predefinita) se NUGET_PERSIST_DG_PATH non impostato verrà archiviato nella directory temporanea (cartella NuGetScratch nella directory temporanea dell'ambiente corrente). |
| NUGET_PERSIST_DG_PATH | Percorso per salvare in modo permanente i file DG. | Specificato come percorso assoluto, questa opzione viene usata solo quando *NUGET_PERSIST_DG* è impostato su true. |
| NUGET_RESTORE_MSBUILD_ARGS | Imposta argomenti MSBuild aggiuntivi. | Passare gli argomenti identici a quelli che verrebbero passati a MSBuild. exe. Un esempio di impostazione di una proprietà di progetto foo dalla riga di comando alla barra dei valori è/p: foo = bar |
| NUGET_RESTORE_MSBUILD_VERBOSITY | Imposta il livello di dettaglio del log di MSBuild. | Il valore predefinito è *quiet* ("/v: q"). Valori possibili *q [uiet]* , *m [inimal]* , *n [ormal]* , *d [etailed]* e *diag [nostic]* . |
| NUGET_SHOW_STACK | Determina se l'eccezione completa (inclusa l'analisi dello stack) deve essere visualizzata all'utente. | Specificato come *true* o *false* (impostazione predefinita). |
| NUGET_XMLDOC_MODE | Determina il modo in cui deve essere gestita l'estrazione del file di documentazione XML degli assembly. | Le modalità supportate sono *Ignora* (non Estrai file di documentazione XML), *Comprimi* (archivia i file doc XML come archivio zip) o *None* (impostazione predefinita, considera i file doc XML come file normali). |
| NUGET_CERT_REVOCATION_MODE | Determina il modo in cui viene eseguito il controllo dello stato di revoca del certificato utilizzato per firmare un pacchetto quando un pacchetto firmato viene installato o ripristinato. Quando non è impostato, il valore `online`predefinito è.| I valori possibili sono *online* (impostazione predefinita), *offline*.  Correlato a [NU3028](../errors-and-warnings/NU3028.md) |

