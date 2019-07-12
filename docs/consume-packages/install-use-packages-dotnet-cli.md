---
title: Installare e gestire pacchetti NuGet usando l'interfaccia della riga di comando di dotnet
description: Istruzioni per usare l'interfaccia della riga di comando di dotnet insieme a pacchetti NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a8fd525f2446f9468664f1d80ef8808127a24be7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427416"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Installare e gestire pacchetti usando l'interfaccia della riga di comando di dotnet

Lo strumento della riga di comando consente di installare, disinstallare e aggiornare facilmente pacchetti NuGet in progetti e soluzioni. Viene eseguito in Windows, Mac OS X e Linux.

L'interfaccia della riga di comando di dotnet viene usata per i progetti .NET Core e .NET Standard (tipi di progetto in stile SDK) e per qualsiasi altro progetto in stile SDK, ad esempio i progetti in stile SDK per .NET Framework. Per altre informazioni, vedere [Attributo SDK](/dotnet/core/tools/csproj#additions).

Questo articolo illustra l'utilizzo di base di alcuni dei comandi più comuni dell'interfaccia della riga di comando di dotnet. Per la maggior parte di questi comandi, lo strumento della riga di comando cerca un file di progetto nella directory corrente, a meno che non venga specificato un file di progetto nel comando. Il file di progetto è un'opzione facoltativa. Per un elenco completo dei comandi e degli argomenti che è possibile usare, vedere [Strumenti dell'interfaccia della riga di comando di .NET Core](../tools/dotnet-commands.md).

## <a name="prerequisites"></a>Prerequisiti

- [.NET Core SDK](https://www.microsoft.com/net/download/), che fornisce lo strumento da riga di comando `dotnet`. A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato.

## <a name="install-a-package"></a>Installa un pacchetto

Il comando [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.

1. Aprire una riga di comando e passare alla directory che contiene il file di progetto.

2. Usare il comando seguente per installare un pacchetto Nuget:

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    Ad esempio, per installare il pacchetto `Newtonsoft.Json`, usare il comando seguente

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. Dopo aver eseguito il comando, esaminare il file di progetto per assicurarsi che il pacchetto sia stato installato.

   È possibile aprire il file `.csproj` per visualizzare il riferimento aggiunto:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Installare una versione specifica di un pacchetto

Se la versione non viene specificata, NuGet installa la versione più recente del pacchetto. È anche possibile usare il comando [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) per installare una versione specifica di un pacchetto Nuget:

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Per aggiungere ad esempio la versione 12.0.1 del pacchetto `Newtonsoft.Json`, usare questo comando:

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Elencare i riferimenti al pacchetto

È possibile elencare i riferimenti al pacchetto per il progetto usando il comando [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).

```cli
dotnet list package
```

## <a name="remove-a-package"></a>Rimuovere un pacchetto

Usare il comando [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) per rimuovere un riferimento al pacchetto dal file di progetto.

```cli
dotnet remove package <PACKAGE_NAME>
```

Ad esempio, per rimuovere il pacchetto `Newtonsoft.Json`, usare il comando seguente

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Aggiornare un pacchetto

Se la versione del pacchetto non viene specificata, NuGet installa la versione del pacchetto più recente quando si usa il comando `dotnet add package` (opzione `-v`).

## <a name="restore-packages"></a>Ripristinare pacchetti

Usare il comando [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) che ripristina i pacchetti elencati nel file di progetto (vedere [PackageReference](../consume-packages/package-references-in-project-files.md)). Con .NET Core 2.0 e versioni successive, il ripristino viene eseguito automaticamente con `dotnet build` e `dotnet run`. A partire da NuGet 4.0, esegue lo stesso codice di `nuget restore`.

Per ripristinare un pacchetto tramite `dotnet restore`:

```cli
dotnet restore 
```