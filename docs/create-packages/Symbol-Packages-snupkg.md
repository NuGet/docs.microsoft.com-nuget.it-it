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
# <a name="creating-symbol-packages-snupkg"></a>Creazione di pacchetti di simboli (estensione snupkg)

Una buona esperienza di debug si basa sulla presenza di simboli di debug in quanto forniscono informazioni critiche come l'associazione tra il codice compilato e il codice sorgente, i nomi delle variabili locali, le tracce dello stack e altro ancora. È possibile utilizzare i pacchetti di simboli (con estensione snupkg) per distribuire questi simboli e migliorare l'esperienza di debug dei pacchetti NuGet.

## <a name="prerequisites"></a>Prerequisiti

[nuget.exe v4.9.0 o versione successiva](https://www.nuget.org/downloads) o [dotnet CLI v2.2.0 o versione successiva,](https://www.microsoft.com/net/download/dotnet-core/2.2)che implementano i [protocolli NuGet](../api/nuget-protocols.md)necessari.

## <a name="creating-a-symbol-package"></a>Creazione di un pacchetto di simboli

Se si usa dotnet CLI o MSBuild, `IncludeSymbols` è `SymbolPackageFormat` necessario impostare le proprietà e per creare un file con estensione snupkg oltre al file nupkg.

* Aggiungere le seguenti proprietà al file con estensione csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* In alternativa, specificare queste proprietà nella riga di comando:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  o

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Se si usa NuGet.exe, è possibile usare i comandi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

La [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) proprietà può avere uno `symbols.nupkg` dei due `snupkg`valori seguenti: (impostazione predefinita) o . Se questa proprietà non è specificata, verrà creato un pacchetto di simboli legacy.

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

NuGet.org supporta il proprio repository del server di simboli e accetta solo il nuovo formato di pacchetto di simboli `.snupkg`. I consumer di pacchetti possono usare i simboli pubblicati nel server di simboli nuget.org aggiungendo `https://symbols.nuget.org/download/symbols` alle loro origini dei simboli in Visual Studio, in modo da consentire l'esecuzione delle istruzioni nel codice del pacchetto nel debugger di Visual Studio. Vedere [Specifica di file di simboli (con estensione pdb) e di file di origine nel debugger di Visual Studio](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) per informazioni dettagliate su questo processo.

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org vincoli dei pacchetti di simboli di NuGet.org

NuGet.org ha i seguenti vincoli per i pacchetti di simboli:

- Nei pacchetti di simboli sono consentite `.xml`solo `.psmdcp` `.rels`le seguenti estensioni di file: `.pdb`, `.nuspec`, , , , ,`.p7s`
- Solo [i file PDB portabili](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gestiti sono supportati nel server di simboli di NuGet.org.
- I File PDB e le DLL nUPkg associate devono essere compilati con il compilatore in Visual Studio versione 15.9 o successiva (vedere [Hash crittografico PDB](https://github.com/dotnet/roslyn/issues/24429))

I pacchetti di simboli pubblicati per NuGet.org non verranno convalidati se questi vincoli non vengono soddisfatti. 

### <a name="symbol-package-validation-and-indexing"></a>Convalida e indicizzazione dei pacchetti di simboli

Pacchetti di simboli pubblicati [per NuGet.org](https://www.nuget.org/) sottoposti a diverse convalide, tra cui la scansione antimalware. Se un pacchetto non supera un controllo di convalida, nella relativa pagina dei dettagli del pacchetto verrà visualizzato un messaggio di errore. Inoltre, i proprietari del pacchetto riceveranno un'e-mail con le istruzioni su come risolvere i problemi identificati.

Quando il pacchetto di simboli ha superato tutte le convalide, i simboli verranno indicizzati dai server di simboli di NuGet.org e saranno disponibili per l'utilizzo.

La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti. Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per verificare se NuGet.org si verificano interruzioni. Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.

## <a name="symbol-package-structure"></a>Struttura di un pacchetto di simboli

Il pacchetto di simboli (.snupkg) presenta le seguenti caratteristiche:

1) Il .snupkg ha lo stesso id e la stessa versione del pacchetto NuGet corrispondente (.nupkg).
2) Il .snupkg ha la stessa struttura di cartelle del corrispondente .nupkg per qualsiasi file DLL o EXE con la distinzione che invece di DLL/EXE, i corrispondenti PDU verranno inclusi nella stessa gerarchia di cartelle. I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.
3) Il file .nuspec del pacchetto `SymbolsPackage` di simboli ha il tipo di pacchetto:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).
5) I seguenti campi verranno esclusi dal nuspec ```authors```di ```owners``` ```requireLicenseAcceptance```snupkg: , , , , ```license type``` ```licenseUrl```, e ```icon```.
6) Non usare l'elemento ```<license>```. Un file con estensione snupkg è coperto dalla stessa licenza del file con estensione nupkg corrispondente.

## <a name="see-also"></a>Vedere anche

Prendere in considerazione l'utilizzo di Collegamento di origine per abilitare il debug del codice sorgente degli assembly .NET. Per ulteriori informazioni, fare riferimento alla Guida al [collegamento di origine](/dotnet/standard/library-guidance/sourcelink).

Per altre informazioni sui pacchetti di simboli, fare riferimento alla specifica di progettazione [NuGet Package Debugging & Symbols Improvements.For](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) more information on symbol packages, please refer to the NuGet Package Debugging & Symbols Improvements design spec.
