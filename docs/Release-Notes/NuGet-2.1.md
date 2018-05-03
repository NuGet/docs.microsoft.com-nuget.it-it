---
title: Note sulla versione 2.1 di NuGet
description: Note sulla versione per NuGet 2.1 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-21-release-notes"></a>Note sulla versione 2.1 di NuGet

[Note sulla versione di NuGet 2.0](../release-notes/nuget-2.0.md) | [note sulla versione 2.2 di NuGet](../release-notes/nuget-2.2.md)

È stata rilasciata NuGet 2.1 il 4 ottobre 2012.

## <a name="hierarchical-nugetconfig"></a>Hierarchical Nuget.Config

2.1 NuGet offre una maggiore flessibilità per controllare le impostazioni di NuGet tramite in modo ricorsivo risalire la struttura di cartelle per `NuGet.Config` file e quindi la compilazione della configurazione dal set di tutti i file trovati.  Ad esempio, si consideri lo scenario in cui un team dispone di un repository di pacchetti interno per le compilazioni di elemento di configurazione di altre dipendenze interne. La struttura di cartelle per un singolo progetto potrebbe essere simile al seguente:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Inoltre, se il ripristino del pacchetto è abilitato per la soluzione, sarà disponibile anche la cartella seguente:

    C:\myteam\solution1\.nuget

Per disporre del repository di pacchetti interno del team disponibile per tutti i progetti che viene eseguita dal team, mentre non renderlo disponibile per ogni progetto nel computer, è possibile creare un nuovo file NuGet. config e inserirlo nella cartella c:\myteam. Non è possibile specificare a una cartella di pacchetti per ogni progetto.

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

Possiamo vedere che l'origine è stato aggiunto tramite il comando 'nuget.exe origini' da qualsiasi cartella sotto c:\myteam come illustrato di seguito:

![Origine del pacchetto dalla configurazione nuget padre](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` i file vengono cercati nell'ordine seguente:

1. `.nuget\Nuget.Config`
2. Ricorsivo percorso dalla cartella di progetto radice
3. Globale `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Le configurazioni sono rispetto all'interno di *invertire l'ordine*, il che significa che in base all'ordinamento precedente, di NuGet. config globale potrebbe essere applicato per primo, seguito dai file NuGet. config individuati dalla radice alla cartella di progetto, seguiti da `.nuget\Nuget.Config`.  Ciò è particolarmente importante se si usa il `<clear/>` elemento per rimuovere un set di elementi di configurazione.

## <a name="specify-packages-folder-location"></a>Specificare 'packages' percorso della cartella

In passato, NuGet ha gestito pacchetti della soluzione da una cartella nota 'packages' trovata sotto la cartella radice della soluzione.  Per i team di sviluppo che dispongono di molte soluzioni diversi che dispongono di pacchetti NuGet installati, ciò può comportare nello stesso pacchetto siano installato in posizioni diverse nel file system.

2.1 NuGet fornisce il percorso della cartella di pacchetti tramite un controllo più granulare di `repositoryPath` elemento il `NuGet.Config` file.  Compilazione dell'esempio precedente del supporto di NuGet. config gerarchico, si presuppone che si desidera che tutti i progetti nella condivisione C:\myteam\ nella stessa cartella di pacchetti.  A tale scopo, aggiungere semplicemente la voce seguente alla `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

In questo esempio, condiviso `Nuget.Config` file specifica una cartella condivisa di pacchetti per ogni progetto che viene creata di sotto di C:\myteam, indipendentemente dalla profondità. Si noti che se si dispone di una cartella di pacchetti esistente di sotto della radice della soluzione, è necessario eliminarlo prima di NuGet verranno posizionati i pacchetti nel nuovo percorso.

## <a name="support-for-portable-libraries"></a>Supporto per le librerie portabili

[Le librerie portabili](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) è una funzionalità introdotta con .NET 4 che consente di compilare gli assembly che possono funzionare senza alcuna modifica su diverse piattaforme Microsoft, dalle versioni di.NET Framework per Silverlight per Windows Phone e Xbox anche 360 (anche se a questo punto, NuGet non supporta la destinazione della libreria portabile Xbox).  Estendendo il [pacchetto convenzioni](../create-packages/supporting-multiple-target-frameworks.md) per i profili e le versioni di framework 2.1 NuGet supporta ora le librerie portabili grazie alla possibilità di creare pacchetti che composta framework sono la destinazione di profilo `lib` cartelle.

Ad esempio, prendere in considerazione piattaforme di destinazione disponibili della libreria di classi portabile seguenti.

![Finestra di dialogo Creazione libreria portabile](./media/releasenotes-21-plib.png)

Dopo aver compilato la libreria e il comando `nuget.exe pack MyPortableProject.csproj` viene eseguito, il formato portabile nuova struttura di cartelle pacchetto libreria può essere visualizzato esaminando il contenuto del pacchetto NuGet generato.

![Layout del pacchetto libreria portabile](./media/releasenotes-21-plib-layout.png)

Come si può notare, la convenzione di denominazione cartella libreria portabile segue il modello 'portabile {framework 1} + {framework n}' in cui gli identificatori di framework seguono esistente [convenzioni di nome e la versione di framework](../reference/target-frameworks.md). Un'eccezione per le convenzioni di nome e la versione è stata trovata nell'identificatore di framework utilizzato per Windows Phone.  Il moniker è necessario utilizzare il nome di framework 'wp' (wp7, wp71 o wp8). Utilizzando 'wp7 silverlight', ad esempio, comporterà un errore.

Quando si installa il pacchetto creato da questa struttura di cartelle, NuGet può applicare le regole di profilo e framework a più destinazioni, come specificato nel nome della cartella.  Dietro le regole di corrispondenza di NuGet è il principio che destinazioni "più specifiche" avrà la precedenza su quelle "meno specifiche".  Ciò significa che moniker come destinazione una piattaforma specifica sarà sempre preferito rispetto alla portabile se sono entrambi compatibili con un progetto.  Inoltre, se più destinazioni portabile sono compatibili con un progetto, NuGet preferiranno quello in cui il set di piattaforme supportate è "più vicino" al progetto che fa riferimento il pacchetto.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Destinazione Windows 8 e Windows Phone 8 progetti

Oltre ad aggiungere il supporto per la definizione dei progetti libreria portabile, 2.1 NuGet fornisce nuovi moniker del framework per progetti Windows 8 Store e Windows Phone 8, nonché alcune nuove moniker generale per Windows Store e i progetti Windows Phone che saranno semplifica la gestione con le versioni future delle rispettive piattaforme.

Per le applicazioni di Windows 8 Store, gli identificatori apparire come segue:

| NuGet 2.0 e versioni precedenti | 2.1 NuGet |
| ---------------- | ----------- |
| winRT45, .NETCore45 | Win di Windows, Windows 8, win8 |

<br/>
Per i progetti Windows Phone, gli identificatori apparire come segue:

| Sistema operativo telefono | NuGet 2.0 e versioni precedenti | 2.1 NuGet |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 wp | WP, WindowsPhone7 wp7, WindowsPhone, |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (non supportato) | wp8, WindowsPhone8 |

<br/>
In tutte le modifiche precedenti, i nomi di framework precedenti continueranno a essere pienamente supportate da NuGet 2.1.  Lo spostamento in avanti, i nuovi nomi devono essere utilizzati poiché saranno più stabile con le versioni future delle rispettive piattaforme. I nuovi nomi verranno *non* essere supportato nelle versioni precedenti di NuGet 2.1, tuttavia, pertanto, pianificare di conseguenza quando l'opzione.

## <a name="improved-search-in-package-manager-dialog"></a>Una funzionalità di ricerca nella finestra di dialogo Gestione pacchetti

Su precedenti diverse iterazioni, le modifiche sono state introdotte per la raccolta NuGet che migliorato notevolmente la velocità e la pertinenza di ricerche di pacchetto.  Tuttavia, questi miglioramenti sono limitati al sito Web nuget.org.  2.1 NuGet rende la ricerca migliorata esperienza disponibili tramite la finestra di dialogo Gestione pacchetti NuGet.  Ad esempio, si supponga che si desidera trovare il pacchetto di anteprima di memorizzazione nella cache di Windows Azure.  Una query di ricerca ragionevole per questo pacchetto potrebbe essere "Cache di Azure".  Nelle versioni precedenti della finestra di dialogo Gestione pacchetti, il pacchetto desiderato sarà non ancora elencato nella prima pagina di risultati.  Tuttavia, in NuGet 2.1, il pacchetto desiderato sia ora visualizzato nella parte superiore dei risultati di ricerca.

![Ricerca di finestra di dialogo Gestione pacchetti](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Forzare l'aggiornamento del pacchetto

Prima di NuGet 2.1, NuGet sarebbe ignorare l'aggiornamento di un pacchetto quando si è non verificato un numero elevato di versione.  Questa situazione ha introdotto le forze di attrito per determinati scenari, in particolare nel caso di compilazione o CI scenari in cui il team non desidera incrementare la versione del pacchetto numerica con ogni compilazione.  Per forzare un aggiornamento indipendentemente dal fatto che è stato il comportamento desiderato.  2.1 NuGet risolvere questo problema con il flag 'reinstallare'.  Ad esempio, le versioni precedenti di NuGet comporta quanto segue durante il tentativo di aggiornare un pacchetto che non dispone di una versione più recente del pacchetto:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Con il flag, reinstallare il pacchetto verrà aggiornato indipendentemente dal fatto che è disponibile una versione più recente.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Un altro scenario in cui il flag Reinstalla si riveli utile è quello di destinazione nuovo framework. Quando si modifica il framework di destinazione di un progetto (ad esempio, da .NET 4 in .NET 4.5), pacchetto di aggiornamento-reinstallare può aggiornare i riferimenti agli assembly corretti per tutti i pacchetti NuGet installati nel progetto.

## <a name="edit-package-sources-within-visual-studio"></a>Modifica dell'origine del pacchetto all'interno di Visual Studio

Nelle versioni precedenti di NuGet, l'aggiornamento da un'origine del pacchetto nella finestra di dialogo Opzioni Visual Studio necessario l'eliminazione e aggiungere nuovamente l'origine del pacchetto.  2.1 NuGet migliora il flusso di lavoro mediante il supporto di aggiornamento come una funzione di prima classe di interfaccia utente di configurazione.

![Finestra di dialogo Configurazione di package manager](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Correzioni di bug

NuGet 2.1 include varie correzioni di bug. Per un elenco completo di lavoro gli elementi corretti in NuGet 2.0, visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
