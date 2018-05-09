---
title: Note sulla versione 2.0 di NuGet
description: Note sulla versione per NuGet 2.0, inclusi i problemi noti, correzioni di bug, le funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-20-release-notes"></a>Note sulla versione 2.0 di NuGet

[Note sulla versione di NuGet 1.8](../release-notes/nuget-1.8.md) | [note sulla versione di NuGet 2.1](../release-notes/nuget-2.1.md)

NuGet 2.0 è stata rilasciata il 19 giugno 2012.

## <a name="known-installation-issue"></a>Problema di installazione noti
Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Vedere [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) per altre informazioni, o [andare direttamente all'hotfix di Visual Studio](http://bit.ly/vsixcertfix).

Nota: Se Visual Studio non consente di disinstallare l'estensione (il pulsante di disinstallazione è disabilitato), quindi probabile che sia necessario riavviare Visual Studio utilizzando "Esegui come amministratore".

## <a name="package-restore-consent-is-now-active"></a>Consenso di ripristino del pacchetto è ora attivo

Come descritto in questo [post nel pacchetto ripristino consenso](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 verrà ora richiesto il consenso per abilitare ripristino del pacchetto passare alla modalità online e scaricare i pacchetti. Verificare di aver fornito il consenso tramite la finestra di dialogo pacchetto configuration manager o la variabile di ambiente EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Gruppo di dipendenze da Framework di destinazione

A partire dalla versione 2.0, pacchetto dipendenze possono variare in base al profilo del framework del progetto di destinazione. Questa operazione viene eseguita utilizzando una versione aggiornata `.nuspec` dello schema. Il `<dependencies>` elemento ora può contenere un set di `<group>` elementi. Ogni gruppo che contiene zero o più `<dependency>` elementi e un `targetFramework` attributo. Se il framework di destinazione è compatibile con il profilo del framework di destinazione progetto, vengono installate insieme tutte le dipendenze all'interno di un gruppo. Ad esempio:

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

Si noti che un gruppo può contenere **zero** dipendenze. Nell'esempio precedente, se il pacchetto è installato in un progetto destinato a Silverlight 3.0 o versione successiva, non verrà installata alcuna dipendenza. Se il pacchetto è installato in un progetto destinato a .NET 4.0 o versioni successive, è possibile che due dipendenze, jQuery e WebActivator, verranno installate.  Se il pacchetto viene installato in un progetto destinato a una versione precedente di questi 2 Framework, o qualsiasi altro framework, RouteMagic 1.1.0 verrà installato. C'è ereditarietà tra i gruppi. Se corrisponde al framework di destinazione di un progetto di `targetFramework` verrà installato l'attributo di un gruppo, solo le dipendenze all'interno di tale gruppo.

Un pacchetto è possibile specificare le dipendenze dei pacchetti in uno dei due formati: il formato precedente di un elenco semplice di `<dependency>` elementi o gruppi. Se il `<group>` viene usato il formato, il pacchetto non può essere installato in versioni precedenti alla 2.0 di NuGet.

Si noti che i due formati non è consentito combinare. Ad esempio, il frammento di codice seguente è **valido** e vengono rifiutati da NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Raggruppamento di file di contenuto e gli script di PowerShell per il framework di destinazione

Oltre ai riferimenti agli assembly, i file di contenuto e gli script di PowerShell inoltre possono essere raggruppati per framework di destinazione. La stessa struttura di cartelle, vedere il `lib` cartella per la specifica di .NET framework di destinazione può essere applicato a questo punto nello stesso modo per il `content` e `tools` cartelle. Ad esempio:

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

**Nota**: poiché `init.ps1` viene eseguita a livello di soluzione senza che sia non dipendente da un singolo progetto, deve essere inserito direttamente sotto il `tools` cartella. Se inserito in una cartella specifica del framework, verrà ignorato.

Inoltre, una nuova funzionalità di NuGet 2.0 è che può essere una cartella per framework *vuoto*, nel qual caso NuGet verrà non aggiungere riferimenti ad assembly, aggiungere i file di contenuto o eseguire gli script di PowerShell per la versione di framework specifici. Nell'esempio precedente, la cartella `content\net40` è vuoto.

## <a name="improved-tab-completion-performance"></a>Prestazioni di completamento tab migliorato
Questa funzionalità nella Console di gestione pacchetti NuGet è stata aggiornata per migliorare significativamente le prestazioni. Esistere molto meno tempo dal momento in cui che viene premuto il tasto tab fino a quando non viene visualizzato l'elenco a discesa di suggerimenti.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2.0 include varie correzioni di bug con particolare attenzione alle prestazioni e di consenso di ripristino del pacchetto.
Per un elenco completo di lavoro gli elementi corretti in NuGet 2.0, visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
