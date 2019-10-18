---
title: Creare un pacchetto NuGet usando MSBuild
description: Guida dettagliata al processo di progettazione e creazione di un pacchetto NuGet, incluse le principali decisioni critiche, ad esempio quelle relative ai file e al controllo delle versioni.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9512899a4086d17d2584f16833aba33efb321eae
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380695"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Creare un pacchetto NuGet usando MSBuild

Quando si crea un pacchetto NuGet dal codice, si rendono disponibili tali funzionalità in un componente condivisibile e utilizzabile da altri sviluppatori. Questo articolo descrive come creare un pacchetto usando MSBuild. MSBuild viene preinstallato con tutti i carichi di lavoro di Visual Studio che contengono NuGet. È anche possibile usare MSBuild tramite l'interfaccia della riga di comando dotnet con [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)

Per i progetti .NET Core e .NET Standard che usano il [formato di tipo SDK](../resources/check-project-format.md), e qualsiasi altro progetto di tipo SDK, NuGet usa le informazioni nel file di progetto direttamente per creare un pacchetto.  Anche per un progetto di tipo non SDK che usa `<PackageReference>`, NuGet usa il file di progetto per creare un pacchetto.

Nei progetti di tipo SDK la funzionalità pack è disponibile per impostazione predefinita. Per i progetti PackageReference di tipo non SDK, è necessario aggiungere il pacchetto NuGet.Build.Tasks.Pack alle dipendenze del progetto. Per informazioni dettagliate sulle destinazioni pack MSBuild, vedere [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md).

Il comando che crea un pacchetto, `msbuild -t:pack`, è una funzionalità equivalente a `dotnet pack`.

> [!IMPORTANT]
> Questo argomento si applica ai progetti di [tipo SDK](../resources/check-project-format.md), in genere progetti .NET Core e .NET Standard, e ai progetti di tipo non SDK che usano PackageReference.

## <a name="set-properties"></a>Imposta proprietà

Per creare un pacchetto, sono necessarie le proprietà seguenti.

- `PackageId`, ovvero l'identificatore del pacchetto, che deve essere univoco nella raccolta che ospita il pacchetto. Se non specificato, il valore predefinito è `AssemblyName`.
- `Version`, ovvero un numero di versione specifico nel formato *Principale.Secondaria.Patch[-Suffisso]* dove *-Suffisso* identifica le [versioni preliminari](prerelease-packages.md). Se non è specificato, il valore predefinito è 1.0.0.
- Titolo del pacchetto come deve essere visualizzato nell'host (ad esempio, nuget.org)
- `Authors`, ovvero informazioni sull'autore e sul proprietario. Se non specificato, il valore predefinito è `AssemblyName`.
- `Company`, ovvero il nome della società. Se non specificato, il valore predefinito è `AssemblyName`.

In Visual Studio è possibile impostare questi valori nelle proprietà del progetto (fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, scegliere **Proprietà** e selezionare la scheda **Pacchetto**). È anche possibile impostare queste proprietà direttamente nei file di progetto (con estensione *csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Assegnare al pacchetto un identificatore univoco in nuget.org o per l'origine di pacchetti in uso.

L'esempio seguente illustra un file di progetto semplice e completo con queste proprietà incluse.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

È anche possibile impostare le proprietà facoltative, ad esempio `Title`, `PackageDescription` e `PackageTags`, come descritto in [Destinazioni di pack per MSBuild](../reference/msbuild-targets.md#pack-target), [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) e [Proprietà dei metadati NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **PackageTags**, perché questi tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.

Per informazioni dettagliate sulla dichiarazione delle dipendenze e sulla specifica dei numeri di versione, vedere [Riferimenti ai pacchetti nei file di progetto](../consume-packages/package-references-in-project-files.md) e [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md). È anche possibile esporre gli asset dalle dipendenze direttamente nel pacchetto usando gli attributi `<IncludeAssets>` e `<ExcludeAssets>`. Per altre informazioni, vedere [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Scegliere un identificatore univoco del pacchetto e impostare il numero di versione

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Aggiungere il pacchetto NuGet.Build.Tasks.Pack

Se si usa MSBuild con un progetto di tipo non SDK e PackageReference, aggiungere il pacchetto NuGet.Build.Tasks.Pack al progetto.

1. Aprire il file di progetto e aggiungere quanto segue dopo l'elemento `<PropertyGroup>`:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Aprire un prompt dei comandi per gli sviluppatori digitando **Prompt dei comandi per gli sviluppatori** nella casella **Cerca**.

   In genere, è consigliabile avviare il prompt dei comandi per gli sviluppatori per Visual Studio dal menu **Start**, in modo che venga configurato con tutti i percorsi necessari per MSBuild.

3. Passare alla cartella contenente il file di progetto e digitare il comando seguente per installare il pacchetto NuGet.Build.Tasks.Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Verificare che l'output di MSBuild indichi che la compilazione è stata completata correttamente.

## <a name="run-the-msbuild--tpack-command"></a>Eseguire il comando msbuild -t:pack

Per compilare un pacchetto NuGet (un file `.nupkg`) dal progetto, eseguire il comando `msbuild -t:pack`, che consente anche di compilare automaticamente il progetto:

Al prompt dei comandi per gli sviluppatori per Visual Studio digitare il comando seguente:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

L'output mostra il percorso del file `.nupkg`.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Generare automaticamente il pacchetto in fase di compilazione

Per eseguire automaticamente `msbuild -t:pack` quando si compila o si ripristina il progetto, aggiungere la riga seguente al file di progetto all'interno di `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Quando si esegue `msbuild -t:pack` per una soluzione, vengono inseriti nel pacchetto tutti i progetti nella soluzione che supportano i pacchetti (proprietà [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) impostata su `true`).

> [!NOTE]
> Quando si genera automaticamente il pacchetto, il tempo di creazione del pacchetto aumenta il tempo di compilazione per il progetto.

### <a name="test-package-installation"></a>Testare l'installazione del pacchetto

Prima di pubblicare un pacchetto, in genere si preferisce testarne il processo di installazione in un progetto. I test assicurano che i file necessari vengano inseriti nei percorsi corretti all'interno del progetto.

È possibile testare manualmente le installazioni in Visual Studio o dalla riga di comando seguendo i normali [passaggi di installazione del pacchetto](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> I pacchetti non sono modificabili. Se si corregge un problema, modificare il contenuto del pacchetto e crearlo di nuovo. Quando si ripetono i test verrà comunque usata la versione precedente del pacchetto fino a quando non si [cancella la cartella dei pacchetti globali](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders). Questo aspetto è particolarmente importante quando si testano pacchetti che non usano un'etichetta di versione preliminare univoca per ogni compilazione.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un pacchetto, ovvero un file `.nupkg`, è possibile pubblicarlo nella raccolta di propria scelta, come descritto in [Pubblicazione di un pacchetto](../nuget-org/publish-a-package.md).

Potrebbe anche essere necessario estendere le funzionalità del pacchetto o supportare altri scenari, come descritto negli argomenti seguenti:

- [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md)
- [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md)
- [Supportare più framework di destinazione](../create-packages/multiple-target-frameworks-project-file.md)
- [Trasformazioni di file di origine e di configurazione](../create-packages/source-and-config-file-transformations.md)
- [Localizzazione](../create-packages/creating-localized-packages.md)
- [Versioni non definitive](../create-packages/prerelease-packages.md)
- [Impostare il tipo di pacchetto](../create-packages/set-package-type.md)
- [Creare pacchetti con assembly di interoperabilità COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Sono infine disponibili altri tipi di pacchetti da tenere presenti:

- [Pacchetti nativi](../guides/native-packages.md)
- [Pacchetti di simboli](../create-packages/symbol-packages-snupkg.md)
