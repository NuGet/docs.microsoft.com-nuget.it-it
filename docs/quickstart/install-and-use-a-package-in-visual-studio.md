---
title: Guida introduttiva all'uso di pacchetti NuGet da Visual Studio
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto di Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: a64a87319e9bc6dc992892783d00dc42db1b1dd8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818854"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Guida introduttiva: Installare e usare un pacchetto in Visual Studio

I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti. Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base. I pacchetti vengono installati in un progetto di Visual Studio usando l'interfaccia utente o la console di Gestione pacchetti. Questo articolo illustra il processo usando il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) e un progetto Universal Windows Platform (UWP). Lo stesso processo si applica a qualsiasi altro progetto .NET o .NET Core.

Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso. Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.

> [!Tip]
> **Iniziare con nuget.org**: le ricerche in nuget.org sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni. È possibile eseguire una ricerca direttamente in nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.

## <a name="prerequisites"></a>Prerequisiti

- Visual Studio 2017 con il carico di lavoro Sviluppo di app per la piattaforma UWP (Universal Windows Platform) oppure
- Visual Studio 2015 Update 3 con gli strumenti per app di Windows universali.

È possibile installare l'edizione 2017 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.

## <a name="create-a-project"></a>Creare un progetto

I pacchetti NuGet possono essere installati in qualsiasi progetto .NET, a condizione che il pacchetto supporti lo stesso framework di destinazione del progetto.

Per questa procedura dettagliata viene usata una semplice app di Windows universale (UWP). Creare un progetto in Visual Studio scegliendo **File > Nuovo progetto** e selezionando **Universale di Windows > App vuota (Windows universale)**. Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Aggiungere il pacchetto NuGet Newtonsoft.Json

Per installare il pacchetto, è possibile usare l'interfaccia utente di Gestione pacchetti o la console di Gestione pacchetti. Quando si installa un pacchetto, NuGet registra la dipendenza nel file di progetto o in un `packages.config` file. Per altre informazioni, vedere [Flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Interfaccia utente di Gestione pacchetti

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use-02-ManageNuGetPackages.png)

1. Scegliere "nuget.org" come **Origine pacchetto**, selezionare la scheda **Sfoglia**, cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e fare clic su **Installa**:

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Accettare eventuali richieste per la licenza.

1. (Visual Studio 2017) Se viene richiesto di selezionare un formato di gestione dei pacchetti, selezionare **Riferimenti al pacchetto nel file di progetto**:

    ![Selezione di un formato di gestione dei pacchetti](media/QS_Use-03b-SelectFormat.png)

1. Se viene richiesto di rivedere le modifiche, selezionare **OK**.

### <a name="package-manager-console"></a>Console di Gestione pacchetti

1. Scegliere i comandi di menu **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**.

1. Quando si apre la console, verificare che l'elenco a discesa **Progetto predefinito** mostri il progetto in cui si vuole installare il pacchetto. Se la soluzione include un solo progetto, è già selezionato.

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Immettere il comando `Install-Package Newtonsoft.json` (vedere [Install-Package](../tools/ps-ref-install-package.md)). Nella finestra della console viene mostrato l'output del comando. Gli errori indicano in genere che il pacchetto non è compatibile con il framework di destinazione del progetto.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usare l'API Newtonsoft.Json nell'app

Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.

1. Aprire `MainPage.xaml` e sostituire l'elemento `Grid` esistente con il codice seguente:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Aprire il file `MainPage.xaml.cs` (disponibile in Esplora soluzioni nel nodo `MainPage.xaml`) e inserire il codice seguente all'interno del costruttore `MainPage`:

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
    using Newtonsoft.json;
    ```

1. Compilare ed eseguire l'app premendo F5 o selezionando **Debug > Avvia debug**:

    ![Output iniziale dell'app UWP](media/QS_Use-06-AppStart.png)

1. Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:

    ![Output dell'app UWP dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Articoli correlati

- [Panoramica e flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/overview-and-workflow.md)
- [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md)
- [Modi per installare pacchetti NuGet](../consume-packages/ways-to-install-a-package.md)
- [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md)
