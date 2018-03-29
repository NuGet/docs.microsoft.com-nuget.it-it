---
title: Riferimento all'interfaccia utente di gestione pacchetti di NuGet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: Istruzioni per l'utilizzo di UI Gestione pacchetti NuGet in Visual Studio per l'utilizzo di pacchetti NuGet.
keywords: UI NuGet, Gestione pacchetti NuGet dell'interfaccia utente, NuGet in Visual Studio, la gestione pacchetti NuGet, interfaccia utente di NuGet, gestione di pacchetti in Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ad36c2ab0c6e62c7fe624b35d92e852303ecfdfb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-package-manager-ui"></a>Interfaccia utente di gestione pacchetti NuGet

L'UI Gestione pacchetti NuGet in Visual Studio in Windows consente di installare, disinstallare e aggiornare i pacchetti NuGet in progetti e soluzioni. Per l'esperienza in Visual Studio per Mac, vedere [pacchetto NuGet un inclusi nel progetto](/visualstudio/mac/nuget-walkthrough). L'UI Package Manager non è inclusa in Visual Studio Code.

In questo argomento

- [Ricerca e l'installazione di un pacchetto (scheda Sfoglia)](#finding-and-installing-a-package)
- [La disinstallazione di un pacchetto (scheda installato)](#uninstalling-a-package)
- [Aggiornamento di un pacchetto (installazione e aggiornamenti schede)](#updating-a-package) (include il ["In modo implicito a cui fa riferimento un SDK" o "AutoReferenced" messaggio](#implicit_reference))
- [La gestione dei pacchetti per la soluzione](#managing-packages-for-the-solution) (utilizzo di più progetti contemporaneamente).
- [Origine del pacchetto](#package-sources)
- [Controllano le opzioni di gestione pacchetti](#package-manager-options-control)

> [!Note]
> Assenza di gestione pacchetti NuGet in Visual Studio 2015, controllare **strumenti > estensioni e aggiornamenti...**  e cercare il *Gestione pacchetti NuGet* estensione. Se non riesci a usare il programma di installazione di estensioni in Visual Studio, scaricare l'estensione direttamente dal [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> In Visual Studio 2017, vengano automaticamente installati con NuGet e gestione pacchetti NuGet. Carichi di lavoro correlati alla rete. Installare singolarmente selezionando il **singoli componenti > codice strumenti > Gestione pacchetti NuGet** opzione nel programma di installazione di Visual Studio 2017.

## <a name="finding-and-installing-a-package"></a>Ricerca e l'installazione di un pacchetto

1. In **Esplora**, fare doppio clic su uno **riferimenti** o un progetto e selezionare **Gestisci pacchetti NuGet...** .

    ![Gestire l'opzione di menu pacchetti NuGet](media/ManagePackagesUICommand.png)

1. Il **Sfoglia** scheda Visualizza pacchetti di popolarità dall'origine attualmente selezionata (vedere [origini del pacchetto](#package-sources)). Ricerca di un pacchetto specifico tramite la casella di ricerca in alto a sinistra. Selezionare un pacchetto dall'elenco per visualizzare le informazioni, che consente anche di **installare** pulsante insieme a un elenco a discesa selezione della versione.

    ![Gestisci NuGet pacchetti finestra di dialogo Sfoglia scheda](media/Search.png)

1. Selezionare la versione desiderata dall'elenco a discesa e selezionare **installare**. Visual Studio installa il pacchetto e le relative dipendenze nel progetto. Potrebbe essere richiesto di accettare le condizioni di licenza. Quando l'installazione è stata completata, i pacchetti aggiunti vengono visualizzati di **installato** scheda. Vengono inoltre elencati i pacchetti nel **riferimenti** nodo di Esplora soluzioni, che indica che è possibile farvi riferimento nel progetto con `using` istruzioni.

    ![Riferimenti in Esplora soluzioni](media/References.png)

> [!Tip]
    > Per includere le versioni non definitive nella ricerca e che le versioni non definitive disponibili nella versione di riepilogo a discesa, selezionare il **Includi versione preliminare** opzione.

## <a name="uninstalling-a-package"></a>La disinstallazione di un pacchetto

1. In **Esplora**, fare doppio clic su uno **riferimenti** o il progetto desiderato e scegliere **Gestisci pacchetti NuGet...** .
1. Selezionare il **installato** scheda.
1. Selezionare il pacchetto da disinstallare (utilizzo della ricerca per filtrare l'elenco, se necessario) e selezionare **Disinstalla**.

    ![La disinstallazione di un pacchetto](media/UninstallPackage.png)

1. Si noti che il **versione provvisoria di inclusione** e **origine pacchetto** controlli non hanno alcun effetto durante la disinstallazione di pacchetti.

## <a name="updating-a-package"></a>Aggiornamento di un pacchetto

1. In **Esplora**, fare doppio clic su uno **riferimenti** o il progetto desiderato e scegliere **Gestisci pacchetti NuGet...** . (In progetti di siti web, fare clic di **Bin** cartella.)
1. Selezionare il **aggiornamenti** scheda per visualizzare i pacchetti con aggiornamenti disponibili dalle origini del pacchetto selezionato. Selezionare **Includi versione preliminare** per includere i pacchetti con versione non definitiva nel relativo elenco.
1. Selezionare il pacchetto da aggiornare, selezionare la versione desiderata dall'elenco a discesa a destra e selezionare **aggiornare**.

    ![Aggiornamento di un pacchetto](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Per alcuni pacchetti, il **aggiornamento** pulsante è disabilitato e viene visualizzato un messaggio che informa che "in modo implicito fa riferimento un SDK" (o "AutoReferenced"). Il messaggio indica che il pacchetto, ad esempio Microsoft.NETCore.App o Microsoft.NETStandard.Library, fa parte di un SDK o di framework più grande e non deve essere aggiornato in modo indipendente. (Tali pacchetti internamente sono contrassegnati con `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Per aggiornare il pacchetto, aggiornare il SDK a cui appartiene.

    ![Pacchetto di esempio è stato contrassegnato come in modo implicito i riferimenti o AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Per aggiornare più pacchetti con le versioni più recenti, selezionarli nell'elenco e selezionare il **aggiornare** pulsante sopra l'elenco.
1. È inoltre possibile aggiornare un singolo pacchetto dal **installato** scheda. In questo caso, i dettagli per il pacchetto includono un selettore di versione (soggetto al **versione provvisoria di inclusione** opzione) e un **aggiornamento** pulsante.

## <a name="managing-packages-for-the-solution"></a>La gestione dei pacchetti per la soluzione

La gestione dei pacchetti per una soluzione è un modo pratico per più progetti contemporaneamente.

1. Selezionare il **strumenti > Gestione pacchetti NuGet > Gestisci pacchetti NuGet per la soluzione...**  menu comando o la soluzione e scegliere **Gestisci pacchetti NuGet...** :

    ![Gestisci pacchetti NuGet per la soluzione](media/ManagePackagesSolutionUICommand.png)

1. Quando la gestione dei pacchetti per la soluzione, l'interfaccia utente consente di selezionare i progetti che sono interessati dalle operazioni:

    ![Selettore di progetto per la gestione di pacchetti per la soluzione](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Consolidare scheda

Gli sviluppatori in genere viene considerano una prassi sbagliata utilizzare versioni diverse dello stesso pacchetto NuGet in progetti diversi nella stessa soluzione. Quando si sceglie di gestire i pacchetti per una soluzione, la UI Package Manager fornisce un **consolida** scheda in cui è possibile visualizzare facilmente in cui i pacchetti con numeri di versione diversi vengono utilizzati da diversi progetti nella soluzione:

![Scheda consolidare dell'interfaccia utente di gestione pacchetti](media/ConsolidateTab.png)

In questo esempio, il progetto ClassLibrary1 utilizza EntityFramework 6.2.0, considerando che utilizza EntityFramework 6.1.0 ConsoleApp1. Per consolidare versioni del pacchetto, effettuare le operazioni seguenti:

- Selezionare i progetti da aggiornare nell'elenco di progetto.
- Selezionare la versione da utilizzare in tutti i progetti nel **versione** controllo, ad esempio EntityFramework 6.2.0.
- Selezionare il **installare** pulsante.

Package Manager installa la versione del pacchetto selezionato in tutti i progetti selezionati, dopo il quale il pacchetto non viene più visualizzata sul **consolida** scheda.

## <a name="package-sources"></a>Origine del pacchetto

Per modificare l'origine da cui Visual Studio Ottiene i pacchetti, selezionare uno dal selettore di origine:

![Selettore di origine del pacchetto nella gestione dei pacchetti dell'interfaccia utente](media/PackageSourceDropDown.png)

Per gestire l'origine del pacchetto:

1. Selezionare il **impostazioni** icona nell'UI Package Manager descritti di seguito oppure utilizzare il **strumenti > Opzioni** comando e scorrere fino a **Gestione pacchetti NuGet**:

    ![Icona di impostazioni dell'interfaccia utente Gestione pacchetto](media/PackageSourceSettings.png)

1. Selezionare il **origini pacchetti** nodo:

    ![Opzioni di origini del pacchetto](media/options.png)

1. Per aggiungere un'origine, selezionare **+**, modificare il nome, immettere l'URL o percorso di **origine** controllo e scegliere **aggiornamento**. L'origine verrà visualizzato nell'elenco a discesa del selettore.
1. Per modificare un'origine del pacchetto, selezionarlo, apportare le modifiche apportate nel **nome** e **origine** finestre e selezionare **aggiornamento**.
1. Per disabilitare un'origine del pacchetto, deselezionare la casella a sinistra del nome nell'elenco.
1. Per rimuovere un'origine del pacchetto, selezionarlo e quindi selezionare il **X** pulsante.
1. Utilizzare le frecce su e freccia giù per modificare l'ordine di priorità delle origini pacchetto. Durante il ripristino dei pacchetti per un progetto, Visual Studio cerca queste origini in ordine di priorità. Per ulteriori informazioni, vedere [ripristino del pacchetto](../consume-packages/package-restore.md).

> [!Tip]
> Se un'origine del pacchetto viene nuovamente visualizzato dopo l'eliminazione, potrebbe essere elencato in un livello di computer o utente `NuGet.Config` file. Vedere [il comportamento di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md) per il percorso di questi file, quindi rimuovere l'origine modificando i file manualmente o utilizzando il [nuget origini comando](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Controllano le opzioni di gestione pacchetti

Quando si seleziona un pacchetto, la UI Package Manager consente di visualizzare una piccola, espandibile **opzioni** controllo sotto il selettore di versione (illustrato di seguito sia compresso ed esteso). Si noti che per un progetto solo tipi di **finestra di anteprima mostra** opzione è disponibile.

![Opzioni di gestione pacchetti](media/PackageManagerUIOptions.png)

Le sezioni seguenti illustrano queste opzioni.

### <a name="show-preview-window"></a>Mostra finestra di anteprima

Quando selezionata, una finestra modale Visualizza che le dipendenze di un pacchetto scelto prima di installata il pacchetto:

![Finestra di dialogo Anteprima esempio](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Installazione e le opzioni di aggiornamento

(Non disponibile per tutti i tipi di progetto).

**Comportamento di dipendenza** Configura modalità NuGet decide quali versioni dei pacchetti dipendenti da installare:

- *Ignorare le dipendenze* ignora l'installazione di tutte le dipendenze, che in genere si interrompe il pacchetto da installare.
- *Più basso* [Default] consente di installare la dipendenza con il numero di versione minima che soddisfi i requisiti del pacchetto scelto primario.
- *Più alto Patch* installa la versione con gli stessi numeri di versione principale e secondaria, ma il numero più alto di patch. Ad esempio, se la versione 1.2.2 è specificata la versione più recente che inizia con 1.2 verrà quindi installata
- *Minore più alto* installa la versione con lo stesso numero di versione principale, ma il numero di patch e il numero minore più alto. Se la versione 1.2.2 è specificata, verrà installata la versione più recente che inizia con 1
- *Più alto* installa la versione disponibile più recente del pacchetto.

**Azione di conflitti di file** specifica come NuGet deve gestire i pacchetti già esistenti nel progetto o nel computer locale:

- *Prompt dei comandi* indica NuGet chiedere se mantenere o sovrascrivere i pacchetti esistenti.
- *Ignora tutto* indica NuGet per ignorare la sovrascrittura di tutti i pacchetti esistenti.
- *Sovrascrivi tutto* indica NuGet per sovrascrivere i pacchetti esistenti.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opzioni di disinstallazione

(Non disponibile per tutti i tipi di progetto).

**Rimuovere le dipendenze**: quando è selezionata, rimuove tutti i pacchetti dipendenti se non si viene fatto riferimento in un' posizione nel progetto.

**Forza la disinstallazione anche se sono presenti dipendenze**: quando è selezionata, disinstalla un pacchetto anche se vi fa ancora riferimento nel progetto. In genere viene utilizzato in combinazione con **rimuovere le dipendenze** per rimuovere un pacchetto e dalle dipendenze è installato. Questa opzione può tuttavia causare ai riferimenti interrotti nel progetto. In questi casi, potrebbe essere necessario [reinstallare tali altri pacchetti](../consume-packages/reinstalling-and-updating-packages.md).
