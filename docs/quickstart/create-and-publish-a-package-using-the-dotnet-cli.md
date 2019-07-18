---
title: Creazione e pubblicazione di un pacchetto NuGet con l'interfaccia della riga di comando di dotnet
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet tramite l'interfaccia della riga di comando di .NET Core, ovvero dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 4e96d9969c8b4570ee69501d6529986f891ea4dc
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842598"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Guida introduttiva: Creare e pubblicare un pacchetto (interfaccia della riga di comando dotnet)

La creazione di un pacchetto NuGet da una libreria di classi .NET e la pubblicazione in nuget.org tramite l'interfaccia della riga di comando di `dotnet` sono un processo semplice.

## <a name="prerequisites"></a>Prerequisiti

1. Installare [.NET Core SDK](https://www.microsoft.com/net/download/), che include l'interfaccia della riga di comando di `dotnet`. A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato.

1. [Registrarsi per ottenere un account gratuito in nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se non è già disponibile. Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma. È necessario confermare l'account prima di poter caricare un pacchetto.

## <a name="create-a-class-library-project"></a>Creare un progetto di libreria di classi

È possibile usare un progetto libreria di classi .NET esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:

1. Creare una cartella denominata `AppLogger` e passare a tale cartella.

1. Creare il progetto con `dotnet new classlib`, che usa il nome della cartella corrente per il progetto.

## <a name="add-package-metadata-to-the-project-file"></a>Aggiungere i metadati del pacchetto al file di progetto

Per ogni pacchetto NuGet è necessario un manifesto che descrive i contenuti e le dipendenze del pacchetto. In un pacchetto finale, il manifesto è un file `.nuspec` generato dalle proprietà dei metadati NuGet incluse nel file di progetto.

1. Aprire il file di progetto (`.csproj`) e aggiungere le seguenti proprietà minime all'interno del tag `<PropertyGroup>` esistente, modificando i valori nel modo appropriato:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Assegnare al pacchetto un identificatore univoco in nuget.org o per l'host in uso. Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).

1. Aggiungere eventuali proprietà facoltative descritte in [Proprietà dei metadati di NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **PackageTags**, perché questi tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.

## <a name="run-the-pack-command"></a>Eseguire il comando pack

Per compilare un pacchetto NuGet (un file `.nupkg`) dal progetto, eseguire il comando `dotnet pack`, che consente anche di compilare automaticamente il progetto:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

L'output mostra il percorso del file `.nupkg`:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Generare automaticamente il pacchetto in fase di compilazione

Per eseguire automaticamente `dotnet pack` quando si esegue `dotnet build`, aggiungere la riga seguente al file di progetto all'interno di `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Pubblicare il pacchetto

Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando il comando `dotnet nuget push` insieme a una chiave API acquisita da nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Acquisire la chiave API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Pubblicare con dotnet nuget push

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Errori di pubblicazione

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Gestire il pacchetto pubblicato

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Argomenti correlati

- [Creare un pacchetto](../create-packages/creating-a-package.md)
- [Pubblicare un pacchetto](../nuget-org/publish-a-package.md)
- [Pacchetti in versione non definitiva](../create-packages/Prerelease-Packages.md)
- [Supportare più framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md)
- [Controllo delle versioni dei pacchetti](../reference/package-versioning.md)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)
- [Creazione di pacchetti di simboli](../create-packages/symbol-packages-snupkg.md)
- [Firma dei pacchetti](../create-packages/Sign-a-package.md)
