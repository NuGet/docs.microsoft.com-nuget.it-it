---
title: Creare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 4771a30ee2ff73e68154d05f1c84efd90b584162
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774479"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Creare un pacchetto NuGet con l'interfaccia della riga di comando di dotnet

Indipendentemente dalle operazioni eseguite dal pacchetto o dal tipo di codice contenuto, è possibile usare uno degli strumenti dell'interfaccia della riga di comando, ovvero `nuget.exe` o `dotnet.exe`. per rendere disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori. Questo articolo descrive come creare un pacchetto usando l'interfaccia della riga di comando di dotnet. Per installare l' interfaccia della riga di comando di `dotnet`, vedere [Installare gli strumenti client di NuGet](../install-nuget-client-tools.md). A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet è inclusa nei carichi di lavoro di .NET Core.

Per i progetti .NET Core e .NET Standard che usano il [formato di tipo SDK](../resources/check-project-format.md), e qualsiasi altro progetto di tipo SDK, NuGet usa le informazioni nel file di progetto direttamente per creare un pacchetto. Per esercitazioni dettagliate, vedere [Creare pacchetti .NET Standard con l'interfaccia della riga di comando di dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) o [Creare pacchetti .NET Standard con Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack` dal punto di vista funzionale equivale a `dotnet pack`. Per eseguire la compilazione con MSBuild, vedere [Creare un pacchetto NuGet usando MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Questo argomento si applica ai progetti [di tipo SDK](../resources/check-project-format.md), in genere progetti .NET Core e .NET Standard.

## <a name="set-properties"></a>Impostare le proprietà

Per creare un pacchetto, sono necessarie le proprietà seguenti.

- `PackageId`, ovvero l'identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto. Se non è specificato, il valore predefinito è `AssemblyName`.
- `Version`, ovvero un numero di versione specifico nel formato *Principale.Secondaria.Patch[-Suffisso]* dove *-Suffisso* identifica le [versioni preliminari](prerelease-packages.md). Se non è specificato, il valore predefinito è 1.0.0.
- Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)
- `Authors`, ovvero informazioni sull'autore e sul proprietario. Se non è specificato, il valore predefinito è `AssemblyName`.
- `Company`, ovvero il nome della società. Se non è specificato, il valore predefinito è `AssemblyName`.

In Visual Studio è possibile impostare questi valori nelle proprietà del progetto (fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere **Proprietà** e selezionare la scheda **Pacchetto**). È anche possibile impostare queste proprietà direttamente nei file di progetto (`.csproj`).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Assegnare al pacchetto un identificatore univoco in nuget.org o per l'origine di pacchetti in uso.

L'esempio seguente illustra un file di progetto semplice e completo con queste proprietà incluse. È possibile creare un nuovo progetto predefinito usando il comando `dotnet new classlib`.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

È anche possibile impostare le proprietà facoltative, ad esempio `Title`, `PackageDescription` e `PackageTags`, come descritto in [Destinazioni di pack per MSBuild](../reference/msbuild-targets.md#pack-target), [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Proprietà dei metadati NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **PackageTags**, perché questi tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.

Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md) e [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md). È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `<IncludeAssets>` e `<ExcludeAssets>`. Per altre informazioni, vedere [controllo delle risorse di dipendenza](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Aggiungere un campo di descrizione facoltativo

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Scegliere un identificatore univoco del pacchetto e impostare il numero di versione

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Eseguire il comando pack

Per compilare un pacchetto NuGet (un file `.nupkg`) dal progetto, eseguire il comando `dotnet pack`, che consente anche di compilare automaticamente il progetto:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

L'output mostra il percorso del file `.nupkg`.

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

Quando si esegue `dotnet pack` su una soluzione, questo comprime tutti i progetti nella soluzione che possono essere compressi (la [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) proprietà è impostata su `true` ).

> [!NOTE]
> Quando si genera automaticamente il pacchetto, il tempo di creazione del pacchetto aumenta il tempo di compilazione per il progetto.

### <a name="test-package-installation"></a>Testare l'installazione del pacchetto

Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto. I test assicurano che i file necessari finiscano tutti nelle posizioni corrette del progetto.

È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> I pacchetti non sono modificabili. Se si corregge un problema, modificare il contenuto del pacchetto e crearlo di nuovo. Quando si ripetono i test verrà comunque usata la versione precedente del pacchetto fino a quando non si [cancella la cartella dei pacchetti globali](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). Questo aspetto è particolarmente importante quando si testano pacchetti che non usano un'etichetta di versione preliminare univoca per ogni compilazione.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).

Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:

- [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md)
- [Supportare più framework di destinazione](../create-packages/multiple-target-frameworks-project-file.md)
- [Icona Aggiungi pacchetto](../reference/nuspec.md#icon)
- [Trasformazioni di file di origine e di configurazione](../create-packages/source-and-config-file-transformations.md)
- [Localizzazione](../create-packages/creating-localized-packages.md)
- [Versioni non definitive](../create-packages/prerelease-packages.md)
- [Impostare il tipo di pacchetto](../create-packages/set-package-type.md)
- [Creare pacchetti con assembly di interoperabilità COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Sono infine disponibili altri tipi di pacchetti da tenere presenti:

- [Pacchetti nativi](../guides/native-packages.md)
- [Pacchetti di simboli](../create-packages/symbol-packages-snupkg.md)
