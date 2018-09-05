---
title: Note sulla versione 1.3 di NuGet
description: Note sulla versione per NuGet 1.3 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551351"
---
# <a name="nuget-13-release-notes"></a>Note sulla versione 1.3 di NuGet

[Note sulla versione di NuGet 1.2](../release-notes/nuget-1.2.md) | [note sulla versione di NuGet 1.4](../release-notes/nuget-1.4.md)

1.3 di NuGet è stato rilasciato il 25 aprile 2011.

## <a name="new-features"></a>Nuove funzionalità

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Creazione di pacchetti semplificata con integrazione del server di simboli

Il team di NuGet ha collaborato con i colleghi [SymbolSource.org](http://www.symbolsource.org/) per offrire un modo molto semplice della pubblicazione di origini e il del PDB insieme il pacchetto. In questo modo i consumer del pacchetto eseguire l'istruzione l'origine per il pacchetto nel debugger. Per altre informazioni, leggere [creazione e pubblicazione di un pacchetto di simboli](../create-packages/symbol-packages.md) il modo più semplice per pubblicare i pacchetti NuGet con le origini. È anche possibile guardare una dimostrazione di questa funzionalità in tempo reale come parte di NuGet in modo approfondito parlare a Mix11. Questa funzionalità è illustrata completamente a partire il contrassegno di 20 minuti del video.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Comando

Questo comando rende più semplice accedere alla pagina del progetto per un pacchetto dall'interno della Console di gestione pacchetti. Fornisce inoltre opzioni per aprire l'URL della licenza e la pagina di uso improprio di report per il pacchetto.
La sintassi del comando è:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

Il `-PassThru` opzione viene usata per restituire il valore dell'URL specificato.

Esempi:

    PM> Open-PackagePage Ninject

Apre un browser all'URL di progetto specificato nel pacchetto Ninject.

    PM> Open-PackagePage Ninject -License

Apre un browser all'URL di licenza specificato nel pacchetto Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Apre un browser all'URL dell'origine pacchetto corrente utilizzato per segnalare abusi per il pacchetto specificato.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Assegnare l'URL di licenza alla variabile, $url, senza dover aprire l'URL in un browser.

### <a name="performance-improvements"></a>Miglioramenti delle prestazioni

1.3 NuGet introduce numerosi miglioramenti delle prestazioni. 1.3 NuGet consente di evitare il download di più volte la stessa versione di un pacchetto tramite l'inclusione di una cache locale per ogni utente. La cache siano accessibili e cancellata tramite la finestra di dialogo Impostazioni di gestione pacchetti:

![Finestra di dialogo Opzioni NuGet con impostazioni della Cache del pacchetto](./media/nuget-options.png)

Altri miglioramenti delle prestazioni includono l'aggiunta del supporto per la compressione HTTP e migliorando la velocità di installazione del pacchetto all'interno di Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio e nuget.exe Usa lo stesso elenco di origini dei pacchetti

Prima di NuGet 1.3, l'elenco delle origini dei pacchetti utilizzato da nuget.exe e il componente aggiuntivo NuGet Visual Studio non sono stati archiviati nella stessa posizione. 1.3 NuGet ora Usa lo stesso elenco in entrambe le posizioni. L'elenco viene archiviato `NuGet.Config` e archiviato nella cartella AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet.exe ignora file e cartelle che iniziano con '.' per impostazione predefinita

Per poter effettuare NuGet funziona bene con sistemi di controllo codice sorgente quali Subversion e Mercurial, nuget.exe ignora file e cartelle che iniziano con il '.' durante la creazione di pacchetti di caratteri. Ciò può essere ignorato usando due nuovi flag:

* __-NoDefaultExcludes__ viene usato per eseguire l'override di questa impostazione e includere tutti i file.
* __-Esclusione__ consente di aggiungere altri file e cartelle da escludere usando un modello. Ad esempio, per escludere tutti i file con estensione '. bak'

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Nota: il modello non è ricorsiva per impostazione predefinita._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Supporto per i progetti di WiX e .NET Micro Framework

Grazie al contributo della community, NuGet include il supporto per tipi di progetto WiX, nonché .NET Micro Framework.

## <a name="bug-fixes"></a>Correzioni di bug

Per un elenco completo delle correzioni di bug, visitare il [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug la pena notare

* I pacchetti con i file di origine funzionano in entrambi i siti Web e nei progetti applicazione Web.
Per i siti Web, i file di origine vengono copiati le `App_Code` cartella
