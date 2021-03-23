---
title: Selezionare gli assembly cui i progetti fanno riferimento
description: Rendere un subset di assembly nel pacchetto disponibile per il compilatore mentre tutti gli assembly sono disponibili al runtime.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859031"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="4b2b9-103">Selezionare gli assembly cui i progetti fanno riferimento</span><span class="sxs-lookup"><span data-stu-id="4b2b9-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="4b2b9-104">I riferimenti espliciti agli assembly consentono a un subset di assembly di essere usato per IntelliSense e per la compilazione mentre tutti gli assembly sono disponibili per il runtime.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="4b2b9-105">`PackageReference` e `packages.config` funzionano in modo diverso e di conseguenza gli autori di pacchetti devono fare attenzione a creare il pacchetto in modo che sia compatibile con entrambi i tipi di progetto.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="4b2b9-106">I riferimenti espliciti agli assembly sono correlati ad assembly .NET.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="4b2b9-107">Non è un metodo per distribuire assembly nativi chiamati tramite PInvoke da un assembly gestito.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="4b2b9-108">Supporto di `PackageReference`</span><span class="sxs-lookup"><span data-stu-id="4b2b9-108">`PackageReference` support</span></span>

<span data-ttu-id="4b2b9-109">Quando un progetto usa un pacchetto con `PackageReference` e il pacchetto contiene una directory `ref\<tfm>\`, NuGet classificherà tali assembly come asset di compilazione, mentre gli assembly `lib\<tfm>\` sono classificati come asset di runtime.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="4b2b9-110">Gli assembly in `ref\<tfm>\` non vengono usati al runtime.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="4b2b9-111">Ciò significa che qualsiasi assembly in `ref\<tfm>\` deve avere un assembly corrispondente in `lib\<tfm>\` o in una directory `runtime\` pertinente, in caso contrario potrebbero verificarsi errori di runtime.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="4b2b9-112">Poiché gli assembly in `ref\<tfm>\` non vengono usati al runtime, possono essere [assembly di soli metadati](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) in modo da ridurre le dimensioni del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="4b2b9-113">Se un pacchetto contiene l'elemento `<references>` nuspec (usato da `packages.config`, vedere di seguito) e non contiene assembly in `ref\<tfm>\`, NuGet annuncerà gli assembly elencati nell'elemento `<references>` nuspec sia come asset di compilazione che come asset di runtime.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="4b2b9-114">Ciò significa che vi saranno eccezioni di runtime quando gli assembly cui si fa riferimento dovranno caricare qualsiasi altro assembly nella directory `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="4b2b9-115">Se il pacchetto contiene una directory `runtime\`, NuGet non può usare gli asset nella directory `lib\`.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="4b2b9-116">Supporto di `packages.config`</span><span class="sxs-lookup"><span data-stu-id="4b2b9-116">`packages.config` support</span></span>

<span data-ttu-id="4b2b9-117">I progetti che usano `packages.config` per gestire i pacchetti NuGet in genere aggiungono riferimenti a tutti gli assembly nella directory `lib\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="4b2b9-118">La directory `ref\` è stata aggiunta per supportare `PackageReference` e pertanto non viene considerata quando si usa `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="4b2b9-119">Per impostare in modo esplicito gli assembly a cui viene fatto riferimento per i progetti che utilizzano `packages.config` , il pacchetto deve utilizzare l' [ `<references>` elemento nel file nuspec](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="4b2b9-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="4b2b9-120">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4b2b9-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="4b2b9-121">Il progetto `packages.config` usa un processo denominato [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) per copiare gli assembly nella directory di output `bin\<configuration>\`.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="4b2b9-122">L'assembly del progetto viene copiato, il sistema di compilazione esamina il manifesto dell'assembly per individuare gli assembly di riferimento e quindi copia gli assembly e ripete l'operazione in modo ricorsivo per tutti gli assembly.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="4b2b9-123">Questo significa che se uno degli assembly nella directory `lib\<tfm>\` non è elencato come una dipendenza nel manifesto di qualsiasi altro assembly (se l'assembly viene caricato al runtime usando `Assembly.Load`, MEF o un altro framework di inserimento delle dipendenze), potrebbe non essere copiato nella directory di output `bin\<configuration>\` del progetto pur trovandosi in `bin\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="4b2b9-124">Esempio</span><span class="sxs-lookup"><span data-stu-id="4b2b9-124">Example</span></span>

<span data-ttu-id="4b2b9-125">Il pacchetto conterrà tre assembly, `MyLib.dll`, `MyHelpers.dll` e `MyUtilities.dll`, destinati a .NET Framework 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="4b2b9-126">`MyUtilities.dll` contiene le classi destinate a essere usate solo dagli altri due assembly, pertanto l'utente non vuole che le classi vengano rese disponibili in IntelliSense o in fase di compilazione per i progetti che usano il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4b2b9-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="4b2b9-127">Il file `nuspec` deve contenere gli elementi XML seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b2b9-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="4b2b9-128">e i file nel pacchetto saranno i seguenti:</span><span class="sxs-lookup"><span data-stu-id="4b2b9-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
