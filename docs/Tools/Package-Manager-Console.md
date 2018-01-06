---
title: Guida alla Console di gestione pacchetti NuGet | Documenti Microsoft
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: Istruzioni per l'utilizzo della Console di gestione pacchetti NuGet in Visual Studio per l'utilizzo di pacchetti.
keywords: NuGet package manager console powershell di NuGet, gestire i pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc11963a9b9bfe9aa456d8cd4c8397e1084f660b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="package-manager-console"></a>Console di gestione pacchetti

La Console di gestione pacchetti NuGet viene compilata in Visual Studio in Windows 2012 e versioni successive. (Non è incluso in Visual Studio per Mac o codice di Visual Studio.)

La console consente di utilizzare [comandi PowerShell di NuGet](../tools/powershell-reference.md) per trovare, installare, disinstallare e aggiornare i pacchetti NuGet. Utilizzando la console è necessario nei casi in cui la UI Package Manager non fornisce un modo per eseguire un'operazione.

Ricerca e l'installazione di un pacchetto, ad esempio, viene eseguita con tre semplici passaggi:

1. Aprire il progetto/soluzione in Visual Studio e aprire la console usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando.

1. Trovare il pacchetto che si desidera installare. Se si conosce già questo, andare al passaggio 3.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. Eseguire il comando di installazione:

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

In questo argomento

- [Aprire la console di](#opening-the-console-and-console-controls)
- [Installa un pacchetto](#installing-a-package)
- [La disinstallazione di un pacchetto](#uninstalling-a-package)
- [Ricerca di un pacchetto](#finding-a-package)
- [Aggiornamento di un pacchetto](#updating-a-package)
- [Disponibilità della console di](#availability-of-the-console)
- [Estendere la Console di gestione pacchetti](#extending-the-package-manager-console)
- [Impostazione di un profilo di PowerShell di NuGet](#setting-up-a-nuget-powershell-profile)

> [!Important]
> Tutte le operazioni che sono disponibili nella console possono essere eseguite anche con il [NuGet CLI](../tools/nuget-exe-cli-reference.md). Tuttavia, i comandi della console operano all'interno del contesto di Visual Studio e una progetto/soluzione salvata e spesso eseguire più i comandi CLI equivalenti. Ad esempio, l'installazione di un pacchetto tramite la console aggiunge un riferimento al progetto mentre il comando CLI non. Per questo motivo, gli sviluppatori che lavorano in Visual Studio, in genere preferiscono utilizzando la console per l'interfaccia CLI.

> [!Tip]
> Molte operazioni di console dipendono dalla presenza di una soluzione aperta in Visual Studio con un nome di percorso noto. Se si dispone di una soluzione non salvata o alcuna soluzione, è possibile visualizzare l'errore, "soluzione non aperta o non salvata. Assicurarsi che disporre di una soluzione aperta e salvata." Indica che la console non è possibile determinare la cartella della soluzione. Salvataggio di una soluzione non salvata, o la creazione e il salvataggio di una soluzione se non si dispone di uno aprire, deve correggere l'errore.

## <a name="opening-the-console-and-console-controls"></a>Apertura della console e i controlli di console

1. Aprire la console in Visual Studio usando il **strumenti > Gestione pacchetti NuGet > Console di gestione pacchetti** comando. La console è una finestra di Visual Studio che può essere disposti e posizionata, tuttavia si desidera (vedere [personalizzare i layout delle finestre in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. Per impostazione predefinita, i comandi della console funzionano in un'origine pacchetto specifico e un progetto di cui il controllo nella parte superiore della finestra:

    ![Controlli di Console di gestione pacchetti per l'origine del pacchetto e progetto](media/PackageManagerConsoleControls1.png)

1. La selezione di un'origine pacchetto diverso e/o il progetto modifica tali impostazioni predefinite per i comandi successivi. La maggior parte dei comandi per esegue l'override queste impostazioni senza modificare le impostazioni predefinite, supportano `-Source` e `-ProjectName` opzioni.

1. Per gestire l'origine del pacchetto, selezionare l'icona dell'ingranaggio. Si tratta di un collegamento per il **strumenti > Opzioni > Gestione pacchetti NuGet > origini pacchetti** come descritto nella finestra di dialogo di [UI Package Manager](Package-Manager-UI.md#package-sources) pagina. Inoltre, il controllo a destra del selettore di progetto Cancella il contenuto della console:

    ![Impostazioni della Console di gestione pacchetti e deselezionare i controlli](media/PackageManagerConsoleControls2.png)

1. Pulsante a destra consente di interrompere un comando a esecuzione prolungata. Ad esempio, in esecuzione `Get-Package -ListAvailable -PageSize 500` Elenca i pacchetti superiore a 500 nell'origine predefinita (ad esempio nuget.org), che potrebbe richiedere alcuni minuti per l'esecuzione.

    ![Controllo di arresto di Console di gestione pacchetti](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>Installa un pacchetto

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

Vedere [Install-Package](../tools/ps-ref-install-package.md).

Installa un pacchetto esegue le azioni seguenti:

- Visualizza condizioni di licenza applicabili nella finestra della console con un contratto implicito. Se non si accettano le condizioni, è necessario disinstallare il pacchetto immediatamente.
- Aggiunge un riferimento al progetto in qualsiasi formato di riferimento è in uso. In Esplora soluzioni e il file di formato di riferimento applicabili sono presenti riferimenti successivamente. Si noti, tuttavia, con PackageReference, è necessario salvare il progetto per visualizzare le modifiche nel file di progetto direttamente.
- Memorizza nella cache il pacchetto:
    - PackageReference: pacchetto memorizzato nella cache `%USERPROFILE%\.nuget\packages` e il blocco di file, ovvero `project.assets.json` viene aggiornato.
    - `packages.config`: crea un `packages` cartella radice della soluzione e copia il pacchetto di file in una sottocartella all'interno di esso. Il `package.config` file viene aggiornato.
- Aggiornamenti `app.config` e/o `web.config` se il pacchetto utilizza [trasformazioni di file di origine e configurazione](../create-packages/source-and-config-file-transformations.md).
- Installa tutte le dipendenze, se non è già presente nel progetto. Questo potrebbe aggiornare versioni del pacchetto del processo, come descritto in [la risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).
- Visualizza file readme del pacchetto, se disponibile, in una finestra di Visual Studio.

> [!Tip]
> Uno dei principali vantaggi dell'installazione di pacchetti con il `Install-Package` nella console di comando è come se è stata utilizzata la UI Package Manager, che aggiunge un riferimento al progetto. Al contrario, il `nuget install` comando CLI di solo download del pacchetto e non aggiunge automaticamente un riferimento.

## <a name="uninstalling-a-package"></a>La disinstallazione di un pacchetto

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

Vedere [Uninstall-Package](../tools/ps-ref-uninstall-package.md). Utilizzare [Get-Package](../tools/ps-ref-get-package.md) per visualizzare tutti i pacchetti installati nel progetto predefinito se è necessario trovare un identificatore.

La disinstallazione di un pacchetto esegue le azioni seguenti:

- Rimuove i riferimenti al pacchetto dal progetto (e qualsiasi formato di riferimento è in uso). Non sono presenti riferimenti in Esplora soluzioni. (Potrebbe essere necessario ricompilare il progetto per visualizzarlo rimossa la **Bin** cartella.)
- Inverte le modifiche apportate al `app.config` o `web.config` quando il pacchetto è stato installato.
- Dipendenze rimuove installato in precedenza, se i pacchetti rimanenti non utilizzano tali dipendenze.

> [!Tip]
> Ad esempio `Install-Package`, il `Uninstall-Package` comando ha il vantaggio di gestione dei riferimenti nel progetto, a differenza di `nuget uninstall` comando CLI.

## <a name="updating-a-package"></a>Aggiornamento di un pacchetto

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

Vedere [Get-Package](../tools/ps-ref-get-package.md) e [pacchetto di aggiornamento](../tools/ps-ref-update-package.md)

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

Vedere [Find-Package](../tools/ps-ref-find-package.md). In Visual Studio 2013 e versioni precedenti, utilizzare [Get-Package](../tools/ps-ref-get-package.md) invece.

## <a name="availability-of-the-console"></a>Disponibilità della console di

In Visual Studio 2017, NuGet e gestione pacchetti NuGet vengono installati automaticamente quando si seleziona uno. Carichi di lavoro correlati alla rete; è possibile anche installare singolarmente controllando il **singoli componenti > codice strumenti > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio 2017.

Inoltre, assenza Gestione pacchetti NuGet in Visual Studio 2015 e versioni precedenti, controllare **strumenti > estensioni e aggiornamenti...**  e cercare l'estensione Gestione pacchetti NuGet. Se non si riesce a usare il programma di installazione di estensioni in Visual Studio, è possibile scaricare l'estensione direttamente da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).

La Console di gestione pacchetti non è attualmente disponibile in Visual Studio per Mac. I comandi equivalenti, tuttavia, sono disponibili tramite il [NuGet CLI](nuget-exe-CLI-reference.md). Visual Studio per Mac hanno un'interfaccia utente per la gestione dei pacchetti NuGet. Vedere [pacchetto NuGet un inclusi nel progetto](/visualstudio/mac/nuget-walkthrough).

Console di gestione pacchetti non è inclusa in Visual Studio Code.

## <a name="extending-the-package-manager-console"></a>Estendere la Console di gestione pacchetti

Alcuni pacchetti installare nuovi comandi per la console. Ad esempio, `MvcScaffolding` crea comandi come `Scaffold` illustrato di seguito, che genera l'errore ASP.NET MVC controller e visualizzazioni:

![Installazione e utilizzo MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>Impostazione di un profilo di PowerShell di NuGet

Un profilo di PowerShell consente di rendere disponibili i comandi di uso comune, ogni volta che è possibile usare PowerShell. NuGet supporta un profilo specifico di NuGet in genere disponibile nel percorso seguente:

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Per trovare il profilo, digitare `$profile` nella console:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

Per ulteriori informazioni, vedere [profili di Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).
