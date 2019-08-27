---
title: Come creare un pacchetto NuGet localizzato
description: Informazioni dettagliate sui due modi per creare pacchetti NuGet localizzati, ovvero includendo tutti gli assembly in un singolo pacchetto o pubblicando assembly separati.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: dbc3781bd17f815c6b32fc70b275469337148f41
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488839"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="d8322-103">Creazione di pacchetti localizzati NuGet</span><span class="sxs-lookup"><span data-stu-id="d8322-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="d8322-104">Le versioni localizzate di una libreria possono essere create in due modi:</span><span class="sxs-lookup"><span data-stu-id="d8322-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="d8322-105">Includere tutti gli assembly di risorse localizzate in un singolo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d8322-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="d8322-106">Creare pacchetti satellite localizzati separati in base a una serie di rigide convenzioni.</span><span class="sxs-lookup"><span data-stu-id="d8322-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="d8322-107">Entrambi i metodi presentano vantaggi e svantaggi, illustrati nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="d8322-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="d8322-108">Assembly di risorse localizzate in un singolo pacchetto</span><span class="sxs-lookup"><span data-stu-id="d8322-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="d8322-109">Includere gli assembly di risorse localizzate in un singolo pacchetto è in genere l'approccio più semplice.</span><span class="sxs-lookup"><span data-stu-id="d8322-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="d8322-110">A questo scopo, creare in `lib` cartelle per la lingua supportata diversa da quella predefinita del pacchetto (presumendo che sia en-us).</span><span class="sxs-lookup"><span data-stu-id="d8322-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="d8322-111">In queste cartelle è possibile inserire assembly di risorse e file XML IntelliSense localizzati.</span><span class="sxs-lookup"><span data-stu-id="d8322-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="d8322-112">La struttura di cartelle seguente, ad esempio, supporta tedesco (de), italiano (it), giapponese (ja), russo (ru), cinese (semplificato) (zh-Hans) e cinese (tradizionale) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="d8322-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="d8322-113">È possibile osservare che tutte le lingue sono elencate sotto la cartella del framework di destinazione `net40`.</span><span class="sxs-lookup"><span data-stu-id="d8322-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="d8322-114">Se si [supportano più framework](../create-packages/supporting-multiple-target-frameworks.md), si avrà una cartella sotto `lib` per ogni variante.</span><span class="sxs-lookup"><span data-stu-id="d8322-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="d8322-115">Con queste cartelle si può quindi fare riferimento a tutti i file presenti in `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="d8322-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="d8322-116">Un pacchetto di esempio che usa questo approccio è [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="d8322-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="d8322-117">Vantaggi e svantaggi (assembly di risorse localizzati)</span><span class="sxs-lookup"><span data-stu-id="d8322-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="d8322-118">La creazione di bundle che includono tutte le lingue in un singolo pacchetto presenta alcuni svantaggi:</span><span class="sxs-lookup"><span data-stu-id="d8322-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="d8322-119">**Metadati condivisi**: poiché un pacchetto NuGet può contenere un solo file `.nuspec`, è possibile fornire i metadati per una sola lingua,</span><span class="sxs-lookup"><span data-stu-id="d8322-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="d8322-120">ovvero NuGet non supporta i metadati localizzati.</span><span class="sxs-lookup"><span data-stu-id="d8322-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="d8322-121">**Dimensioni del pacchetto**: a seconda del numero di lingue supportate, le dimensioni della libreria possono aumentare considerevolmente e rallentare di conseguenza l'installazione e il ripristino del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d8322-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="d8322-122">**Rilasci simultanei**: quando si creano bundle che includono i file localizzati in un solo pacchetto, è necessario rilasciare tutti gli asset di tale pacchetto simultaneamente e non è possibile rilasciare separatamente ogni localizzazione.</span><span class="sxs-lookup"><span data-stu-id="d8322-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="d8322-123">Qualsiasi aggiornamento di qualsiasi localizzazione, inoltre, richiede una nuova versione dell'intero pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d8322-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="d8322-124">Esistono tuttavia anche alcuni vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d8322-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="d8322-125">**Semplicità**: gli utenti del pacchetto ottengono tutte le lingue supportate in una singola installazione, invece di dover installare separatamente ogni lingua.</span><span class="sxs-lookup"><span data-stu-id="d8322-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="d8322-126">Un pacchetto singolo è anche più facile da trovare su nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d8322-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="d8322-127">**Versioni accoppiate**: poiché tutti gli assembly di risorse sono nello stesso pacchetto dell'assembly primario, condividono tutti lo stesso numero di versione e non corrono il rischio di essere erroneamente disaccoppiati.</span><span class="sxs-lookup"><span data-stu-id="d8322-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="d8322-128">Pacchetti satellite localizzati</span><span class="sxs-lookup"><span data-stu-id="d8322-128">Localized satellite packages</span></span>

<span data-ttu-id="d8322-129">Analogamente al supporto di assembly satellite in .NET Framework, questo metodo separa le risorse localizzate e i file XML IntelliSense in pacchetti satellite.</span><span class="sxs-lookup"><span data-stu-id="d8322-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="d8322-130">Il pacchetto primario usa di conseguenza la convenzione di denominazione `{identifier}.{version}.nupkg` e contiene l'assembly per la lingua predefinita (ad esempio, en-US).</span><span class="sxs-lookup"><span data-stu-id="d8322-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="d8322-131">`ContosoUtilities.1.0.0.nupkg`, ad esempio, conterrà la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="d8322-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="d8322-132">Un assembly satellite usa quindi la convenzione di denominazione `{identifier}.{language}.{version}.nupkg`, ad esempio `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="d8322-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="d8322-133">L'identificatore **deve** corrispondere esattamente a quello del pacchetto primario.</span><span class="sxs-lookup"><span data-stu-id="d8322-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="d8322-134">Essendo un pacchetto separato, ha il proprio file `.nuspec` contenente i metadati localizzati.</span><span class="sxs-lookup"><span data-stu-id="d8322-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="d8322-135">Tenere presente che la lingua in `.nuspec` **deve** corrispondere a quella usata nel nome file.</span><span class="sxs-lookup"><span data-stu-id="d8322-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="d8322-136">L'assembly satellite **deve** anche dichiarare una versione esatta del pacchetto primario come dipendenza, usando la notazione di versione []. Vedere [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d8322-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="d8322-137">`ContosoUtilities.de.1.0.0.nupkg`, ad esempio, deve dichiarare una dipendenza da `ContosoUtilities.1.0.0.nupkg` usando la notazione `[1.0.0]`.</span><span class="sxs-lookup"><span data-stu-id="d8322-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="d8322-138">Il pacchetto satellite può ovviamente avere un numero di versione diverso da quello del pacchetto primario.</span><span class="sxs-lookup"><span data-stu-id="d8322-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="d8322-139">La struttura del pacchetto satellite deve quindi includere l'assembly di risorse e il file IntelliSense XML in una sottocartella che corrisponde all'elemento `{language}` del nome file del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="d8322-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="d8322-140">**Nota**: a meno che non siano necessarie impostazioni cultura secondarie specifiche, ad esempio `ja-JP`, usare sempre l'identificatore lingua di livello superiore, ad esempio `ja`.</span><span class="sxs-lookup"><span data-stu-id="d8322-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="d8322-141">In un assembly satellite NuGet riconoscerà **solo** i file nella cartella che corrisponde all'elemento `{language}` del nome file.</span><span class="sxs-lookup"><span data-stu-id="d8322-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="d8322-142">Tutti gli altri vengono ignorati.</span><span class="sxs-lookup"><span data-stu-id="d8322-142">All others are ignored.</span></span>

<span data-ttu-id="d8322-143">Quando tutte queste convenzioni sono soddisfatte, NuGet riconoscerà il pacchetto come pacchetto satellite e installerà i file localizzati nella cartella `lib` del pacchetto primario, come se in origine ne fosse stato creato un bundle.</span><span class="sxs-lookup"><span data-stu-id="d8322-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="d8322-144">La disinstallazione del pacchetto satellite rimuoverà i file provenienti dalla stessa cartella.</span><span class="sxs-lookup"><span data-stu-id="d8322-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="d8322-145">Gli assembly satellite aggiuntivi verranno creati nello stesso modo per ogni lingua supportata.</span><span class="sxs-lookup"><span data-stu-id="d8322-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="d8322-146">Per un esempio, esaminare il set di pacchetti MVC ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="d8322-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="d8322-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (inglese primario)</span><span class="sxs-lookup"><span data-stu-id="d8322-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="d8322-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (tedesco)</span><span class="sxs-lookup"><span data-stu-id="d8322-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="d8322-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (giapponese)</span><span class="sxs-lookup"><span data-stu-id="d8322-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="d8322-150">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (cinese semplificato)</span><span class="sxs-lookup"><span data-stu-id="d8322-150">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="d8322-151">[Microsoft.AspNet.Mvc.zh-Hany](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (cinese tradizionale)</span><span class="sxs-lookup"><span data-stu-id="d8322-151">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="d8322-152">Riepilogo delle convenzioni obbligatorie</span><span class="sxs-lookup"><span data-stu-id="d8322-152">Summary of required conventions</span></span>

- <span data-ttu-id="d8322-153">Il pacchetto primario deve essere denominato `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="d8322-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="d8322-154">Un pacchetto satellite deve essere denominato `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="d8322-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="d8322-155">Il file `.nuspec` di un pacchetto satellite deve specificare la lingua in modo che corrisponda al nome file.</span><span class="sxs-lookup"><span data-stu-id="d8322-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="d8322-156">Un pacchetto satellite deve dichiarare una dipendenza da una versione esatta di quello primario usando la notazione [] nel file `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d8322-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="d8322-157">Gli intervalli non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="d8322-157">Ranges are not supported.</span></span>
- <span data-ttu-id="d8322-158">Un pacchetto satellite deve inserire i file nella cartella `lib\[{framework}\]{language}` che corrisponde esattamente all'elemento `{language}` del nome file.</span><span class="sxs-lookup"><span data-stu-id="d8322-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="d8322-159">Vantaggi e svantaggi (pacchetti satellite)</span><span class="sxs-lookup"><span data-stu-id="d8322-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="d8322-160">L'uso di pacchetti satellite presenta alcuni vantaggi:</span><span class="sxs-lookup"><span data-stu-id="d8322-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="d8322-161">**Dimensioni del pacchetto**: il footprint complessivo del pacchetto primario è ridotto al minimo e agli utenti vengono addebitati solo i costi di ogni lingua che vogliono usare.</span><span class="sxs-lookup"><span data-stu-id="d8322-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="d8322-162">**Metadati separati**: ogni pacchetto satellite ha il proprio file `.nuspec` e quindi i propri metadati localizzati.</span><span class="sxs-lookup"><span data-stu-id="d8322-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="d8322-163">In questo modo alcuni utenti possono trovare più facilmente i pacchetti cercando i termini localizzati in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d8322-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="d8322-164">**Rilasci disaccoppiati**: gli assembly satellite possono essere rilasciati nel corso del tempo, invece che tutti insieme. In questo modo è possibile distribuire le attività di localizzazione.</span><span class="sxs-lookup"><span data-stu-id="d8322-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="d8322-165">I pacchetti satellite tuttavia presentano una serie di svantaggi:</span><span class="sxs-lookup"><span data-stu-id="d8322-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="d8322-166">**Confusione**: invece di un singolo pacchetto, ne esistono diversi, che possono generare un numero eccessivo di risultati della ricerca su nuget.org e un lungo elenco di riferimenti in un progetto di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8322-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="d8322-167">**Convenzioni rigide**.</span><span class="sxs-lookup"><span data-stu-id="d8322-167">**Strict conventions**.</span></span> <span data-ttu-id="d8322-168">I pacchetti satellite devono seguire esattamente le convenzioni, altrimenti le versioni localizzate non verranno selezionate correttamente.</span><span class="sxs-lookup"><span data-stu-id="d8322-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="d8322-169">**Controllo delle versioni**: ogni pacchetto satellite deve avere una dipendenza della versione esatta dal pacchetto primario.</span><span class="sxs-lookup"><span data-stu-id="d8322-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="d8322-170">Per aggiornare il pacchetto primario, potrebbe quindi essere necessario aggiornare anche tutti i pacchetti satellite, anche se le risorse non sono state modificate.</span><span class="sxs-lookup"><span data-stu-id="d8322-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
