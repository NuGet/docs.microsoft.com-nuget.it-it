---
title: Multitargeting per i pacchetti NuGet nel file di progetto
description: Descrizione dei vari metodi per la destinazione di più versioni .NET Framework dall'interno di un singolo pacchetto NuGet nel file di progetto.
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: a05d053340bb2fe795991dfa5a2b95d8625dfd44
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774373"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Supportare più versioni di .NET Framework nel file di progetto

Quando si crea un progetto per la prima volta, si consiglia di creare una libreria di classi .NET Standard, in quanto garantisce la compatibilità con la più ampia gamma di progetti. Con .NET Standard è possibile aggiungere il [supporto multipiattaforma](/dotnet/standard/library-guidance/cross-platform-targeting) a una libreria .NET per impostazione predefinita. Tuttavia, in alcuni scenari potrebbe essere necessario includere anche codice destinato a un framework specifico. Questo articolo illustra come eseguire questa operazione per i progetti [di tipo SDK](../resources/check-project-format.md).

Per i progetti di tipo SDK, è possibile configurare il supporto per più framework di destinazione ([TFM](/dotnet/standard/frameworks)) nel file di progetto e quindi usare `dotnet pack` o `msbuild /t:pack` per creare il pacchetto.

> [!NOTE]
> L'interfaccia della riga di comando di nuget.exe non supporta i progetti di tipo SDK, quindi è consigliabile usare solo `dotnet pack` o `msbuild /t:pack`. Si consiglia di [includere tutte le proprietà](../reference/msbuild-targets.md#pack-target) che in genere si trovano nel file `.nuspec` nel file del progetto. Per usare più versioni di .NET Framework in un progetto non di tipo SDK, vedere [Supporto di più versioni di .NET Framework](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Creare un progetto che supporta più versioni di .NET Framework

1. Creare una nuova libreria di classi .NET Standard in Visual Studio o usare `dotnet new classlib`.

   Si consiglia di creare una libreria di classi .NET Standard per ottenere una compatibilità ottimale.

2. Modificare il file con estensione *csproj* per supportare i framework di destinazione. Ad esempio, modificare
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   in:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   Assicurarsi di modificare l'elemento XML modificato da singolare a plurale, ovvero aggiungere "s" ai tag di apertura e di chiusura.

3. In presenza di codice che funziona in un solo TFM, è possibile usare `#if NET45` o `#if NETSTANDARD2_0` per separare il codice dipendente dal TFM. Per ulteriori informazioni, vedere [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget). Ad esempio, è possibile usare il codice seguente:

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. Aggiungere eventuali metadati NuGet desiderati nel file *csproj* come proprietà di MSBuild.

   Per l'elenco dei metadati del pacchetto disponibili e i nomi delle proprietà di MSBuild, vedere [Destinazione per pack](../reference/msbuild-targets.md#pack-target). Vedere anche [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Se si vogliono separare le proprietà correlate alla compilazione dai metadati NuGet, è possibile usare un diverso `PropertyGroup` o inserire le proprietà NuGet in un altro file e usare la direttiva `Import` di MSBuild per includerlo. A partire da MSBuild 15.0 sono supportati anche `Directory.Build.Props` e `Directory.Build.Targets`.

5. Usare ora `dotnet pack` e il pacchetto *.nupkg* risultante sarà destinato sia a .NET Standard 2.0 che a .NET Framework 4.5.

Questo è il file *.csproj* generato con i passaggi precedenti e .NET Core SDK 2,2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Vedere anche

* [Come specificare framework di destinazione](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Specifica di destinazioni multipiattaforma](/dotnet/standard/library-guidance/cross-platform-targeting)
