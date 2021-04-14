---
title: Come pubblicare i pacchetti di simboli NuGet usando il nuovo formato di pacchetto di simboli con estensione snupkg | Microsoft Docs
author: JonDouglas
ms.author: jodou
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
ms.openlocfilehash: a62996a28348bf95e4581af180597d72cd5aa298
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387335"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="dcd0d-104">Creazione di pacchetti di simboli (estensione snupkg)</span><span class="sxs-lookup"><span data-stu-id="dcd0d-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="dcd0d-105">Una buona esperienza di debug si basa sulla presenza di simboli di debug perché forniscono informazioni critiche come l'associazione tra il codice sorgente e compilato, i nomi delle variabili locali, le analisi dello stack e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="dcd0d-106">È possibile usare i pacchetti di simboli (con estensione snupkg) per distribuire questi simboli e migliorare l'esperienza di debug dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

> <span data-ttu-id="dcd0d-107">Si noti che il pacchetto di simboli non è l'unica strategia per rendere i simboli di debug disponibili per i consumer della libreria.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-107">Note that symbol package isn't the only strategy to make the debug symbols available to the consumers of your library.</span></span> <span data-ttu-id="dcd0d-108">È anche possibile [eseguire queste operazioni `embed` ](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) in o con la proprietà di progetto `dll` `exe` seguente:`<DebugType>embedded</DebugType>`</span><span class="sxs-lookup"><span data-stu-id="dcd0d-108">It's also [possible to `embed`](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) them in the `dll` or `exe` with the following project property: `<DebugType>embedded</DebugType>`</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcd0d-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dcd0d-109">Prerequisites</span></span>

<span data-ttu-id="dcd0d-110">[nuget.exe v4.9.0 o](https://www.nuget.org/downloads) versione precedente o l'interfaccia della riga di comando [dotnet v2.2.0](https://www.microsoft.com/net/download/dotnet-core/2.2)o versione precedente, che implementano i protocolli [NuGet necessari.](../api/nuget-protocols.md)</span><span class="sxs-lookup"><span data-stu-id="dcd0d-110">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="dcd0d-111">Creazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="dcd0d-111">Creating a symbol package</span></span>

<span data-ttu-id="dcd0d-112">Se si usa l'interfaccia della riga di comando dotnet o MSBuild, è necessario impostare le proprietà e per creare un file con estensione snupkg oltre al file con estensione `IncludeSymbols` `SymbolPackageFormat` nupkg.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-112">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="dcd0d-113">Aggiungere le proprietà seguenti al file con estensione csproj:</span><span class="sxs-lookup"><span data-stu-id="dcd0d-113">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="dcd0d-114">Oppure specificare queste proprietà nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="dcd0d-114">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="dcd0d-115">oppure</span><span class="sxs-lookup"><span data-stu-id="dcd0d-115">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="dcd0d-116">Se si usa NuGet.exe, è possibile usare i comandi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:</span><span class="sxs-lookup"><span data-stu-id="dcd0d-116">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="dcd0d-117">La [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) proprietà può avere uno dei due valori seguenti: `symbols.nupkg` (impostazione predefinita) o `snupkg` .</span><span class="sxs-lookup"><span data-stu-id="dcd0d-117">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="dcd0d-118">Se questa proprietà non viene specificata, verrà creato un pacchetto di simboli legacy.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-118">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="dcd0d-119">Il formato legacy `.symbols.nupkg` è ancora supportato, ma solo per motivi di compatibilità come i pacchetti nativi (vedere [Pacchetti di simboli legacy).](Symbol-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="dcd0d-119">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons like native packages (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="dcd0d-120">Il server di simboli di NuGet.org accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-120">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="dcd0d-121">Pubblicazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="dcd0d-121">Publishing a symbol package</span></span>

1. <span data-ttu-id="dcd0d-122">Per praticità, salvare prima la chiave API con NuGet (vedere [Pubblicazione di pacchetti](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="dcd0d-122">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="dcd0d-123">Dopo la pubblicazione del pacchetto principale su nuget.org, eseguire il push del pacchetto di simboli come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-123">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="dcd0d-124">È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali contemporaneamente usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-124">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="dcd0d-125">Nella cartella corrente devono essere presenti sia i file con estensione nupkg sia quelli con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-125">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="dcd0d-126">NuGet pubblicherà entrambi i pacchetti in nuget.org. `MyPackage.nupkg` verrà pubblicato per primo, seguito da `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-126">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="dcd0d-127">Se il pacchetto di simboli non viene pubblicato, verificare di aver configurato l'origine di NuGet.org come `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-127">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="dcd0d-128">La pubblicazione del pacchetto di simboli è supportata solo dall'[API NuGet V3](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="dcd0d-128">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="dcd0d-129">Server di simboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="dcd0d-129">NuGet.org symbol server</span></span>

<span data-ttu-id="dcd0d-130">NuGet.org supporta il proprio repository del server di simboli e accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-130">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="dcd0d-131">I consumer di pacchetti possono usare i simboli pubblicati nel server di simboli nuget.org aggiungendo `https://symbols.nuget.org/download/symbols` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-131">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="dcd0d-132">Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-132">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="dcd0d-133">NuGet.org dei pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="dcd0d-133">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="dcd0d-134">NuGet.org presenta i vincoli seguenti per i pacchetti di simboli:</span><span class="sxs-lookup"><span data-stu-id="dcd0d-134">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="dcd0d-135">Nei pacchetti di simboli sono consentite solo le estensioni di file seguenti: `.pdb` , , , , , `.nuspec` `.xml` `.psmdcp` `.rels` , `.p7s`</span><span class="sxs-lookup"><span data-stu-id="dcd0d-135">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="dcd0d-136">Solo i [PDB portatili gestiti](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) sono supportati nel server di simboli di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-136">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="dcd0d-137">I file PDB e le DLL con estensione nupkg associate devono essere compilati con il compilatore in Visual Studio versione 15.9 o successiva (vedere L'hash di crittografia [PDB)](https://github.com/dotnet/roslyn/issues/24429)</span><span class="sxs-lookup"><span data-stu-id="dcd0d-137">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="dcd0d-138">I pacchetti di simboli pubblicati NuGet.org non verranno convalidati se questi vincoli non vengono soddisfatti.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-138">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

> [!NOTE]
> <span data-ttu-id="dcd0d-139">I progetti nativi, ad esempio i progetti C++, producono PDB Windows anziché PDB portatili.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-139">Native projects, such as C++ projects, produce Windows PDBs instead of Portable PDBs.</span></span> <span data-ttu-id="dcd0d-140">Questi non sono supportati dal server di simboli di NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-140">These are not supported by NuGet.org's symbol server.</span></span> <span data-ttu-id="dcd0d-141">In alternativa, [usare pacchetti di simboli](Symbol-Packages.md) legacy.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-141">Please use [Legacy Symbol Packages](Symbol-Packages.md) instead.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="dcd0d-142">Convalida e indicizzazione dei pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="dcd0d-142">Symbol package validation and indexing</span></span>

<span data-ttu-id="dcd0d-143">I pacchetti di [simboli](https://www.nuget.org/) pubblicati NuGet.org diverse convalide, tra cui l'analisi malware.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-143">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="dcd0d-144">Se un pacchetto non supera un controllo di convalida, nella pagina dei dettagli del pacchetto verrà visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-144">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="dcd0d-145">Inoltre, i proprietari del pacchetto riceveranno un messaggio di posta elettronica con istruzioni su come risolvere i problemi identificati.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-145">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="dcd0d-146">Quando il pacchetto di simboli ha superato tutte le convalide, i simboli verranno indicizzati dai server di simboli di NuGet.org e saranno disponibili per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-146">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="dcd0d-147">La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-147">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="dcd0d-148">Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per verificare se NuGet.org si verificano interruzioni.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-148">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="dcd0d-149">Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-149">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="dcd0d-150">Struttura di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="dcd0d-150">Symbol package structure</span></span>

<span data-ttu-id="dcd0d-151">Il pacchetto di simboli (con estensione snupkg) presenta le caratteristiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="dcd0d-151">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="dcd0d-152">Il file con estensione snupkg ha lo stesso ID e la stessa versione del pacchetto NuGet corrispondente (con estensione nupkg).</span><span class="sxs-lookup"><span data-stu-id="dcd0d-152">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="dcd0d-153">Il file con estensione snupkg ha la stessa struttura di cartelle del file con estensione nupkg corrispondente per tutti i file DLL o EXE con la distinzione che anziché DLL/EXE, i PDB corrispondenti verranno inclusi nella stessa gerarchia di cartelle.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-153">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="dcd0d-154">I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-154">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="dcd0d-155">Il file con estensione nuspec del pacchetto di simboli ha il `SymbolsPackage` tipo di pacchetto:</span><span class="sxs-lookup"><span data-stu-id="dcd0d-155">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="dcd0d-156">Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).</span><span class="sxs-lookup"><span data-stu-id="dcd0d-156">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="dcd0d-157">I campi seguenti verranno esclusi dal nuspec di snupkg: ```authors``` , , , , e ```owners``` ```requireLicenseAcceptance``` ```license type``` ```licenseUrl```  ```icon``` .</span><span class="sxs-lookup"><span data-stu-id="dcd0d-157">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="dcd0d-158">Non usare l'elemento ```<license>```.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-158">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="dcd0d-159">Un file con estensione snupkg è coperto dalla stessa licenza del file con estensione nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-159">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="dcd0d-160">Vedi anche</span><span class="sxs-lookup"><span data-stu-id="dcd0d-160">See also</span></span>

<span data-ttu-id="dcd0d-161">Prendere in considerazione l'uso di Collegamento all'origine per abilitare il debug del codice sorgente degli assembly .NET.</span><span class="sxs-lookup"><span data-stu-id="dcd0d-161">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="dcd0d-162">Per altre informazioni, vedere le linee guida [di Collegamento all'origine](/dotnet/standard/library-guidance/sourcelink).</span><span class="sxs-lookup"><span data-stu-id="dcd0d-162">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="dcd0d-163">Per altre informazioni sui pacchetti di simboli, vedere la specifica di progettazione NuGet Package Debugging & Symbols Improvements (Miglioramenti dei simboli [nuGet).](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)</span><span class="sxs-lookup"><span data-stu-id="dcd0d-163">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>