---
title: Impostare un tipo di pacchetto NuGet
description: Descrizione dei tipi di pacchetto con indicazione dell'uso previsto.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067278"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="d4fa9-103">Impostare un tipo di pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="d4fa9-103">Set a NuGet package type</span></span>

<span data-ttu-id="d4fa9-104">I pacchetti possono essere contrassegnati con uno o *più tipi di pacchetto* per indicare l'utilizzo previsto.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="d4fa9-105">Tipi di pacchetto noti</span><span class="sxs-lookup"><span data-stu-id="d4fa9-105">Known package types</span></span>

- <span data-ttu-id="d4fa9-106">I pacchetti di tipo `Dependency` aggiungono asset in fase di compilazione o di esecuzione ad applicazioni e librerie e possono essere installati in qualsiasi tipo di progetto, presupponendo che siano compatibili.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="d4fa9-107">`DotnetTool` I pacchetti di tipo sono strumenti .NET che possono essere installati dall'interfaccia della [riga di comando dotnet](/dotnet/articles/core/tools/index).</span><span class="sxs-lookup"><span data-stu-id="d4fa9-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="d4fa9-108">`Template` I pacchetti di tipo [forniscono modelli](/dotnet/core/tools/custom-templates) personalizzati che possono essere usati per creare file o progetti come un'app, un servizio, uno strumento o una libreria di classi.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="d4fa9-109">I pacchetti non contrassegnati con un tipo, inclusi tutti i pacchetti creati con versioni precedenti di NuGet, usano il tipo `Dependency` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="d4fa9-110">Il supporto per i tipi di pacchetto è stato aggiunto in NuGet 3.5.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="d4fa9-111">Se non è necessario un tipo di pacchetto personalizzato, è meglio non *impostare* in modo esplicito il tipo di pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="d4fa9-112">NuGet viene utilizzato per impostazione `Dependency` predefinita per il tipo quando non viene specificato alcun tipo.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="d4fa9-113">Tipi di pacchetto personalizzati</span><span class="sxs-lookup"><span data-stu-id="d4fa9-113">Custom package types</span></span>

<span data-ttu-id="d4fa9-114">È possibile contrassegnare il pacchetto con uno o più tipi di pacchetto personalizzati se il relativo utilizzo non corrisponde ai [tipi di pacchetto noti](#known-package-types).</span><span class="sxs-lookup"><span data-stu-id="d4fa9-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="d4fa9-115">Si supponga, ad esempio, che i clienti `Contoso` dell'app possano installare le estensioni.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="d4fa9-116">L'app potrebbe richiedere agli autori di estensioni di usare il tipo di pacchetto personalizzato per identificare i pacchetti come `ContosoExtension` estensioni appropriate che seguono le convenzioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="d4fa9-117">Un pacchetto con un tipo di pacchetto personalizzato non può essere installato Visual Studio o nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="d4fa9-118">Per [altre informazioni, vedere NuGet/Home#10468.](https://github.com/NuGet/Home/issues/10468)</span><span class="sxs-lookup"><span data-stu-id="d4fa9-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="d4fa9-119">Uso dell'interfaccia della riga di comando dotnet</span><span class="sxs-lookup"><span data-stu-id="d4fa9-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="d4fa9-120">I tipi di pacchetto possono essere impostati nel file di progetto ( `.csproj` ):</span><span class="sxs-lookup"><span data-stu-id="d4fa9-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="d4fa9-121">I pacchetti con più usi specifici possono essere contrassegnati con più tipi di pacchetto usando `;` il delimitatore :</span><span class="sxs-lookup"><span data-stu-id="d4fa9-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="d4fa9-122">È possibile eseguire il controllo delle versioni dei tipi di pacchetto usando un `,` delimitatore tra il tipo di pacchetto e la relativa [`Version`](/dotnet/api/system.version) stringa:</span><span class="sxs-lookup"><span data-stu-id="d4fa9-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="d4fa9-123">Uso di nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d4fa9-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="d4fa9-124">I tipi di pacchetto vengono impostati nel `.nuspec` file all'interno `packageTypes\packageType` di un nodo sotto `<metadata>` l'elemento :</span><span class="sxs-lookup"><span data-stu-id="d4fa9-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="d4fa9-125">I pacchetti con più usi specifici possono essere contrassegnati con più tipi di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="d4fa9-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="d4fa9-126">È possibile eseguire il controllo delle versioni dei tipi di pacchetto usando una [`Version`](/dotnet/api/system.version) stringa:</span><span class="sxs-lookup"><span data-stu-id="d4fa9-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="d4fa9-127">Il formato di una stringa di tipo pacchetto è esattamente come un ID pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="d4fa9-128">In altri casi, un tipo di pacchetto è una stringa senza distinzione tra maiuscole e minuscole corrispondente all'espressione regolare con almeno un carattere e al massimo `^\w+([_.-]\w+)*$` 100 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="d4fa9-129">Se specificato, la versione del tipo di pacchetto è una [`Version`](/dotnet/api/system.version) stringa.</span><span class="sxs-lookup"><span data-stu-id="d4fa9-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="d4fa9-130">La versione del tipo di pacchetto è facoltativa e il valore predefinito è `0.0` .</span><span class="sxs-lookup"><span data-stu-id="d4fa9-130">The package type version is optional and defaults to `0.0`.</span></span>
