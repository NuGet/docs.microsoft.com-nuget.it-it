---
title: Installare e gestire pacchetti NuGet in Visual Studio
description: Istruzioni per l'uso dell'interfaccia utente di Gestione pacchetti NuGet in Visual Studio per utilizzare pacchetti NuGet.
author: JonDouglas
ms.author: jodou
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 87024dc6bd8e17a39fa7952deb39aa5bd48f6af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774997"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Installare e gestire i pacchetti in Visual Studio con Gestione pacchetti NuGet

L'interfaccia utente di Gestione pacchetti NuGet in Visual Studio in Windows consente di installare, disinstallare e aggiornare facilmente i pacchetti NuGet in progetti e soluzioni. Per l'esperienza in Visual Studio per Mac, vedere [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). L'interfaccia utente di Gestione pacchetti non è inclusa in Visual Studio Code.

> [!NOTE]
> Se non si trova Gestione pacchetti NuGet in Visual Studio 2015, selezionare **Strumenti > Estensioni e aggiornamenti** e cercare l'estensione *Gestione pacchetti NuGet*. Se non si è in grado di usare il programma di installazione delle estensioni in Visual Studio, scaricare l'estensione direttamente da [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .
>
> A partire da Visual Studio 2017, NuGet e Gestione pacchetti NuGet vengono installati automaticamente con qualsiasi carico di lavoro correlato a NET. Per installarli singolarmente, selezionare **Singoli componenti > Strumenti per il codice > Gestione pacchetti NuGet** nel programma di installazione di Visual Studio.

## <a name="find-and-install-a-package"></a>Trovare e installare un pacchetto

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** o su un progetto e scegliere **Gestisci pacchetti NuGet**.

    ![Opzione di menu Gestisci pacchetti NuGet](media/ManagePackagesUICommand.png)

1. La scheda **Sfoglia** visualizza i pacchetti in base alla popolarità dall'origine attualmente selezionata (vedere [Origini dei pacchetti](#package-sources)). Cercare un pacchetto specifico usando la casella di ricerca in alto a sinistra. Selezionare un pacchetto nell'elenco per visualizzarne le informazioni. In questo modo viene anche abilitato il pulsante **Installa** insieme a un elenco a discesa per la selezione della versione.

    ![Finestra di dialogo Gestisci pacchetti NuGet, scheda Sfoglia](media/Search.png)

1. Selezionare la versione desiderata nell'elenco a discesa e selezionare **Installa**. Visual Studio installa il pacchetto e le relative dipendenze nel progetto. Potrebbe essere richiesto di accettare le condizioni di licenza. Al termine dell'installazione, i pacchetti aggiunti verranno visualizzati nella scheda **installato** . I pacchetti sono elencati anche nel nodo **riferimenti** di Esplora soluzioni, a indicare che è possibile farvi riferimento nel progetto con le `using` istruzioni.

    ![Riferimenti in Esplora soluzioni](media/References.png)

> [!Tip]
> Per includere le versioni preliminari nella ricerca e per rendere disponibili le versioni preliminari nell'elenco a discesa delle versioni, selezionare l'opzione **Includi versione preliminare**.

> [!Note]
> NuGet presenta due formati in cui un progetto può usare i pacchetti: [`PackageReference`](package-references-in-project-files.md) e [`packages.config`](../reference/packages-config.md) . [Il valore predefinito può essere impostato nella finestra delle opzioni di Visual Studio](Package-Restore.md#choose-default-package-management-format).

## <a name="uninstall-a-package"></a>Disinstalla un pacchetto

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti** o sul progetto desiderato e scegliere **Gestisci pacchetti NuGet**.
1. Selezionare la scheda **Installati**.
1. Selezionare il pacchetto da disinstallare (usando la ricerca per filtrare l'elenco, se necessario) e selezionare **Disinstalla**.

    ![Disinstallazione di un pacchetto](media/UninstallPackage.png)

1. Si noti che i controlli **Includi versione preliminare** e **Origine pacchetto** non hanno effetto quando si disinstallano i pacchetti.

## <a name="update-a-package"></a>Aggiornare un pacchetto

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **riferimenti** o sul progetto desiderato e scegliere **Gestisci pacchetti NuGet...**. (In progetti sito Web fare clic con il pulsante destro del mouse sulla cartella **bin** ).
1. Selezionare la scheda **Aggiornamenti** per visualizzare i pacchetti con aggiornamenti disponibili dalle origini dei pacchetti selezionate. Selezionare **Includi versione preliminare** per includere i pacchetti di versioni preliminari nell'elenco degli aggiornamenti.
1. Selezionare il pacchetto da aggiornare, selezionare la versione desiderata nell'elenco a discesa a destra e selezionare **Aggiorna**.

    ![Aggiornamento di un pacchetto](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Per alcuni pacchetti, il pulsante **Aggiorna** è disabilitato e viene visualizzato un messaggio che informa che "Un SDK vi fa riferimento in modo implicito" (o "con riferimento automatico"). Questo messaggio indica che il pacchetto fa parte di un framework o di un SDK più ampio e non deve essere aggiornato in modo indipendente. (Tali pacchetti sono contrassegnati internamente con `<IsImplicitlyDefined>True</IsImplicitlyDefined>` .) Ad esempio, `Microsoft.NETCore.App` fa parte del .NET Core SDK e la versione del pacchetto non corrisponde alla versione del Framework di runtime usato dall'applicazione. È necessario [aggiornare l'installazione di .NET Core](https://aka.ms/dotnet-download) per ottenere le nuove versioni del runtime di ASP.NET Core e .NET Core. [Per informazioni dettagliate sui metapacchetti e sul controllo delle versioni di .NET Core, vedere questo documento](/dotnet/core/packages). Si applica ai seguenti pacchetti di uso comune:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Pacchetto di esempio contrassegnato come con riferimento implicito o riferimento automatico](media/PackageManagerUIAutoReferenced.png)

1. Per aggiornare più pacchetti alle versioni più recenti, selezionarli nell'elenco e selezionare il pulsante **Aggiorna** sopra l'elenco.
1. È anche possibile aggiornare un singolo pacchetto dalla scheda **installato** . In questo caso, i dettagli per il pacchetto includono un selettore di versione (soggetto all'opzione **Includi versione preliminare** ) e un pulsante **Aggiorna** .

## <a name="manage-packages-for-the-solution"></a>Gestisci i pacchetti per la soluzione

La gestione dei pacchetti per una soluzione è un metodo pratico per utilizzare più progetti contemporaneamente.

1. Scegliere **Strumenti > Gestione pacchetti NuGet > Gestisci pacchetti NuGet per la soluzione** oppure fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Gestisci pacchetti NuGet**:

    ![Gestisci pacchetti NuGet per la soluzione](media/ManagePackagesSolutionUICommand.png)

1. Quando si gestiscono i pacchetti per la soluzione, l'interfaccia utente consente di selezionare i progetti interessati dalle operazioni:

    ![Selettore di progetto durante la gestione dei pacchetti per la soluzione](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Scheda Consolida

Gli sviluppatori in genere considerano una procedura non corretta l'uso di versioni diverse dello stesso pacchetto NuGet in progetti diversi nella stessa soluzione. Quando si sceglie di gestire i pacchetti per una soluzione, l'interfaccia utente di Gestione pacchetti include una scheda **Consolida** in cui è possibile visualizzare facilmente i pacchetti con numeri di versione distinti usati da progetti diversi nella soluzione:

![Scheda Consolida dell'interfaccia utente di Gestione pacchetti](media/ConsolidateTab.png)

In questo esempio, il progetto ClassLibrary1 usa EntityFramework 6.2.0, mentre ConsoleApp1 usa EntityFramework 6.1.0. Per consolidare le versioni dei pacchetti, seguire questa procedura:

- Selezionare i progetti da aggiornare nell'elenco dei progetti.
- Selezionare la versione da usare in tutti i progetti nel controllo **Versione**, ad esempio EntityFramework 6.2.0.
- Selezionare il pulsante **Installa**.

Gestione pacchetti installa la versione del pacchetto selezionata in tutti i progetti selezionati e in seguito il pacchetto non compare più nella scheda **Consolida**.

## <a name="package-sources"></a>Origini dei pacchetti

Per modificare l'origine da cui Visual Studio ottiene i pacchetti, selezionarne una nel selettore delle origini:

![Selettore delle origini dei pacchetti nell'interfaccia utente di Gestione pacchetti](media/PackageSourceDropDown.png)

Per gestire le origini dei pacchetti:

1. Selezionare l'icona **Impostazioni** nell'interfaccia utente di Gestione pacchetti illustrata di seguito oppure usare il comando **Strumenti > Opzioni** e scorrere fino a **Gestione pacchetti NuGet**:

    ![Icona delle impostazioni dell'interfaccia utente di Gestione pacchetti](media/PackageSourceSettings.png)

1. Selezionare il nodo **Origini pacchetti**:

    ![Opzioni per le origini dei pacchetti](media/options.png)

1. Per aggiungere un'origine, selezionare **+** , modificare il nome, immettere l'URL o il percorso nel controllo del **codice sorgente** e selezionare  **Aggiorna**. L'origine viene ora visualizzata nell'elenco a discesa del selettore.
1. Per modificare un'origine di pacchetti, selezionarla, apportare modifiche nelle caselle **Nome** e **Origine** e selezionare **Aggiorna**.
1. Per disabilitare un'origine di pacchetti, deselezionare la casella a sinistra del nome nell'elenco.
1. Per rimuovere un'origine di pacchetti, selezionarla e quindi selezionare il pulsante **X**.
1. L'uso dei pulsanti freccia su e giù non cambia l'ordine di priorità delle origini dei pacchetti. Visual Studio ignora l'ordine delle origini dei pacchetti e usa il pacchetto da qualsiasi origine risponde per prima alle richieste. Per altre informazioni, vedere [Ripristino di pacchetti](../consume-packages/package-restore.md).

> [!Tip]
> Se un'origine di pacchetti viene visualizzata nuovamente dopo l'eliminazione, potrebbe essere elencata in un file `NuGet.Config` a livello di computer o di utente. Vedere [Configurazioni NuGet comuni](../consume-packages/configuring-nuget-behavior.md) per il percorso di questi file, quindi rimuovere l'origine modificando manualmente i file o usando il [comando nuget sources](../reference/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Controllo Opzioni di Gestione pacchetti

Quando si seleziona un pacchetto, l'interfaccia utente di Gestione pacchetti visualizza un piccolo controllo **Opzioni** espandibile sotto il selettore della versione (visualizzato nella figura sia compresso che espanso). Si noti che per alcuni tipi di progetto viene visualizzata solo l'opzione **Visualizza finestra di anteprima**.

![Opzioni di Gestione pacchetti](media/PackageManagerUIOptions.png)

Nelle sezioni seguenti vengono illustrate queste opzioni.

### <a name="show-preview-window"></a>Visualizza finestra di anteprima

Quando questa opzione è selezionata, una finestra modale visualizza le dipendenze di un pacchetto scelto prima dell'installazione del pacchetto:

![Finestra di dialogo di anteprima di esempio](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Opzioni di installazione e aggiornamento

(Non disponibile per tutti i tipi di progetto.)

**Comportamento dipendenza** configura il modo in cui NuGet decide quali versioni dei pacchetti dipendenti installare:

- *Ignora dipendenze* ignora l'installazione di eventuali dipendenze, che in genere può causare problemi di funzionamento per il pacchetto da installare.
- *Più bassa* [impostazione predefinita] installa la dipendenza con il numero di versione minimo che soddisfa i requisiti del pacchetto scelto primario.
- *Patch più alta* installa la versione con gli stessi numeri di versione principale e secondaria, ma con il numero di patch più alto. Ad esempio, se viene specificata la versione 1.2.2, verrà installata la versione più recente che inizia con 1.2
- *Minore più alta* installa la versione con lo stesso numero di versione principale, ma con il numero di versione secondaria e il numero di patch più alti. Se si specifica la versione 1.2.2 verrà installata la versione più recente che inizia con 1
- *Più alta* installa la versione più alta disponibile del pacchetto.

**Azione conflitto file** specifica il modo in cui NuGet deve gestire i pacchetti già esistenti nel progetto o nel computer locale:

- *Chiedi conferma* indica a NuGet di richiedere se si vogliono mantenere o sovrascrivere i pacchetti esistenti.
- *Ignora tutto* indica a NuGet di non sovrascrivere eventuali pacchetti esistenti.
- *Sovrascrivi tutto* indica a NuGet di sovrascrivere eventuali pacchetti esistenti.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Opzioni di disinstallazione

(Non disponibile per tutti i tipi di progetto.)

**Rimuovi dipendenze**: quando si seleziona questa opzione, eventuali pacchetti dipendenti vengono rimossi se non esistono riferimenti altrove nel progetto.

**Forza la disinstallazione anche se sono presenti dipendenze**: quando si seleziona questa opzione, un pacchetto viene disinstallato anche se sono ancora presenti riferimenti nel progetto. Questa opzione viene in genere usata in combinazione con **Rimuovi dipendenze** per rimuovere un pacchetto e tutte le eventuali dipendenze installate. L'uso di questa opzione può, tuttavia, causare riferimenti interrotti nel progetto. In questi casi, potrebbe essere necessario [reinstallare gli altri pacchetti](../consume-packages/reinstalling-and-updating-packages.md).
