---
title: Note sulla versione di NuGet 2,1
description: Note sulla versione per NuGet 2,1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777024"
---
# <a name="nuget-21-release-notes"></a>Note sulla versione di NuGet 2,1

Note sulla versione di [NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Note sulla versione di NuGet 2,2](../release-notes/nuget-2.2.md)

NuGet 2,1 è stato rilasciato il 4 ottobre 2012.

## <a name="hierarchical-nugetconfig"></a>Nuget.Config gerarchico

NuGet 2,1 offre una maggiore flessibilità nel controllo delle impostazioni di NuGet in modo ricorsivo la struttura di cartelle che cerca `NuGet.Config` i file e quindi compila la configurazione dal set di tutti i file trovati.  Si consideri ad esempio uno scenario in cui un team ha un repository di pacchetti interno per le compilazioni CI di altre dipendenze interne. La struttura di cartelle per un singolo progetto potrebbe essere simile alla seguente:

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

Inoltre, se il ripristino dei pacchetti è abilitato per la soluzione, sarà disponibile anche la cartella seguente:

```
C:\myteam\solution1\.nuget
```

Per fare in modo che il repository dei pacchetti interno del team sia disponibile per tutti i progetti su cui il team lavora, senza renderlo disponibile per ogni progetto nel computer, è possibile creare un nuovo file di Nuget.Config e inserirlo nella cartella c:\myteam. Non esiste alcun modo per la specifica di una cartella di pacchetti per ogni progetto.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

È ora possibile vedere che l'origine è stata aggiunta eseguendo il comando ' nuget.exe sources ' da qualsiasi cartella sotto c:\myteam, come illustrato di seguito:

![Origini pacchetti dalla configurazione di NuGet padre](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` i file vengono cercati nell'ordine seguente:

1. `.nuget\Nuget.Config`
2. Percorso ricorsivo dalla cartella del progetto alla radice
3. Globale `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

Le configurazioni vengono applicate in *ordine inverso*, vale a dire che in base all'ordinamento precedente, viene applicata prima l'Nuget.Config globale, seguita dalla Nuget.Config file individuati dalla radice alla cartella del progetto, seguiti da `.nuget\Nuget.Config` .  Questa operazione è particolarmente importante se si usa l' `<clear/>` elemento per rimuovere un set di elementi dalla configurazione.

## <a name="specify-packages-folder-location"></a>Specificare il percorso della cartella ' Packages '

In passato, NuGet ha gestito i pacchetti di una soluzione da una cartella "Packages" nota trovata sotto la cartella radice della soluzione.  Per i team di sviluppo con diverse soluzioni con pacchetti NuGet installati, questo può comportare l'installazione dello stesso pacchetto in molte posizioni diverse sul file system.

NuGet 2,1 fornisce un controllo più granulare sul percorso della cartella dei pacchetti tramite l' `repositoryPath` elemento nel `NuGet.Config` file.  Basandosi sull'esempio precedente di supporto gerarchico Nuget.Config, si supponga di voler fare in modo che tutti i progetti in C:\myteam\ condividano la stessa cartella pacchetti.  A tale scopo, aggiungere semplicemente la voce seguente a `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

In questo esempio, il `Nuget.Config` file condiviso specifica una cartella di pacchetti condivisi per ogni progetto creato al di sotto di C:\myteam, indipendentemente dalla profondità. Si noti che se si dispone di una cartella pacchetti esistente sotto la radice della soluzione, è necessario eliminarla prima che NuGet inserisca i pacchetti nella nuova posizione.

## <a name="support-for-portable-libraries"></a>Supporto per le librerie portabili

Le [librerie](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) portabili sono una funzionalità introdotta per la prima volta con .NET 4 che consente di compilare assembly che possono funzionare senza modifiche su diverse piattaforme Microsoft, da versioni di The.NET Framework a Silverlight a Windows Phone e persino a Xbox 360 (anche se al momento, NuGet non supporta la destinazione della libreria portabile Xbox).  Estendendo le [convenzioni dei pacchetti](../create-packages/supporting-multiple-target-frameworks.md) per le versioni e i profili del Framework, NuGet 2,1 supporta ora le librerie portabili consentendo di creare pacchetti con cartelle di destinazione del profilo e del Framework composto `lib` .

Si considerino, ad esempio, le piattaforme di destinazione disponibili della libreria di classi portabile seguenti.

![Finestra di dialogo Creazione libreria portabile](./media/releasenotes-21-plib.png)

Dopo che la libreria è stata compilata e il comando `nuget.exe pack MyPortableProject.csproj` è stato eseguito, è possibile visualizzare la nuova struttura di cartelle dei pacchetti della libreria portabile esaminando il contenuto del pacchetto NuGet generato.

![Layout del pacchetto della libreria portatile](./media/releasenotes-21-plib-layout.png)

Come si può notare, la convenzione relativa al nome della cartella della libreria portabile segue il modello ' Portable-{Framework 1} + {Framework n}', in cui gli identificatori del Framework seguono le [convenzioni di versione e il nome del Framework](../reference/target-frameworks.md)esistente. Un'eccezione alle convenzioni di nome e versione è disponibile nell'identificatore del Framework usato per Windows Phone.  Questo moniker deve usare il nome di Framework ' wp ' (WP7, wp71 o WP8). Se si usa ' Silverlight-WP7', ad esempio, verrà generato un errore.

Quando si installa il pacchetto creato da questa struttura di cartelle, NuGet è ora in grado di applicare le regole del Framework e del profilo a più destinazioni, come specificato nel nome della cartella.  Dietro le regole di corrispondenza di NuGet è il principio che gli obiettivi "più specifici" avranno la precedenza su quelli "meno specifici".  Ciò significa che i moniker destinati a una piattaforma specifica verranno sempre preferiti rispetto a quelli portabili se sono entrambi compatibili con un progetto.  Inoltre, se più destinazioni portabili sono compatibili con un progetto, NuGet preferisce quello in cui il set di piattaforme supportate è "più vicino" al progetto che fa riferimento al pacchetto.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Destinazione di progetti Windows 8 e Windows Phone 8

Oltre ad aggiungere il supporto per la destinazione dei progetti di libreria portabile, NuGet 2,1 fornisce nuovi moniker di Framework per i progetti Windows 8 Store e Windows Phone 8, oltre ad alcuni nuovi moniker generali per i progetti Windows Store e Windows Phone che saranno più facili da gestire nelle versioni future delle rispettive piattaforme.

Per le applicazioni Windows 8 Store, gli identificatori hanno un aspetto simile al seguente:

| NuGet 2,0 e versioni precedenti | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, . NETCore45 | Windows, Windows8, Win, Win8 |

<br/>
Per i progetti Windows Phone, gli identificatori hanno un aspetto simile al seguente:

| Sistema operativo telefono | NuGet 2,0 e versioni precedenti | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-WP | WP, WP7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7,5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (non supportato) | WP8, WindowsPhone8 |

<br/>
In tutte le modifiche precedenti, i nomi di Framework precedenti continueranno a essere completamente supportati da NuGet 2,1.  In futuro, è consigliabile usare i nuovi nomi perché saranno più stabili nelle versioni future delle rispettive piattaforme. I nuovi nomi *non* saranno supportati nelle versioni di NuGet precedenti alla 2,1, quindi pianificare di conseguenza il momento in cui eseguire l'opzione.

## <a name="improved-search-in-package-manager-dialog"></a>Miglioramento della ricerca nella finestra di dialogo Gestione pacchetti

Nel corso delle diverse iterazioni sono state introdotte modifiche alla raccolta NuGet che hanno migliorato notevolmente la velocità e la pertinenza delle ricerche di pacchetti.  Tuttavia, questi miglioramenti erano limitati al sito Web nuget.org.  NuGet 2,1 rende disponibile l'esperienza di ricerca migliorata tramite la finestra di dialogo Gestione pacchetti NuGet.  Si supponga, ad esempio, di voler trovare il pacchetto di anteprima di Caching di Windows Azure.  Una query di ricerca ragionevole per questo pacchetto può essere "cache di Azure".  Nelle versioni precedenti della finestra di dialogo Gestione pacchetti, il pacchetto desiderato non è incluso nella prima pagina di risultati.  Tuttavia, in NuGet 2,1, il pacchetto desiderato ora viene visualizzato nella parte superiore dei risultati della ricerca.

![Finestra di dialogo Gestione pacchetti-ricerca](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forza aggiornamento pacchetto

Prima di NuGet 2,1, NuGet ignorava l'aggiornamento di un pacchetto in assenza di un numero di versione elevato.  Questo ha introdotto un attrito per determinati scenari, in particolare nel caso di scenari di compilazione o CI in cui il team non ha voluto incrementare il numero di versione del pacchetto con ogni compilazione.  Il comportamento desiderato consisteva nel forzare un aggiornamento indipendentemente da.  NuGet 2,1 risolve questo problema con il flag ' reinstall '.  Ad esempio, le versioni precedenti di NuGet generano quanto segue quando si tenta di aggiornare un pacchetto che non dispone di una versione più recente del pacchetto:

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

Con il flag REINSTALL, il pacchetto verrà aggiornato indipendentemente dal fatto che sia presente una versione più recente.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

Un altro scenario in cui il flag di reinstallazione dimostra vantaggioso è quello della ridefinizione della destinazione del Framework. Quando si modifica il Framework di destinazione di un progetto, ad esempio da .NET 4 a .NET 4,5, Update-Package-REINSTALL può aggiornare i riferimenti agli assembly corretti per tutti i pacchetti NuGet installati nel progetto.

## <a name="edit-package-sources-within-visual-studio"></a>Modificare le origini del pacchetto in Visual Studio

Nelle versioni precedenti di NuGet, per aggiornare un'origine del pacchetto dalla finestra di dialogo Opzioni di Visual Studio, è necessario eliminare e aggiungere nuovamente l'origine del pacchetto.  NuGet 2,1 migliora questo flusso di lavoro supportando Update come una funzione di prima classe dell'interfaccia utente di configurazione.

![Finestra di dialogo di configurazione di gestione pacchetti](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correzioni di bug

NuGet 2,1 include numerose correzioni di bug. Per un elenco completo degli elementi di lavoro corretti in NuGet 2,0, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
