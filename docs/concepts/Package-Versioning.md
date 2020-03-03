---
title: Informazioni di riferimento sulle versioni dei pacchetti NuGet
description: Informazioni dettagliate su come specificare i numeri di versione e gli intervalli per altri pacchetti da cui dipende un pacchetto NuGet e sulla modalità di installazione delle dipendenze.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 912c0d015e2f499bc7386483bc6c35ecd765d3d4
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230863"
---
# <a name="package-versioning"></a>Controllo delle versioni dei pacchetti

A un pacchetto specifico viene sempre fatto riferimento usando l'identificatore del pacchetto e un numero di versione esatto. Per [Entity Framework](https://www.nuget.org/packages/EntityFramework/) su nuget.org, ad esempio, sono disponibili alcune decine di pacchetti specifici, compresi tra la versione *4.1.10311* e la versione *6.1.3* (la versione stabile più recente) e svariate versioni non definitive come *6.2.0-beta1*.

Quando si crea un pacchetto, si assegna un numero di versione specifico con un suffisso di testo per la versione non definitiva facoltativo. Quando si utilizzano i pacchetti, invece, è possibile specificare un numero di versione esatto o un intervallo di versioni accettabili.

In questo argomento

- [Nozioni di base sulle versioni](#version-basics), inclusi i suffissi di versione non definitiva.
- [Intervalli di versione](#version-ranges)
- [Numeri di versione normalizzati](#normalized-version-numbers)

## <a name="version-basics"></a>Nozioni di base sulle versioni

Un numero di versione specifico è nel formato *Principale.Secondaria.Patch[-Suffisso]*, dove i singoli componenti hanno i significati seguenti:

- *Principale*: modifiche di rilievo
- *Minor*: nuove funzionalità, ma compatibili con le versioni precedenti
- *Patch*: solo correzioni di bug compatibili con le versioni precedenti
- *-Suffisso* (facoltativo): un trattino seguito da una stringa che indica una versione non definitiva (in base alla [convenzione Semantic Versioning o SemVer 1.0](https://semver.org/spec/v1.0.0.html)).

**Esempi:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org rifiuta il caricamento di un pacchetto senza un numero di versione esatto. La versione deve essere specificata nel file `.nuspec` o nel file di progetto usato per creare il pacchetto.

### <a name="pre-release-versions"></a>Versioni non definitive

Dal punto di vista tecnico, i creatori di pacchetti possono usare qualsiasi stringa come suffisso per indicare una versione non definitiva, perché NuGet considera una versione con questa caratteristica non definitiva senza altre interpretazioni. In altre parole, NuGet visualizza la stringa di versione completa in qualsiasi interfaccia utente, lasciando l'interpretazione del significato del suffisso all'utente.

Ciò premesso, gli sviluppatori di pacchetti seguono generalmente convenzioni di denominazione riconosciute:

- `-alpha`: versione Alpha, in genere usata per il lavoro in corso e la sperimentazione.
- `-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.
- `-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.

> [!Note]
> NuGet 4.3.0+ supporta [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), ovvero numeri di versione non definitiva con la notazione con punto, come in *1.0.1-build.23*. La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0. È possibile usare un formato come *1.0.1-build23*.

Se durante la risoluzione dei riferimenti al pacchetto risultano più versioni del pacchetto che differiscono solo per il suffisso, NuGet sceglie prima una versione senza suffisso, quindi applica la precedenza alle versioni non definitive in ordine alfabetico inverso. Le versioni seguenti, ad esempio, verrebbero scelte nell'esatto ordine indicato:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantic Versioning 2.0.0

Con NuGet 4.3.0+ e Visual Studio 2017 versione 15.3+, NuGet supporta la convenzione [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

Certe regole semantiche di SemVer 2.0.0 non sono supportate nei client meno recenti. NuGet considera la versione di un pacchetto come specifica di SemVer 2.0.0 se una delle affermazioni seguenti è vera:

- L'etichetta della versione non definitiva è separata da punti, ad esempio *1.0.0-alpha.1*
- La versione include metadati di compilazione, ad esempio *1.0.0+githash*

Per nuget.org, un pacchetto viene definito come pacchetto SemVer 2.0.0 se una delle affermazioni seguenti è vera:

- La versione del pacchetto è conforme a SemVer 2.0.0 ma non è conforme a SemVer 1.0.0, come definito sopra.
- Uno degli intervalli di versioni delle dipendenze del pacchetto ha una versione minima o massima conforme a SemVer 2.0.0 ma non conforme a SemVer 1.0.0, definita in precedenza. Ad esempio, *[1.0.0-alpha.1, )*.

Se si carica un pacchetto specifico di SemVer 2.0.0 in nuget.org, il pacchetto è invisibile ai client meno recenti e disponibile solo per i client NuGet seguenti:

- NuGet 4.3.0+
- Visual Studio 2017 versione 15.3+
- Visual Studio 2015 con [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Client di terze parti:

- JetBrains Rider
- Paket versione 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Intervalli di versione

Quando si fa riferimento alle dipendenze dei pacchetti, NuGet supporta l'uso della notazione con intervallo per specificare gli intervalli di versione, riepilogati come segue:

| Notation | Regola applicata | Descrizione |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Versione minima, inclusiva |
| (1.0,) | x > 1.0 | Versione minima, esclusiva |
| [1.0] | x == 1.0 | Corrispondenza esatta della versione |
| (,1.0] | x ≤ 1.0 | Versione massima, inclusiva |
| (,1.0) | x < 1.0 | Versione massima, esclusiva |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Intervallo esatto, inclusivo |
| (1.0,2.0) | 1.0 < x < 2.0 | Intervallo esatto, esclusivo |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Versione minima inclusiva e massima esclusiva mista |
| (1.0)    | non valido | non valido |

Quando si usa il formato PackageReference, NuGet supporta anche l'uso di una notazione mobile, \*, per le parti principali, secondarie, patch e del suffisso di versione non definitiva del numero. Le versioni a virgola mobile non sono supportate con il formato `packages.config`.

> [!Note]
> Gli intervalli di versione in PackageReference includono le versioni non definitive. Per impostazione predefinita, le versioni mobili non risolvono le versioni non definitive se non con consenso esplicito. Per lo stato della richiesta di funzionalità correlata, vedere il [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Esempi

Specificare sempre una versione o un intervallo di versioni per le dipendenze dei pacchetti nei file di progetto, nei file `packages.config` e nei file `.nuspec`. Senza una versione o un intervallo di versioni, NuGet 2.8.x e versioni precedenti scelgono la versione più recente del pacchetto disponibile durante la risoluzione di una dipendenza, mentre NuGet 3.x e versioni successive scelgono la versione del pacchetto più bassa. La specifica di una versione o di un intervallo di versioni evita questa incertezza.

#### <a name="references-in-project-files-packagereference"></a>Riferimenti nei file di progetto (PackageReference)

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

**Riferimenti in `packages.config`:**

In `packages.config` ogni dipendenza viene elencata con un attributo `version` esatto usato durante il ripristino dei pacchetti. L'attributo `allowedVersions` viene usato solo durante le operazioni di aggiornamento per vincolare le versioni per l'aggiornamento del pacchetto.

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

**Riferimenti nei file `.nuspec`**

L'attributo `version` in un elemento `<dependency>` descrive le versioni di intervallo accettabili per una dipendenza.

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

## <a name="normalized-version-numbers"></a>Numeri di versione normalizzati

> [!Note]
> Si tratta di una modifica di rilievo per NuGet 3.4 e versioni successive.

Quando si ottengono pacchetti da un repository durante le operazioni di installazione, reinstallazione o ripristino, NuGet 3.4+ gestisce i numeri di versione come segue:

- Gli zeri iniziali vengono rimossi dai numeri di versione:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- uno zero nella quarta parte del numero di versione verrà omesso

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Le operazioni `pack` e `restore` normalizzano le versioni quando possibile. Per i pacchetti già compilati, la normalizzazione non influisce sui numeri di versione dei pacchetti stessi, ma influisce solo sul modo in cui NuGet abbina le versioni durante la risoluzione delle dipendenze.

Tuttavia, i repository di pacchetti NuGet devono gestire questi valori nello stesso modo di NuGet per evitare la duplicazione della versione del pacchetto. Un repository che contiene la versione *1.0* di un pacchetto non deve inoltre ospitare la versione *1.0.0* come pacchetto separato e diverso.
