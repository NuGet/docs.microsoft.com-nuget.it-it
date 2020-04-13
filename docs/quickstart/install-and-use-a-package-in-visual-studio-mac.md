---
title: Installare e usare un pacchetto NuGet in Visual Studio per MacInstall and use a NuGet package in Visual Studio for Mac
description: Un'esercitazione dettagliata sul processo di installazione e utilizzo di un pacchetto NuGet in un progetto di Visual Studio per Mac.A walkthrough tutorial on the process of installing and using a NuGet package in a Visual Studio for Mac project.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238477"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Guida introduttiva: Installare e usare un pacchetto in Visual Studio per Mac

I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti. Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base. I pacchetti vengono installati in un progetto di Visual Studio per Mac usando Gestione pacchetti NuGet.Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager. In questo articolo viene illustrato il processo utilizzando il pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) popolare e un progetto console .NET Core. Lo stesso processo si applica a qualsiasi altro progetto Xamarin o .NET Core.

Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso. Dopo avere creato il riferimento, è possibile chiamare il pacchetto tramite la relativa API.

> [!Tip]
> **Iniziare con nuget.org**: l'esplorazione *nuget.org* è il modo in cui gli sviluppatori .NET in genere trovano i componenti che possono riutilizzare nelle proprie applicazioni. È possibile eseguire una ricerca direttamente in *nuget.org* o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo. Per informazioni generali, vedere [Trovare e valutare i pacchetti NuGet](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Prerequisiti

- Visual Studio 2019 per Mac.

È possibile installare l'edizione 2019 Community gratuitamente da [visualstudio.com](https://www.visualstudio.com/) o usare le edizioni Professional o Enterprise.

Se si usa Visual Studio in Windows, vedere [Installare e usare un pacchetto in Visual Studio (solo Windows).](install-and-use-a-package-in-visual-studio.md)

## <a name="create-a-project"></a>Creare un progetto

I pacchetti NuGet possono essere installati in qualsiasi progetto .NET, a condizione che il pacchetto supporti lo stesso framework di destinazione del progetto.

Per questa procedura dettagliata, usare una semplice app console .NET Core.For this walkthrough, use a simple .NET Core Console app. Creare un progetto in Visual Studio per Mac usando **File > nuova soluzione...**, selezionare il modello Applicazione > applicazione > console di **.NET Core.** Fare clic su **Avanti**. Quando richiesto, accettare i valori predefiniti per Framework di **destinazione.**

Visual Studio crea il progetto, che viene aperto in Esplora soluzioni.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Aggiungere il pacchetto NuGet Newtonsoft.Json

Per installare il pacchetto, utilizzare Gestione pacchetti NuGet. Quando si installa un pacchetto, NuGet registra la dipendenza `packages.config` nel file di progetto o in un file (a seconda del formato del progetto). Per altre informazioni, vedere [Flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>Gestione pacchetti NuGet

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su **Dipendenze** e scegliere **Aggiungi pacchetti...**.

    ![Comando Gestisci pacchetti NuGet per i riferimenti del progetto](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. Scegliere "nuget.org" come **Origine pacchetto** nell'angolo superiore sinistro della finestra di dialogo e cercare **Newtonsoft.Json**, selezionare il pacchetto nell'elenco e selezionare **Aggiungi pacchetti...**:

    ![Individuazione del pacchetto Newtonsoft.Json](media/QS_Use_Mac-03-NewtonsoftJson.png)

    Per ulteriori informazioni su NuGet Package Manager, consultate [Installare e gestire pacchetti utilizzando Visual Studio per Mac.](../consume-packages/install-use-packages-visual-studio.md)

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usare l'API Newtonsoft.Json nell'app

Con il pacchetto Newtonsoft.Json nel progetto, è possibile chiamare il relativo metodo `JsonConvert.SerializeObject` per convertire un oggetto in una stringa leggibile.

1. Aprire `Program.cs` il file (che si trova nel riquadro della soluzione) e sostituire il contenuto del file con il codice seguente:

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. Compilare ed eseguire l'app selezionando **Esegui > avvia debug**:

1. Dopo l'esecuzione dell'app, l'output JSON serializzato verrà visualizzato nella console:

  ![Output dell'app Console](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Passaggi successivi
È stato installato e usato il primo pacchetto NuGet.

> [!div class="nextstepaction"]
> [Installare e gestire pacchetti con Visual Studio per Mac](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

Per esplorare in modo più approfondito ciò che NuGet può offrire, selezionare i collegamenti seguenti.

- [Panoramica e flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/overview-and-workflow.md)
- [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md)
