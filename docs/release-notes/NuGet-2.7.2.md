---
title: Note sulla versione di NuGet 2.7.2
description: Note sulla versione per NuGet 2.7.2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776783"
---
# <a name="nuget-272-release-notes"></a>Note sulla versione di NuGet 2.7.2

Note sulla versione di [NuGet 2.7.1](../release-notes/nuget-2.7.1.md)  |  [Note sulla versione di NuGet 2,8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 è stato rilasciato l'11 novembre 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Funzionalità e correzioni di bug importanti

### <a name="license-text"></a>Testo della licenza
Per un certo periodo di tempo, Microsoft ha incluso i pacchetti NuGet per diverse librerie open source più diffuse nell'ambito dei modelli predefiniti per i progetti di applicazioni Web in Visual Studio. jQuery è probabilmente l'esempio più noto di questo tipo di libreria. A causa del contratto di supporto associato ai componenti recapitati insieme a un prodotto, il file di script del pacchetto contiene un testo di licenza diverso da quello del file script trovato nello stesso pacchetto nella raccolta nuget.org pubblica. Questa differenza nel testo può impedire la continuazione degli aggiornamenti dei pacchetti in seguito a diversi blocchi di testo della licenza che causano valori hash del contenuto diversi per i file di script e che pertanto devono essere considerati modificati all'interno del progetto.

Per attenuare questo problema, NuGet 2.7.2 consente all'autore dello script di includere il blocco di testo della licenza all'interno di una sezione contrassegnata in modo speciale, che ha un aspetto simile al seguente.

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

Quando si aggiornano i pacchetti con file di contenuto che contengono questo blocco, NuGet non esegue il factoring del contenuto del blocco nel confronto con la versione nella raccolta NuGet ed è quindi in grado di eliminare e aggiornare il file di contenuto come se corrispondesse alla copia originale.

Questo blocco è identificato dal testo "NUGET: BEGIN LICENSE TEXT" e "NUGET: END LICENSE TEXT" in qualsiasi punto della riga iniziale e finale.  Non esistono altri requisiti di formattazione che consentono di usare questa funzionalità in qualsiasi tipo di file di testo indipendentemente dal linguaggio.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Aggiungere reindirizzamenti di binding per gli assembly non Framework
Per gli assembly che fanno parte del .NET Framework, NuGet ignora l'aggiunta di reindirizzamenti di associazione nel file di configurazione dell'applicazione durante l'aggiornamento del pacchetto. Questa correzione risolve una regressione in NuGet 2,7, che indica che i reindirizzamenti di binding non sono stati aggiunti per alcuni assembly, anche se tali assembly non sono considerati parte del .NET Framework. NuGet 2.7.2 ripristina il comportamento NuGet 2,5 e 2,6 precedente e aggiunge i reindirizzamenti di binding.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Installazione delle librerie portabili con gli strumenti Novell installati
Quando gli strumenti di sviluppo di Novell sono installati in un computer, modificano i dati di configurazione dei Framework supportati per specificare la compatibilità tra le combinazioni di Framework di destinazione esistenti e i Framework Novell. Con la versione 2.7.2, NuGet è ora in grado di riconoscere queste regole di compatibilità implicita e pertanto rende più semplice per gli sviluppatori la definizione di piattaforme Novell per l'installazione di librerie portabili compatibili con Novell ma non esplicitamente contrassegnate come tali nei metadati del pacchetto stesso.

### <a name="machine-wide-configuration-settings-honored"></a>Impostazioni di configurazione a livello di computer rispettate
Quando si usano file di Nuget.Config gerarchici, la chiave repositoryPath non è stata rispettata per i file Nuget.Config più vicini alla radice della soluzione. In Visual Studio 2013, NuGet installa un file di Nuget.Config personalizzato in% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config per aggiungere l'origine del pacchetto "Microsoft e .NET". Di conseguenza, la soluzione ideale per l'uso di un repositoryPath personalizzato in una soluzione consiste nell'eliminare il Nuget.Config a livello di computer, che significava anche la rimozione dell'origine del pacchetto "Microsoft e .NET". NuGet 2.7.2 ora rispetta le regole di precedenza per repositoryPath quando si usano file di Nuget.Config gerarchici.

## <a name="all-changes"></a>Tutte le modifiche
Per un elenco completo degli elementi di lavoro corretti in NuGet 2.7.2, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
