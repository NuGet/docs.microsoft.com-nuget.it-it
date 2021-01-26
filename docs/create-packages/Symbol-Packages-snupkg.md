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
ms.openlocfilehash: 001637348fdd435e4ffd3a5a55e8128d1eab453c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774573"
---
# <a name="creating-symbol-packages-snupkg"></a>Creazione di pacchetti di simboli (estensione snupkg)

Un'esperienza di debug ottimale si basa sulla presenza di simboli di debug poiché forniscono informazioni critiche, come l'associazione tra il codice compilato e il codice sorgente, i nomi delle variabili locali, le analisi dello stack e altro ancora. È possibile usare i pacchetti di simboli (con estensione snupkg) per distribuire questi simboli e migliorare l'esperienza di debug dei pacchetti NuGet.

> Si noti che il pacchetto di simboli non è l'unica strategia per rendere i simboli di debug disponibili per gli utenti della libreria. È anche [possibile `embed` ](https://docs.microsoft.com/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) in `dll` o `exe` con la seguente proprietà del progetto:`<DebugType>embedded</DebugType>`

## <a name="prerequisites"></a>Prerequisiti

[nuget.exe v 4.9.0 o versioni successive](https://www.nuget.org/downloads) o [DotNet CLI v 2.2.0 o versioni successive](https://www.microsoft.com/net/download/dotnet-core/2.2), che implementano i [protocolli NuGet](../api/nuget-protocols.md)necessari.

## <a name="creating-a-symbol-package"></a>Creazione di un pacchetto di simboli

Se si usa l'interfaccia della riga di comando DotNet o MSBuild, è necessario impostare le `IncludeSymbols` `SymbolPackageFormat` proprietà e per creare un file con estensione snupkg oltre al file nupkg.

* Aggiungere le proprietà seguenti al file con estensione csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* In alternativa, specificare le proprietà seguenti nella riga di comando:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  oppure

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Se si usa NuGet.exe, è possibile usare i comandi seguenti per creare un file con estensione snupkg oltre al file con estensione nupkg:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

La [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) proprietà può avere uno dei due valori seguenti: `symbols.nupkg` (valore predefinito) o `snupkg` . Se questa proprietà non è specificata, verrà creato un pacchetto di simboli legacy.

> [!Note]
> Il formato legacy `.symbols.nupkg` è ancora supportato, ma solo per motivi di compatibilità come i pacchetti nativi (vedere [pacchetti di simboli legacy](Symbol-Packages.md)). Il server di simboli di NuGet.org accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.

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

### <a name="nugetorg-symbol-package-constraints"></a>Vincoli del pacchetto di simboli NuGet.org

NuGet.org presenta i vincoli seguenti per i pacchetti di simboli:

- Nei pacchetti di simboli sono consentite solo le estensioni di file seguenti: `.pdb` , `.nuspec` , `.xml` , `.psmdcp` , `.rels` , `.p7s`
- Nel server di simboli di NuGet. org sono supportati solo [PDB portatili](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) gestiti.
- I PDB e le dll nupkg associate devono essere compilati con il compilatore in Visual Studio versione 15,9 o successiva (vedere l' [hash Crypto PDB](https://github.com/dotnet/roslyn/issues/24429))

Se questi vincoli non vengono soddisfatti, i pacchetti di simboli pubblicati in NuGet.org non verranno convalidati. 

> [!NOTE]
> I progetti nativi, ad esempio i progetti C++, producono Windows PDB invece di PDB portatili. Questi non sono supportati dal server di simboli di NuGet. org. Usare invece i [pacchetti di simboli legacy](Symbol-Packages.md) .

### <a name="symbol-package-validation-and-indexing"></a>Convalida e indicizzazione dei pacchetti di simboli

I pacchetti di simboli pubblicati in [NuGet.org](https://www.nuget.org/) vengono sottoposti a diverse convalide, inclusa l'analisi di malware. Se un pacchetto non supera un controllo di convalida, nella pagina dei dettagli del pacchetto verrà visualizzato un messaggio di errore. Inoltre, i proprietari del pacchetto riceveranno un messaggio di posta elettronica con le istruzioni su come risolvere i problemi identificati.

Quando il pacchetto di simboli ha superato tutte le convalide, i simboli verranno indicizzati dai server dei simboli di NuGet. org e saranno disponibili per l'utilizzo.

La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti. Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.NuGet.org](https://status.nuget.org/) per verificare se NuGet.org sta riscontrando interruzioni. Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.

## <a name="symbol-package-structure"></a>Struttura di un pacchetto di simboli

Il pacchetto di simboli (con estensione snupkg) presenta le caratteristiche seguenti:

1) Il. snupkg ha lo stesso ID e la stessa versione del pacchetto NuGet corrispondente (. nupkg).
2) Il file con estensione snupkg ha la stessa struttura di cartelle della corrispondente. nupkg per tutti i file DLL o EXE, con la differenza che anziché dll/exe, il corrispondente PDB verrà incluso nella stessa gerarchia di cartelle. I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.
3) Il file con estensione NuSpec del pacchetto di simboli presenta il `SymbolsPackage` tipo di pacchetto:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).
5) I campi seguenti verranno esclusi dal NuSpec di snupkg: ```authors``` , ```owners``` , ```requireLicenseAcceptance``` , ```license type``` , ```licenseUrl``` e  ```icon``` .
6) Non usare l'elemento ```<license>```. Un file con estensione snupkg è coperto dalla stessa licenza del file con estensione nupkg corrispondente.

## <a name="see-also"></a>Vedere anche

Provare a usare il collegamento di origine per abilitare il debug del codice sorgente degli assembly .NET. Per ulteriori informazioni, consultare le [linee guida](/dotnet/standard/library-guidance/sourcelink)per il collegamento all'origine.

Per altre informazioni sui pacchetti di simboli, fare riferimento alla specifica di [debug del pacchetto NuGet & simboli](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) di progettazione.
