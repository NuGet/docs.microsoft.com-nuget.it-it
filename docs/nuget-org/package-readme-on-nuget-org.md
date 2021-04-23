---
title: File Leggimi del pacchetto NuGet.org
description: Spiegazione dettagliata del rendering dei file Readme NuGet.org e delle operazioni da eseguire quando si verificano problemi.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902248"
---
# <a name="package-readme-on-nugetorg"></a>File Leggimi del pacchetto NuGet.org

[Includere un file Leggimi nel pacchetto NuGet per](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) rendere i dettagli del pacchetto più completi e più informativi per gli utenti.

Questo è probabilmente uno dei primi elementi che gli utenti visualizzano quando visualizzano la pagina dei dettagli del pacchetto NuGet.org ed è essenziale per fare una buona impressione.

> [!IMPORTANT]
> NuGet.org supporta solo file Leggimi in [Markdown](https://daringfireball.net/projects/markdown/) e immagini da un set limitato di domini. Vedere i [domini consentiti per le immagini e](#allowed-domains-for-images-and-badges) le funzionalità [markdown](#supported-markdown-features) supportate per assicurarsi che il rendering del file Leggimi venga eseguito correttamente NuGet.org.

## <a name="what-should-my-readme-include"></a>Cosa deve includere il file Leggimi?

È consigliabile includere gli elementi seguenti nel file Leggimi:
* Introduzione a che cos'è e cosa fa il pacchetto, quali problemi risolve?
* Come iniziare a usare il pacchetto: esistono requisiti specifici?
* Collegamenti a una documentazione più completa, se non inclusa nel file Leggimi stesso.
* Almeno alcuni frammenti di codice/esempi o immagini di esempio.
* Dove e come lasciare commenti e suggerimenti, ad esempio un collegamento ai problemi del progetto, Twitter, lo tracker di bug o un'altra piattaforma.
* Come contribuire, se applicabile.

Tenere presente che i file leggimi di alta qualità possono essere disponibili in un'ampia gamma di formati, forme e dimensioni. Se in NuGet.org è già disponibile un pacchetto, è probabile che nel repository sia già presente un file di documentazione o un altro file che rappresenta un'ottima aggiunta alla pagina dei dettagli `readme.md` NuGet.org.

## <a name="preview-your-readme"></a>Visualizzare in anteprima il file Leggimi

Per visualizzare in anteprima il file Leggimi prima che sia live in NuGet.org, caricare il pacchetto usando il portale Web carica pacchetto [in NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) e scorrere verso il basso fino alla sezione "File Leggimi" dell'anteprima dei metadati. L'output dovrebbe essere simile al seguente:

![Anteprima file Leggimi](media\readme-upload-preview.PNG)

Prendere in considerazione la possibilità di [](#allowed-domains-for-images-and-badges) esaminare e [](#supported-markdown-features) visualizzare in anteprima il file Leggimi per la conformità delle immagini e la formattazione supportata per assicurarsi che sia una buona prima impressione per i potenziali utenti. Per correggere gli errori nel file leggimi del pacchetto dopo che è stato pubblicato NuGet.org, è necessario eseguire il push di una versione aggiornata del pacchetto con la correzione. Assicurarsi che tutto sia a posto in anticipo può far risparmiare il mal di testa lungo la strada.
## <a name="allowed-domains-for-images-and-badges"></a>Domini consentiti per immagini e notifiche

A causa di problemi di sicurezza e privacy, NuGet.org i domini da cui è possibile eseguire il rendering di immagini e notifiche agli host attendibili. 

NuGet.org il rendering di tutte le immagini, incluse le notifiche, dei domini attendibili seguenti:
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Se si desidera aggiungere un altro dominio all'elenco degli [](https://github.com/NuGet/NuGetGallery/issues) elementi consentiti, è possibile determinare un problema che verrà esaminato dal team tecnico per la conformità alla privacy e alla sicurezza. Le immagini con percorsi locali relativi e le immagini ospitate da domini non supportati non verranno visualizzate e genereranno un avviso nella pagina di anteprima del file Leggimi e nella pagina dei dettagli del pacchetto visibile solo ai proprietari del pacchetto.

## <a name="supported-markdown-features"></a>Funzionalità markdown supportate
[Markdown è](https://daringfireball.net/projects/markdown/) un linguaggio di markup leggero con sintassi di formattazione del testo normale. NuGet.org readmes supportano Markdown conforme a [CommonMark](https://commonmark.org/) tramite il [motore di analisi Markdig.](https://github.com/lunet-io/markdig)

NuGet.org attualmente supporta le funzionalità Markdown seguenti:
* [Intestazioni](https://spec.commonmark.org/0.29/#atx-headings)
* [Immagini](https://spec.commonmark.org/0.29/#images)
* [Enfasi aggiuntiva](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Elenchi](https://spec.commonmark.org/0.29/#lists)
* [Collegamenti](https://spec.commonmark.org/0.29/#links)
* [Citazioni](https://spec.commonmark.org/0.29/#block-quotes)
* [Escape barra rovesciata](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Intervalli di codice](https://spec.commonmark.org/0.29/#code-spans)
* [Elenchi di attività](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tabelle](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emoji](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Collegamenti automatici](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

