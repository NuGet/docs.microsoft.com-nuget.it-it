---
title: Guida introduttiva all'uso di pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: Un'esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto.
keywords: installare NuGet, utilizzo di un pacchetto NuGet, installazione di pacchetti NuGet, riferimenti ai pacchetti NuGet, uso di pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bcccc7139de31a8d07e9ed52abfd12fe9e6d687b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="install-and-use-a-package"></a>Installare e usare un pacchetto

[!INCLUDE [install-methods](../includes/install-methods.md)]

Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso. Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.

La parte restante di questo argomento illustra il processo di utilizzo dell'interfaccia utente di Gestione pacchetti per installare il popolare pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) in un progetto di piattaforma UWP (Universal Windows Platform). Viene quindi illustrato un esempio di uso del pacchetto. Si usa un flusso di lavoro analogo per quasi tutti i pacchetti NuGet usati in un progetto.

- [Installare i prerequisiti](#install-pre-requisites)
- [Creare un progetto](#create-a-project)
- [Aggiungere il pacchetto NuGet Newtonsoft.Json](#add-the-newtonsoftjson-nuget-package)
- [Usare l'API Newtonsoft.Json nell'app](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Iniziare con nuget.org**: l'installazione di pacchetti da nuget.org è un flusso di lavoro comune che gli sviluppatori .NET usano per trovare componenti riutilizzabili nelle loro applicazioni. È sempre possibile eseguire una ricerca direttamente su nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo argomento.

## <a name="install-pre-requisites"></a>Installare i prerequisiti

Questa esercitazione richiede Visual Studio 2015 Update 3 con Strumenti per app di Windows universale o Visual Studio 2017 con il carico di lavoro Sviluppo di app per la piattaforma UWP (Universal Windows Platform). Se Visual Studio è già installato, è possibile eseguire nuovamente il programma di installazione per aggiungere gli strumenti per la piattaforma UWP.

È possibile installare l'edizione Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise. 

## <a name="create-a-project"></a>Creare un progetto

Per installare un pacchetto NuGet, è necessario un progetto basato su .NET in Visual Studio. Per questa procedura dettagliata è possibile usare una semplice app di Windows Presentation Foundation (WPF) o di Windows universale (UWP):

- Per WPF (Windows 7+), scegliere **File > Nuovo > Progetto**, espandere **Visual C#**, selezionare **Desktop classico di Windows > App WPF (.NET Framework)** e scegliere **OK**.
- Per UWP (Windows 10), usare invece **Universale di Windows > App vuota (Windows universale)**. Accettare i valori predefiniti per Versione di destinazione e Versione minima quando richiesto.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Aggiungere il pacchetto NuGet Newtonsoft.Json

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use-02-ManageNuGetPackages.png)

1. Scegliere "nuget.org" come **Origine pacchetto**, selezionare la scheda **Sfoglia**, cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e fare clic su **Installa**:

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Se viene richiesto di selezionare un formato di gestione del pacchetto, scegliere tra PackageReference (scelta consigliata) e `packages.config`:

    ![Selezione di un formato di riferimento del pacchetto](media/QS_Use-03b-SelectFormat.png)

1. Se viene richiesto di rivedere le modifiche, selezionare **OK**.

1. Fare clic con il pulsante destro del mouse sulla soluzione in Esplora soluzioni e selezionare **Compila soluzione**. Ciò consente di ripristinare i pacchetti NuGet elencati in **Riferimenti**. Per maggiori dettagli, vedere [Ripristino di pacchetti](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usare l'API Newtonsoft.Json nell'app

Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.

1. Aprire `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) e sostituire l'elemento `Grid` esistente con il codice seguente:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Espandere il nodo `MainWindow.xaml` (WPF) o `MainPage.xaml` (UWP) in Esplora soluzioni, aprire il file `.cs` e inserire il codice seguente all'interno della classe `MainWindow` o `MainPage`, dopo il costruttore:

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

1. Anche se il pacchetto Newtonsoft.Json è stato aggiunto al progetto, vengono visualizzate sottolineature a zigzag rosse sotto `JsonConvert` perché è richiesta un'istruzione `using`. Passare il mouse sulla sottolineatura di `JsonConvert`: verrà visualizzato un indicatore Lampadina con l'opzione **Mostra possibili correzioni**:

    ![Indicatore Lampadina con il comando Mostra possibili correzioni](media/QS_Use-04-ShowPotentialFixes.png)


1. Fare clic su **Mostra possibili correzioni** (o sull'indicatore Lampadina) e selezionare la prima correzione suggerita, `using Newtonsoft.Json;`. La riga necessaria verrà aggiunta all'inizio del file.

    ![Indicatore Lampadina con l'opzione per l'aggiunta di un'istruzione Using](media/QS_Use-05-AddUsing.png)

1. Compilare ed eseguire l'app premendo F5 o selezionando **Debug > Avvia debug** (in questa immagine è illustrato UWP, per WPF la schermata è simile):

    ![Output iniziale dell'app UWP](media/QS_Use-06-AppStart.png)

1. Selezionare il pulsante per visualizzare il contenuto del controllo TextBlock sostituito con testo JSON:

    ![Output dell'app UWP dopo la selezione del pulsante](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>Argomenti correlati

- [Panoramica e flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/overview-and-workflow.md)
- [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md)
- [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md)
