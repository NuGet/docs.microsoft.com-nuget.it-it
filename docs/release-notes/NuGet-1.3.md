---
title: Note sulla versione di NuGet 1,3
description: Note sulla versione per NuGet 1,3, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777118"
---
# <a name="nuget-13-release-notes"></a>Note sulla versione di NuGet 1,3

Note sulla versione di [NuGet 1,2](../release-notes/nuget-1.2.md)  |  [Note sulla versione di NuGet 1,4](../release-notes/nuget-1.4.md)

NuGet 1,3 è stato rilasciato il 25 aprile 2011.

## <a name="new-features"></a>Nuove funzioni e caratteristiche

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Creazione semplificata di pacchetti con l'integrazione del server dei simboli

Il team NuGet ha collaborato con gli utenti di [symbolsource.org](http://www.symbolsource.org/) per offrire un modo molto semplice per pubblicare le origini e i file PDB insieme al pacchetto. Questo consente ai consumer del pacchetto di eseguire un'istruzione nell'origine del pacchetto nel debugger. Per altri dettagli, vedere [creazione e pubblicazione di un pacchetto di simboli](../create-packages/symbol-packages.md) il modo più semplice per pubblicare pacchetti NuGet con origini. È anche possibile guardare una dimostrazione diretta di questa funzionalità come parte di NuGet approfondita in Mix11. Questa funzionalità è completamente illustrata a partire dal contrassegno di 20 minuti del video.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Command

Questo comando consente di ottenere facilmente la pagina del progetto per un pacchetto all'interno della console di gestione pacchetti. Sono inoltre disponibili opzioni per aprire l'URL della licenza e la pagina relativa all'abuso del report per il pacchetto.
La sintassi per il comando è:

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

L' `-PassThru` opzione viene utilizzata per restituire il valore dell'URL specificato.

Esempi:

```
PM> Open-PackagePage Ninject
```

Apre un browser per l'URL del progetto specificato nel pacchetto Ninject.

```
PM> Open-PackagePage Ninject -License
```

Apre un browser per l'URL di licenza specificato nel pacchetto Ninject.

```
PM> Open-PackagePage Ninject -ReportAbuse
```

Apre un browser per l'URL nell'origine del pacchetto corrente utilizzata per segnalare gli abusi per il pacchetto specificato.

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

Assegna l'URL della licenza alla variabile, $url, senza aprire l'URL in un browser.

### <a name="performance-improvements"></a>Miglioramenti alle prestazioni

NuGet 1,3 introduce un notevole miglioramento delle prestazioni. NuGet 1,3 evita di scaricare la stessa versione di un pacchetto più volte includendo una cache per utente locale. È possibile accedere alla cache e cancellarla tramite la finestra di dialogo Impostazioni di gestione pacchetti:

![Finestra di dialogo Opzioni NuGet con impostazioni della cache dei pacchetti](./media/nuget-options.png)

Altri miglioramenti alle prestazioni includono l'aggiunta del supporto per la compressione HTTP e il miglioramento della velocità di installazione dei pacchetti in Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio e nuget.exe utilizzano lo stesso elenco di origini di pacchetti

Prima di NuGet 1,3, l'elenco di origini dei pacchetti usato da nuget.exe e NuGet Visual Studio Add-In non venivano archiviati nella stessa posizione. NuGet 1,3 ora usa lo stesso elenco in entrambe le posizioni. L'elenco viene archiviato in `NuGet.Config` e archiviato nella cartella AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe ignora i file e le cartelle che iniziano con ' .' per impostazione predefinita

Per consentire a NuGet di funzionare correttamente con sistemi di controllo del codice sorgente quali Subversion e Mercurial, nuget.exe ignora le cartelle e i file che iniziano con il carattere ' .' durante la creazione dei pacchetti. È possibile eseguirne l'override usando due nuovi flag:

* __-NoDefaultExcludes__ viene usato per eseguire l'override di questa impostazione e includere tutti i file.
* __-Exclude__ viene usato per aggiungere altri file o cartelle da escludere usando un modello. Ad esempio, per escludere tutti i file con l'estensione di file '. bak '

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Nota: il criterio non è ricorsivo per impostazione predefinita._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Supporto per progetti WiX e .NET Micro Framework

Grazie ai contributi della community, NuGet include il supporto per i tipi di progetto WiX e .NET Micro Framework.

## <a name="bug-fixes"></a>Correzioni di bug

Per un elenco completo delle correzioni di bug, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug da notare

* I pacchetti con file di origine funzionano sia nei siti Web che nei progetti di applicazione Web.
Per i siti Web, i file di origine vengono copiati nella `App_Code` cartella
