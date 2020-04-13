---
title: Multitargeting per i pacchetti NuGet nel file di progetto
description: Descrizione dei vari metodi per selezionare come destinazione più versioni di .NET Framework da un singolo pacchetto NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380683"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="11406-103">Supportare più versioni di .NET Framework nel file di progetto</span><span class="sxs-lookup"><span data-stu-id="11406-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="11406-104">Quando si crea un progetto per la prima volta, si consiglia di creare una libreria di classi .NET Standard, in quanto garantisce la compatibilità con la più ampia gamma di progetti.</span><span class="sxs-lookup"><span data-stu-id="11406-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="11406-105">Con .NET Standard è possibile aggiungere il [supporto multipiattaforma](/dotnet/standard/library-guidance/cross-platform-targeting) a una libreria .NET per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="11406-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="11406-106">Tuttavia, in alcuni scenari potrebbe essere necessario includere anche codice destinato a un framework specifico.</span><span class="sxs-lookup"><span data-stu-id="11406-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="11406-107">Questo articolo illustra come eseguire questa operazione per i progetti [di tipo SDK](../resources/check-project-format.md).</span><span class="sxs-lookup"><span data-stu-id="11406-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="11406-108">Per i progetti di tipo SDK, è possibile configurare il supporto per più framework di destinazione ([TFM](/dotnet/standard/frameworks)) nel file di progetto e quindi usare `dotnet pack` o `msbuild /t:pack` per creare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="11406-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="11406-109">L'interfaccia della riga di comando di nuget.exe non supporta i progetti di tipo SDK, quindi è consigliabile usare solo `dotnet pack` o `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="11406-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="11406-110">Si consiglia di [includere tutte le proprietà](../reference/msbuild-targets.md#pack-target) che in genere si trovano nel file `.nuspec` nel file del progetto.</span><span class="sxs-lookup"><span data-stu-id="11406-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="11406-111">Per usare più versioni di .NET Framework in un progetto non di tipo SDK, vedere [Supporto di più versioni di .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="11406-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="11406-112">Creare un progetto che supporta più versioni di .NET Framework</span><span class="sxs-lookup"><span data-stu-id="11406-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="11406-113">Creare una nuova libreria di classi .NET Standard in Visual Studio o usare `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="11406-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="11406-114">Si consiglia di creare una libreria di classi .NET Standard per ottenere una compatibilità ottimale.</span><span class="sxs-lookup"><span data-stu-id="11406-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="11406-115">Modificare il file con estensione *csproj* per supportare i framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="11406-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="11406-116">Ad esempio, modificare</span><span class="sxs-lookup"><span data-stu-id="11406-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="11406-117">in:</span><span class="sxs-lookup"><span data-stu-id="11406-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="11406-118">Assicurarsi di modificare l'elemento XML modificato da singolare a plurale, ovvero aggiungere "s" ai tag di apertura e di chiusura.</span><span class="sxs-lookup"><span data-stu-id="11406-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="11406-119">In presenza di codice che funziona in un solo TFM, è possibile usare `#if NET45` o `#if NETSTANDARD2_0` per separare il codice dipendente dal TFM.</span><span class="sxs-lookup"><span data-stu-id="11406-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="11406-120">Per ulteriori informazioni, vedere [Come multitarget.](/dotnet/core/tutorials/libraries#how-to-multitarget) Ad esempio, è possibile utilizzare il codice seguente:For example, you can use the following code:</span><span class="sxs-lookup"><span data-stu-id="11406-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="11406-121">Aggiungere eventuali metadati NuGet desiderati nel file *csproj* come proprietà di MSBuild.</span><span class="sxs-lookup"><span data-stu-id="11406-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="11406-122">Per l'elenco dei metadati del pacchetto disponibili e i nomi delle proprietà di MSBuild, vedere [Destinazione per pack](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="11406-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="11406-123">Vedere anche [Controllo degli asset delle dipendenze](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="11406-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="11406-124">Se si vogliono separare le proprietà correlate alla compilazione dai metadati NuGet, è possibile usare un diverso `PropertyGroup` o inserire le proprietà NuGet in un altro file e usare la direttiva `Import` di MSBuild per includerlo.</span><span class="sxs-lookup"><span data-stu-id="11406-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="11406-125">A partire da MSBuild 15.0 sono supportati anche `Directory.Build.Props` e `Directory.Build.Targets`.</span><span class="sxs-lookup"><span data-stu-id="11406-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="11406-126">Usare ora `dotnet pack` e il pacchetto *.nupkg* risultante sarà destinato sia a .NET Standard 2.0 che a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="11406-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="11406-127">Questo è il file *.csproj* generato con i passaggi precedenti e .NET Core SDK 2,2.</span><span class="sxs-lookup"><span data-stu-id="11406-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="11406-128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="11406-128">See also</span></span>

* [<span data-ttu-id="11406-129">Come specificare framework di destinazione</span><span class="sxs-lookup"><span data-stu-id="11406-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="11406-130">Specifica di destinazioni multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="11406-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
