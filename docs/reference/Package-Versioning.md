---
title: Riferimento al pacchetto NuGet di versione
description: Informazioni precise e dettagliate su come specificare i numeri di versione e gli intervalli per altri pacchetti su cui dipende un pacchetto NuGet e modalità di installazione delle dipendenze.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: db529a4aa92f0f0bce0b52b21d2a01bf973d01f2
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817597"
---
# <a name="package-versioning"></a>Controllo delle versioni dei pacchetti

Un pacchetto specifico viene sempre definito tramite il relativo identificatore di pacchetto e un numero di versione esatta. Ad esempio, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) in nuget.org dispone di diversi i dozzina pacchetti di specifici disponibili, dalla versione *4.1.10311* alla versione *6.1.3* (l'ultima versione stabile Release) e un'ampia gamma di versioni non definitive *6.2.0-beta1*.

Quando si crea un pacchetto, si assegna un numero di versione specifico con un suffisso di testo pre-release facoltativo. Quando si utilizzano pacchetti, d'altra parte, è possibile specificare un numero di versione esatta o un intervallo di versioni accettabile.

In questo argomento

- [Nozioni fondamentali sulla versione](#version-basics) inclusi suffissi pre-release.
- [I caratteri jolly e intervalli di versione](#version-ranges-and-wildcards)
- [Numeri di versione normalizzata](#normalized-version-numbers)

## <a name="version-basics"></a>Nozioni fondamentali sulla versione

Il formato è un numero di versione specifico *patch [-suffisso]*, in cui i componenti presentano i significati seguenti:

- *Principali*: modifiche di rilievo
- *Secondaria*: nuove funzionalità, ma compatibile con le versioni precedenti
- *Patch*: compatibile solo correzioni di bug
- *-Suffisso* (facoltativo): un trattino seguito da una stringa che indica una versione non definitiva (seguente il [convenzione controllo delle versioni semantico o SemVer 1.0](http://semver.org/spec/v1.0.0.html)).

**Esempi:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org Rifiuta qualsiasi il caricamento del pacchetto che non dispone di un numero di versione esatta. La versione deve essere specificata nel `.nuspec` o file di progetto utilizzato per creare il pacchetto.

### <a name="pre-release-versions"></a>Versioni non definitive

Tecnicamente, agli autori dei pacchetti possono utilizzare qualsiasi stringa come suffisso per indicare una versione non definitiva, come NuGet considera qualsiasi versione di tale versione non definitiva e non rende interpretazione di altri. Vale a dire, NuGet consente di visualizzare la versione completa di stringa in qualsiasi interfaccia utente è interessata, lasciando l'interpretazione del significato del suffisso per il consumer.

Ciò premesso, sviluppatori del pacchetto è in genere seguono convenzioni di denominazione riconosciute:

- `-alpha`: Versione alfa, in genere utilizzata per la sperimentazione e in fase di elaborazione.
- `-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.
- `-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.

> [!Note]
> Supporta NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), che supporta i numeri di versione non definitiva con la notazione del punto, come in *1.0.1-build.23*. La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0. È possibile utilizzare un modulo come *1.0.1-build23*.

Durante la risoluzione dei riferimenti del pacchetto e più versioni di pacchetto diversi solo dal suffisso, NuGet sceglie innanzitutto una versione senza un suffisso, quindi si applica la priorità per la versione preliminare in ordine alfabetico inverso. Ad esempio, verrebbero scelta le versioni seguenti nell'ordine esatto indicato:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Controllo delle versioni semantico 2.0.0

Con Visual Studio 2017 versione 15.3 + e NuGet 4.3.0+ NuGet supporta [controllo delle versioni semantico 2.0.0](http://semver.org/spec/v2.0.0.html).

Determinate semantica di v 2.0.0 SemVer non è supportata in client meno recenti. NuGet si basa su una versione del pacchetto per essere v 2.0.0 SemVer specifico se viene soddisfatta una delle istruzioni seguenti:

- L'etichetta di versione non definitiva è delimitato da punti, ad esempio, *1.0.0-alpha.1*
- La versione dispone di metadati di compilazione, ad esempio, *1.0.0+githash*

Per nuget.org, un pacchetto è definito come un pacchetto v 2.0.0 SemVer se viene soddisfatta una delle istruzioni seguenti:

- La versione del pacchetto è v 2.0.0 SemVer compatibile ma non versione 1.0.0 SemVer compatibile, come precedentemente definito.
- Uno degli intervalli di versione del pacchetto dipendenza con una versione minima o massima è v 2.0.0 SemVer conforme, ma non versione 1.0.0 SemVer conforme, definiti in precedenza; ad esempio, *[1.0.0-alpha.1,)*.

Se si carica un pacchetto specifico v 2.0.0 SemVer nuget.org, il pacchetto è invisibile a client meno recenti e disponibile per i seguenti client NuGet:

- 4.3.0+ NuGet
- Visual Studio 2017 versione 15.3 +
- Visual Studio 2015 con [v3.6.0 VSIX NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (2.0.0+ .NET SDK)

Client di terze parti:

- JetBrains Roc
- Paket versione 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>I caratteri jolly e intervalli di versione

Quando si fa riferimento alle dipendenze di pacchetto, NuGet supporta utilizzando una notazione di intervallo per specificare gli intervalli di versione, riepilogati come segue:

| Notation | Regola applicata | Descrizione |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Versione minima, inclusivo |
| (1.0,) | x > 1.0 | Versione minima, esclusivo |
| [1.0] | x = = 1.0 | Corrispondenza esatta versione |
| (,1.0] | x ≤ 1.0 | Versione massima, inclusivo |
| (,1.0) | x < 1.0 | Versione massima, esclusivo |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Esatto intervallo |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervallo esatto, esclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Inclusivo minimo ed esclusivo massimo misto |
| (1.0)    | non valido | non valido |

Quando si utilizza il formato PackageReference, NuGet supporta inoltre l'utilizzo di una notazione dei caratteri jolly, \*, per principale, secondaria, Patch e parti di pre-release suffisso del numero. I caratteri jolly non sono supportate con il `packages.config` formato.

> [!Note]
> Le versioni non definitive non sono incluse durante la risoluzione di intervalli di versione. Versioni non definitive *sono* incluso quando si utilizza un carattere jolly (\*). L'intervallo di versioni *[1.0,2.0]*, ad esempio, non includere 2.0 beta, ma la notazione dei caratteri jolly _2.0-*_ does. Vedere [emettere 912](https://github.com/NuGet/Home/issues/912) per ulteriori informazioni sui caratteri jolly di pre-release.

### <a name="examples"></a>Esempi

Specificare una versione o l'intervallo di versioni per le dipendenze dei pacchetti nel file di progetto, `packages.config` file, e `.nuspec` file. Senza una versione o l'intervallo di versioni, NuGet 2.8.x e precedenza sceglie la versione più recente di pacchetti disponibili durante la risoluzione di una dipendenza, mentre NuGet 3. x e versioni successive sceglie la versione del pacchetto più bassa. Specificare una versione o intervallo evita l'incertezza.

#### <a name="references-in-project-files-packagereference"></a>Riferimenti nel file di progetto (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Fa riferimento nelle `packages.config`:**

In `packages.config`, tutte le dipendenze sia elencata con un valore esatto `version` attributo utilizzato durante il ripristino dei pacchetti. Il `allowedVersions` attributo viene utilizzato solo durante le operazioni di aggiornamento per vincolare le versioni a cui il pacchetto potrebbe essere aggiornato.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Fa riferimento nelle `.nuspec` file**

Il `version` attributo un `<dependency>` elemento descrive le versioni di intervallo sono accettabili per una dipendenza.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Numeri di versione normalizzata

> [!Note]
> Si tratta di una modifica di rilievo per NuGet 3.4 e versioni successive.

Quando l'acquisizione di pacchetti da un repository durante l'installazione, reinstallare o ripristinare le operazioni, NuGet 3.4 + considera i numeri di versione nel modo seguente:

- Gli zeri iniziali vengono rimossi dai numeri di versione:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Verrà omesso uno zero nella quarta parte del numero di versione

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Questa normalizzazione non influisce sui numeri di versione dei pacchetti. interessa solo la modalità NuGet versioni corrispondenti durante la risoluzione delle dipendenze.

Tuttavia, il repository di pacchetti NuGet deve considerare questi valori nello stesso modo come NuGet per evitare la duplicazione di versione del pacchetto. In questo modo un repository che contiene la versione *1.0* di un pacchetto non dovrebbero inoltre ospitare versione *1.0.0* come pacchetto separato e diverso.
