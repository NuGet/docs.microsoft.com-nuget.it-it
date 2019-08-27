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
ms.openlocfilehash: 992b3ddd04a1bb34e7aca25dfaa6f7df5485907b
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564540"
---
# <a name="creating-symbol-packages-snupkg"></a>Creazione di pacchetti di simboli (estensione snupkg)

I pacchetti di simboli consentono di migliorare l'esperienza di debug dei pacchetti NuGet.

## <a name="prerequisites"></a>Prerequisiti

[nuget.exe v4.9.0 o versione successiva](https://www.nuget.org/downloads) oppure [dotnet.exe v2.2.0 o versione successiva](https://www.microsoft.com/net/download/dotnet-core/2.2), che implementano i [protocolli NuGet](../api/nuget-protocols.md) necessari.

## <a name="creating-a-symbol-package"></a>Creazione di un pacchetto di simboli

È possibile creare un pacchetto di simboli snupkg tramite dotnet.exe, NuGet.exe o MSBuild. Se si usa NuGet.exe, è possibile usare i comandi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Se si usa dotnet.exe o MSBuild, è possibile usare i passaggi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:

1. Aggiungere le proprietà seguenti al file con estensione csproj:

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. Eseguire un pacchetto del progetto con `dotnet pack MyPackage.csproj` o `msbuild -t:pack MyPackage.csproj`.

La proprietà [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) può avere uno dei due valori seguenti: `symbols.nupkg` (predefinito) o `snupkg`. Se non viene specificata la proprietà [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat), verrà creato un pacchetto di simboli legacy.

> [!Note]
> Il formato legacy `.symbols.nupkg` è ancora supportato ma solo per motivi di compatibilità (vedere [Pacchetti di simboli legacy](Symbol-Packages.md)). Il server di simboli di NuGet.org accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Pubblicazione di un pacchetto di simboli

1. Per praticità, salvare prima la chiave API con NuGet (vedere [Pubblicazione di pacchetti](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Dopo la pubblicazione del pacchetto principale su nuget.org, eseguire il push del pacchetto di simboli come indicato di seguito.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. È anche possibile eseguire il push sia dei pacchetti di simboli che di quelli principali contemporaneamente usando il comando seguente. Nella cartella corrente devono essere presenti sia i file con estensione nupkg sia quelli con estensione snupkg.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet pubblicherà entrambi i pacchetti in nuget.org. `MyPackage.nupkg` verrà pubblicato per primo, seguito da `MyPackage.snupkg`.

> [!Note]
> Se il pacchetto di simboli non viene pubblicato, verificare di aver configurato l'origine di NuGet.org come `https://api.nuget.org/v3/index.json`. La pubblicazione del pacchetto di simboli è supportata solo dall'[API NuGet V3](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>Server di simboli NuGet.org

NuGet.org supporta il proprio repository del server di simboli e accetta solo il nuovo formato di pacchetto di simboli `.snupkg`. I consumer di pacchetti possono usare i simboli pubblicati nel server di simboli nuget.org aggiungendo `https://symbols.nuget.org/download/symbols` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio. Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) per informazioni dettagliate su questo processo.

### <a name="nugetorg-symbol-package-constraints"></a>Vincoli del pacchetto di simboli NuGet.org

I pacchetti di simboli supportati in nuget.org hanno i vincoli seguenti

- Solo le estensioni di file seguenti possono essere aggiunte a un pacchetto di simboli. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- Solo i [file PDB portatili](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gestiti sono attualmente supportati nel server di simboli nuget.
- Il file PDB e DLL nupkg associati devono essere compilati con il compilatore in Visual Studio versione 15.9 o versione successiva (vedere la pagina sulla [funzione crittografica di hash dei file PDB](https://github.com/dotnet/roslyn/issues/24429))

La pubblicazione del pacchetto di simboli in nuget.org avrà esito negativo se nel file con estensione snupkg sono inclusi altri tipi di file.

### <a name="symbol-package-validation-and-indexing"></a>Convalida e indicizzazione dei pacchetti di simboli

I pacchetti di simboli pubblicati in [NuGet.org](https://www.nuget.org/) vengono sottoposti a diverse convalide, ad esempio il controllo antivirus.

Quando il pacchetto ha superato tutti i controlli di convalida, potrebbe essere necessario un po' di tempo prima che i simboli vengano indicizzati e siano disponibili per l'utilizzo dai server di simboli NuGet.org. Se il pacchetto non supera un controllo di convalida, la pagina dei dettagli del pacchetto per il file con estensione nupkg verrà aggiornata con l'errore associato e si riceverà anche una notifica tramite posta elettronica.

La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti. Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per controllare se si stanno verificando interruzioni in nuget.org. Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.

## <a name="symbol-package-structure"></a>Struttura di un pacchetto di simboli

Il file con estensione nupkg è esattamente lo stesso di oggi, ma il file con estensione snupkg presenta le caratteristiche seguenti:

1) Il file con estensione snupkg avrà lo stesso ID e versione del file con estensione nupkg corrispondente.
2) Il file con estensione snupkg avrà la struttura di cartelle del pacchetto nupkg per tutti i file DLL o EXE con la differenza che, invece di DLL/exe, i file PDB corrispondenti verranno inclusi nella stessa gerarchia di cartelle. I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.
3) Il file con estensione nuspec nel pacchetto con estensione snupkg specificherà anche un nuovo PackageType come indicato di seguito. Deve essere l'unico PackageType specificato.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).
5) I campi ```authors``` e ```owners``` verranno esclusi dal file con estensione nuspec del pacchetto con estensione snupkg.
6) Non usare l'elemento <license>. Un file con estensione snupkg è coperto dalla stessa licenza del file con estensione nupkg corrispondente.

## <a name="see-also"></a>Vedere anche

[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) (Debug del pacchetto NuGet e miglioramenti dei simboli)
