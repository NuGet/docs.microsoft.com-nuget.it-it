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
# <a name="creating-symbol-packages-snupkg"></a>Creazione di pacchetti di simboli (estensione snupkg)

Una buona esperienza di debug si basa sulla presenza di simboli di debug perché forniscono informazioni critiche come l'associazione tra il codice sorgente e compilato, i nomi delle variabili locali, le analisi dello stack e altro ancora. È possibile usare i pacchetti di simboli (con estensione snupkg) per distribuire questi simboli e migliorare l'esperienza di debug dei pacchetti NuGet.

> Si noti che il pacchetto di simboli non è l'unica strategia per rendere i simboli di debug disponibili per i consumer della libreria. È anche possibile [eseguire queste operazioni `embed` ](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle) in o con la proprietà di progetto `dll` `exe` seguente:`<DebugType>embedded</DebugType>`

## <a name="prerequisites"></a>Prerequisiti

[nuget.exe v4.9.0 o](https://www.nuget.org/downloads) versione precedente o l'interfaccia della riga di comando [dotnet v2.2.0](https://www.microsoft.com/net/download/dotnet-core/2.2)o versione precedente, che implementano i protocolli [NuGet necessari.](../api/nuget-protocols.md)

## <a name="creating-a-symbol-package"></a>Creazione di un pacchetto di simboli

Se si usa l'interfaccia della riga di comando dotnet o MSBuild, è necessario impostare le proprietà e per creare un file con estensione snupkg oltre al file con estensione `IncludeSymbols` `SymbolPackageFormat` nupkg.

* Aggiungere le proprietà seguenti al file con estensione csproj:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Oppure specificare queste proprietà nella riga di comando:

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

La [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) proprietà può avere uno dei due valori seguenti: `symbols.nupkg` (impostazione predefinita) o `snupkg` . Se questa proprietà non viene specificata, verrà creato un pacchetto di simboli legacy.

> [!Note]
> Il formato legacy `.symbols.nupkg` è ancora supportato, ma solo per motivi di compatibilità come i pacchetti nativi (vedere [Pacchetti di simboli legacy).](Symbol-Packages.md) Il server di simboli di NuGet.org accetta solo il nuovo formato di pacchetto di simboli `.snupkg`.

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

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org dei pacchetti di simboli

NuGet.org presenta i vincoli seguenti per i pacchetti di simboli:

- Nei pacchetti di simboli sono consentite solo le estensioni di file seguenti: `.pdb` , , , , , `.nuspec` `.xml` `.psmdcp` `.rels` , `.p7s`
- Solo i [PDB portatili gestiti](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) sono supportati nel server di simboli di NuGet.org.
- I file PDB e le DLL con estensione nupkg associate devono essere compilati con il compilatore in Visual Studio versione 15.9 o successiva (vedere L'hash di crittografia [PDB)](https://github.com/dotnet/roslyn/issues/24429)

I pacchetti di simboli pubblicati NuGet.org non verranno convalidati se questi vincoli non vengono soddisfatti. 

> [!NOTE]
> I progetti nativi, ad esempio i progetti C++, producono PDB Windows anziché PDB portatili. Questi non sono supportati dal server di simboli di NuGet.org. In alternativa, [usare pacchetti di simboli](Symbol-Packages.md) legacy.

### <a name="symbol-package-validation-and-indexing"></a>Convalida e indicizzazione dei pacchetti di simboli

I pacchetti di [simboli](https://www.nuget.org/) pubblicati NuGet.org diverse convalide, tra cui l'analisi malware. Se un pacchetto non supera un controllo di convalida, nella pagina dei dettagli del pacchetto verrà visualizzato un messaggio di errore. Inoltre, i proprietari del pacchetto riceveranno un messaggio di posta elettronica con istruzioni su come risolvere i problemi identificati.

Quando il pacchetto di simboli ha superato tutte le convalide, i simboli verranno indicizzati dai server di simboli di NuGet.org e saranno disponibili per l'utilizzo.

La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti. Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per verificare se NuGet.org si verificano interruzioni. Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina dei dettagli del pacchetto.

## <a name="symbol-package-structure"></a>Struttura di un pacchetto di simboli

Il pacchetto di simboli (con estensione snupkg) presenta le caratteristiche seguenti:

1) Il file con estensione snupkg ha lo stesso ID e la stessa versione del pacchetto NuGet corrispondente (con estensione nupkg).
2) Il file con estensione snupkg ha la stessa struttura di cartelle del file con estensione nupkg corrispondente per tutti i file DLL o EXE con la distinzione che anziché DLL/EXE, i PDB corrispondenti verranno inclusi nella stessa gerarchia di cartelle. I file e le cartelle con estensioni diverse da PDB verranno lasciati fuori dal file con estensione snupkg.
3) Il file con estensione nuspec del pacchetto di simboli ha il `SymbolsPackage` tipo di pacchetto:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Se un autore decide di usare un file con estensione nuspec personalizzato per compilare i propri file con estensione nupkg e snupkg, il file con estensione snupkg deve avere la stessa gerarchia di cartelle e gli stessi file descritti in dettaglio al punto 2).
5) I campi seguenti verranno esclusi dal nuspec di snupkg: ```authors``` , , , , e ```owners``` ```requireLicenseAcceptance``` ```license type``` ```licenseUrl```  ```icon``` .
6) Non usare l'elemento ```<license>```. Un file con estensione snupkg è coperto dalla stessa licenza del file con estensione nupkg corrispondente.

## <a name="see-also"></a>Vedi anche

Prendere in considerazione l'uso di Collegamento all'origine per abilitare il debug del codice sorgente degli assembly .NET. Per altre informazioni, vedere le linee guida [di Collegamento all'origine](/dotnet/standard/library-guidance/sourcelink).

Per altre informazioni sui pacchetti di simboli, vedere la specifica di progettazione NuGet Package Debugging & Symbols Improvements (Miglioramenti dei simboli [nuGet).](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)