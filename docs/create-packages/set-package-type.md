---
title: Impostare un tipo di pacchetto NuGet
description: Descrizione dei tipi di pacchetto con indicazione dell'uso previsto.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774361"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="8efc7-103">Impostare un tipo di pacchetto NuGet</span><span class="sxs-lookup"><span data-stu-id="8efc7-103">Set a NuGet package type</span></span>

<span data-ttu-id="8efc7-104">Con NuGet 3.5+, i pacchetti possono essere contrassegnati con uno specifico *tipo di pacchetto* per indicarne l'uso previsto.</span><span class="sxs-lookup"><span data-stu-id="8efc7-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="8efc7-105">I pacchetti non contrassegnati con un tipo, inclusi tutti i pacchetti creati con versioni precedenti di NuGet, usano il tipo `Dependency` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="8efc7-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="8efc7-106">I pacchetti di tipo `Dependency` aggiungono asset in fase di compilazione o di esecuzione ad applicazioni e librerie e possono essere installati in qualsiasi tipo di progetto, presupponendo che siano compatibili.</span><span class="sxs-lookup"><span data-stu-id="8efc7-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="8efc7-107">I pacchetti di tipo `DotnetTool` sono estensioni dell'[interfaccia della riga di comando dotnet](/dotnet/articles/core/tools/index) e vengono richiamati dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8efc7-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="8efc7-108">Tali pacchetti possono essere installati solo nei progetti .NET Core e non hanno effetto sulle operazioni di ripristino.</span><span class="sxs-lookup"><span data-stu-id="8efc7-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="8efc7-109">Per altre informazioni su queste estensioni in base al progetto, vedere la documentazione sull'[estendibilità in .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="8efc7-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="8efc7-110">`Template` i pacchetti di tipi forniscono [modelli personalizzati](/dotnet/core/tools/custom-templates) che possono essere usati per creare file o progetti come un'app, un servizio, uno strumento o una libreria di classi.</span><span class="sxs-lookup"><span data-stu-id="8efc7-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="8efc7-111">I pacchetti di tipo personalizzato usano un identificatore di tipo arbitrario che è conforme alle stesse regole di formato degli ID dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8efc7-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="8efc7-112">I tipi diversi da `Dependency` e `DotnetTool`, tuttavia, non vengono riconosciuti da Gestione pacchetti NuGet in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8efc7-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="8efc7-113">I tipi di pacchetto vengono impostati nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="8efc7-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="8efc7-114">Per la compatibilità con le versioni precedenti è meglio *non* impostare in modo esplicito il tipo `Dependency` e basarsi invece sul fatto che NuGet presuppone questo tipo quando non viene specificato alcun tipo.</span><span class="sxs-lookup"><span data-stu-id="8efc7-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="8efc7-115">`.nuspec`: indica il tipo di pacchetto in un nodo `packageTypes\packageType` sotto l'elemento `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="8efc7-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
