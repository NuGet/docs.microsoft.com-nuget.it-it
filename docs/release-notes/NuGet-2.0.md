---
title: Note sulla versione 2.0 per NuGet
description: Note sulla versione per NuGet 2.0 tra problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547575"
---
# <a name="nuget-20-release-notes"></a>Note sulla versione 2.0 per NuGet

[Note sulla versione di NuGet 1.8](../release-notes/nuget-1.8.md) | [note sulla versione di NuGet 2.1](../release-notes/nuget-2.1.md)

NuGet 2.0 è stato rilasciato il 19 giugno 2012.

## <a name="known-installation-issue"></a>Problema di installazione noti
Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

Per risolvere il problema è sufficiente disinstallare NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Visualizzare [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) per altre informazioni, o [passare direttamente all'hotfix di Visual Studio](http://bit.ly/vsixcertfix).

Nota: Se Visual Studio non consentirà di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), quindi probabile che sia necessario riavviare Visual Studio tramite "Esegui come amministratore".

## <a name="package-restore-consent-is-now-active"></a>Il consenso di ripristino del pacchetto è ora attivo

Come descritto in questo [inserire un post nel package restore consenso](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 questo punto verrà richiesto il consenso per abilitare il ripristino dei pacchetti passare alla modalità online e scaricare i pacchetti. Assicurarsi di aver specificato il consenso tramite la finestra di dialogo pacchetto configuration manager o la variabile di ambiente EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Gruppo di dipendenze dal framework di destinazione

A partire dalla versione 2.0, pacchetto dipendenze possono variare in base al profilo del framework del progetto di destinazione. Ciò avviene utilizzando una versione aggiornata `.nuspec` dello schema. Il `<dependencies>` elemento può ora contenere un set di `<group>` elementi. Ogni gruppo contiene zero o più `<dependency>` elementi e un `targetFramework` attributo. Tutte le dipendenze all'interno di un gruppo vengono installate insieme se il framework di destinazione è compatibile con il profilo del framework di progetto di destinazione. Ad esempio:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Si noti che un gruppo può contenere **zero** dipendenze. Nell'esempio precedente, se il pacchetto viene installato in un progetto destinato a Silverlight 3.0 o versione successiva, non verranno installate dipendenze. Se il pacchetto viene installata in un progetto destinato a .NET 4.0 o versioni successive, due dipendenze, jQuery e WebActivator, verranno installate.  Se il pacchetto viene installato in un progetto destinato a una versione precedente di tali 2 Framework, o qualsiasi altro framework, verrà installato RouteMagic 1.1.0. Non c'è Nessuna ereditarietà tra gruppi. Se corrisponde al framework di destinazione di un progetto di `targetFramework` attributo di un gruppo, solo le dipendenze all'interno di tale gruppo verrà installato.

Un pacchetto è possibile specificare le dipendenze del pacchetto in uno dei due formati: il formato precedente di un elenco semplice di `<dependency>` elementi o gruppi. Se il `<group>` formato viene usato, il pacchetto non può essere installato nelle versioni di NuGet precedenti alla 2.0.

Si noti che i due formati non è consentito combinare. Ad esempio, è il seguente frammento **valido** e vengono rifiutati da NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Raggruppamento di file di contenuto e gli script di PowerShell dal framework di destinazione

Oltre ai riferimenti di assembly, i file di contenuto e script di PowerShell anche possono essere raggruppati per framework di destinazione. La stessa struttura di cartelle trovato nel `lib` cartella per la specifica di framework di destinazione è ora possibile applicare nello stesso modo per il `content` e `tools` cartelle. Ad esempio:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Nota**: poiché `init.ps1` viene eseguita a livello di soluzione e permane non dipendente da qualsiasi singolo progetto, deve essere inserito direttamente sotto il `tools` cartella. Se posizionata all'interno di una cartella specifica del framework, verrà ignorato.

Inoltre, una nuova funzionalità di NuGet 2.0 è che può essere una cartella framework *vuoto*, nel qual caso, NuGet non aggiungere riferimenti ad assembly, aggiungere i file di contenuto o eseguire gli script di PowerShell per la versione del framework specifico. Nell'esempio precedente, la cartella `content\net40` è vuoto.

## <a name="improved-tab-completion-performance"></a>Prestazioni di completamento tab migliorato
La funzionalità di completamento della scheda nella Console di gestione pacchetti NuGet è stata aggiornata per migliorare significativamente le prestazioni. Ci sarà molto meno ritardo dal momento in cui che viene premuto il tasto tab fino a quando non viene visualizzato l'elenco a discesa di suggerimenti.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2.0 include varie correzioni di bug con particolare attenzione alle prestazioni e il consenso di ripristino del pacchetto.
Per un elenco completo di lavoro gli elementi corretti in NuGet 2.0, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
