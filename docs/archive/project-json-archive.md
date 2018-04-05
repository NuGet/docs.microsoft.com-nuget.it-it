---
title: Contenuto dell'archivio project.json NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/17/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Varie parti del contenuto di project.json rimosse da altre aree della documentazione di NuGet.
keywords: File project.json di NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 16361fe16d8ecc7064af4b6d636435a31a5663dc
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-archive"></a>archivio project.json

Il formato di gestione `project.json` è stato introdotto con NuGet 3.x e usato per determinati tipi di progetto. È stato deprecato in seguito all'introduzione del formato PackageReference, con il quale le dipendenze vengono elencate direttamente in un file di progetto.

Vedere anche:

- [Schema di project.json](project-json.md)
- [project.json impact on package authors](project-json-impact.md) (Impatto di project.json sugli autori di pacchetti)
- [project.json e UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>Formato di gestione project.json

*Originariamente in [Ripristino di pacchetti](../what-is-nuget.md).*

Nell'elenco dei formati di gestione:

- [`project.json`](project-json.md): *(deprecato)* File JSON che gestisce un elenco delle dipendenze del progetto con un grafico dei pacchetti complessivo in un file associato, `project.lock.json`. Questo formato è deprecato a favore di PackageReference.

## <a name="nuget-restore-on-mono"></a>nuget restore su Mono

*Originariamente in [Installare gli strumenti client di NuGet](../install-nuget-client-tools.md).*

Funziona con `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Vincolo delle versioni dei pacchetti con il ripristino

*Originariamente in [Ripristino di pacchetti](../consume-packages/package-restore.md#constraining-package-versions-with-restore).*

- `project.json`: specificare un intervallo di versioni direttamente con il numero di versione della dipendenza. Ad esempio:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>Comandi dell'interfaccia della riga di comando di NuGet

- `nuget install` non funziona con `project.json`.
- `nuget restore`: con i progetti che usano `project.json`, genera un file `project.lock.json` e un file `<project>.nuget.props`, all'occorrenza. (Entrambi i file possono essere omessi dal controllo del codice sorgente). L'argomento `<projectPath>` può puntare a un file `project.json`, con un comportamento uguale a puntare a `packages.config` o un file di progetto. Nell'ordine di priorità per le cartelle dei pacchetti, la ricerca viene prima eseguita in `%userprofile%\.nuget\packages` quando si usa `project.json`.
- `nuget update`: in Mono questo comando non funziona con i progetti che usano `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>Risoluzione delle dipendenze con PackageReference

*Originariamente in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Il comportamento di PackageReference si applica anche a `project.json`. Il ripristino NuGet scrive il grafico dipendenze in un file denominato `project.lock.json` insieme a `project.json`.

## <a name="managing-dependency-assets"></a>Gestione degli asset delle dipendenze

*Originariamente in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Quando si usa il formato `project.json`, è possibile controllare quali asset delle dipendenze vengono inseriti nel progetto di primo livello. Per informazioni dettagliate, vedere [project.json](project-json.md).

## <a name="excluding-references"></a>Esclusione dei riferimenti

*Originariamente in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: aggiungere `"exclude" : "all"` nella dipendenza per il pacchetto C (PackageC):

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Risoluzione degli errori dei pacchetti incompatibili

*Originariamente in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Un ulteriore metodo per la risoluzione degli errori:

- **Non consigliato**: come soluzione temporanea mentre si collabora con l'autore del pacchetto, i progetti che hanno come destinazione `netcore`, `netstandard` e `netcoreapp` possono indicare altri framework come compatibili, consentendo pertanto di usare i pacchetti che hanno come destinazione questi altri framework. Vedere la [sezione Imports di project.json](project-json.md#imports) e la [sezione PackageTargetFallback delle destinazioni di ripristino di MSBuild](../reference/msbuild-targets.md#packagetargetfallback). Ciò può causare comportamenti imprevisti, pertanto ancora una volta è consigliabile risolvere le incompatibilità dei pacchetti collaborando con l'autore del pacchetto alla realizzazione di un aggiornamento.

## <a name="target-frameworks"></a>Framework di destinazione

*Originariamente in [Framework di destinazione](../reference/target-frameworks.md).*

- [project.json](project-json.md): il nodo `frameworks` specifica le versioni del framework per le quali può essere compilato il progetto.

## <a name="creating-a-package"></a>Creazione di un pacchetto

*Originariamente in [Creazione di un pacchetto](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Impostazione di un tipo di pacchetto

Con .NET Core 1.x, quando viene installato un pacchetto DotnetCliTool, Visual Studio inserisce il pacchetto nel nodo `tools` di `project.json` invece che nel nodo `dependencies`.

I tipi di pacchetto vengono impostati in `project.json`.

- `project.json`: indica il tipo di pacchetto in un codice json della proprietà `packOptions.packageType`:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>Aggiunta di destinazioni e proprietà per MSBuild

*Originariamente in [Creare pacchetti NuGet di .NET Standard con Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*

Quando si usa `project.json`, le destinazioni non vengono aggiunte al progetto, ma vengono rese disponibili tramite `project.lock.json`.

### <a name="package-versioning"></a>Controllo delle versioni dei pacchetti

*Originariamente in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md).*

Quando si usa il formato `project.json`, NuGet supporta anche l'uso di una notazione con caratteri jolly, \*, per le parti del numero suffisso per versione principale, secondaria, patch e non definitiva.

### <a name="nugetconfig-reference"></a>Informazioni di riferimento su NuGet.config

*Originariamente in [Informazioni di riferimento su NuGet.config](../reference/nuget-config-file.md).*

`globalPackagesFolder` si applica solo a `project.json`. (Aggiunta di una nota: si applica anche a PackageReference.)

### <a name="nuspec-file-reference"></a>Informazioni di riferimento sul file .nuspec

*Originariamente in [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md).*

L'elemento `<contentFiles>` viene usato al posto di `<files>` con `project.json`.

### <a name="package-manager-options-control"></a>Controllo delle opzioni di Gestione pacchetti

*Originariamente in [Package Manager UI reference](../tools/package-manager-ui.md) (Informazioni di riferimento sull'interfaccia utente di Gestione pacchetti).*

I progetti che usano il formato di gestione `project.json` mostrano solo l'opzione **Visualizza finestra di anteprima**.

### <a name="visual-studio-templates"></a>Modelli di Visual Studio

*Originariamente in [Pacchetti NuGet nei modelli di Visual Studio](../visual-studio-extensibility/visual-studio-templates.md).*

Procedure consigliate: i modelli non includono un file `project.json` e non includono riferimenti o contenuto che verrebbero aggiunti durante l'installazione di pacchetti NuGet.