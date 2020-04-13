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
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380418"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="40410-104">Creazione di pacchetti di simboli (estensione snupkg)</span><span class="sxs-lookup"><span data-stu-id="40410-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="40410-105">Una buona esperienza di debug si basa sulla presenza di simboli di debug in quanto forniscono informazioni critiche come l'associazione tra il codice compilato e il codice sorgente, i nomi delle variabili locali, le tracce dello stack e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="40410-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="40410-106">È possibile utilizzare i pacchetti di simboli (con estensione snupkg) per distribuire questi simboli e migliorare l'esperienza di debug dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="40410-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40410-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="40410-107">Prerequisites</span></span>

<span data-ttu-id="40410-108">[nuget.exe v4.9.0 o versione successiva](https://www.nuget.org/downloads) o [dotnet CLI v2.2.0 o versione successiva,](https://www.microsoft.com/net/download/dotnet-core/2.2)che implementano i [protocolli NuGet](../api/nuget-protocols.md)necessari.</span><span class="sxs-lookup"><span data-stu-id="40410-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="40410-109">Creazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="40410-109">Creating a symbol package</span></span>

<span data-ttu-id="40410-110">Se si usa dotnet CLI o MSBuild, `IncludeSymbols` è `SymbolPackageFormat` necessario impostare le proprietà e per creare un file con estensione snupkg oltre al file nupkg.</span><span class="sxs-lookup"><span data-stu-id="40410-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="40410-111">Aggiungere le seguenti proprietà al file con estensione csproj:</span><span class="sxs-lookup"><span data-stu-id="40410-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="40410-112">In alternativa, specificare queste proprietà nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="40410-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="40410-113">o</span><span class="sxs-lookup"><span data-stu-id="40410-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="40410-114">Se si usa NuGet.exe, è possibile usare i comandi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:</span><span class="sxs-lookup"><span data-stu-id="40410-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="40410-115">La [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) proprietà può avere uno `symbols.nupkg` dei due `snupkg`valori seguenti: (impostazione predefinita) o .</span><span class="sxs-lookup"><span data-stu-id="40410-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="40410-116">Se questa proprietà non è specificata, verrà creato un pacchetto di simboli legacy.</span><span class="sxs-lookup"><span data-stu-id="40410-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="40410-117">Il formato legacy `.symbols.nupkg` è ancora supportato ma solo per motivi di compatibilità (vedere [Pacchetti di simboli legacy](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="40410-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="40410-118">Il server di simboli di NuGet.org accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="40410-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="40410-119">Pubblicazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="40410-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="40410-120">Per praticità, salvare prima la chiave API con NuGet (vedere [Pubblicazione di pacchetti](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="40410-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="40410-121">Dopo la pubblicazione del pacchetto principale su nuget.org, eseguire il push del pacchetto di simboli come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="40410-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="40410-122">È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali contemporaneamente usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="40410-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="40410-123">Nella cartella corrente devono essere presenti sia i file con estensione nupkg sia quelli con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="40410-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="40410-124">NuGet pubblicherà entrambi i pacchetti in nuget.org. `MyPackage.nupkg` verrà pubblicato per primo, seguito da `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="40410-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="40410-125">Se il pacchetto di simboli non viene pubblicato, verificare di aver configurato l'origine di NuGet.org come `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="40410-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="40410-126">La pubblicazione del pacchetto di simboli è supportata solo dall'[API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="40410-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="40410-127">Server di simboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="40410-127">NuGet.org symbol server</span></span>

<span data-ttu-id="40410-128">NuGet.org supporta il proprio repository del server di simboli e accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="40410-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="40410-129">I consumer di pacchetti possono usare i simboli pubblicati nel server di simboli nuget.org aggiungendo `https://symbols.nuget.org/download/symbols` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40410-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="40410-130">Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.</span><span class="sxs-lookup"><span data-stu-id="40410-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="40410-131">NuGet.org vincoli dei pacchetti di simboli di NuGet.org</span><span class="sxs-lookup"><span data-stu-id="40410-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="40410-132">NuGet.org ha i seguenti vincoli per i pacchetti di simboli:</span><span class="sxs-lookup"><span data-stu-id="40410-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="40410-133">Nei pacchetti di simboli sono consentite `.xml`solo `.psmdcp` `.rels`le seguenti estensioni di file: `.pdb`, `.nuspec`, , , , ,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="40410-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="40410-134">Solo [i file PDB portabili](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gestiti sono supportati nel server di simboli di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="40410-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="40410-135">I File PDB e le DLL nUPkg associate devono essere compilati con il compilatore in Visual Studio versione 15.9 o successiva (vedere [Hash crittografico PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="40410-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="40410-136">I pacchetti di simboli pubblicati per NuGet.org non verranno convalidati se questi vincoli non vengono soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="40410-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="40410-137">Convalida e indicizzazione dei pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="40410-137">Symbol package validation and indexing</span></span>

<span data-ttu-id="40410-138">Pacchetti di simboli pubblicati [per NuGet.org](https://www.nuget.org/) sottoposti a diverse convalide, tra cui la scansione antimalware.</span><span class="sxs-lookup"><span data-stu-id="40410-138">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="40410-139">Se un pacchetto non supera un controllo di convalida, nella relativa pagina dei dettagli del pacchetto verrà visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="40410-139">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="40410-140">Inoltre, i proprietari del pacchetto riceveranno un'e-mail con le istruzioni su come risolvere i problemi identificati.</span><span class="sxs-lookup"><span data-stu-id="40410-140">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="40410-141">Quando il pacchetto di simboli ha superato tutte le convalide, i simboli verranno indicizzati dai server di simboli di NuGet.org e saranno disponibili per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="40410-141">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="40410-142">La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="40410-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="40410-143">Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per verificare se NuGet.org si verificano interruzioni.</span><span class="sxs-lookup"><span data-stu-id="40410-143">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="40410-144">Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="40410-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="40410-145">Struttura di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="40410-145">Symbol package structure</span></span>

<span data-ttu-id="40410-146">Il pacchetto di simboli (.snupkg) presenta le seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="40410-146">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="40410-147">Il .snupkg ha lo stesso id e la stessa versione del pacchetto NuGet corrispondente (.nupkg).</span><span class="sxs-lookup"><span data-stu-id="40410-147">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="40410-148">Il .snupkg ha la stessa struttura di cartelle del corrispondente .nupkg per qualsiasi file DLL o EXE con la distinzione che invece di DLL/EXE, i corrispondenti PDU verranno inclusi nella stessa gerarchia di cartelle.</span><span class="sxs-lookup"><span data-stu-id="40410-148">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="40410-149">I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="40410-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="40410-150">Il file .nuspec del pacchetto `SymbolsPackage` di simboli ha il tipo di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="40410-150">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="40410-151">Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).</span><span class="sxs-lookup"><span data-stu-id="40410-151">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="40410-152">I seguenti campi verranno esclusi dal nuspec ```authors```di ```owners``` ```requireLicenseAcceptance```snupkg: , , , , ```license type``` ```licenseUrl```, e ```icon```.</span><span class="sxs-lookup"><span data-stu-id="40410-152">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="40410-153">Non usare l'elemento ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="40410-153">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="40410-154">Un file con estensione snupkg è coperto dalla stessa licenza del file con estensione nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="40410-154">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="40410-155">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="40410-155">See also</span></span>

<span data-ttu-id="40410-156">Prendere in considerazione l'utilizzo di Collegamento di origine per abilitare il debug del codice sorgente degli assembly .NET.</span><span class="sxs-lookup"><span data-stu-id="40410-156">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="40410-157">Per ulteriori informazioni, fare riferimento alla Guida al [collegamento di origine](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="40410-157">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="40410-158">Per altre informazioni sui pacchetti di simboli, fare riferimento alla specifica di progettazione [NuGet Package Debugging & Symbols Improvements.For](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) more information on symbol packages, please refer to the NuGet Package Debugging & Symbols Improvements design spec.</span><span class="sxs-lookup"><span data-stu-id="40410-158">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
