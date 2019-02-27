---
title: Riferimenti della versione del pacchetto NuGet
description: Tutti i dettagli su come specificare i numeri di versione e gli intervalli per gli altri pacchetti su cui dipende un pacchetto NuGet e modalità di installazione delle dipendenze.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852468"
---
# <a name="package-versioning"></a>Controllo delle versioni dei pacchetti

Un pacchetto specifico fa sempre riferimento utilizzando il relativo identificatore di pacchetto e un numero di versione esatto. Ad esempio, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) ha diverse decine specifici dei pacchetti disponibili, che vanno dalla versione in nuget.org *4.1.10311* alla versione *6.1.3* (l'ultima versione stabile da Release) e, ad esempio un'ampia gamma di versioni non definitive *6.2.0-beta1*.

Quando si crea un pacchetto, si assegna un numero di versione specifico con un suffisso di versione non definitiva facoltativa in formato testo. Quando si utilizzano i pacchetti, d'altra parte, è possibile specificare un numero di versione esatto o un intervallo di versioni accettabili.

In questo argomento

- [Nozioni fondamentali sulla versione](#version-basics) incluse versioni non definitive suffissi.
- [I caratteri jolly e intervalli di versione](#version-ranges-and-wildcards)
- [Numeri di versione normalizzata](#normalized-version-numbers)

## <a name="version-basics"></a>Nozioni fondamentali sulla versione

Numero di versione specifico è nel formato *Major [-suffisso]*, in cui i componenti hanno i significati seguenti:

- *Principali*: Modifiche che causano un'interruzione
- *Minori*: nuove funzionalità, ma compatibili con le versioni precedenti
- *Patch*: solo correzioni di bug compatibili con le versioni precedenti
- *-Suffisso* (facoltativo): un trattino seguita da una stringa che indica una versione non definitiva (segue il [convenzione di Versionamento semantico o SemVer 1.0](http://semver.org/spec/v1.0.0.html)).

**Esempi:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> NuGet.org Rifiuta qualsiasi il caricamento del pacchetto che non dispone di un numero di versione esatto. La versione deve essere specificata nel `.nuspec` o file di progetto usato per creare il pacchetto.

### <a name="pre-release-versions"></a>Versioni non definitive

Tecnicamente, gli autori dei pacchetti possono utilizzare qualsiasi stringa come un suffisso per indicare una versione non definitiva, perché NuGet considera tale versione di qualsiasi versione non definitiva e non rende interpretazione di altri. Vale a dire, NuGet consente di visualizzare la versione completa di stringhe nell'interfaccia utente di qualsiasi è coinvolta, lasciando l'interpretazione del significato del suffisso per il consumer.

Ciò premesso, gli sviluppatori di pacchetti in genere seguono le convenzioni di denominazione riconosciute:

- `-alpha`: Versioni alfa, in genere usata per lavoro in corso e sperimentazione.
- `-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.
- `-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.

> [!Note]
> NuGet 4.3.0 + supporta [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), che supporta i numeri di versione non definitiva con la notazione del punto, come mostrato nella *1.0.1-build.23*. La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0. È possibile usare un modulo, ad esempio *1.0.1-build23*.

Durante la risoluzione di riferimenti ai pacchetti e più versioni del pacchetto sono diversi solo per il suffisso, NuGet sceglie una versione senza suffisso, prima di tutto, quindi si applica la priorità per versioni non definitive in ordine alfabetico inverso. Ad esempio, le versioni seguenti viene scelta in base all'ordine esatto illustrato:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Versionamento semantico 2.0.0

Con NuGet 4.3.0 + e Visual Studio 2017 versione 15.3 +, NuGet supporta [Versionamento semantico 2.0.0](http://semver.org/spec/v2.0.0.html).

Determinati semantica di SemVer v2.0.0 non è supportata nel client meno recenti. NuGet considera una versione del pacchetto sia v2.0.0 SemVer specifici se una delle seguenti affermazioni è vera:

- L'etichetta di versioni non definitive è delimitato da punti, ad esempio, *1.0.0-alpha.1*
- La versione contiene metadati di compilazione, ad esempio, *1.0.0+githash*

Per nuget.org, un pacchetto è definito come un pacchetto v2.0.0 SemVer se una delle seguenti affermazioni è vera:

- La versione del pacchetto è compatibile con SemVer v2.0.0 ma non SemVer v1.0.0 conforme, come definito in precedenza.
- Uno degli intervalli di versione delle dipendenze del pacchetto ha una versione minima o massima che è compatibile con SemVer v2.0.0 ma non SemVer v1.0.0 conforme, definiti in precedenza; ad esempio, *[1.0.0-alpha.1,)*.

Se si carica un pacchetto specifico v2.0.0 SemVer su nuget.org, il pacchetto sia visibile ai client meno recenti e disponibile per i seguenti client di NuGet:

- NuGet 4.3.0+
- Visual Studio 2017 version 15.3+
- Visual Studio 2015 con [v3.6.0 VSIX di NuGet](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Client di terze parti:

- Rider JetBrains
- Paket versione 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>I caratteri jolly e intervalli di versione

Quando si fa riferimento alle dipendenze di pacchetto, NuGet supporta utilizzando la notazione di intervallo per la specifica di intervalli di versione, riepilogati come segue:

| Notation | Regola applicata | Descrizione |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Versione minima, inclusivo |
| (1.0,) | x > 1.0 | Versione minima, esclusivo |
| [1.0] | x == 1.0 | Corrispondenza esatta della versione |
| (,1.0] | x ≤ 1.0 | Versione massima, inclusivo |
| (,1.0) | x < 1.0 | Versione massima, esclusivo |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervallo esatto, inclusivo |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervallo esatto, esclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Inclusivo minimo ed esclusivo massimo mista |
| (1.0)    | non valido | non valido |

Quando si usa il formato PackageReference, NuGet supporta anche l'utilizzo di una notazione con caratteri jolly, \*per principale, secondaria, Patch e parti del suffisso di versione non definitiva del numero. I caratteri jolly non sono supportate con il `packages.config` formato.

> [!Note]
> Le versioni non definitive non sono incluse durante la risoluzione di intervalli di versione. Versioni non definitive *vengono* incluso quando si usa un carattere jolly (\*). L'intervallo di versioni *[1.0,2.0]*, ad esempio, non includere 2.0-beta, ma la notazione con caratteri jolly _2.0-*_ viene. Visualizzare [emettere 912](https://github.com/NuGet/Home/issues/912) per ulteriori informazioni sui caratteri jolly di versioni non definitive.

### <a name="examples"></a>Esempi

Specificare sempre una versione o intervallo di versioni per le dipendenze dei pacchetti nei file di progetto `packages.config` file, e `.nuspec` file. Senza una versione o intervallo di versioni, NuGet 2.8.x e in precedenza sceglie la versione più recente del pacchetto disponibile quando si risolve una dipendenza, mentre NuGet 3.x e versioni successive sceglie la versione del pacchetto più bassa. Specificare una versione o intervallo consente di evitare questa incertezza.

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

**Fa riferimento `packages.config`:**

Nelle `packages.config`, tutte le dipendenze sia elencata con un valore esatto `version` attributo che viene usato quando il ripristino dei pacchetti. Il `allowedVersions` attributo viene utilizzato solo durante le operazioni di aggiornamento per vincolare le versioni a cui il pacchetto potrebbe essere aggiornato.

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

**Fa riferimento `.nuspec` file**

Il `version` dell'attributo un `<dependency>` elemento descrive le versioni di intervallo sono accettabili per una dipendenza.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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

Durante l'acquisizione di pacchetti da un repository durante l'installazione, reinstallare o ripristinare le operazioni, NuGet 3.4 + considera i numeri di versione come segue:

- Gli zeri iniziali vengono rimossi dai numeri di versione:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Verrà omesso uno zero nella quarta parte del numero di versione

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Questa normalizzazione non influisce sui numeri di versione nei pacchetti stessi; ha effetto sul modo in cui NuGet corrisponde solo versioni quando la risoluzione delle dipendenze.

Tuttavia, i repository dei pacchetti NuGet devono considerare questi valori nello stesso modo come NuGet per evitare la duplicazione di versione del pacchetto. In questo modo un repository che contiene la versione *1.0* di un pacchetto non deve inoltre ospitare versione *1.0.0* come pacchetto separato e diverso.
