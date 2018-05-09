---
title: Riferimento a File Packages. config di NuGet
description: In alcuni tipi di progetto, il file packages.config include l'elenco aggiornato dei pacchetti NuGet usati nel progetto.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 73234f79cb9eb30327c4e206a5bc51c5bc1c6f1d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="cb272-103">Informazioni di riferimento su packages.config</span><span class="sxs-lookup"><span data-stu-id="cb272-103">packages.config reference</span></span>

<span data-ttu-id="cb272-104">Il file `packages.config` viene usato in alcuni tipi di progetto per gestire l'elenco dei pacchetti a cui fa riferimento il progetto.</span><span class="sxs-lookup"><span data-stu-id="cb272-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="cb272-105">In questo modo NuGet può ripristinare facilmente le dipendenze del progetto quando il progetto devono essere trasportato in un computer diverso, ad esempio un server di compilazione, senza tutti i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cb272-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="cb272-106">Schema</span><span class="sxs-lookup"><span data-stu-id="cb272-106">Schema</span></span>

<span data-ttu-id="cb272-107">Lo schema è semplice. Dopo l'intestazione XML standard è presente un singolo nodo `<packages>` che contiene uno o più elementi `<package>`, uno per ogni riferimento.</span><span class="sxs-lookup"><span data-stu-id="cb272-107">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="cb272-108">Ogni elemento `<package>` può avere gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb272-108">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="cb272-109">Attributo</span><span class="sxs-lookup"><span data-stu-id="cb272-109">Attribute</span></span> | <span data-ttu-id="cb272-110">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="cb272-110">Required</span></span> | <span data-ttu-id="cb272-111">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cb272-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cb272-112">ID</span><span class="sxs-lookup"><span data-stu-id="cb272-112">id</span></span> | <span data-ttu-id="cb272-113">Yes</span><span class="sxs-lookup"><span data-stu-id="cb272-113">Yes</span></span> | <span data-ttu-id="cb272-114">Identificatore del pacchetto, ad esempio Newtonsoft.json o Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="cb272-114">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="cb272-115">version</span><span class="sxs-lookup"><span data-stu-id="cb272-115">version</span></span> | <span data-ttu-id="cb272-116">Yes</span><span class="sxs-lookup"><span data-stu-id="cb272-116">Yes</span></span> | <span data-ttu-id="cb272-117">Versione esatta del pacchetto da installare, ad esempio 3.1.1 o 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="cb272-117">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="cb272-118">La stringa di versione deve includere almeno tre numeri. Il quarto numero è facoltativo, così come un suffisso di versione non definitiva.</span><span class="sxs-lookup"><span data-stu-id="cb272-118">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="cb272-119">Non sono consentiti intervalli.</span><span class="sxs-lookup"><span data-stu-id="cb272-119">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="cb272-120">targetFramework</span><span class="sxs-lookup"><span data-stu-id="cb272-120">targetFramework</span></span> | <span data-ttu-id="cb272-121">No</span><span class="sxs-lookup"><span data-stu-id="cb272-121">No</span></span> | <span data-ttu-id="cb272-122">[Moniker del framework di destinazione (TFM)](target-frameworks.md) da applicare durante l'installazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cb272-122">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="cb272-123">Viene inizialmente impostato sulla destinazione del progetto quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="cb272-123">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="cb272-124">Ne consegue che elementi `<package>` diversi possono avere moniker del framework di destinazione differenti.</span><span class="sxs-lookup"><span data-stu-id="cb272-124">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="cb272-125">Ad esempio, se si crea un progetto destinato a .NET 4.5.2, i pacchetti installati in quel punto useranno il moniker del framework di destinazione net452.</span><span class="sxs-lookup"><span data-stu-id="cb272-125">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="cb272-126">Se in un secondo momento si imposta .NET 4.6 come destinazione del progetto e si aggiungono altri pacchetti, questi useranno il moniker del framework di destinazione net46.</span><span class="sxs-lookup"><span data-stu-id="cb272-126">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="cb272-127">In caso di mancata corrispondenza tra la destinazione del progetto e gli attributi `targetFramework`, verranno generati avvisi e in tal caso è possibile reinstallare i pacchetti interessati.</span><span class="sxs-lookup"><span data-stu-id="cb272-127">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="cb272-128">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="cb272-128">allowedVersions</span></span> | <span data-ttu-id="cb272-129">No</span><span class="sxs-lookup"><span data-stu-id="cb272-129">No</span></span> | <span data-ttu-id="cb272-130">Intervallo di versioni consentite per questo pacchetto applicate durante l'aggiornamento del pacchetto (vedere [Limitazione delle versioni per l'aggiornamento](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="cb272-130">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="cb272-131">Questo attributo *non* influisce sul pacchetto installato durante un'operazione di installazione o di ripristino.</span><span class="sxs-lookup"><span data-stu-id="cb272-131">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="cb272-132">Per la sintassi, vedere [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="cb272-132">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="cb272-133">Anche l'interfaccia utente di Gestione pacchetti disabilita tutte le versioni non comprese nell'intervallo consentito.</span><span class="sxs-lookup"><span data-stu-id="cb272-133">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="cb272-134">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="cb272-134">developmentDependency</span></span> | <span data-ttu-id="cb272-135">No</span><span class="sxs-lookup"><span data-stu-id="cb272-135">No</span></span> | <span data-ttu-id="cb272-136">Se il progetto stesso che utilizza il pacchetto crea un pacchetto NuGet, l'impostazione di questo attributo su `true` per una dipendenza impedisce l'inclusione di tale pacchetto quando viene creato il pacchetto utilizzato.</span><span class="sxs-lookup"><span data-stu-id="cb272-136">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="cb272-137">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="cb272-137">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="cb272-138">Esempi</span><span class="sxs-lookup"><span data-stu-id="cb272-138">Examples</span></span>

<span data-ttu-id="cb272-139">Il file `packages.config` seguente fa riferimento a due dipendenze:</span><span class="sxs-lookup"><span data-stu-id="cb272-139">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="cb272-140">Il file `packages.config` seguente fa riferimento a nove pacchetti, ma `Microsoft.Net.Compilers` non verrà incluso durante la compilazione del pacchetto utilizzato a causa dell'attributo `developmentDependency`.</span><span class="sxs-lookup"><span data-stu-id="cb272-140">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="cb272-141">Il riferimento a Newtonsoft.Json limita inoltre gli aggiornamenti solo alle versioni 8.x e 9.x.</span><span class="sxs-lookup"><span data-stu-id="cb272-141">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
