---
title: Comando pack NuGet CLI
description: Informazioni di riferimento per il comando pack nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b5bd8bd30ad134f36433b8e4721ce131425a1483
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453364"
---
# <a name="pack-command-nuget-cli"></a>Comando pack (interfaccia della riga di comando di NuGet)

**Si applica a:** creazione del pacchetto &bullet; **le versioni supportate:** 2.7 +

Crea un pacchetto NuGet basato sull'oggetto specificato `.nuspec` o file di progetto. Il `dotnet pack` comando (vedere [comandi dotnet](dotnet-Commands.md)) e `msbuild -t:pack` (vedere [destinazioni di MSBuild](../reference/msbuild-targets.md)) può essere usato come alternative.

> [!Important]
> In Mono, creazione di un pacchetto da un file di progetto non è supportata. È anche necessario modificare i percorsi locali non nel `.nuspec` file ai percorsi in stile Unix, come nuget.exe non converte percorsi di Windows se stesso.

## <a name="usage"></a>Utilizzo

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

in cui `<nuspecPath>` e `<projectPath>` specificare il `.nuspec` o file, rispettivamente del progetto.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| BasePath | Imposta il percorso dei file definiti base il `.nuspec` file. |
| Compilazione | Specifica che il progetto deve essere compilato prima di compilare il pacchetto. |
| Escludi | Specifica uno o più modelli con caratteri jolly da escludere durante la creazione di un pacchetto. Per specificare più di un criterio, ripetere il - flag di esclusione. Vedere l'esempio riportato di seguito. |
| ExcludeEmptyDirectories | Impedisce l'inclusione delle directory vuota quando si compila il pacchetto. |
| ForceEnglishOutput | *(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ConfigFile | Specificare il file di configurazione per il comando pack. |
| ? | Visualizza la Guida informazioni per il comando. |
| IncludeReferencedProjects | Indica che il pacchetto generato deve includere progetti con riferimenti come dipendenze o come parte del pacchetto. Se un progetto di riferimento ha un corrispondente `.nuspec` file con lo stesso nome del progetto, tale progetto cui viene fatto riferimento viene aggiunto come dipendenza. In caso contrario, il progetto di riferimento viene aggiunto come parte del pacchetto. |
| MinClientVersion | Impostare il *minClientVersion* attributo per il pacchetto creato. Questo valore sostituirà il valore dell'oggetto esistente *minClientVersion* attributo (se presente) nel `.nuspec` file. |
| MSBuildPath | *(4.0 +)*  Specifica il percorso di MSBuild da usare con il comando, hanno la precedenza sui `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Specifica la versione di MSBuild da usare con questo comando. Valori supportati sono 4, 12, 14, 15. Per impostazione predefinita che viene selezionato nel proprio percorso di MSBuild, in caso contrario, per impostazione predefinita la versione installata più recente di MSBuild. |
| NoDefaultExcludes | Impedisce l'esclusione predefinita di NuGet package file e i file e cartelle che iniziano con un punto, ad esempio `.svn` e `.gitignore`. |
| NoPackageAnalysis | Specifica che pack non deve eseguire l'analisi del pacchetto dopo la compilazione di quest'ultimo. |
| OutputDirectory | Specifica la cartella in cui è archiviato il pacchetto creato. Se si specifica alcuna cartella, viene utilizzata la cartella corrente. |
| Proprietà | Dovrebbe essere visualizzato ultima nella riga di comando dopo le altre opzioni. Specifica un elenco di proprietà che eseguono l'override di valori nel file di progetto. visualizzare [proprietà di progetto MSBuild comuni](/visualstudio/msbuild/common-msbuild-project-properties) per i nomi delle proprietà. In questo caso l'argomento della proprietà è un elenco di token = coppie valore, separate da punti e virgola, in cui ogni occorrenza di `$token$` nella `.nuspec` file verrà sostituito con il valore specificato. I valori possono essere stringhe tra virgolette. Si noti che per la proprietà "Configurazione", il valore predefinito è "Debug". Per modificare una configurazione rilascio, usare `-Properties Configuration=Release`. |
| Suffisso | *(3.4.4+)*  Aggiunge un suffisso per il numero di versione generata internamente, in genere usato per l'accodamento compilazione o altri identificatori di versione non definitiva. Ad esempio, usando `-suffix nightly` verrà creato un pacchetto con una simile a numeri di versione `1.2.3-nightly`. I suffissi devono iniziare con una lettera per evitare gli avvisi, errori e potenziali incompatibilità con diverse versioni di NuGet e la gestione pacchetti NuGet. |
| Simboli | Specifica che il pacchetto contiene origini e simboli. Se usato con un `.nuspec` file, verrà creato un file di pacchetto NuGet normale e di pacchetto di simboli corrispondente. Per impostazione predefinita viene creato un [pacchetto di simboli legacy](../create-packages/Symbol-Packages.md). Il nuovo formato consigliato per i pacchetti di simboli è l'estensione snupkg. Vedere [Creazione di pacchetti di simboli (estensione snupkg)](../create-packages/Symbol-Packages-snupkg.md). |
| Strumento | Specifica che i file di output del progetto devono essere inseriti nel `tool` cartella. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |
| Versione | Sostituisce il numero di versione dal `.nuspec` file. |

Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Esclusione delle dipendenze di sviluppo

Alcuni pacchetti NuGet sono utili come dipendenze di sviluppo, che aiuta a creare una libreria personalizzata, ma non sono necessariamente necessarie come dipendenze di pacchetto effettivo.

Il `pack` comando verrà ignorati `package` voci `packages.config` che hanno il `developmentDependency` attributo impostato su `true`. Queste voci non includerà come delle dipendenze del pacchetto creato.

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

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
