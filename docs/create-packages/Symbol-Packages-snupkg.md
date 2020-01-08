---
title: Come pubblicare i pacchetti di simboli NuGet usando il nuovo formato di pacchetto di simboli con estensione snupkg | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Come creare pacchetti di simboli NuGet (estensione snupkg).
keywords: Pacchetti di simboli NuGet, debug dei pacchetti NuGet, supporto per il debug di NuGet, simboli in pacchetti, convenzioni dei pacchetti di simboli
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: de37cbf1f63da3de07774281eceef99c51abdaa5
ms.sourcegitcommit: 96aab8a1ad35eca0c029679d0158d9cc93d66009
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/06/2020
ms.locfileid: "75676380"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="39814-104">Creazione di pacchetti di simboli (estensione snupkg)</span><span class="sxs-lookup"><span data-stu-id="39814-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="39814-105">I pacchetti di simboli consentono di migliorare l'esperienza di debug dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="39814-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39814-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="39814-106">Prerequisites</span></span>

<span data-ttu-id="39814-107">[nuget.exe v4.9.0 o versione successiva](https://www.nuget.org/downloads) oppure [dotnet.exe v2.2.0 o versione successiva](https://www.microsoft.com/net/download/dotnet-core/2.2), che implementano i [protocolli NuGet](../api/nuget-protocols.md) necessari.</span><span class="sxs-lookup"><span data-stu-id="39814-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="39814-108">Creazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="39814-108">Creating a symbol package</span></span>

<span data-ttu-id="39814-109">Se si usa dotnet. exe o MSBuild, è necessario impostare le proprietà `IncludeSymbols` e `SymbolPackageFormat` per creare un file con estensione snupkg oltre al file nupkg.</span><span class="sxs-lookup"><span data-stu-id="39814-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="39814-110">Aggiungere le proprietà seguenti al file con estensione csproj:</span><span class="sxs-lookup"><span data-stu-id="39814-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="39814-111">In alternativa, specificare le proprietà seguenti nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="39814-111">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="39814-112">oppure</span><span class="sxs-lookup"><span data-stu-id="39814-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="39814-113">Se si usa NuGet.exe, è possibile usare i comandi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:</span><span class="sxs-lookup"><span data-stu-id="39814-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="39814-114">La proprietà [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) può avere uno dei due valori seguenti: `symbols.nupkg` (predefinito) o `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="39814-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="39814-115">Se questa proprietà non è specificata, verrà creato un pacchetto di simboli legacy.</span><span class="sxs-lookup"><span data-stu-id="39814-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="39814-116">Il formato legacy `.symbols.nupkg` è ancora supportato ma solo per motivi di compatibilità (vedere [Pacchetti di simboli legacy](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="39814-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="39814-117">Il server di simboli di NuGet.org accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="39814-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="39814-118">Pubblicazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="39814-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="39814-119">Per praticità, salvare prima la chiave API con NuGet (vedere [Pubblicazione di pacchetti](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="39814-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="39814-120">Dopo la pubblicazione del pacchetto principale su nuget.org, eseguire il push del pacchetto di simboli come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="39814-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="39814-121">È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali contemporaneamente usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="39814-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="39814-122">Nella cartella corrente devono essere presenti sia i file con estensione nupkg sia quelli con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="39814-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="39814-123">NuGet pubblicherà entrambi i pacchetti in nuget.org. `MyPackage.nupkg` verrà pubblicato per primo, seguito da `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="39814-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="39814-124">Se il pacchetto di simboli non viene pubblicato, verificare di aver configurato l'origine di NuGet.org come `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="39814-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="39814-125">La pubblicazione del pacchetto di simboli è supportata solo dall'[API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="39814-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="39814-126">Server di simboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="39814-126">NuGet.org symbol server</span></span>

<span data-ttu-id="39814-127">NuGet.org supporta il proprio repository del server di simboli e accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="39814-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="39814-128">I consumer di pacchetti possono usare i simboli pubblicati nel server di simboli nuget.org aggiungendo `https://symbols.nuget.org/download/symbols` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39814-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="39814-129">Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.</span><span class="sxs-lookup"><span data-stu-id="39814-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="39814-130">Vincoli del pacchetto di simboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="39814-130">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="39814-131">NuGet.org presenta i vincoli seguenti per i pacchetti di simboli:</span><span class="sxs-lookup"><span data-stu-id="39814-131">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="39814-132">Nei pacchetti di simboli sono consentite solo le estensioni di file seguenti: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels``.p7s`</span><span class="sxs-lookup"><span data-stu-id="39814-132">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="39814-133">Nel server di simboli di NuGet. org sono supportati solo [PDB portatili](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gestiti.</span><span class="sxs-lookup"><span data-stu-id="39814-133">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="39814-134">I PDB e le dll nupkg associate devono essere compilati con il compilatore in Visual Studio versione 15,9 o successiva (vedere l' [hash Crypto PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="39814-134">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="39814-135">Se questi vincoli non vengono soddisfatti, i pacchetti di simboli pubblicati in NuGet.org non verranno convalidati.</span><span class="sxs-lookup"><span data-stu-id="39814-135">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="39814-136">Convalida e indicizzazione dei pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="39814-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="39814-137">I pacchetti di simboli pubblicati in [NuGet.org](https://www.nuget.org/) vengono sottoposti a diverse convalide, inclusa l'analisi di malware.</span><span class="sxs-lookup"><span data-stu-id="39814-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="39814-138">Se un pacchetto non supera un controllo di convalida, nella pagina dei dettagli del pacchetto verrà visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="39814-138">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="39814-139">Inoltre, i proprietari del pacchetto riceveranno un messaggio di posta elettronica con le istruzioni su come risolvere i problemi identificati.</span><span class="sxs-lookup"><span data-stu-id="39814-139">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="39814-140">Quando il pacchetto di simboli ha superato tutte le convalide, i simboli verranno indicizzati dai server dei simboli di NuGet. org.</span><span class="sxs-lookup"><span data-stu-id="39814-140">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers.</span></span> <span data-ttu-id="39814-141">Una volta indicizzate, il simbolo sarà disponibile per l'utilizzo da parte dei server di simboli NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="39814-141">Once indexed, the symbol will be available for consumption from the NuGet.org symbol servers.</span></span>

<span data-ttu-id="39814-142">La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="39814-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="39814-143">Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per controllare se si stanno verificando interruzioni in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="39814-143">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="39814-144">Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="39814-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="39814-145">Struttura di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="39814-145">Symbol package structure</span></span>

<span data-ttu-id="39814-146">Il file con estensione nupkg è esattamente lo stesso di oggi, ma il file con estensione snupkg presenta le caratteristiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="39814-146">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="39814-147">Il file con estensione snupkg avrà lo stesso ID e versione del file con estensione nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="39814-147">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="39814-148">Il file con estensione snupkg avrà la struttura di cartelle del pacchetto nupkg per tutti i file DLL o EXE con la differenza che, invece di DLL/exe, i file PDB corrispondenti verranno inclusi nella stessa gerarchia di cartelle.</span><span class="sxs-lookup"><span data-stu-id="39814-148">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="39814-149">I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="39814-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="39814-150">Il file con estensione nuspec nel pacchetto con estensione snupkg specificherà anche un nuovo PackageType come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="39814-150">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="39814-151">Deve essere l'unico PackageType specificato.</span><span class="sxs-lookup"><span data-stu-id="39814-151">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="39814-152">Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).</span><span class="sxs-lookup"><span data-stu-id="39814-152">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="39814-153">I campi ```authors``` e ```owners``` verranno esclusi dal file con estensione nuspec del pacchetto con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="39814-153">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="39814-154">Non usare l'elemento ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="39814-154">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="39814-155">Un file con estensione snupkg è coperto dalla stessa licenza del file con estensione nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="39814-155">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="39814-156">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="39814-156">See also</span></span>

<span data-ttu-id="39814-157">Provare a usare il collegamento di origine per abilitare il debug del codice sorgente degli assembly .NET.</span><span class="sxs-lookup"><span data-stu-id="39814-157">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="39814-158">Per ulteriori informazioni, consultare le [linee guida](/dotnet/standard/library-guidance/sourcelink)per il collegamento all'origine.</span><span class="sxs-lookup"><span data-stu-id="39814-158">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="39814-159">Per altre informazioni sui pacchetti di simboli, fare riferimento alla specifica di [debug del pacchetto NuGet & simboli](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) di progettazione.</span><span class="sxs-lookup"><span data-stu-id="39814-159">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
