---
title: Installare e usare un pacchetto NuGet in Visual Studio
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto di Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: a2be42aeb322cfd0ab43c9cec6ad1b063cbc3089
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462497"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Guida introduttiva: Installare e usare un pacchetto in Visual Studio (solo Windows)

I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti. Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base. I pacchetti vengono installati in un progetto di Visual Studio usando Gestione pacchetti NuGet o la console di Gestione pacchetti. Questo articolo illustra il processo usando il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e un progetto Windows Presentation Foundation (WPF). Lo stesso processo si applica a qualsiasi altro progetto .NET o .NET Core.

Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso. Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.

> [!Tip]
> **Iniziare con nuget.org**: le ricerche in *nuget.org* sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni. È possibile eseguire una ricerca direttamente in *nuget.org* o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo. Per informazioni generali, vedere [Trovare e valutare i pacchetti NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Prerequisiti

- Visual Studio 2019 con il carico di lavoro Sviluppo per desktop .NET.

È possibile installare l'edizione 2019 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.

Se si usa Visual Studio per Mac, vedere [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).

## <a name="create-a-project"></a>Creare un progetto

I pacchetti NuGet possono essere installati in qualsiasi progetto .NET, a condizione che il pacchetto supporti lo stesso framework di destinazione del progetto.

Per questa procedura dettagliata, usare una semplice app WPF. Creare un progetto in Visual Studio: usare **File > Nuovo progetto**, digitare **.NET** nella casella di ricerca e quindi selezionare **App WPF (.NET Framework)** . Scegliere **Avanti**. Quando richiesto, accettare i valori predefiniti per **Framework**.

Visual Studio crea il progetto, che viene aperto in Esplora soluzioni.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Aggiungere il pacchetto NuGet Newtonsoft.Json

Per installare il pacchetto, è possibile usare Gestione pacchetti NuGet o la console di Gestione pacchetti. Quando si installa un pacchetto, NuGet registra la dipendenza nel file di progetto o in un file `packages.config`, a seconda del formato del progetto. Per altre informazioni, vedere [Flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Gestione pacchetti NuGet

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use-02-ManageNuGetPackages.png)

1. Scegliere "nuget.org" come **Origine pacchetto**, selezionare la scheda **Sfoglia**, cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e fare clic su **Installa**:

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

    Per altre informazioni su Gestione pacchetti NuGet, vedere [Installare e gestire pacchetti con Visual Studio](../consume-packages/install-use-packages-visual-studio.md).

1. Accettare eventuali richieste per la licenza.

1. (Solo Visual Studio 2017) Se viene richiesto di selezionare un formato di gestione dei pacchetti, selezionare **PackageReference nel file di progetto**:

    ![Selezione di un formato di gestione dei pacchetti](media/QS_Use-03b-SelectFormat.png)

1. Se viene richiesto di rivedere le modifiche, selezionare **OK**.

### <a name="package-manager-console"></a>Console di Gestione pacchetti

1. Scegliere i comandi di menu **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**.

1. Quando si apre la console, verificare che l'elenco a discesa **Progetto predefinito** mostri il progetto in cui si vuole installare il pacchetto. Se la soluzione include un solo progetto, è già selezionato.

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Immettere il comando `Install-Package Newtonsoft.Json` (vedere [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). Nella finestra della console viene mostrato l'output del comando. Gli errori indicano in genere che il pacchetto non è compatibile con il framework di destinazione del progetto.

   Per altre informazioni sulla console di Gestione pacchetti, vedere [Installare e gestire pacchetti con la console di Gestione pacchetti](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usare l'API Newtonsoft.Json nell'app

Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.

1. Aprire `MainWindow.xaml` e sostituire l'elemento `Grid` esistente con il codice seguente:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Aprire il file `MainWindow.xaml.cs` (disponibile in Esplora soluzioni nel nodo `MainWindow.xaml`) e inserire il codice seguente all'interno della classe `MainWindow`:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Anche se il pacchetto Newtonsoft.Json è stato aggiunto al progetto, vengono visualizzate sottolineature a zigzag rosse sotto `JsonConvert` perché è richiesta un'istruzione `using` all'inizio del file di codice:

    ```cs
    using Newtonsoft.Json;
    ```

1. Compilare ed eseguire l'app premendo F5 o selezionando **Debug > Avvia debug**:

    ![Output iniziale dell'app WPF](media/QS_Use-06-AppStart.png)

1. Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:

    ![Output dell'app WPF dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a>Passaggi successivi

È stato installato e usato il primo pacchetto NuGet.

> [!div class="nextstepaction"]
> [Installare e gestire pacchetti con Visual Studio](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Installare e gestire pacchetti con la console di Gestione pacchetti](../consume-packages/install-use-packages-powershell.md)

Per esplorare in modo più approfondito ciò che NuGet può offrire, selezionare i collegamenti seguenti.

- [Panoramica e flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/overview-and-workflow.md)
- [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md)
- [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md)
