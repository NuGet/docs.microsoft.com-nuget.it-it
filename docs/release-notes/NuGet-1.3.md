---
title: Note sulla versione 1.3 di NuGet
description: Note sulla versione per NuGet 1.3 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821148"
---
# <a name="nuget-13-release-notes"></a>Note sulla versione 1.3 di NuGet

[Note sulla versione di NuGet 1.2](../release-notes/nuget-1.2.md) | [note sulla versione 1.4 di NuGet](../release-notes/nuget-1.4.md)

NuGet 1.3 è stata rilasciata il 25 aprile 2011.

## <a name="new-features"></a>Nuove funzionalità

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Creazione del pacchetto ottimizzata con l'integrazione di server di simboli

Il team di NuGet collaborato con i colleghi [SymbolSource.org](http://www.symbolsource.org/) per offrire un modo semplice di pubblicare le origini e del file PDB con il pacchetto. Questo consente ai consumer del pacchetto di eseguire l'istruzione di origine per il pacchetto nel debugger. Per altre informazioni, leggere [creazione e la pubblicazione di un pacchetto di simboli](../create-packages/symbol-packages.md) il modo più semplice per pubblicare i pacchetti NuGet con origini. È anche possibile guardare una dimostrazione in tempo reale di questa funzionalità, come parte di NuGet in modo approfondito comunicare in Mix11. Questa funzionalità è completamente illustrata a partire dal contrassegno di 20 minuti del video.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Comando

Questo comando consente di connettersi alla pagina del progetto per un pacchetto dall'interno della Console di gestione pacchetti. Fornisce inoltre opzioni per aprire l'URL di licenza e la pagina del report abusi per il pacchetto.
La sintassi per il comando è:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

Il `-PassThru` opzione viene utilizzata per restituire il valore dell'URL specificato.

Esempi:

    PM> Open-PackagePage Ninject

Apre un browser all'URL di progetto specificato nel pacchetto Ninject.

    PM> Open-PackagePage Ninject -License

Apre un browser all'URL della licenza specificato nel pacchetto Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Apre un browser all'URL nell'origine pacchetto corrente usato per segnalare abusi per il pacchetto specificato.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Assegna l'URL della licenza alla variabile, $url, senza aprire l'URL in un browser.

### <a name="performance-improvements"></a>Miglioramenti delle prestazioni

1.3 NuGet introduce numerosi miglioramenti delle prestazioni. 1.3 NuGet consente di evitare il download di più volte la stessa versione di un pacchetto con l'inclusione di una cache locale per ogni utente. La cache siano accessibili e mediante la finestra di dialogo Impostazioni di gestione pacchetti:

![Finestra di dialogo Opzioni NuGet con le impostazioni della Cache di pacchetto](./media/nuget-options.png)

Altri miglioramenti delle prestazioni includono l'aggiunta del supporto per la compressione HTTP e migliorare la velocità di installazione del pacchetto all'interno di Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio e nuget.exe utilizza lo stesso elenco di origini dei pacchetti

Prima di NuGet 1.3, l'elenco delle origini pacchetto utilizzato da nuget.exe e il componente aggiuntivo NuGet Visual Studio non sono stati archiviati nella stessa posizione. 1.3 NuGet ora utilizza lo stesso elenco in entrambe le posizioni. L'elenco viene archiviato `NuGet.Config` e archiviati nella cartella AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe ignora i file e cartelle che iniziano con '.' per impostazione predefinita

Per rendere NuGet funzionano bene con sistemi di controllo codice sorgente, ad esempio Subversion e Mercurial, nuget.exe ignora le cartelle e i file che iniziano con il '.' carattere durante la creazione di pacchetti. Può essere sottoposta a override utilizzando due nuovi flag:

* __-NoDefaultExcludes__ viene utilizzato per eseguire l'override di questa impostazione e include tutti i file.
* __-Escludere__ consente di aggiungere altri file e cartelle da escludere usando un modello. Ad esempio, per escludere tutti i file con estensione '. bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Nota: il modello non è ricorsiva per impostazione predefinita._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Supporto per i progetti di WiX e Micro .NET Framework

Grazie ai contributi della community, NuGet include il supporto per i tipi di progetto WiX nonché Micro .NET Framework.

## <a name="bug-fixes"></a>Correzioni di bug

Per un elenco completo delle correzioni di bug, visitare il [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug non degni di nota

* Pacchetti con file di origine funzionano in entrambi i siti Web e progetti di applicazione Web.
Per i siti Web, file di origine vengono copiati nel `App_Code` cartella
