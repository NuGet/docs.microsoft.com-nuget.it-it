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
ms.openlocfilehash: 48ca4b62e722988b3dfe69306565d7f159805962
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453455"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="d892c-104">Creazione di pacchetti di simboli (estensione snupkg)</span><span class="sxs-lookup"><span data-stu-id="d892c-104">Creating symbol packages (.snupkg)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d892c-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d892c-105">Prerequisites</span></span>

<span data-ttu-id="d892c-106">[nuget.exe v4.9.0 o versione successiva](https://www.nuget.org/downloads) oppure [dotnet.exe v2.2.0 o versione successiva](https://www.microsoft.com/net/download/dotnet-core/2.2), che implementano i [protocolli NuGet](../api/nuget-protocols.md) necessari.</span><span class="sxs-lookup"><span data-stu-id="d892c-106">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="d892c-107">Creazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="d892c-107">Creating a symbol package</span></span>

<span data-ttu-id="d892c-108">È possibile creare un pacchetto di simboli con estensione snupkg da un file con estensione nuspec o csproj.</span><span class="sxs-lookup"><span data-stu-id="d892c-108">A snupkg symbol package can be created from a .nuspec file or from a .csproj file.</span></span> <span data-ttu-id="d892c-109">Sono supportati sia NuGet.exe sia dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="d892c-109">NuGet.exe and dotnet.exe are both supported.</span></span> <span data-ttu-id="d892c-110">Quando vengono usate le opzioni ```-Symbols -SymbolPackageFormat snupkg``` nel comando pack nuget.exe verrà creato un file con estensione snupkg in aggiunta al file con estensione nupkg.</span><span class="sxs-lookup"><span data-stu-id="d892c-110">When the options ```-Symbols -SymbolPackageFormat snupkg``` are used on the nuget.exe pack command a .snupkg file will be created in additon to the .nupkg file.</span></span>

<span data-ttu-id="d892c-111">Comandi di esempio per la creazione di file con estensione snupkg</span><span class="sxs-lookup"><span data-stu-id="d892c-111">Example commands to create .snupkg files</span></span>
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

<span data-ttu-id="d892c-112">I file `.snupkgs` non vengono prodotti per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d892c-112">`.snupkgs` are not produced by default.</span></span> <span data-ttu-id="d892c-113">È necessaria la proprietà `SymbolPackageFormat` insieme a `-Symbols` in caso di nuget.exe, `--include-symbols` in caso di dotnet.exe o `-p:IncludeSymbols` in caso di msbuild.</span><span class="sxs-lookup"><span data-stu-id="d892c-113">You must pass the `SymbolPackageFormat` property along with `-Symbols` in case of nuget.exe, `--include-symbols` in case of dotnet.exe, or `-p:IncludeSymbols` in case of msbuild.</span></span>

<span data-ttu-id="d892c-114">La proprietà SymbolPackageFormat può avere uno di due valori: `symbols.nupkg` (predefinito) o `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="d892c-114">SymbolPackageFormat property can have one of the two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="d892c-115">Se non viene specificato un valore per SymbolPackageFormat, la proprietà verrà impostata sul valore predefinito `symbols.nupkg` e verrà creato un pacchetto di simboli legacy.</span><span class="sxs-lookup"><span data-stu-id="d892c-115">If the SymbolPackageFormat is not specified, it defaults to `symbols.nupkg` and a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="d892c-116">Il formato legacy `.symbols.nupkg` è ancora supportato ma solo per motivi di compatibilità (vedere [Pacchetti di simboli legacy](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="d892c-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="d892c-117">Il server di simboli di NuGet.org accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="d892c-117">NuGet.org symbols server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="d892c-118">Pubblicazione di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="d892c-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="d892c-119">Per praticità, salvare prima la chiave API con NuGet (vedere [Pubblicazione di pacchetti](../create-packages/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="d892c-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="d892c-120">Dopo la pubblicazione del pacchetto principale su nuget.org, eseguire il push del pacchetto di simboli come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d892c-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="d892c-121">È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali contemporaneamente usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="d892c-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="d892c-122">Nella cartella corrente devono essere presenti sia i file con estensione nupkg sia quelli con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="d892c-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="d892c-123">NuGet pubblicherà entrambi i pacchetti in nuget.org. `MyPackage.nupkg` verrà pubblicato per primo, seguito da `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="d892c-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="d892c-124">Server di simboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="d892c-124">NuGet.org symbol server</span></span>

<span data-ttu-id="d892c-125">NuGet.org supporta il proprio repository del server di simboli e accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="d892c-125">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="d892c-126">I consumer di pacchetti possono usare i simboli pubblicati nel server di simboli nuget.org aggiungendo `https://symbols.nuget.org/download/symbols` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d892c-126">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="d892c-127">Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) per informazioni dettagliate su questo processo.</span><span class="sxs-lookup"><span data-stu-id="d892c-127">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="d892c-128">Vincoli del pacchetto di simboli NuGet.org</span><span class="sxs-lookup"><span data-stu-id="d892c-128">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="d892c-129">I pacchetti di simboli supportati in nuget.org hanno i vincoli seguenti</span><span class="sxs-lookup"><span data-stu-id="d892c-129">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="d892c-130">Solo le estensioni di file seguenti possono essere aggiunte a un pacchetto di simboli.</span><span class="sxs-lookup"><span data-stu-id="d892c-130">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="d892c-131">Solo i [file PDB portatili](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gestiti sono attualmente supportati nel server di simboli nuget.</span><span class="sxs-lookup"><span data-stu-id="d892c-131">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="d892c-132">Il file PDB e DLL nupkg associati devono essere compilati con il compilatore in Visual Studio versione 15.9 o versione successiva (vedere la pagina sulla [funzione crittografica di hash dei file PDB](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="d892c-132">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="d892c-133">La pubblicazione del pacchetto di simboli in nuget.org avrà esito negativo se nel file con estensione snupkg sono inclusi altri tipi di file.</span><span class="sxs-lookup"><span data-stu-id="d892c-133">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="d892c-134">Convalida e indicizzazione dei pacchetti di simboli</span><span class="sxs-lookup"><span data-stu-id="d892c-134">Symbol package validation and indexing</span></span>

<span data-ttu-id="d892c-135">I pacchetti di simboli pubblicati in [NuGet.org](https://www.nuget.org/) vengono sottoposti a diverse convalide, ad esempio il controllo antivirus.</span><span class="sxs-lookup"><span data-stu-id="d892c-135">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="d892c-136">Quando il pacchetto ha superato tutti i controlli di convalida, potrebbe essere necessario un po' di tempo prima che i simboli vengano indicizzati e siano disponibili per l'utilizzo dai server di simboli NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="d892c-136">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="d892c-137">Se il pacchetto non supera un controllo di convalida, la pagina dei dettagli del pacchetto per il file con estensione nupkg verrà aggiornata con l'errore associato e si riceverà anche una notifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="d892c-137">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="d892c-138">La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="d892c-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="d892c-139">Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per controllare se si stanno verificando interruzioni in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d892c-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="d892c-140">Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d892c-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="d892c-141">Struttura di un pacchetto di simboli</span><span class="sxs-lookup"><span data-stu-id="d892c-141">Symbol package structure</span></span>

<span data-ttu-id="d892c-142">Il file con estensione nupkg è esattamente lo stesso di oggi, ma il file con estensione snupkg presenta le caratteristiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="d892c-142">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="d892c-143">Il file con estensione snupkg avrà lo stesso ID e versione del file con estensione nupkg corrispondente.</span><span class="sxs-lookup"><span data-stu-id="d892c-143">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="d892c-144">Il file con estensione snupkg avrà la struttura di cartelle del pacchetto nupkg per tutti i file DLL o EXE con la differenza che, invece di DLL/exe, i file PDB corrispondenti verranno inclusi nella stessa gerarchia di cartelle.</span><span class="sxs-lookup"><span data-stu-id="d892c-144">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="d892c-145">I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="d892c-145">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="d892c-146">Il file con estensione nuspec nel pacchetto con estensione snupkg specificherà anche un nuovo PackageType come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d892c-146">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="d892c-147">Deve essere l'unico PackageType specificato.</span><span class="sxs-lookup"><span data-stu-id="d892c-147">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="d892c-148">Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).</span><span class="sxs-lookup"><span data-stu-id="d892c-148">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="d892c-149">I campi ```authors``` e ```owners``` verranno esclusi dal file con estensione nuspec del pacchetto con estensione snupkg.</span><span class="sxs-lookup"><span data-stu-id="d892c-149">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="d892c-150">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d892c-150">See Also</span></span>

<span data-ttu-id="d892c-151">[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) (Debug del pacchetto NuGet e miglioramenti dei simboli)</span><span class="sxs-lookup"><span data-stu-id="d892c-151">[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)</span></span>
