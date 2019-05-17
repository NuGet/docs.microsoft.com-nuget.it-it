---
title: Come pubblicare i pacchetti di simboli NuGet usando il nuovo formato di pacchetto di simboli con estensione snupkg | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
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
ms.openlocfilehash: 18d54e28d77f2bdcfea70ff9ae9def05278cb26c
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610564"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="8146e-104">Creazione di pacchetti di simboli (estensione snupkg)</span><span class="sxs-lookup"><span data-stu-id="8146e-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="8146e-105">I pacchetti di simboli consentono di migliorare l'esperienza di debug dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="8146e-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8146e-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8146e-106">Prerequisites</span></span>

<span data-ttu-id="8146e-107">[nuget.exe v4.9.0 o versione successiva](https://www.nuget.org/downloads) oppure [dotnet.exe v2.2.0 o versione successiva](https://www.microsoft.com/net/download/dotnet-core/2.2), che implementano i [protocolli NuGet](../api/nuget-protocols.md) necessari.</span><span class="sxs-lookup"><span data-stu-id="8146e-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="8146e-108">Creazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="8146e-108">Creating a symbol package</span></span>

<span data-ttu-id="8146e-109">È possibile creare un pacchetto di simboli snupkg tramite dotnet.exe, NuGet.exe o MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8146e-109">You can create a snupkg symbol package using dotnet.exe, NuGet.exe, or MSBuild.</span></span> <span data-ttu-id="8146e-110">Se si usa NuGet.exe, è possibile usare i comandi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:</span><span class="sxs-lookup"><span data-stu-id="8146e-110">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="8146e-111">Se si usa dotnet.exe o MSBuild, è possibile usare i passaggi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:</span><span class="sxs-lookup"><span data-stu-id="8146e-111">If you're using dotnet.exe or MSBuild, use the following steps to create a .snupkg file in addition to the .nupkg file:</span></span>

1. <span data-ttu-id="8146e-112">Aggiungere le proprietà seguenti al file con estensione csproj:</span><span class="sxs-lookup"><span data-stu-id="8146e-112">Add the following properties to your .csproj file:</span></span>

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. <span data-ttu-id="8146e-113">Eseguire un pacchetto del progetto con `dotnet pack MyPackage.csproj` o `msbuild -t:pack MyPackage.csproj`.</span><span class="sxs-lookup"><span data-stu-id="8146e-113">Pack your project with `dotnet pack MyPackage.csproj` or `msbuild -t:pack MyPackage.csproj`.</span></span>

<span data-ttu-id="8146e-114">La proprietà [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) può avere uno dei due valori seguenti: `symbols.nupkg` (predefinito) o `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="8146e-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="8146e-115">Se non viene specificata la proprietà [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat), verrà creato un pacchetto di simboli legacy.</span><span class="sxs-lookup"><span data-stu-id="8146e-115">If the [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="8146e-116">Il formato legacy `.symbols.nupkg` è ancora supportato ma solo per motivi di compatibilità (vedere [Pacchetti di simboli legacy](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="8146e-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="8146e-117">Il server di simboli di NuGet.org accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="8146e-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="8146e-118">Pubblicazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="8146e-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="8146e-119">Per praticità, salvare prima la chiave API con NuGet (vedere [Pubblicazione di pacchetti](../create-packages/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="8146e-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="8146e-120">Dopo la pubblicazione del pacchetto principale su nuget.org, eseguire il push del pacchetto di simboli come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8146e-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="8146e-121">È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali contemporaneamente usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8146e-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="8146e-122">Nella cartella corrente devono essere presenti sia i file con estensione nupkg sia quelli con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="8146e-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="8146e-123">NuGet pubblicherà entrambi i pacchetti in nuget.org. `MyPackage.nupkg` verrà pubblicato per primo, seguito da `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="8146e-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="8146e-124">Se il pacchetto di simboli non viene pubblicato, verificare di aver configurato l'origine di NuGet.org come `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="8146e-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="8146e-125">La pubblicazione del pacchetto di simboli è supportata solo dall'[API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="8146e-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="8146e-126">Server di simboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="8146e-126">NuGet.org symbol server</span></span>

<span data-ttu-id="8146e-127">NuGet.org supporta il proprio repository del server di simboli e accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="8146e-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="8146e-128">I consumer di pacchetti possono usare i simboli pubblicati nel server di simboli nuget.org aggiungendo `https://symbols.nuget.org/download/symbols` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8146e-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="8146e-129">Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) per informazioni dettagliate su questo processo.</span><span class="sxs-lookup"><span data-stu-id="8146e-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="8146e-130">Vincoli del pacchetto di simboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="8146e-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="8146e-131">I pacchetti di simboli supportati in nuget.org hanno i vincoli seguenti</span><span class="sxs-lookup"><span data-stu-id="8146e-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="8146e-132">Solo le estensioni di file seguenti possono essere aggiunte a un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="8146e-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="8146e-133">Solo i [file PDB portatili](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gestiti sono attualmente supportati nel server di simboli nuget.</span><span class="sxs-lookup"><span data-stu-id="8146e-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="8146e-134">Il file PDB e DLL nupkg associati devono essere compilati con il compilatore in Visual Studio versione 15.9 o versione successiva (vedere la pagina sulla [funzione crittografica di hash dei file PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="8146e-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="8146e-135">La pubblicazione del pacchetto di simboli in nuget.org avrà esito negativo se nel file con estensione snupkg sono inclusi altri tipi di file.</span><span class="sxs-lookup"><span data-stu-id="8146e-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="8146e-136">Convalida e indicizzazione dei pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="8146e-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="8146e-137">I pacchetti di simboli pubblicati in [NuGet.org](https://www.nuget.org/) vengono sottoposti a diverse convalide, ad esempio il controllo antivirus.</span><span class="sxs-lookup"><span data-stu-id="8146e-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="8146e-138">Quando il pacchetto ha superato tutti i controlli di convalida, potrebbe essere necessario un po' di tempo prima che i simboli vengano indicizzati e siano disponibili per l'utilizzo dai server di simboli NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="8146e-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="8146e-139">Se il pacchetto non supera un controllo di convalida, la pagina dei dettagli del pacchetto per il file con estensione nupkg verrà aggiornata con l'errore associato e si riceverà anche una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="8146e-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="8146e-140">La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="8146e-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="8146e-141">Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per controllare se si stanno verificando interruzioni in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8146e-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="8146e-142">Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="8146e-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="8146e-143">Struttura di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="8146e-143">Symbol package structure</span></span>

<span data-ttu-id="8146e-144">Il file con estensione nupkg è esattamente lo stesso di oggi, ma il file con estensione snupkg presenta le caratteristiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="8146e-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="8146e-145">Il file con estensione snupkg avrà lo stesso ID e versione del file con estensione nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="8146e-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="8146e-146">Il file con estensione snupkg avrà la struttura di cartelle del pacchetto nupkg per tutti i file DLL o EXE con la differenza che, invece di DLL/exe, i file PDB corrispondenti verranno inclusi nella stessa gerarchia di cartelle.</span><span class="sxs-lookup"><span data-stu-id="8146e-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="8146e-147">I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="8146e-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="8146e-148">Il file con estensione nuspec nel pacchetto con estensione snupkg specificherà anche un nuovo PackageType come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8146e-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="8146e-149">Deve essere l'unico PackageType specificato.</span><span class="sxs-lookup"><span data-stu-id="8146e-149">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="8146e-150">Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).</span><span class="sxs-lookup"><span data-stu-id="8146e-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="8146e-151">I campi ```authors``` e ```owners``` verranno esclusi dal file con estensione nuspec del pacchetto con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="8146e-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="8146e-152">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8146e-152">See Also</span></span>

<span data-ttu-id="8146e-153">[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) (Debug del pacchetto NuGet e miglioramenti dei simboli)</span><span class="sxs-lookup"><span data-stu-id="8146e-153">[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)</span></span>
