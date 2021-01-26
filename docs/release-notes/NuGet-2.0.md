---
title: Note sulla versione di NuGet 2,0
description: Note sulla versione per NuGet 2,0, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776987"
---
# <a name="nuget-20-release-notes"></a>Note sulla versione di NuGet 2,0

Note sulla versione di [NuGet 1,8](../release-notes/nuget-1.8.md)  |  [Note sulla versione di NuGet 2,1](../release-notes/nuget-2.1.md)

NuGet 2,0 è stato rilasciato il 19 giugno 2012.

## <a name="known-installation-issue"></a>Problema di installazione noto
Se si esegue VS 2010 SP1, potrebbe essere rilevato un errore di installazione quando si tenta di aggiornare NuGet se è installata una versione precedente.

La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Vedere <https://support.microsoft.com/kb/2581019> per altre informazioni oppure [passare direttamente all'hotfix di Visual](http://bit.ly/vsixcertfix)Studio.

Nota: se Visual Studio non consente di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), probabilmente è necessario riavviare Visual Studio usando "Esegui come amministratore".

## <a name="package-restore-consent-is-now-active"></a>Il consenso per il ripristino del pacchetto è ora attivo

Come descritto in questo [post relativo al consenso per il ripristino dei pacchetti](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2,0 richiederà il consenso per consentire il ripristino del pacchetto in modo che possa andare online e scaricare i pacchetti. Assicurarsi che sia stato fornito il consenso tramite la finestra di dialogo di configurazione di gestione pacchetti o la variabile di ambiente EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Raggruppare le dipendenze per Framework di destinazione

A partire dalla versione 2,0, le dipendenze dei pacchetti possono variare in base al profilo del Framework del progetto di destinazione. Questa operazione viene eseguita utilizzando uno `.nuspec` schema aggiornato. L' `<dependencies>` elemento può ora contenere un set di `<group>` elementi. Ogni gruppo contiene zero o più `<dependency>` elementi e un `targetFramework` attributo. Tutte le dipendenze all'interno di un gruppo vengono installate insieme se il Framework di destinazione è compatibile con il profilo del Framework del progetto di destinazione. Ad esempio:

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

Si noti che un gruppo può contenere **zero** dipendenze. Nell'esempio precedente, se il pacchetto viene installato in un progetto destinato a Silverlight 3,0 o versione successiva, non verrà installata alcuna dipendenza. Se il pacchetto viene installato in un progetto destinato a .NET 4,0 o versione successiva, verranno installati due dipendenze, jQuery e WebActivator.  Se il pacchetto viene installato in un progetto destinato a una versione iniziale di questi due Framework, o qualsiasi altro Framework, verrà installato RouteMagic 1.1.0. Non esiste alcuna ereditarietà tra i gruppi. Se il Framework di destinazione di un progetto corrisponde all' `targetFramework` attributo di un gruppo, verranno installate solo le dipendenze all'interno di tale gruppo.

Un pacchetto può specificare le dipendenze del pacchetto in uno dei due formati seguenti: il formato precedente di un elenco semplice di `<dependency>` elementi o gruppi. Se `<group>` viene usato il formato, il pacchetto non può essere installato in versioni di NuGet precedenti alla 2,0.

Si noti che non è consentito combinare i due formati. Ad esempio, il frammento di codice seguente **non è valido** e verrà rifiutato da NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Raggruppamento di file di contenuto e script di PowerShell in base a Framework di destinazione

Oltre ai riferimenti agli assembly, i file di contenuto e gli script di PowerShell possono essere raggruppati in base al Framework di destinazione. La stessa struttura di cartelle trovata nella `lib` cartella per specificare il Framework di destinazione ora può essere applicata in modo analogo `content` alle `tools` cartelle e. Ad esempio:

```
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
```

**Nota**: poiché `init.ps1` viene eseguito a livello di soluzione e non dipende da un singolo progetto, deve essere inserito direttamente nella `tools` cartella. Se inserito in una cartella specifica del Framework, verrà ignorato.

Inoltre, una nuova funzionalità di NuGet 2,0 è che una cartella del Framework può essere *vuota*. in questo caso, NuGet non aggiunge i riferimenti ad assembly, aggiunge i file di contenuto o esegue script di PowerShell per la versione specifica del Framework. Nell'esempio precedente la cartella `content\net40` è vuota.

## <a name="improved-tab-completion-performance"></a>Miglioramento delle prestazioni di completamento tramite TAB
La funzionalità di completamento tramite TAB nella console di gestione pacchetti NuGet è stata aggiornata per migliorare significativamente le prestazioni. Si verifica un ritardo molto inferiore dal momento in cui viene premuto il tasto TAB fino a quando non viene visualizzato l'elenco a discesa dei suggerimenti.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 2,0 include molte correzioni di bug con particolare attenzione al consenso e alle prestazioni per il ripristino dei pacchetti.
Per un elenco completo degli elementi di lavoro corretti in NuGet 2,0, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
