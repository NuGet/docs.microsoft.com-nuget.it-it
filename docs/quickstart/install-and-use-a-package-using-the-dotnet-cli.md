---
title: Installare e usare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet
description: Esercitazione dettagliata sul processo di installazione e uso di un pacchetto NuGet in un progetto .NET Core.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231276"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Guida introduttiva: Installare e usare un pacchetto con l'interfaccia della riga di comando di dotnet

I pacchetti NuGet contengono codice riutilizzabile che altri sviluppatori rendono disponibile per l'uso nei progetti. Vedere [Che cos'è NuGet?](../What-is-NuGet.md) per le informazioni di base. I pacchetti vengono installati in un progetto .NET Core usando il comando `dotnet add package`, come descritto in questo articolo per il famoso pacchetto [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/).

Al termine dell'installazione, fare riferimento al pacchetto nel codice con `using <namespace>`, dove \<spazio dei nomi\> è specifico per il pacchetto in uso. È quindi possibile usare l'API del pacchetto.

> [!Tip]
> **Iniziare con nuget.org**: le ricerche in nuget.org sono il modo in cui gli sviluppatori di .NET individuano in genere componenti che possono riutilizzare nelle loro applicazioni. È possibile eseguire una ricerca direttamente in nuget.org o trovare e installare pacchetti all'interno di Visual Studio, come illustrato in questo articolo.

## <a name="prerequisites"></a>Prerequisites

- [.NET Core SDK](https://www.microsoft.com/net/download/), che fornisce lo strumento da riga di comando `dotnet`. A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato.

## <a name="create-a-project"></a>Creare un progetto

I pacchetti NuGet possono essere installati in un progetto .NET di qualche tipo. Per questa procedura dettagliata creare un progetto console .NET Core semplice come segue:

1. Creare una cartella per il progetto.

1. Aprire un prompt dei comandi e passare alla nuova cartella.

1. Creare il progetto usando il comando seguente:

    ```dotnetcli
    dotnet new console
    ```

1. Usare `dotnet run` per verificare che l'app sia stata creata correttamente.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Aggiungere il pacchetto NuGet Newtonsoft.Json

1. Usare il comando seguente per installare il pacchetto `Newtonsoft.json`.

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Al termine dell'esecuzione del comando, aprire il file `.csproj` per vedere il riferimento aggiunto:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Usare l'API Newtonsoft.Json nell'app

1. Aprire il file `Program.cs` e aggiungere la riga seguente all'inizio del file:

    ```cs
    using Newtonsoft.Json;
    ```

1. Aggiungere il codice seguente prima della riga `class Program`:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Sostituire la funzione `Main` con il codice seguente:

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. Compilare ed eseguire l'app usando il comando `dotnet run`. L'output deve essere la rappresentazione JSON dell'oggetto `Account` nel codice:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>Video correlato

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

Trova altri video su NuGet su [Channel 9](https://channel9.msdn.com/Series/NuGet-101) e [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Passaggi successivi

È stato installato e usato il primo pacchetto NuGet.

> [!div class="nextstepaction"]
> [Installare e usare pacchetti tramite l'interfaccia della riga di comando di dotnet](../consume-packages/install-use-packages-dotnet-cli.md)

Per esplorare in modo più approfondito ciò che NuGet può offrire, selezionare i collegamenti seguenti.

- [Panoramica e flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/overview-and-workflow.md)
- [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md)
- [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md)
