---
title: Installare e usare un pacchetto NuGet in Visual Studio
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto di Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775532"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Guida introduttiva: installare e usare un pacchetto in Visual Studio (solo Windows)

I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti. Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base. I pacchetti vengono installati in un progetto di Visual Studio usando Gestione pacchetti NuGet, la [console di gestione pacchetti](../consume-packages/install-use-packages-powershell.md)o l'interfaccia della riga di comando [DotNet](install-and-use-a-package-using-the-dotnet-cli.md). Questo articolo illustra il processo usando il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e un progetto Windows Presentation Foundation (WPF). Lo stesso processo si applica a qualsiasi altro progetto .NET o .NET Core.

Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>` dove \<namespace\> è specifico del pacchetto in uso. Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.

> [!Tip]
> **Iniziare con NuGet.org**: l'esplorazione di *NuGet.org* è il modo in cui gli sviluppatori .NET trovano in genere i componenti che possono riutilizzare nelle proprie applicazioni. È possibile eseguire una ricerca direttamente in *nuget.org* o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo. Per informazioni generali, vedere [Trovare e valutare i pacchetti NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Prerequisiti

- Visual Studio 2019 con il carico di lavoro Sviluppo per desktop .NET.

È possibile installare l'edizione 2019 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.

Se si usa Visual Studio per Mac, vedere [installare e usare un pacchetto nel Visual Studio per Mac](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Creare un progetto

I pacchetti NuGet possono essere installati in qualsiasi progetto .NET, a condizione che il pacchetto supporti lo stesso framework di destinazione del progetto.

Per questa procedura dettagliata, usare una semplice app WPF. Creare un progetto in Visual Studio usando **file**  >  **nuovo progetto**, digitando **.NET** nella casella di ricerca e quindi selezionando l' **app WPF (.NET Framework)**. Fare clic su **Avanti**. Quando richiesto, accettare i valori predefiniti per **Framework**.

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

1. Selezionare il comando di menu **strumenti** gestione pacchetti  >  **NuGet**  >  **console** di gestione pacchetti.

1. Quando si apre la console, verificare che l'elenco a discesa **Progetto predefinito** mostri il progetto in cui si vuole installare il pacchetto. Se la soluzione include un solo progetto, è già selezionato.

    ![Selezionare un progetto per il pacchetto](media/QS_Use-08-Console1.png)

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

1. Compilare ed eseguire l'app premendo F5 o selezionando **debug**  >  **Avvia debug**:

    ![Output iniziale dell'app WPF](media/QS_Use-06-AppStart.png)

1. Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:

    ![Output dell'app WPF dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>Video correlato

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

Trova altri video su NuGet su [Channel 9](https://channel9.msdn.com/Series/NuGet-101) e [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

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
