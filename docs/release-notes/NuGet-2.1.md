---
title: Note sulla versione 2.1 di NuGet
description: Note sulla versione per NuGet 2.1 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548597"
---
# <a name="nuget-21-release-notes"></a>Note sulla versione 2.1 di NuGet

[Note sulla versione di NuGet 2.0](../release-notes/nuget-2.0.md) | [note sulla versione di NuGet 2.2](../release-notes/nuget-2.2.md)

NuGet 2.1 è stato rilasciato il 4 ottobre 2012.

## <a name="hierarchical-nugetconfig"></a>Hierarchical Nuget.Config

2.1 NuGet ti offre una maggiore flessibilità per controllare le impostazioni di NuGet tramite risalire la struttura di cartelle cercando in modo ricorsivo `NuGet.Config` file e quindi compilare la configurazione dall'insieme di tutti i file trovati.  Ad esempio, si consideri lo scenario in cui un team ha un repository di pacchetti interni per le compilazioni di integrazione continua di altre dipendenze interne. La struttura di cartelle per un singolo progetto potrebbe essere simile al seguente:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Inoltre, se il ripristino del pacchetto è abilitato per la soluzione, sarà disponibile anche la cartella seguente:

    C:\myteam\solution1\.nuget

Per avere repository di pacchetti interni del team disponibili per tutti i progetti che il team lavora a, non rendendole al tempo stesso disponibile per tutti i progetti nel computer, è possibile creare un nuovo file NuGet. config e posizionarlo nella cartella c:\myteam. Non è possibile specificare a una cartella di pacchetti per ogni progetto.

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

È ora possibile osservare che l'origine è stata aggiunta eseguendo il comando 'nuget.exe origini' da qualsiasi cartella sotto c:\myteam come illustrato di seguito:

![Origini dei pacchetti nel file di configurazione nuget padre](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` i file vengono cercati nell'ordine seguente:

1. `.nuget\Nuget.Config`
2. Ricorsivo illustrato dalla cartella del progetto radice
3. Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Le configurazioni sono applicate le *invertire l'ordine*, vale a dire che in base all'ordine riportato sopra, il file NuGet. config globale sarebbe essere applicato per primo, seguito dai file NuGet. config individuati dalla radice alla cartella del progetto, seguiti da `.nuget\Nuget.Config`.  Ciò è particolarmente importante se si usa il `<clear/>` elemento da cui rimuovere un set di elementi dalla configurazione.

## <a name="specify-packages-folder-location"></a>Specificare 'package' percorso della cartella

In passato, NuGet ha gestito i pacchetti della soluzione da una cartella nota 'package' trovata sotto la cartella radice della soluzione.  Per i team di sviluppo che dispongono di molte soluzioni diverse che hanno installati i pacchetti NuGet, ciò può comportare lo stesso pacchetto viene installato in posizioni diverse nel file system.

2.1 NuGet fornisce un controllo più granulare sulla posizione della cartella dei pacchetti tramite il `repositoryPath` elemento il `NuGet.Config` file.  Compila l'esempio precedente di supporto di NuGet. config gerarchico, presuppongono che si desidera avere tutti i progetti nella condivisione C:\myteam\ nella stessa cartella dei pacchetti.  A tale scopo, è sufficiente aggiungere la voce seguente alla `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

In questo esempio, condiviso `Nuget.Config` file consente di specificare una cartella di pacchetti condivisi per ogni progetto che viene creata di sotto di C:\myteam, indipendentemente dalla profondità. Si noti che se si dispone di una cartella di pacchetti esistente sotto la radice della soluzione, è necessario eliminarlo prima di NuGet verranno posizionati i pacchetti nel nuovo percorso.

## <a name="support-for-portable-libraries"></a>Supporto per le librerie portabili

[Le librerie portabili](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) è una funzionalità introdotta con la versione 4 di .NET che consente di compilare gli assembly che possono funzionare senza alcuna modifica su diverse piattaforme Microsoft, rispetto alle versioni di.NET Framework per Silverlight per Windows Phone e Xbox anche 360 (anche se in questo momento, NuGet non supporta la destinazione di libreria portabile Xbox).  Estendendo il [convenzioni del pacchetto](../create-packages/supporting-multiple-target-frameworks.md) per i profili e le versioni di framework 2.1 NuGet supporta ora le librerie portabili grazie alla possibilità di creare i pacchetti con framework composte e destinazione del profilo `lib` cartelle.

Ad esempio, prendere in considerazione piattaforme di destinazione disponibili della libreria di classi portabile seguenti.

![Finestra di dialogo Creazione della libreria portabile](./media/releasenotes-21-plib.png)

Dopo che la libreria viene compilata e il comando `nuget.exe pack MyPortableProject.csproj` viene eseguito, il formato portabile nuova struttura di cartelle pacchetto della libreria può essere visti da esaminando il contenuto del pacchetto NuGet generato.

![Layout del pacchetto della libreria portabile](./media/releasenotes-21-plib-layout.png)

Come può notare, la convenzione di denominazione cartella libreria portabile segue il modello "portabile-{framework 1} + {framework n}" in cui gli identificatori di framework seguono esistente [convenzioni di nome e la versione di framework](../reference/target-frameworks.md). Un'eccezione per le convenzioni di nome e la versione è stata trovata nell'identificatore del framework utilizzato per Windows Phone.  Il moniker deve usare il nome del framework 'wp' (wp7, wp71 o wp8). Usando 'silverlight-wp7', ad esempio, verrà generato un errore.

Quando si installa il pacchetto creato da questa struttura di cartelle, NuGet possono ora applicare le regole di framework e il profilo a più destinazioni, come specificato nel nome della cartella.  Dietro le regole di corrispondenza di NuGet è il principio che "più specifiche" destinazioni avrà la precedenza su quelle "meno specifici".  Ciò significa che i moniker come destinazione una piattaforma specifica sarà sempre preferiti su quelli portabile se sono entrambi compatibili con un progetto.  Inoltre, se più destinazioni portabili compatibili con un progetto, NuGet preferiranno quello in cui il set di piattaforme supportate è "più vicino" al progetto il pacchetto di riferimento.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Destinazione Windows 8 e Windows Phone 8 progetti

Oltre ad aggiungere il supporto per i progetti libreria portabile di destinazione, NuGet 2.1 offre nuovo moniker del framework per progetti Store di Windows 8 sia Windows Phone 8, nonché alcuni nuovo moniker generale per Windows Store e i progetti Windows Phone che saranno più facile da gestire con le versioni future delle rispettive piattaforme.

Per le applicazioni Windows 8 Store, gli identificatori simile alla seguente:

| NuGet 2.0 e versioni precedenti | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Win Windows, Windows8, win8 |

<br/>
Per i progetti Windows Phone, gli identificatori simile alla seguente:

| Sistema operativo di telefono | NuGet 2.0 e versioni precedenti | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 wp | Windows Phone, WindowsPhone7 wp7, WindowsPhone, |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (non supportato) | wp8, WindowsPhone8 |

<br/>
In tutte le modifiche precedenti, i nomi di framework precedenti continueranno a essere pienamente supportati da NuGet 2.1.  In futuro, i nuovi nomi devono essere utilizzati come verranno più stabili in tutte le versioni future delle rispettive piattaforme. I nuovi nomi verranno *non* essere supportato nelle versioni di NuGet precedenti alla 2.1, tuttavia, pertanto, pianificare di conseguenza cui si vuole passare.

## <a name="improved-search-in-package-manager-dialog"></a>Nella finestra di dialogo Gestione pacchetti di ricerca ottimizzata

Nel corso delle ultime diverse iterazioni, le modifiche sono state introdotte in NuGet gallery che migliorato notevolmente la velocità e la pertinenza delle ricerche di pacchetto.  Tuttavia, questi miglioramenti erano limitati al sito Web nuget.org.  2.1 NuGet rende la funzionalità di ricerca migliorata esperienza disponibile tramite la finestra di dialogo Gestione pacchetti NuGet.  Ad esempio, si supponga che si desidera trovare il pacchetto di anteprima di memorizzazione nella cache di Windows Azure.  Una query di ricerca ragionevole per questo pacchetto potrebbe essere "Cache di Azure".  Nelle versioni precedenti della finestra di dialogo Gestione pacchetti, il pacchetto desiderato non potrebbe anche essere elencato nella prima pagina di risultati.  Tuttavia, NuGet 2.1, il pacchetto desiderato a questo punto viene visualizzato nella parte superiore dei risultati della ricerca.

![Ricerca di finestra di dialogo Gestione pacchetti](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forzare l'aggiornamento del pacchetto

Prima 2.1 NuGet, NuGet potrebbe ignorare l'aggiornamento di un pacchetto quando si è verificato un non un numero di versione elevata.  Questa situazione ha introdotto attrito per determinati scenari, in particolare nel caso di compilazione o gli scenari di integrazione continua in cui il team non si desidera incrementare la versione del pacchetto numerica con ogni compilazione.  Per forzare un aggiornamento indipendentemente dal fatto che è stato il comportamento desiderato.  2.1 NuGet risolve questo problema con il flag 'reinstallare'.  Ad esempio, le versioni precedenti di NuGet comporta quanto segue quando si tenta di aggiornare un pacchetto che non disponevano di una versione più recente del pacchetto:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Con il flag di reinstallare l'applicazione, il pacchetto verrà aggiornato indipendentemente dal fatto che è disponibile una versione più recente.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Un altro scenario in cui il flag di reinstallare l'applicazione si riveli utile è quello del reindirizzamento del framework. Quando si modifica il framework di destinazione di un progetto (ad esempio, da .NET 4 in .NET 4.5), Update-Package-reinstallare può aggiornare i riferimenti agli assembly corretti per tutti i pacchetti NuGet installati nel progetto.

## <a name="edit-package-sources-within-visual-studio"></a>Modifica di origini dei pacchetti all'interno di Visual Studio

Nelle versioni precedenti di NuGet, aggiornamento di un'origine di pacchetto da entro la finestra di dialogo Opzioni di Visual Studio richiede l'eliminazione e aggiungere di nuovo l'origine del pacchetto.  2.1 NuGet migliora il flusso di lavoro mediante il supporto di aggiornamento come una funzione di prima classe di interfaccia utente di configurazione.

![Finestra di dialogo Configurazione di package manager](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correzioni di bug

NuGet 2.1 include varie correzioni di bug. Per un elenco completo di lavoro gli elementi corretti in NuGet 2.0, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
