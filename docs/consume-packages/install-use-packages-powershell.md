---
title: Installare e gestire i pacchetti NuGet usando la console in Visual Studio
description: Istruzioni per l'uso della console di Gestione pacchetti NuGet in Visual Studio per utilizzare i pacchetti.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 8b23b6cc22eff5413e317fbe619edd3d4f4716ee
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237400"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>Installare e gestire i pacchetti con la console di Gestione pacchetti in Visual Studio (PowerShell)

La console di Gestione pacchetti NuGet consente di usare i [comandi di PowerShell di NuGet](../reference/powershell-reference.md) per trovare, installare, disinstallare e aggiornare i pacchetti NuGet. L'uso della console è necessario nei casi in cui l'interfaccia utente di Gestione pacchetti non offre un modo per eseguire un'operazione. Per usare i comandi dell'interfaccia della riga di comando di `nuget.exe` nella console, vedere [Uso dell'interfaccia della riga di comando di nuget.exe nella console](#use-the-nugetexe-cli-in-the-console).

La console è inclusa in Visual Studio in Windows. Non è disponibile in Visual Studio per Mac o Visual Studio Code.

## <a name="find-and-install-a-package"></a>Trovare e installare un pacchetto

La ricerca e l'installazione di un pacchetto, ad esempio, vengono eseguite con tre semplici passaggi:

1. Aprire il progetto o la soluzione in Visual Studio e aprire la console usando il comando **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**.

1. Trovare il pacchetto che si vuole installare. Se lo si conosce già, andare al passaggio 3.

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
> Tutte le operazioni disponibili nella console possono essere eseguite anche con l'[interfaccia della riga di comando di NuGet](../reference/nuget-exe-cli-reference.md). Tuttavia, i comandi della console operano all'interno del contesto di Visual Studio e di un progetto o una soluzione salvati e spesso consentono di ottenere maggiori risultati rispetto ai comandi dell'interfaccia della riga di comando equivalenti. Ad esempio, l'installazione di un pacchetto tramite la console aggiunge un riferimento al progetto, diversamente dal comando dell'interfaccia della riga di comando. Per questo motivo, gli sviluppatori che lavorano in Visual Studio in genere preferiscono usare la console rispetto all'interfaccia della riga di comando.

> [!Tip]
> Molte operazioni della console dipendono dalla presenza di una soluzione aperta in Visual Studio con un nome di percorso noto. Se è aperta una soluzione non salvata o non è disponibile alcuna soluzione, è possibile che venga visualizzato l'errore "Soluzione non aperta o non salvata. Assicurarsi di disporre di una soluzione aperta e salvata." Ciò indica che la console non è in grado di determinare la cartella della soluzione. Il salvataggio di una soluzione non salvata o la creazione e il salvataggio di una soluzione, se non ce n'è una aperta, dovrebbero risolvere il problema.

## <a name="opening-the-console-and-console-controls"></a>Apertura della console e dei controlli della console

1. Aprire la console in Visual Studio usando il comando **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**. La console è una finestra di Visual Studio che può essere disposta e posizionata nel modo preferito (vedere [Personalizzare il layout delle finestre in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Per impostazione predefinita, i comandi della console agiscono su un'origine e un progetto di pacchetto specifici impostati nel controllo nella parte superiore della finestra:

    ![Controlli della console di Gestione pacchetti per l'origine e il progetto del pacchetto](media/PackageManagerConsoleControls1.png)

1. Se si seleziona un'origine e/o un progetto diverso per il pacchetto, verranno modificate le impostazioni predefinite per i comandi successivi. Per sostituire queste impostazioni senza modificare le impostazioni predefinite, la maggior parte dei comandi supporta le opzioni `-Source` e `-ProjectName`.

1. Per gestire le origini dei pacchetti, selezionare l'icona a forma di ingranaggio. Si tratta di un collegamento alla finestra di dialogo **Strumenti > Opzioni > Gestione pacchetti NuGet > Origini pacchetti** , come descritto nella pagina [Interfaccia utente di Gestione pacchetti](install-use-packages-visual-studio.md#package-sources). Inoltre, il controllo a destra del selettore del progetto cancella il contenuto della console:

    ![Impostazioni della console di Gestione pacchetti e controlli per cancellare](media/PackageManagerConsoleControls2.png)

1. Il pulsante più a destra interrompe un comando con esecuzione prolungata. Ad esempio, l'esecuzione di `Get-Package -ListAvailable -PageSize 500` elenca i primi 500 pacchetti nell'origine predefinita, ad esempio nuget.org, un'operazione che potrebbe richiedere vari minuti per l'esecuzione.

    ![Controllo di interruzione nella console di Gestione pacchetti](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a>Installare un pacchetto

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Vedere [Install-Package](../reference/ps-reference/ps-ref-install-package.md).

L'installazione di un pacchetto nella console esegue gli stessi passaggi descritti in [Cosa accade quando viene installato un pacchetto](../concepts/package-installation-process.md), con le aggiunte seguenti:

- Nella console vengono visualizzate le condizioni di licenza applicabili nella finestra con contratto implicito. Se non si accettano le condizioni, è necessario disinstallare il pacchetto immediatamente.
- Viene inoltre aggiunto un riferimento al pacchetto al file di progetto, visualizzato in **Esplora soluzioni** nel nodo **Riferimenti**. È necessario salvare il progetto per visualizzare direttamente le modifiche nel file di progetto.

## <a name="uninstall-a-package"></a>Disinstalla un pacchetto

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Vedere [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md). Usare [Get-Package](../reference/ps-reference/ps-ref-get-package.md) per visualizzare tutti i pacchetti attualmente installati nel progetto predefinito, se è necessario trovare un identificatore.

Con la disinstallazione di un pacchetto vengono eseguite le azioni seguenti:

- Rimozione dei riferimenti al pacchetto dal progetto (qualsiasi sia il formato di gestione in uso). I riferimenti non vengono più visualizzati in **Esplora soluzioni**. Potrebbe essere necessario ricompilare il progetto per verificarne la rimozione dalla cartella **Bin**.
- Ripristino delle eventuali modifiche apportate a `app.config` o `web.config` al momento dell'installazione del pacchetto.
- Rimozione delle dipendenze installate in precedenza se nessun pacchetto rimanente usa tali dipendenze.

## <a name="update-a-package"></a>Aggiornare un pacchetto

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

Vedere [Get-Package](../reference/ps-reference/ps-ref-get-package.md) e [Update-Package](../reference/ps-reference/ps-ref-update-package.md)

## <a name="find-a-package"></a>Trovare un pacchetto

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

Vedere [Find-Package](../reference/ps-reference/ps-ref-find-package.md). In Visual Studio 2013 e versioni precedenti usare invece [Get-Package](../reference/ps-reference/ps-ref-get-package.md).

## <a name="availability-of-the-console"></a>Disponibilità della console

A partire da Visual Studio 2017, NuGet e Gestione pacchetti NuGet vengono installati automaticamente quando si seleziona uno dei carichi di lavoro correlati a NET. È anche possibile installarlo singolarmente selezionando **Singoli componenti >Strumenti per il codice > Gestione pacchetti NuGet** nel programma di installazione di Visual Studio.

Inoltre, se non si trova Gestione pacchetti NuGet in Visual Studio 2015 e versioni precedenti, selezionare **Strumenti > Estensioni e aggiornamenti** e cercare l'estensione Gestione pacchetti NuGet. Se non si è in grado di usare il programma di installazione delle estensioni in Visual Studio, è possibile scaricare l'estensione direttamente da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .

La console di Gestione pacchetti non è attualmente disponibile con Visual Studio per Mac. I comandi equivalenti, tuttavia, sono disponibili tramite l'[interfaccia della riga di comando di NuGet](../reference/nuget-exe-CLI-reference.md). Visual Studio per Mac include un'interfaccia utente per la gestione dei pacchetti NuGet. Vedere [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).

La console di Gestione pacchetti non è inclusa in Visual Studio Code.

## <a name="extend-the-package-manager-console"></a>Estendere la console di Gestione pacchetti

Alcuni pacchetti installano nuovi comandi per la console. Ad esempio, `MvcScaffolding` crea comandi come `Scaffold` mostrato di seguito, che genera i controller e le visualizzazioni MVC ASP.NET:

![Installazione e uso di MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a>Configurare un profilo di PowerShell per NuGet

Un profilo di PowerShell consente di rendere disponibili i comandi usati comunemente ogni volta che si usa PowerShell. NuGet supporta un profilo specifico di NuGet disponibile in genere nel percorso seguente:

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

Per trovare il profilo, digitare `$profile` nella console:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Per altri dettagli, vedere [Profili di Windows PowerShell](/previous-versions//bb613488(v=vs.85)).

## <a name="use-the-nugetexe-cli-in-the-console"></a>Usare l'interfaccia della riga di comando di nuget.exe nella console

Per rendere disponibile l' [ `nuget.exe` interfaccia](../reference/nuget-exe-cli-reference.md) della riga di comando nella console di gestione pacchetti, installare il pacchetto [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) dalla console di:

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```