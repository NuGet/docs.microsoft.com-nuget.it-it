---
title: File Leggimi del pacchetto in NuGet.org
description: Spiegazione dettagliata del rendering dei file Readme in NuGet.org e delle operazioni da eseguire quando si verificano problemi.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: ac0e89c1f5ef9eb19c29646bcc76bcb0b460c5cd
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209943"
---
# <a name="package-readme-on-nugetorg"></a>File Leggimi del pacchetto in NuGet.org

[Includere un file leggimi nel pacchetto NuGet per](/nuget/reference/msbuild-targets#packagereadmefile) rendere i dettagli del pacchetto più completi e più informativi per gli utenti.

Questo è probabilmente uno dei primi elementi che gli utenti visualizzano quando visualizzano la pagina dei dettagli del pacchetto su NuGet.org ed è essenziale per fare una buona impressione.

> [!IMPORTANT]
> NuGet.org supporta solo i file Leggimi in [Markdown](https://daringfireball.net/projects/markdown/) e le immagini di un set limitato di domini. Vedere i [domini consentiti per le immagini e](#allowed-domains-for-images-and-badges) le funzionalità [markdown](#supported-markdown-features) supportate per assicurarsi che il file Leggimi venga eseguito correttamente in NuGet.org.

## <a name="what-should-my-readme-include"></a>Che cosa deve includere il file leggimi?

Prendere in considerazione l'inclusione degli elementi seguenti nel file Leggimi:
* Introduzione al pacchetto e alle funzioni: quali problemi risolve?
* Come iniziare a usare il pacchetto: sono presenti requisiti specifici?
* Collegamenti a una documentazione più completa, se non inclusa nel file Leggimi stesso.
* Almeno alcuni frammenti di codice/esempi o immagini di esempio.
* Dove e come lasciare commenti e suggerimenti, ad esempio un collegamento ai problemi del progetto, Twitter, bug tracker o un'altra piattaforma.
* Come contribuire, se applicabile.

Tenere presente che i file leggimi di alta qualità possono essere disponibili in un'ampia gamma di formati, forme e dimensioni. Se è già disponibile un pacchetto in NuGet.org, è probabile che nel repository sia già presente un o un altro file di documentazione che sarebbe un'ottima aggiunta alla pagina dei dettagli `readme.md` di NuGet.org.

## <a name="preview-your-readme"></a>Visualizzare in anteprima il file Leggimi

Per visualizzare in anteprima il file Leggimi prima che sia live su NuGet.org, caricare il pacchetto usando il portale Web del pacchetto [Upload in NuGet.org](/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) e scorrere verso il basso fino alla sezione "File Leggimi" dell'anteprima dei metadati. L'output dovrebbe essere simile al seguente:

![Anteprima del file Leggimi](media\readme-upload-preview.PNG)

Prendere in considerazione la possibilità di [](#allowed-domains-for-images-and-badges) esaminare e [](#supported-markdown-features) visualizzare in anteprima il file Leggimi per la conformità delle immagini e la formattazione supportata per assicurarsi che sia una buona prima impressione per i potenziali utenti. Per correggere gli errori nel file leggimi del pacchetto dopo che è stato pubblicato in NuGet.org, è necessario eseguire il push di una versione aggiornata del pacchetto con la correzione. Assicurarsi che tutto sia a posto in anticipo può far risparmiare il mal di testa lungo la strada.
## <a name="allowed-domains-for-images-and-badges"></a>Domini consentiti per immagini e notifiche

A causa di problemi di sicurezza e privacy, NuGet.org limita i domini da cui è possibile eseguire il rendering di immagini e notifiche agli host attendibili. 

NuGet.org consente il rendering di tutte le immagini, incluse le notifiche, dei domini attendibili seguenti:
* api.bintray.com
* api.codacy.com
* app.codacy.com
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
* cdn.jsdelivr.net
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* i.imgur.com
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Se si desidera aggiungere un altro dominio all'elenco degli [](https://github.com/NuGet/NuGetGallery/issues) elementi consentiti, è possibile determinare un problema che verrà esaminato dal team di progettazione per la conformità alla privacy e alla sicurezza. Le immagini con percorsi locali relativi e immagini ospitate da domini non supportati non verranno sottoposte a rendering e genereranno un avviso nella pagina di anteprima del file Leggimi e nella pagina dei dettagli del pacchetto visibile solo ai proprietari del pacchetto.

## <a name="supported-markdown-features"></a>Funzionalità di Markdown supportate
[Markdown è](https://daringfireball.net/projects/markdown/) un linguaggio di markup leggero con sintassi di formattazione testo normale. NuGet.org readmes supporta [Markdown](https://commonmark.org/) conforme a CommonMark tramite il [motore di analisi Markdig.](https://github.com/lunet-io/markdig)

NuGet.org supporta attualmente le funzionalità Markdown seguenti:
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

