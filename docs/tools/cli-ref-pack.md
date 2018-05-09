---
title: Comando pack NuGet CLI
description: Riferimento per il comando di nuget.exe pack
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a2468b099a822e69298ea78c80cfd1d5d5c09938
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="pack-command-nuget-cli"></a>comando Pack (NuGet CLI)

**Si applica a:** creazione di pacchetti &bullet; **le versioni supportate:** 2.7 +

Crea un pacchetto NuGet in base all'opzione `.nuspec` o file di progetto. Il `dotnet pack` comando (vedere [comandi dotnet](dotnet-Commands.md)) e `msbuild /t:pack` (vedere [destinazioni di MSBuild](../reference/msbuild-targets.md)) possono essere utilizzati come valori alternativi.

> [!Important]
> In Mono, crea un pacchetto da un file di progetto non è supportata. È inoltre necessario modificare i percorsi locali non nel `.nuspec` file per i percorsi di tipo Unix, come nuget.exe non converte i nomi di percorso di Windows se stesso.

## <a name="usage"></a>Utilizzo

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

dove `<nuspecPath>` e `<projectPath>` specificare il `.nuspec` o un progetto di file, rispettivamente.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| BasePath | Imposta il percorso dei file definiti base il `.nuspec` file. |
| Compilazione | Specifica che il progetto deve essere compilato prima di creare il pacchetto. |
| Escludi | Specifica uno o più modelli jolly da escludere quando si crea un pacchetto. Per specificare più di un modello, ripetere il flag-Exclude. Vedere l'esempio riportato di seguito. |
| ExcludeEmptyDirectories | Impedisce l'inclusione di una directory vuota quando si compila il pacchetto. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe per eseguire utilizzando le impostazioni cultura invariante, in lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| IncludeReferencedProjects | Indica che il pacchetto generato deve includere i progetti di riferimento come dipendenze o come parte del pacchetto. Se un progetto a cui fa riferimento ha un corrispondente `.nuspec` file con lo stesso nome del progetto, quindi il progetto di cui viene fatto riferimento viene aggiunto come dipendenza. In caso contrario, il progetto di riferimento viene aggiunto come parte del pacchetto. |
| MinClientVersion | Impostare il *minClientVersion* attributo per il pacchetto creato. Questo valore sostituirà il valore dell'oggetto esistente *minClientVersion* attributo (se presente) di `.nuspec` file. |
| MSBuildPath | *(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, che avrà la precedenza `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando. Valori supportati sono 4, 12, 14, 15. Per impostazione predefinita che viene selezionato il percorso di MSBuild, in caso contrario il valore predefinito la versione più aggiornata di MSBuild. |
| NoDefaultExcludes | Impedisce l'esclusione predefinito di NuGet file del pacchetto e i file e cartelle inizia con un punto, ad esempio `.svn` e `.gitignore`. |
| NoPackageAnalysis | Specifica che pack non deve eseguire l'analisi del pacchetto dopo la compilazione di quest'ultimo. |
| OutputDirectory | Specifica la cartella in cui è archiviato il pacchetto creato. Se viene specificata alcuna cartella, viene utilizzata la cartella corrente. |
| Proprietà | Deve comparire come ultimo elemento nella riga di comando dopo le altre opzioni. Specifica un elenco di proprietà che eseguono l'override di valori nel file di progetto. vedere [proprietà di progetto MSBuild comuni](/visualstudio/msbuild/common-msbuild-project-properties) per i nomi delle proprietà. In questo caso l'argomento della proprietà è un elenco di token = coppie di valore, separate da punti e virgola, in cui ogni occorrenza di `$token$` nel `.nuspec` file verrà sostituito con il valore specificato. I valori possono essere stringhe tra virgolette. Si noti che per la proprietà "Configurazione", il valore predefinito è "Debug". Per modificare in una configurazione di rilascio, utilizzare `-Properties Configuration=Release`. |
| Suffisso | *(3.4.4+)*  Aggiunge un suffisso per il numero di versione generato internamente, in genere utilizzato per l'aggiunta di compilazione o altri identificatori di versione non definitiva. Ad esempio, usando `-suffix nightly` verrà creato un pacchetto con un tipo di numero versione `1.2.3-nightly`. I suffissi devono iniziare con una lettera per evitare potenziali problemi di incompatibilità con diverse versioni di NuGet e gestione pacchetti NuGet, errori e avvisi. |
| Simboli | Specifica che il pacchetto contiene origini e simboli. Quando si utilizza un `.nuspec` file, verrà creato un file del pacchetto NuGet regolari e il corrispondente il pacchetto di simboli. |
| Strumento | Specifica che i file di output del progetto devono essere inseriti nel `tool` cartella. |
| Livello di dettaglio | Specifica la quantità di dettagli visualizzati nell'output: *normale*, *quiet*, *dettagliate*. |
| Versione | Sostituisce il numero di versione di `.nuspec` file. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Esclusione delle dipendenze di sviluppo

Alcuni pacchetti NuGet sono utili come dipendenze di sviluppo, che consentono di creare la propria libreria, ma non necessariamente necessari come dipendenze di pacchetto effettivo.

Il `pack` verrà ignorata `package` voci `packages.config` che dispongono di `developmentDependency` attributo impostato su `true`. Queste voci non includerà come delle dipendenze del pacchetto creato.

Ad esempio, tenere presente quanto segue `packages.config` file nel progetto di origine:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Per questo progetto, il pacchetto creato da `nuget pack` avrà una dipendenza sulla `jQuery` e `microsoft-web-helpers` ma non `netfx-Guard`.

## <a name="examples"></a>Esempi

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
