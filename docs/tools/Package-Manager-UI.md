---
title: Installare e gestire pacchetti NuGet in Visual Studio
description: Istruzioni per l'uso di NuGet Package Manager UI in Visual Studio per l'uso di pacchetti NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426241"
---
# <a name="install-and-manage-packages-in-visual-studio"></a>Installare e gestire pacchetti in Visual Studio

L'UI Gestione pacchetti NuGet in Visual Studio in Windows consente di installare, disinstallare e aggiornare i pacchetti NuGet in progetti e soluzioni. Per l'esperienza in Visual Studio per Mac, vedere [tra cui un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough). Il Package Manager UI non è inclusa in Visual Studio Code.

> [!NOTE]
> Se sono necessari i pacchetti NuGet in Visual Studio 2015, controllare **strumenti > estensioni e aggiornamenti...**  e cercare la *Gestione pacchetti NuGet* estensione. Se non si riesce a usare il programma di installazione di estensioni in Visual Studio, scaricare l'estensione direttamente dal [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> A partire da Visual Studio 2017, NuGet e la gestione pacchetti NuGet vengono installati automaticamente con qualsiasi. Carichi di lavoro correlate alla rete. Installare singolarmente selezionando i **singoli componenti > strumenti per il codice > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio.

## <a name="finding-and-installing-a-package"></a>Ricerca e installazione di un pacchetto

1. Nelle **Esplora soluzioni**, fare doppio clic su uno **riferimenti** o un progetto e selezionare **Gestisci pacchetti NuGet...** .

    ![I pacchetti NuGet dal menu Opzioni di gestione](media/ManagePackagesUICommand.png)

1. Il **esplorare** scheda consente di visualizzare i pacchetti per popolarità dell'origine attualmente selezionata (vedere [origini di pacchetti](#package-sources)). Ricerca di un pacchetto specifico usando la casella di ricerca in alto a sinistra. Selezionare un pacchetto dall'elenco per visualizzare informazioni, che abilita anche il **installare** pulsante insieme a un elenco a discesa-selezione della versione.

    ![Gestione scheda Sfoglia di NuGet package finestra di dialogo](media/Search.png)

1. Selezionare la versione desiderata dall'elenco a discesa e selezionare **installare**. Visual Studio installa il pacchetto e le relative dipendenze nel progetto. Potrebbe essere richiesto di accettare le condizioni di licenza. Quando l'installazione è stata completata, i pacchetti aggiunti vengono visualizzati nella **Installed** scheda. I pacchetti sono elencati anche nella **riferimenti** nodo di Esplora soluzioni, che indica che è possibile farvi riferimento nel progetto con `using` istruzioni.

    ![Riferimenti in Esplora soluzioni](media/References.png)

> [!Tip]
> Per includere le versioni non definitive nella ricerca e per rendere le versioni non definitive disponibili nella versione di elenco a discesa, selezionare la **Includi versione preliminare** opzione.

## <a name="uninstalling-a-package"></a>Disinstallazione di un pacchetto

1. Nelle **Esplora soluzioni**, fare doppio clic su uno **riferimenti** oppure il progetto desiderato e selezionare **Gestisci pacchetti NuGet...** .
1. Selezionare il **Installed** scheda.
1. Selezionare il pacchetto da disinstallare (uso di ricerca per filtrare l'elenco se necessario) e scegliere **Disinstalla**.

    ![Disinstallazione di un pacchetto](media/UninstallPackage.png)

1. Si noti che il **Includi versione preliminare** e **origine pacchetto** controlli non hanno alcun effetto durante la disinstallazione dei pacchetti.

## <a name="updating-a-package"></a>Aggiorna un pacchetto

1. Nelle **Esplora soluzioni**, fare doppio clic su uno **riferimenti** oppure il progetto desiderato e selezionare **Gestisci pacchetti NuGet...** . (In progetti di siti web, fare doppio clic il **Bin** cartella.)
1. Selezionare il **aggiornamenti** scheda per visualizzare i pacchetti sono disponibili aggiornamenti dalle origini pacchetto selezionato. Selezionare **Includi versione preliminare** per includere i pacchetti di versione non definitivo nel relativo elenco.
1. Selezionare il pacchetto da aggiornare, selezionare la versione desiderata dall'elenco a discesa a destra e selezionare **aggiornare**.

    ![Aggiorna un pacchetto](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Per alcuni pacchetti, la **Update** pulsante è disabilitato e viene visualizzato un messaggio che informa che è "in modo implicito fa un SDK" (o "AutoReferenced"). Questo messaggio indica che il pacchetto fa parte di un framework o SDK di dimensioni superiori e non deve essere aggiornato in modo indipendente. (Tali pacchetti internamente sono contrassegnati con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Ad esempio, `Microsoft.NETCore.App` fa parte di .NET Core SDK e la versione del pacchetto non è la stessa versione di framework runtime usati dall'applicazione. Devi [aggiornare l'installazione di .NET Core](https://aka.ms/dotnet-download) per ottenere nuove versioni del runtime di ASP.NET Core e .NET Core. [Vedere questo documento per altri dettagli sulla metapacchetti .NET Core e controllo delle versioni](/dotnet/core/packages). Questo vale per i pacchetti di usati comune seguenti:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Pacchetto di esempio viene contrassegnato come in modo implicito i riferimenti o AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Per aggiornare più pacchetti alle corrispondenti versioni più recenti, selezionarli nell'elenco e selezionare il **aggiornare** pulsante sopra l'elenco.
1. È anche possibile aggiornare un pacchetto singolo dal **Installed** scheda. In questo caso, i dettagli per il pacchetto includono un selettore di versione (soggetto al **Includi versione preliminare** opzione) e un **Update** pulsante.

## <a name="managing-packages-for-the-solution"></a>La gestione dei pacchetti per la soluzione

La gestione dei pacchetti per una soluzione è un modo pratico per lavorare con più progetti contemporaneamente.

1. Selezionare il **strumenti > Gestione pacchetti NuGet > Gestisci pacchetti NuGet per la soluzione...**  dal menu di comando, o la soluzione e scegliere **Gestisci pacchetti NuGet...** :

    ![Gestisci pacchetti NuGet per la soluzione](media/ManagePackagesSolutionUICommand.png)

1. Quando si gestiscono i pacchetti per la soluzione, l'interfaccia utente consente di selezionare i progetti che sono interessati dalle operazioni:

    ![Selettore progetti durante la gestione dei pacchetti per la soluzione](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Consolidare scheda

Gli sviluppatori considerano in genere una buona prassi di usare versioni diverse dello stesso pacchetto NuGet in progetti diversi nella stessa soluzione. Quando si sceglie di gestire i pacchetti per una soluzione, il Package Manager UI offre una **consolida** scheda in cui è possibile visualizzare facilmente in cui i pacchetti con numeri di versione distinti vengono utilizzati da diversi progetti nella soluzione:

![Scheda di consolidamento dell'interfaccia utente di gestione pacchetti](media/ConsolidateTab.png)

In questo esempio, il progetto ClassLibrary1 Usa EntityFramework 6.2.0, considerando che utilizza EntityFramework 6.1.0 ConsoleApp1. Per consolidare le versioni dei pacchetti, eseguire le operazioni seguenti:

- Selezionare i progetti da aggiornare nell'elenco di progetti.
- Selezionare la versione da usare in tutti i progetti nel **versione** controllo, ad esempio EntityFramework 6.2.0.
- Selezionare il **installare** pulsante.

La gestione dei pacchetti consente di installare la versione del pacchetto selezionato in tutti i progetti selezionati, dopo il quale il pacchetto non viene più visualizzata nella **consolida** scheda.

## <a name="package-sources"></a>Origini dei pacchetti

Per modificare l'origine da cui Visual Studio Ottiene i pacchetti, selezionare uno dal selettore di origine:

![Selettore di origine del pacchetto in package manager UI](media/PackageSourceDropDown.png)

Gestire le origini pacchetto:

1. Selezionare il **le impostazioni** icona nel Package Manager UI descritti di seguito oppure utilizzare il **strumenti > Opzioni** comando e scorrere fino alla **Gestione pacchetti NuGet**:

    ![Icona delle impostazioni dell'interfaccia utente di gestione pacchetti](media/PackageSourceSettings.png)

1. Selezionare il **origini dei pacchetti** nodo:

    ![Opzioni di origini dei pacchetti](media/options.png)

1. Per aggiungere un'origine, selezionare **+** , modificare il nome, immettere l'URL o percorso nel **origine** controllare, quindi selezionare **Update**. L'origine viene ora visualizzato nel selettore di elenco a discesa.
1. Per modificare un'origine del pacchetto, selezionarlo, apportare modifiche nel **Name** e **origine** caselle, quindi selezionare **Update**.
1. Per disabilitare un'origine del pacchetto, deselezionare la casella a sinistra del nome nell'elenco.
1. Per rimuovere un'origine del pacchetto, selezionarlo e quindi selezionare il **X** pulsante.
1. Utilizzando la freccia giù e freccia giù pulsanti non viene modificato l'ordine di priorità le origini pacchetto. Visual Studio ignora l'ordine delle origini dei pacchetti, Usa il pacchetto da qualsiasi origine prima di rispondere alle richieste. Per altre informazioni, vedere [ripristino del pacchetto](../consume-packages/package-restore.md).

> [!Tip]
> Se un'origine del pacchetto viene nuovamente visualizzato dopo l'eliminazione, potrebbe essere presente in un livello di computer o utente `NuGet.Config` file. Visualizzare [configurazioni comuni per NuGet](../consume-packages/configuring-nuget-behavior.md) per il percorso di questi file, quindi rimuovere l'origine modificando i file manualmente o tramite il [nuget origini comando](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Controllano le opzioni di gestione pacchetti

Quando viene selezionato un pacchetto, il Package Manager UI viene visualizzato un piccolo, espandibile **opzioni** controllo sotto il selettore di versione (illustrato di seguito entrambe compresse ed espanse). Si noti che per alcuni progetti solo con tipi, il **Visualizza finestra di anteprima** opzione è disponibile.

![Opzioni di gestione pacchetti](media/PackageManagerUIOptions.png)

Le sezioni seguenti illustrano queste opzioni.

### <a name="show-preview-window"></a>Visualizzare la finestra di anteprima

Quando selezionata, una finestra modale Visualizza che le dipendenze di un pacchetto scelta prima di installata il pacchetto:

![Finestra di anteprima di esempio](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Installare e aggiornare le opzioni

(Non disponibile per tutti i tipi di progetto).

**Comportamento di dipendenza** configura come NuGet decide quali versioni dei pacchetti dipendenti da installare:

- *Ignora le dipendenze* ignora l'installazione di eventuali dipendenze, creando in genere un'interruzione del pacchetto da installare.
- *Più basso* [Default] la dipendenza viene installato con il numero di versione minima che soddisfi i requisiti del pacchetto primario scelto.
- *Più alto Patch* viene installata la versione con gli stessi numeri di versione principale e secondaria, ma il numero più alto di patch. Ad esempio, se viene specificata una versione 1.2.2 quindi la versione più recente che inizia con 1.2 verrà installata
- *Minore più alto* viene installata la versione con lo stesso numero di versione principale, ma il numero di patch e il numero minore. Se la versione 1.2.2 è specificata, verrà installata la versione più alto che inizia con 1
- *Più alto* installa la versione disponibile più recente del pacchetto.

**Azione di conflitti di file** specifica come NuGet deve gestire i pacchetti già esistenti nel progetto o nel computer locale:

- *Messaggio di richiesta* indica a NuGet per chiedere se mantenere o sovrascrivere i pacchetti esistenti.
- *Ignora tutto* indica a NuGet a saltare la sovrascrittura di tutti i pacchetti esistenti.
- *Sovrascrivi tutto* indica a NuGet per sovrascrivere tutti i pacchetti esistenti.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opzioni di disinstallazione

(Non disponibile per tutti i tipi di progetto).

**Rimuovere le dipendenze**: quando è selezionata, consente di rimuovere eventuali pacchetti dipendenti se non si viene fatto riferimento in un' posizione nel progetto.

**Forza la disinstallazione anche se sono presenti dipendenze su di esso**: quando è selezionata, consente di disinstallare un pacchetto anche se vi fanno ancora riferimento nel progetto. Viene in genere utilizzato in combinazione con **rimuovere le dipendenze** per rimuovere un pacchetto e tutti i valori delle dipendenze è installato. Utilizzo di questa opzione potrebbe, tuttavia, causare ai riferimenti interrotti nel progetto. In questi casi, potrebbe essere necessario [reinstallare tali altri pacchetti](../consume-packages/reinstalling-and-updating-packages.md).
