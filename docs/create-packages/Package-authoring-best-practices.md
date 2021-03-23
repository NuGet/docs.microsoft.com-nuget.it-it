---
title: Procedure consigliate per la creazione di pacchetti
description: Guida generale alle procedure consigliate per la creazione di pacchetti NuGet di alta qualità.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 7475cf655876f2c127e79a16ccf67c0c723d164f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859070"
---
# <a name="package-authoring-best-practices"></a>Procedure consigliate per la creazione di pacchetti

Questa guida è destinata a offrire agli autori di pacchetti NuGet un riferimento leggero per la creazione e la pubblicazione di pacchetti di alta qualità. Si concentra principalmente sulle procedure consigliate specifiche del pacchetto, ad esempio i metadati e la compressione. Per suggerimenti più approfonditi per la creazione di librerie di alta qualità, vedere la [Guida alla libreria open source](https://docs.microsoft.com/dotnet/standard/library-guidance/).NET.

## <a name="types-of-recommendations"></a>Tipi di suggerimenti

Ogni articolo presenta quattro tipi di suggerimenti: **Da fare**, **Da considerare**, **Da evitare** e **Da non fare**. Il tipo di raccomandazione indica il modo in cui deve essere rispettato.

È opportuno seguire quasi sempre un suggerimento di tipo **Da fare**. Ad esempio:

✔️ includere una breve descrizione del pacchetto che ne descriva le finalità.

D'altra parte, è opportuno **tenere in considerazione** le raccomandazioni, ma esistono eccezioni legittime alla regola:

✔️ VALUTARE la scelta di un nome di pacchetto NuGet con un prefisso che soddisfi i [criteri](https://docs.microsoft.com/nuget/reference/id-prefix-reservation) per riservare il prefisso NuGet.

I suggerimenti di tipo **Da evitare** si riferiscono a operazioni in genere non consigliabili, ma che talvolta possono avere un'utilità:

❌ EVITARE i riferimenti ai pacchetti NuGet che richiedono una versione esatta.

E infine, i suggerimenti di tipo **Da non fare** indicano operazioni che quasi sempre è necessario evitare:

❌ Non utilizzare la `LicenseUrl` Proprietà Metadata.

## <a name="create-a-nuget-package"></a>Creare un pacchetto NuGet

L'ultimo modo consigliato per creare un pacchetto NuGet è da un [progetto di tipo SDK](https://docs.microsoft.com/nuget/resources/check-project-format). Le proprietà del progetto di tipo SDK, inclusi il [Framework di destinazione](https://docs.microsoft.com/dotnet/standard/frameworks) e i [metadati del pacchetto](#package-metadata), sono definite nel file di [progetto](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Creare un pacchetto dal progetto in stile SDK definendo le proprietà e la compressione richieste in [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) o nell'interfaccia della riga di comando [DotNet](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).

✔️ creare un progetto di tipo SDK e creare (Pack) il pacchetto usando Visual Studio o l'interfaccia della riga di comando di DotNet.

Per istruzioni più dettagliate sulla creazione di pacchetti, inclusi gli strumenti client necessari, l'esempio di file di progetto e i comandi, vedere [creare un pacchetto NuGet con l'interfaccia della](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli)riga di comando di DotNet.

Per decidere quali .NET Framework usare come destinazione, vedere le [linee guida più recenti per la destinazione multipiattaforma](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).

## <a name="package-metadata"></a>Metadati dei pacchetti

I metadati sono un componente fondamentale di qualsiasi pacchetto NuGet. La qualità dei metadati può influenzare notevolmente l'individuabilità, l'usabilità e l'affidabilità del pacchetto.

In Visual Studio, la modalità consigliata per specificare i metadati del pacchetto consiste nel passare al progetto > proprietà [nome progetto] > pacchetto.

Gli elementi dei metadati del pacchetto possono essere [specificati anche direttamente nel file di progetto](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).

Di seguito è riportato un mapping di tabella che descrive gli elementi dei metadati del pacchetto disponibili:

| Nome proprietà di Visual Studio                   | [Nome file di progetto/proprietà MSBuild](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [Nome della proprietà NuSpec](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | Descrizione                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | Nome o identificatore del pacchetto.                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | Versione del pacchetto NuGet.                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | Elenco delimitato da virgole di autori di pacchetti, che spesso utilizzano il nome dell'utente o dell'organizzazione.                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | Descrizione del pacchetto.                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | Informazioni sul copyright per il pacchetto.                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | Espressione di licenza SPDX.       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | Percorso di un file di licenza personalizzato.                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | URL per la Home page del progetto.                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | Percorso del file di immagine dell'icona del pacchetto.                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | URL del repository da cui è stato compilato il pacchetto.                                                           |
| [`Repository type`](#repository-type-and-url) | [`RepositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | Tipo di repository a cui punta l'URL del repository (ad esempio "git").                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | Elenco di tag e parole chiave delimitati da spazi che descrivono il pacchetto. I tag vengono usati per la ricerca di pacchetti. |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | Descrizione delle modifiche apportate in questa versione del pacchetto.                                                 |

### <a name="package-id"></a>ID pacchetto

Se si pubblica un pacchetto completamente nuovo:

✔️ scegliere un ID pacchetto univoco e chiaramente differenziato dai pacchetti esistenti in NuGet.org.
> È possibile verificare se l'ID di un pacchetto è univoco e differenziabile eseguendo la ricerca dell'ID in NuGet.org o verificando che esista il collegamento seguente: https://www.nuget.org/packages/<package Name \> .

✔️ prendere in considerazione la scelta di un nome di pacchetto NuGet con un prefisso che soddisfi i [criteri di prenotazione del prefisso](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)di NuGet.
> Se si riserva l'ID prefisso per il pacchetto, sarà possibile ottenere il segno di spunta verificato: ![ immagine](media/Verified-check-mark.png)
> 
> Per altre informazioni, vedere la documentazione relativa alla [prenotazione del prefisso dell'ID pacchetto](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) .

### <a name="package-version"></a>Versione pacchetto

✔️ PROVARE a usare [SemVer](https://semver.org/) per la versione del pacchetto NuGet.
> Essenzialmente, ciò significa usare il formato Major. minor. patch [-prerelease].

✔️ pubblicare un pacchetto come pacchetto non [definitiva](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) se non è stabile o in anteprima.

Per informazioni più avanzate, vedere la [Guida al controllo delle versioni della libreria .NET](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) .

### <a name="authors"></a>Autori

✔️ usare il campo Author (autore) per il o il nome dell'organizzazione.
> Se, ad esempio, il nome utente di NuGet.org è "jdoe", l'uso di "Jane Doe" per il campo autore può aiutare gli utenti a riconoscerlo come autore. Se il nome utente NuGet.org dell'organizzazione è "ContosoToolkit", l'uso di "Contoso Corporation" può essere più riconoscibile e ispirare maggiore fiducia al consumatore.
### <a name="description"></a>Descrizione

✔️ includere una breve descrizione (fino a 4000 caratteri) per descrivere il pacchetto.
> Le descrizioni dei pacchetti sono uno dei campi più importanti emersi nella ricerca NuGet ed è probabilmente la prima cosa che i potenziali consumatori esaminano per determinare se un pacchetto è adatto.

### <a name="copyright"></a>Copyright

✔️ prendere in considerazione il copyright del pacchetto con "Copyright (c) <nome/azienda \> <anno \> ".
>Un avviso di copyright essenzialmente indica che non è possibile copiare il lavoro senza l'autorizzazione dell'utente. L'inclusione di un avviso sul copyright nel pacchetto è facile e non può causare danni.

Esempio: Copyright (c) Contoso 2020

### <a name="licensing"></a>Gestione delle licenze

✔️ [includere un'espressione di licenza o un file di licenza nel pacchetto](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Un progetto senza licenza viene impostato su [copyright esclusivo](https://choosealicense.com/no-permission/), ovvero non è stata concessa l'autorizzazione per l'utilizzo del progetto.

❌ Non utilizzare la `LicenseUrl` proprietà dei metadati deprecata.
> Questa operazione presenta ambiguità giuridica poiché le modifiche apportate alle licenze nell'URL verranno modificate in modo retroattivo per le versioni precedenti del pacchetto.

#### <a name="if-your-package-is-open-source"></a>Se il pacchetto è [Open Source](https://opensource.org/osd)

✔️ [scegliere una licenza open source](https://choosealicense.com/) per rendere disponibile l'origine del pacchetto.
> *"Le licenze open source sono licenze conformi alla definizione Open Source: in breve, consentono di usare, modificare e condividere il software liberamente".* -Iniziativa Open Source. Per ulteriori informazioni sul software open source e sull'iniziativa Open Source, vedere https://opensource.org/ .

✔️ CONSIGLIABILE [includere un'espressione di licenza nel pacchetto](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Le espressioni di licenza vengono rilevate più chiaramente e diventano più evidenti per i consumer se possono usare il pacchetto o se la licenza è cambiata. 
> [!Note]
> NuGet.org accetta solo le espressioni di licenza per le licenze approvate dall'iniziativa Open Source o dalla versione gratuita di Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Se il pacchetto non è open source

✔️ [includere un file di licenza nel pacchetto](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Qualsiasi file di licenza (. txt o. MD) può essere aggiunto al pacchetto, incluse le licenze non standard. 

### <a name="project-url"></a>URL progetto

✔️ CONSIDERARE l'inclusione di un collegamento a un progetto, un repository o un sito Web aziendale associato.
> Il sito del progetto deve avere tutti gli utenti che devono conoscere il pacchetto ed è probabile che gli utenti cercheranno la documentazione.

### <a name="icon"></a>Icona

✔️ CONSIGLIABILE [includere un'icona con il pacchetto](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) per distinguerlo visivamente. Si tratta di un'aggiunta relativamente piccola che può migliorare la percezione della qualità del pacchetto.
> Le icone possono essere specifiche dei singoli pacchetti o essere un logo del marchio.

✔️ usare un'immagine 128x128 e con uno sfondo trasparente (PNG) per la visualizzazione ottimale dei risultati.
> NuGet scala automaticamente l'immagine nel client in cui viene visualizzata.

❌ Non utilizzare la `IconUrl` proprietà dei metadati deprecata.

### <a name="repository-type-and-url"></a>Tipo di repository e URL

✔️ CONSIGLIABILE configurare il [collegamento all'origine](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) per aggiungere automaticamente i metadati del controllo del codice sorgente al pacchetto NuGet e semplificare il debug della libreria.
> Il collegamento all'origine aggiunge automaticamente `Repository URL` e `Repository Type` ai metadati del pacchetto. Viene inoltre aggiunto il commit specifico associato alla versione del pacchetto.

### <a name="tags"></a>Tag

✔️ includere diversi tag con termini chiave correlati al pacchetto per migliorare l'individuabilità.
> I tag vengono presi in considerazione nell'algoritmo di ricerca di NuGet. org e sono particolarmente utili per i termini che non sono inclusi nell'ID del pacchetto, ma sono rilevanti.

Ad esempio, se è stato pubblicato un pacchetto per la registrazione di stringhe nella console, includere: "log, log, console, String, output"

### <a name="release-notes"></a>Note sulla versione

✔️ CONSIGLIABILE includere le note sulla versione con ogni aggiornamento che descrive le modifiche apportate.
> Sebbene non esista un formato specifico necessario per le note sulla versione, è consigliabile includere:
>
> 1. Modifiche che causano un'interruzione
> 2. Nuove funzionalità
> 3. Correzioni di bug
> 
> Se si è già tenuta traccia delle note sulla versione o di un log delle modifiche nel repository, è anche possibile includere un collegamento al file pertinente.

## <a name="related-topics"></a>Argomenti correlati

- [Creare e pubblicare un pacchetto (interfaccia della riga di comando dotnet)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [Creare e pubblicare un pacchetto (Visual Studio)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
