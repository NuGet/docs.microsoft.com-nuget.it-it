---
title: Procedure consigliate per la creazione di pacchetti
description: Guida generale alle procedure consigliate per la creazione di pacchetti di NuGet qualità elevata.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: ec1532900bed7d13ea2400afe9f855105a5c2fde
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209891"
---
# <a name="package-authoring-best-practices"></a>Procedure consigliate per la creazione di pacchetti

Queste linee guida hanno lo scopo di fornire agli NuGet di pacchetti un riferimento leggero per creare e pubblicare pacchetti di alta qualità. Si concentrerà principalmente sulle procedure consigliate specifiche del pacchetto, ad esempio i metadati e la creazione di pacchetti. Per suggerimenti più approfonditi per la creazione di librerie di alta qualità, vedere le linee guida per le librerie [open source](/dotnet/standard/library-guidance/).NET.

## <a name="types-of-recommendations"></a>Tipi di suggerimenti

Ogni articolo presenta quattro tipi di suggerimenti: **Da fare**, **Da considerare**, **Da evitare** e **Da non fare**. Il tipo di raccomandazione indica quanto deve essere seguita.

È opportuno seguire quasi sempre un suggerimento di tipo **Da fare**. Esempio:

✔️ DO includere una breve descrizione del pacchetto che ne descriva lo scopo.

D'altra parte, **è** in genere consigliabile seguire le raccomandazioni, ma esistono eccezioni legittime alla regola:

✔️ VALUTARE la scelta di un nome di pacchetto NuGet con un prefisso che soddisfi i [criteri](../nuget-org/id-prefix-reservation.md) per riservare il prefisso NuGet.

I suggerimenti di tipo **Da evitare** si riferiscono a operazioni in genere non consigliabili, ma che talvolta possono avere un'utilità:

❌EVITARE NuGet di pacchetti che richiedono una versione esatta.

E infine, i suggerimenti di tipo **Da non fare** indicano operazioni che quasi sempre è necessario evitare:

❌ NON usare la `LicenseUrl` proprietà metadata.

## <a name="create-a-nuget-package"></a>Creare un pacchetto NuGet

Il modo più recente consigliato per creare un pacchetto NuGet pacchetto è da un [progetto di tipo SDK.](../resources/check-project-format.md) Le proprietà del progetto in stile SDK, inclusi [i metadati del pacchetto](/dotnet/standard/frameworks) e del framework di destinazione, sono definite nel file di [progetto](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file). [](#package-metadata)

Creare un pacchetto dal progetto di tipo SDK definendo le proprietà necessarie e includendo in Visual Studio [o](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) nell'interfaccia della riga di comando [dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

✔️ creare un progetto di tipo SDK e creare (creare un pacchetto) il pacchetto usando Visual Studio o l'interfaccia della riga di comando dotnet.

Per indicazioni più dettagliate sulla creazione di pacchetti, inclusi gli strumenti client necessari, l'esempio di file di progetto e i comandi, vedere Creare un pacchetto NuGet usando l'interfaccia della riga di comando [dotnet.](./creating-a-package-dotnet-cli.md)

Per decidere quali framework .NET sono di destinazione, vedere le linee guida più recenti per la destinazione [multipiattaforma.](/dotnet/standard/library-guidance/cross-platform-targeting)

## <a name="package-metadata"></a>Metadati dei pacchetti

I metadati sono un componente fondamentale di qualsiasi NuGet pacchetto. La qualità dei metadati può influenzare notevolmente l'individuabilità, l'usabilità e l'affidabilità del pacchetto.

In Visual Studio, il modo consigliato per specificare i metadati del pacchetto è Project > proprietà [nome Project] > pacchetto.

Gli elementi dei metadati del pacchetto possono [anche essere specificati direttamente nel file di progetto](./creating-a-package-msbuild.md#set-properties).

Di seguito è riportato un mapping di tabella e la descrizione degli elementi dei metadati del pacchetto disponibili:

| Visual Studio proprietà                       | [Project nome file/MSBuild proprietà](/dotnet/core/tools/csproj#packagereleasenotes)                              | [Nome proprietà Nuspec](/nuget/reference/nuspec#general-form-and-schema)   | Descrizione                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`id`](/nuget/reference/nuspec#id)                                        | Nome o identificatore del pacchetto.                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](/nuget/reference/msbuild-targets#pack-target)                                                      | [`version`](/nuget/reference/nuspec#version)                              | Versione del pacchetto NuGet.                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](/nuget/reference/msbuild-targets#pack-target)                                                                 | [`authors`](/nuget/reference/nuspec#authors)                              | Elenco delimitato da virgole di autori di pacchetti, spesso usando il nome "pretty name" dell'utente o di un'organizzazione.           |
| [`Description`](#description)                     | [`Description`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`description`](/nuget/reference/nuspec#description)                      | Descrizione del pacchetto.                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`copyright`](/nuget/reference/nuspec#copyright)                          | Informazioni sul copyright per il pacchetto.                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)     | [`license type="expression"`](/nuget/reference/nuspec#license)            | Espressione di licenza SPDX.                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)           | [`license type="file"`](/nuget/reference/nuspec#license)                  | Percorso di un file di licenza personalizzato.                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](/nuget/reference/nuspec#projecturl)                        | URL per la home page del progetto.                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                      | [`icon`](/nuget/reference/nuspec#icon)                                    | Percorso del file di immagine dell'icona del pacchetto.                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](/nuget/reference/msbuild-targets#pack-target)                                                       | [`repository url`](/nuget/reference/nuspec#repository)                    | URL del repository da cui è stato compilato il pacchetto.                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](/nuget/reference/msbuild-targets#pack-target)                                                     | [`repository type`](/nuget/reference/nuspec#repository)                   | Tipo di repository a cui punta l'URL del repository ,ad esempio "git".                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`tags`](/nuget/reference/nuspec#tags)                                    | Elenco di tag e parole chiave delimitati da spazi che descrivono il pacchetto. I tag vengono usati per la ricerca di pacchetti.     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](/nuget/reference/msbuild-targets#pack-target)                                         | [`releaseNotes`](/nuget/reference/nuspec#releasenotes)                    | Descrizione delle modifiche apportate in questa versione del pacchetto.                                                     |
### <a name="package-id"></a>ID pacchetto

Se si pubblica un pacchetto completamente nuovo:

✔️ scegliere un ID pacchetto univoco e chiaramente differenziato dai pacchetti esistenti in NuGet.org.
> È possibile verificare se un ID pacchetto è univoco e differenziale cercando l'ID in NuGet.org o controllando se esiste il collegamento seguente: https://www.nuget.org/packages/<package name \> .

✔️ prendere in considerazione la scelta NuGet nome di un pacchetto con un prefisso che soddisfi i NuGet di [prenotazione del prefisso di .](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)
> La prenotazione dell'ID prefisso per il pacchetto consente di ottenere il segno di spunta verificato: ![ immagine](media/Verified-check-mark.png)
> 
> Per altre [informazioni, vedere la documentazione sulla prenotazione del](../nuget-org/id-prefix-reservation.md) prefisso ID pacchetto.

### <a name="package-version"></a>Versione pacchetto

✔️ considerare l'uso [di SemVer per](https://semver.org/) la versione NuGet pacchetto.
> In sostanza, ciò significa usare il formato Major.Minor.Patch[-prerelease].

✔️ è possibile pubblicare un pacchetto come pacchetto [non](./prerelease-packages.md) definitiva se non è stabile o in anteprima.

Per indicazioni più avanzate, vedere la guida al controllo delle versioni della libreria [.NET.](/dotnet/standard/library-guidance/versioning)

### <a name="authors"></a>Autori

✔️ usare il campo autore per il nome "pretty name" dell'organizzazione o dell'utente.
> Ad esempio, se il nome utente di NuGet.org è "jdoe", l'uso di "Jane Doe" per il campo autore può aiutare gli utenti a riconoscermi come autore. Se il nome utente di NuGet.org dell'organizzazione è "ContosoToolkit", l'uso di "Contoso Corporation" può essere più riconoscibile e ispirare una maggiore fiducia dei consumatori.
### <a name="description"></a>Descrizione

✔️ DO includere una breve descrizione (fino a 4000 caratteri) per descrivere il pacchetto.
> Le descrizioni dei pacchetti sono uno dei campi più importanti visualizzati nella ricerca NuGet e saranno probabilmente la prima cosa che i potenziali consumer esaminano per determinare se un pacchetto è più indicato.

### <a name="copyright"></a>Copyright

✔️ PRENDERE IN CONSIDERAZIONE il copyright del pacchetto con "Copyright (c) <nome/società \> <\> anno."
>Un'informativa sul copyright indica essenzialmente che il lavoro non può essere copiato senza l'autorizzazione dell'utente. Includere un'informativa sul copyright nel pacchetto è facile e non può causare danni.

Esempio: Copyright (c) Contoso 2020

### <a name="licensing"></a>Gestione delle licenze

✔️ includere [un'espressione di licenza o un file di licenza nel pacchetto](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Per impostazione predefinita, per un progetto senza licenza viene utilizzato [il copyright esclusivo,](https://choosealicense.com/no-permission/)vale a dire che non è stata concessa a nessuno l'autorizzazione per usare il progetto.

❌ NON usare la proprietà dei `LicenseUrl` metadati deprecata.
> Ciò presenta ambiguità legale perché le modifiche delle licenze all'URL modificheranno retroattivamente la licenza visualizzata per le versioni precedenti del pacchetto.

#### <a name="if-your-package-is-open-source"></a>Se il pacchetto è [open source](https://opensource.org/osd)

✔️ scegliere [una licenza open source per](https://choosealicense.com/) rendere il pacchetto open source.
> *"Le licenze open source sono licenze conformi alla definizione open source. In breve, consentono di usare, modificare e condividere liberamente il software".* - Iniziativa open source. Per altre informazioni sul open source software e sull'iniziativa open source, vedere https://opensource.org/ .

✔️ CONSIDERARE [l'inclusione di un'espressione di licenza nel pacchetto](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Le espressioni di licenza vengono mostrate più chiaramente e rendono più evidente agli utenti se possono usare il pacchetto o se la licenza è cambiata. 
> [!Note]
> NuGet.org accetta solo espressioni di licenza per le licenze approvate dall'iniziativa Open Source o da Free Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Se il pacchetto non è open source

✔️ [includere un file di licenza nel pacchetto](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Qualsiasi file di licenza (.txt o MD) può essere aggiunto al pacchetto, incluse le licenze non standard. 

### <a name="project-url"></a>URL progetto

✔️ prendere in considerazione l'inclusione di un collegamento a un progetto, un repository o un sito Web aziendale associato.
> Il sito del progetto deve avere tutto ciò che gli utenti devono conoscere sul pacchetto e probabilmente sarà la posizione in cui gli utenti cercano la documentazione.

### <a name="icon"></a>Icona

✔️ considerare [l'inclusione di un'icona con il pacchetto](../reference/msbuild-targets.md#packing-an-icon-image-file) per differenziarlo visivamente. Si tratta di un'aggiunta relativamente piccola che può migliorare la percezione della qualità del pacchetto.
> Le icone possono essere specifiche di singoli pacchetti o essere un logo del marchio.

✔️ do use an image that is 128x128 and has a transparent background (PNG) for best viewing results.
> NuGet ridimensiona automaticamente l'immagine in base al client in cui viene visualizzata.

❌ NON usare la proprietà dei `IconUrl` metadati deprecata.

### <a name="repository-type-and-url"></a>Tipo di repository e URL

✔️ configurare il [collegamento](/dotnet/standard/library-guidance/sourcelink) all'origine per aggiungere automaticamente i metadati del controllo del codice sorgente al pacchetto NuGet e semplificare il debug della libreria.
> Collegamento all'origine aggiunge `Repository URL` automaticamente `Repository Type` e ai metadati del pacchetto. Aggiunge anche il commit specifico associato alla versione del pacchetto.

### <a name="tags"></a>Tag

✔️ includere diversi tag con termini chiave correlati al pacchetto per migliorare l'individuabilità.
> I tag vengono presi in considerazione nell'algoritmo di ricerca di NuGet.org e sono particolarmente utili per i termini che non sono presenti nell'ID pacchetto ma sono rilevanti.

Ad esempio, se si pubblicasse un pacchetto per registrare le stringhe nella console, si includerebbe: "registrazione, log, console, stringa, output"

### <a name="release-notes"></a>Note sulla versione

✔️ prendere in considerazione l'inclusione di note sulla versione con ogni aggiornamento che descrive le modifiche apportate.
> Anche se non è necessario un formato specifico per le note sulla versione, è consigliabile includere:
>
> 1. Modifiche che causano un'interruzione
> 2. Nuove funzionalità
> 3. Correzioni di bug
> 
> Se si tiene già traccia delle note sulla versione o di un log delle modifiche nel proprio repo, è anche possibile includere un collegamento al file pertinente.

## <a name="related-topics"></a>Argomenti correlati

- [Creare e pubblicare un pacchetto (interfaccia della riga di comando dotnet)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Creare e pubblicare un pacchetto (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)
