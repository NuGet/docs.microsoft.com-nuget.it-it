---
title: Informazioni di riferimento sulla versione del pacchetto NuGet
description: Informazioni dettagliate su come specificare i numeri di versione e gli intervalli per altri pacchetti da cui dipende un pacchetto NuGet e sulla modalità di installazione delle dipendenze.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020003"
---
# <a name="package-versioning"></a>Controllo delle versioni dei pacchetti

A un pacchetto specifico viene sempre fatto riferimento usando l'identificatore del pacchetto e un numero di versione esatto. [Entity Framework](https://www.nuget.org/packages/EntityFramework/) su NuGet.org, ad esempio, sono disponibili diverse dozzine di pacchetti specifici, che vanno dalla versione *4.1.10311* alla versione *6.1.3* (la versione stabile più recente) e da un'ampia gamma di versioni non definitive come *6.2.0-beta1* .

Quando si crea un pacchetto, si assegna un numero di versione specifico con un suffisso di testo non definitiva facoltativo. Quando si utilizzano i pacchetti, d'altra parte, è possibile specificare un numero di versione esatto o un intervallo di versioni accettabili.

In questo argomento

- [Nozioni di base sulle versioni](#version-basics) , inclusi i suffissi di versione non definitiva.
- [Intervalli di versione e caratteri jolly](#version-ranges-and-wildcards)
- [Numeri di versione normalizzati](#normalized-version-numbers)

## <a name="version-basics"></a>Nozioni fondamentali sulle versioni

Un numero di versione specifico è nel formato *Major. minor. patch [-suffisso]* , dove i componenti hanno i significati seguenti:

- *Principale*: Modifiche che causano un'interruzione
- *Secondario*: nuove funzionalità, ma compatibili con le versioni precedenti
- *Patch*: solo correzioni di bug compatibili con le versioni precedenti
- *-Suffisso* (facoltativo): un trattino seguito da una stringa che indica una versione non definitiva (in base al [controllo delle versioni semantico o alla convenzione SemVer 1,0](http://semver.org/spec/v1.0.0.html)).

**Esempi:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org rifiuta il caricamento di un pacchetto che non dispone di un numero di versione esatto. La versione deve essere specificata nel `.nuspec` file di progetto o utilizzato per creare il pacchetto.

### <a name="pre-release-versions"></a>Versioni non definitive

Tecnicamente, i creatori di pacchetti possono usare qualsiasi stringa come suffisso per indicare una versione provvisoria, perché NuGet considera la versione non definitiva e non esegue altre interpretazioni. In altre parole, NuGet Visualizza la stringa di versione completa in qualsiasi interfaccia utente, lasciando l'interpretazione del significato del suffisso al consumer.

Ciò premesso, gli sviluppatori di pacchetti seguono generalmente le convenzioni di denominazione riconosciute:

- `-alpha`: Versione Alpha, in genere usata per la sperimentazione e il lavoro in corso.
- `-beta`: versione beta, in genere completa dal punto di vista funzionale per il successivo rilascio pianificato, ma può contenere bug noti.
- `-rc`: versione finale candidata, in genere potenzialmente finale (stabile) se non emergono bug significativi.

> [!Note]
> NuGet 4.3.0 + supporta [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), che supporta i numeri di versione non definitiva con la notazione del punto, come in *1.0.1-Build. 23*. La notazione con punto non è supportata con le versioni di NuGet precedenti alla versione 4.3.0. È possibile usare un form come *1.0.1-build23*.

Quando si risolvono i riferimenti del pacchetto e più versioni del pacchetto differiscono solo per il suffisso, NuGet sceglie una versione senza suffisso, quindi applica la precedenza alle versioni non definitive in ordine alfabetico inverso. Le seguenti versioni, ad esempio, verrebbero scelte nell'ordine esatto indicato:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Controllo delle versioni semantico 2.0.0

Con NuGet 4.3.0 + e Visual Studio 2017 versione 15.3 +, NuGet supporta il [controllo delle versioni semantico 2.0.0](http://semver.org/spec/v2.0.0.html).

Una certa semantica di SemVer versione 2.0.0 non è supportata nei client meno recenti. NuGet considera la versione del pacchetto come SemVer v 2.0.0 specifica se una delle seguenti istruzioni è vera:

- L'etichetta della versione non definitiva è separata da punti, ad esempio *1.0.0-Alpha. 1*
- La versione include metadati di compilazione, ad esempio *1.0.0 + githash*

Per nuget.org, un pacchetto viene definito come pacchetto SemVer versione 2.0.0 se una delle seguenti istruzioni è vera:

- La versione del pacchetto è conforme a SemVer v 2.0.0 ma non è conforme a SemVer v 1.0.0, come definito sopra.
- Uno degli intervalli di versioni delle dipendenze del pacchetto ha una versione minima o massima conforme a SemVer v 2.0.0 ma non conforme a SemVer v 1.0.0, definita in precedenza; ad esempio, *[1.0.0-Alpha. 1,)* .

Se si carica un pacchetto specifico di SemVer v 2.0.0 in nuget.org, il pacchetto è invisibile ai client meno recenti e disponibile solo per i client NuGet seguenti:

- NuGet 4.3.0 +
- Visual Studio 2017 versione 15.3 +
- Visual Studio 2015 con [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Client di terze parti:

- Rider JetBrains
- Paket versione 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Intervalli di versione e caratteri jolly

Quando si fa riferimento alle dipendenze dei pacchetti, NuGet supporta l'uso della notazione intervallo per specificare gli intervalli di versione, riepilogati come segue:

| Notation | Regola applicata | DESCRIZIONE |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | Versione minima, inclusivo |
| (1.0,) | x > 1,0 | Versione minima, esclusiva |
| [1.0] | x = = 1,0 | Corrispondenza esatta della versione |
| (,1.0] | x ≤ 1,0 | Versione massima, inclusivo |
| (,1.0) | x < 1,0 | Versione massima, esclusiva |
| [1.0,2.0] | 1,0 ≤ x ≤ 2,0 | Intervallo esatto, inclusivo |
| (1.0,2.0) | 1,0 < x < 2,0 | Intervallo esatto, esclusivo |
| [1.0,2.0) | 1,0 ≤ x < 2,0 | Versione minima e esclusiva mista inclusa |
| (1.0)    | non valido | non valido |

Quando si usa il formato PackageReference, NuGet supporta anche l'uso di una \*notazione con caratteri jolly,, per le parti del numero del suffisso principale, secondario, patch e di versione non definitiva. I caratteri jolly non sono supportati con `packages.config` il formato.

> [!Note]
> Gli intervalli di versione in PackageReference includono versioni preliminari. Per impostazione predefinita, le versioni a virgola mobile non risolvono le versioni provvisorie a meno che non sia stato scelto Per lo stato della richiesta di funzionalità correlata, vedere il [problema 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Esempi

Specificare sempre un intervallo di versione o di versione per le dipendenze dei `packages.config` pacchetti nei file `.nuspec` di progetto, file e file. Senza una versione o un intervallo di versioni, NuGet 2.8. x e versioni precedenti scelgono la versione più recente del pacchetto disponibile durante la risoluzione di una dipendenza, mentre NuGet 3. x e versioni successive scelgono la versione del pacchetto più bassa. La specifica di una versione o di un intervallo di versioni evita questa incertezza.

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

In `packages.config`ogni dipendenza viene elencata con un attributo `version` esatto utilizzato durante il ripristino dei pacchetti. L' `allowedVersions` attributo viene utilizzato solo durante le operazioni di aggiornamento per vincolare le versioni a cui è possibile aggiornare il pacchetto.

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

**Riferimenti nei `.nuspec` file**

L' `version` attributo in un `<dependency>` elemento descrive le versioni di intervallo accettabili per una dipendenza.

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
> Si tratta di una modifica di rilievo per NuGet 3,4 e versioni successive.

Quando si ottengono pacchetti da un repository durante le operazioni di installazione, reinstallazione o ripristino, NuGet 3.4 + considera i numeri di versione come segue:

- Gli zeri iniziali vengono rimossi dai numeri di versione:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Uno zero nella quarta parte del numero di versione verrà omesso

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`le `restore` operazioni e normalizzano le versioni quando possibile. Per i pacchetti già compilati, la normalizzazione non influisce sui numeri di versione dei pacchetti stessi. influiscono solo sul modo in cui NuGet corrisponde alle versioni durante la risoluzione delle dipendenze.

Tuttavia, i repository dei pacchetti NuGet devono considerare questi valori nello stesso modo in cui NuGet per evitare la duplicazione della versione del pacchetto. Un repository che contiene la versione *1,0* di un pacchetto non deve inoltre ospitare la versione *1.0.0* come pacchetto separato e diverso.
