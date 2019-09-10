---
title: Comando Pack dell'interfaccia della riga di comando NuGet
description: Informazioni di riferimento sul comando NuGet. exe Pack
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 76829d45ea9821da3b7fdaa2f88d30dbb104fea1
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815357"
---
# <a name="pack-command-nuget-cli"></a>Comando pack (interfaccia della riga di comando di NuGet)

**Si applica a:** &bullet; **versioni supportate** per la creazione di pacchetti: 2.7+

Crea un pacchetto NuGet basato sul file con [estensione NuSpec](../nuspec.md) o Project specificato. Il `dotnet pack` comando (vedere i [comandi DotNet](../dotnet-Commands.md)) `msbuild -t:pack` e (vedere [destinazioni MSBuild](../msbuild-targets.md)) può essere usato come alternativa.

> [!Important]
> In mono la creazione di un pacchetto da un file di progetto non è supportata. È anche necessario modificare i `.nuspec` percorsi non locali nel file nei percorsi di tipo UNIX, perché NuGet. exe non converte i nomi di percorso di Windows.

## <a name="usage"></a>Utilizzo

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

dove `<nuspecPath>` `.nuspec` e `<projectPath>` specificano rispettivamente il file di progetto o.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| BasePath | Imposta il percorso di base dei file definiti nel file con [estensione NuSpec](../nuspec.md) . |
| Compilazione | Specifica che il progetto deve essere compilato prima della compilazione del pacchetto. |
| Deterministico | Specificare se il comando deve creare un pacchetto deterministico. Più chiamate del comando Pack generano esattamente lo stesso pacchetto byte-byte. L'output del comando Pack non è influenzato dallo stato di ambiente del computer. In particolare, le voci zip verranno restituite come 1980-01-01. Per ottenere il determinismo completo, gli assembly devono essere compilati con l'opzione del compilatore corrispondente [deterministica](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option). |
| Escludi | Specifica uno o più criteri jolly da escludere durante la creazione di un pacchetto. Per specificare più di un modello, ripetere il flag-exclude. Vedere l'esempio seguente. |
| ExcludeEmptyDirectories | Impedisce l'inclusione di directory vuote durante la compilazione del pacchetto. |
| ForceEnglishOutput | *(3.5 +)* Impone l'esecuzione di NuGet. exe con impostazioni cultura invarianti basate sull'inglese. |
| ConfigFile | Specificare il file di configurazione per il comando Pack. |
| ? | Visualizza le informazioni della Guida per il comando. |
| IncludeReferencedProjects | Indica che il pacchetto compilato deve includere i progetti a cui si fa riferimento come dipendenze o come parte del pacchetto. Se un progetto a cui viene fatto riferimento `.nuspec` ha un file corrispondente con lo stesso nome del progetto, il progetto a cui si fa riferimento viene aggiunto come dipendenza. In caso contrario, il progetto a cui si fa riferimento viene aggiunto come parte del pacchetto. |
| MinClientVersion | Impostare l'attributo *minClientVersion* per il pacchetto creato. Questo valore eseguirà l'override del valore dell'attributo *minClientVersion* esistente, se presente, nel `.nuspec` file. |
| MSBuildPath | *(4.0 +)* Specifica il percorso di MSBuild da usare con il comando, avendo la precedenza `-MSBuildVersion`su. |
| MSBuildVersion | *(3.2 +)* Specifica la versione di MSBuild da usare con questo comando. I valori supportati sono 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Per impostazione predefinita, viene scelto MSBuild nel percorso; in caso contrario, per impostazione predefinita viene impostata la versione più recente di MSBuild. |
| NoDefaultExcludes | Impedisce l'esclusione predefinita dei file e delle cartelle del pacchetto NuGet a partire da un punto, `.svn` ad `.gitignore`esempio e. |
| NoPackageAnalysis | Specifica che pack non deve eseguire l'analisi del pacchetto dopo la compilazione di quest'ultimo. |
| OutputDirectory | Specifica la cartella in cui è archiviato il pacchetto creato. Se non viene specificata alcuna cartella, viene utilizzata la cartella corrente. |
| Properties | Viene visualizzato per ultimo nella riga di comando dopo le altre opzioni. Specifica un elenco di proprietà che eseguono l'override dei valori nel file di progetto. vedere [proprietà del progetto MSBuild comuni](/visualstudio/msbuild/common-msbuild-project-properties) per i nomi di proprietà. L'argomento Properties è un elenco di coppie token = valore, separate da punti e virgola, `$token$` `.nuspec` in cui ogni occorrenza di nel file verrà sostituita con il valore specificato. I valori possono essere stringhe tra virgolette. Si noti che per la proprietà "Configuration", il valore predefinito è "debug". Per passare a una configurazione di versione, `-Properties Configuration=Release`usare. |
| Suffisso | *(3.4.4 +)* Accoda un suffisso al numero di versione generato internamente, usato in genere per accodare gli identificatori della versione non definitiva. Usando `-suffix nightly` , ad esempio, viene creato un pacchetto con un numero di `1.2.3-nightly`versione come. I suffissi devono iniziare con una lettera per evitare avvisi, errori e potenziali incompatibilità con versioni diverse di NuGet e gestione pacchetti NuGet. |
| Simboli | Specifica che il pacchetto contiene origini e simboli. Quando viene usato con `.nuspec` un file, viene creato un normale file di pacchetto NuGet e il pacchetto di simboli corrispondente. Per impostazione predefinita, crea un [pacchetto di simboli legacy](../../create-packages/Symbol-Packages.md). Il nuovo formato consigliato per i pacchetti di simboli è l'estensione snupkg. Vedere [Creazione di pacchetti di simboli (estensione snupkg)](../../create-packages/Symbol-Packages-snupkg.md). |
| Strumento | Specifica che i file di output del progetto devono essere inseriti nella `tool` cartella. |
| Verbosity | Specifica il livello di dettaglio visualizzato nell'output: *normale*, *silenzioso*, *dettagliato*. |
| Versione | Esegue l'override del numero di `.nuspec` versione dal file. |

Vedere anche [variabili di ambiente](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Esclusione delle dipendenze di sviluppo

Alcuni pacchetti NuGet sono utili come dipendenze di sviluppo, che consentono di creare una libreria personalizzata, ma non sono necessariamente necessari come dipendenze effettive del pacchetto.

Il `pack` comando ignorerà `package` le voci `packages.config` in con l' `developmentDependency` attributo impostato su `true`. Queste voci non verranno incluse come dipendenze nel pacchetto creato.

Si consideri, ad `packages.config` esempio, il file seguente nel progetto di origine:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Per questo progetto, il pacchetto creato da `nuget pack` avrà una dipendenza da `jQuery` e `microsoft-web-helpers` non `netfx-Guard`.

## <a name="examples"></a>Esempi

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
