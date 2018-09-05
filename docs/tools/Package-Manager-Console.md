---
title: Guida alla Console di gestione pacchetti NuGet
description: Istruzioni per l'utilizzo della Console di gestione pacchetti NuGet in Visual Studio per l'uso di pacchetti.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546878"
---
# <a name="package-manager-console"></a>Console di Gestione pacchetti

La Console di gestione pacchetti NuGet è incorporata in Visual Studio in Windows 2012 e versioni successive. (Non è incluso in Visual Studio per Mac o Visual Studio Code.)

La console consente di usare [comandi di PowerShell di NuGet](../tools/powershell-reference.md) per trovare, installare, disinstallare e aggiornare i pacchetti NuGet. Utilizzo della console è necessario nei casi in cui il Package Manager UI non fornisce un modo per eseguire un'operazione. Per utilizzare `nuget.exe` comandi nella console, vedere [tramite la CLI nuget.exe nella console di](#using-the-nugetexe-cli-in-the-console).

Ad esempio, ricerca e installazione di un pacchetto avviene in tre semplici passaggi:

1. Aprire il progetto/soluzione in Visual Studio e aprire la console usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando.

1. Trovare il pacchetto da installare. Se si conosce già questo, andare al passaggio 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Eseguire il comando di installazione:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> Tutte le operazioni disponibili nella console possono essere eseguite anche con il [NuGet CLI](../tools/nuget-exe-cli-reference.md). Tuttavia, i comandi della console operano all'interno del contesto di Visual Studio e una progetto/soluzione salvata e spesso a una maggiore rispetto i comandi equivalenti di CLI. Ad esempio, installazione di un pacchetto tramite la console aggiunge un riferimento al progetto mentre la riga di comando non le supporta. Per questo motivo, gli sviluppatori che lavorano in genere in Visual Studio preferiscono usare la console per l'interfaccia della riga di comando.

> [!Tip]
> Molte operazioni di console dipendono da una soluzione aperta in Visual Studio con un nome di percorso noto. Se si dispone di una soluzione non sono stata salvata o alcuna soluzione, è possibile visualizzare l'errore, "soluzione non è aperto o non salvate. Assicurarsi di che avere una soluzione aperta e viene salvata." Ciò indica che la console non è possibile determinare la cartella della soluzione. Salvataggio di una soluzione non sono stata salvata, o creando e salvando una soluzione se non è aperto, deve correggere l'errore.

## <a name="opening-the-console-and-console-controls"></a>Aprire la console e i controlli di console

1. Aprire la console in Visual Studio usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando. La console è una finestra di Visual Studio che può essere disposti e posizionata, tuttavia si desidera che (vedere [personalizzare i layout delle finestre in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Per impostazione predefinita, i comandi della console funzionano su un'origine di pacchetto specifico e un progetto come impostato nel controllo nella parte superiore della finestra:

    ![Controlli di Console di gestione pacchetti per l'origine del pacchetto e progetto](media/PackageManagerConsoleControls1.png)

1. Selezione un'origine dei pacchetti diversi e/o progetto comporta la modifica i valori predefiniti per i comandi successivi. La maggior parte dei comandi per esegue l'override queste impostazioni senza dover modificare le impostazioni predefinite, supportano `-Source` e `-ProjectName` opzioni.

1. Per la gestione di origini dei pacchetti, selezionare l'icona a forma di ingranaggio. Si tratta di un collegamento per il **strumenti > Opzioni > Gestione pacchetti NuGet > origini pacchetti** come descritto nella finestra di dialogo il [Package Manager UI](package-manager-ui.md#package-sources) pagina. Inoltre, il controllo a destra del selettore di progetto Cancella il contenuto della console:

    ![Controlli non crittografati e le impostazioni della Console di gestione pacchetti](media/PackageManagerConsoleControls2.png)

1. Il pulsante all'estrema destra consente di interrompere un comando a esecuzione prolungata. Ad esempio, l'esecuzione `Get-Package -ListAvailable -PageSize 500` Elenca i primi 500 pacchetti sull'origine predefinita (ad esempio, nuget.org), che potrebbe richiedere alcuni minuti per l'esecuzione.

    ![Controllo stop Console di gestione pacchetti](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Installazione di un pacchetto

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Visualizzare [Install-Package](../tools/ps-ref-install-package.md).

Installazione di un pacchetto nella console esegue gli stessi passaggi come descritto nella [cosa accade quando viene installato un pacchetto](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), con le aggiunte seguenti:

- La Console Visualizza condizioni di licenza applicabili nella relativa finestra con un contratto implicito. Se si accettano le condizioni, è necessario disinstallare il pacchetto immediatamente.
- Anche un riferimento al pacchetto viene aggiunto al file di progetto e viene visualizzato nella **Esplora soluzioni** sotto il **riferimenti** nodo, è necessario salvare il progetto per visualizzare le modifiche nel file di progetto direttamente.

## <a name="uninstalling-a-package"></a>Disinstallazione di un pacchetto

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Visualizzare [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Uso [Get-Package](../tools/ps-ref-get-package.md) per visualizzare tutti i pacchetti attualmente installati nel progetto predefinito se è necessario trovare un identificatore.

Disinstallazione di un pacchetto esegue le azioni seguenti:

- Rimuove i riferimenti al pacchetto dal progetto (e qualsiasi formato di gestione è in uso). I riferimenti non siano più presenti **Esplora soluzioni**. (Potrebbe essere necessario ricompilare il progetto per visualizzarne il rimosso dal **Bin** cartella.)
- Le eventuali modifiche apportate al `app.config` o `web.config` quando è stato installato il pacchetto.
- Dipendenze rimuove installata in precedenza, se non ci sono pacchetti rimanenti usano tali dipendenze.

## <a name="updating-a-package"></a>Aggiorna un pacchetto

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

Visualizzare [Get-Package](../tools/ps-ref-get-package.md) e [Update-Package](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>Ricerca di un pacchetto

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

Visualizzare [Find-Package](../tools/ps-ref-find-package.md). In Visual Studio 2013 e versioni precedenti, usare [Get-Package](../tools/ps-ref-get-package.md) invece.

## <a name="availability-of-the-console"></a>Disponibilità della console

In Visual Studio 2017, NuGet e la gestione pacchetti NuGet vengono installati automaticamente quando si seleziona uno. Carichi di lavoro correlati NET; è possibile anche installare singolarmente controllando il **singoli componenti > strumenti per il codice > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio 2017.

Inoltre, se sono necessari i pacchetti NuGet in Visual Studio 2015 e versioni precedenti, controllare **strumenti > estensioni e aggiornamenti...**  e cercare l'estensione Gestione pacchetti NuGet. Se non si riesce a usare il programma di installazione di estensioni in Visual Studio, è possibile scaricare l'estensione direttamente dal [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).

La Console di gestione pacchetti non è attualmente disponibile in Visual Studio per Mac. I comandi equivalenti, tuttavia, sono disponibili tramite il [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio per Mac ha un'interfaccia utente per la gestione pacchetti NuGet. Visualizzare [tra cui un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).

Console di gestione pacchetti non è inclusa in Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Estendere la Console di gestione pacchetti

Alcuni pacchetti installati nuovi comandi per la console. Ad esempio, `MvcScaffolding` consente di creare comandi, ad esempio `Scaffold` illustrato di seguito, che genera le visualizzazioni e controller ASP.NET MVC:

![Installazione e l'utilizzo MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Configurazione di un profilo di PowerShell di NuGet

Un profilo di PowerShell consente di rendere disponibili i comandi di uso comune, ogni volta che si usa PowerShell. NuGet supporta un profilo specifico di NuGet in genere disponibile nel percorso seguente:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Per trovare il profilo, digitare `$profile` nella console:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Per altri dettagli, consultare [profili di Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).

## <a name="using-the-nugetexe-cli-in-the-console"></a>Tramite la CLI nuget.exe nella console di

Per rendere il [ `nuget.exe` CLI](nuget-exe-cli-reference.md) disponibile nella Console di gestione pacchetti, installare il [NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pacchetto dalla console:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
