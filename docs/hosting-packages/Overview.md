---
title: Panoramica dell'hosting dei feed NuGet
description: Panoramica delle opzioni per l'hosting dei feed o delle raccolte di pacchetti NuGet localmente o in remoto.
author: JonDouglas
ms.author: jodou
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 1b7bad6bcd897b746ea9eb6e89b80a88ee5e891a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774053"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hosting dei feed NuGet

Invece di rendere i pacchetti pubblicamente disponibili, potrebbe essere necessario rilasciarli solo per un pubblico limitato, ad esempio un'organizzazione o un gruppo di lavoro. Inoltre, per alcune aziende potrebbe essere necessario limitare le librerie di terze parti utilizzabili dagli sviluppatori, vincolandoli ad attingere a un'origine pacchetto limitata anziché a nuget.org.

Per tutti questi scopi, NuGet supporta l'impostazione di origini pacchetto private secondo le modalità seguenti:

- Feed locale: i pacchetti vengono semplicemente inseriti in una condivisione file di rete appropriata, preferibilmente usando `nuget init` e `nuget add` per creare una struttura di cartelle gerarchica (NuGet 3.3+). Per maggiori dettagli, vedere [Feed locali](../hosting-packages/local-feeds.md).
- NuGet.Server: i pacchetti vengono resi disponibili tramite un server HTTP locale. Per maggiori dettagli, vedere [NuGet.Server](../hosting-packages/nuget-server.md).
- Raccolta NuGet: i pacchetti sono ospitati in un server Internet tramite il [progetto della raccolta NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). La raccolta NuGet fornisce la gestione degli utenti e funzionalità quali un'interfaccia utente Web completa che consente la ricerca e l'esplorazione dei pacchetti dall'interno del browser, analogamente a nuget.org.

Sono disponibili anche diversi altri prodotti di hosting NuGet, ad esempio [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) e il [Registro dei pacchetti GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) che supportano i feed privati remoti. Di seguito è riportato un elenco di tali prodotti:

- [Artifactory](https://www.jfrog.com/artifactory/) di JFrog
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), disponibile anche in Team Foundation Server 2017 e versioni successive.
- [BaGet](https://github.com/loic-sharma/BaGet), un'implementazione open source di NuGet Server V3 basata su ASP.NET Core
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), una soluzione SaaS di gestione dei pacchetti completamente gestita
- [Registro dei pacchetti GitHub](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), un'implementazione open source di NuGet Server V2 in esecuzione su Kestrel in Docker
- [MyGet](https://myget.org)
- [OSS del repository Nexus](https://www.sonatype.com/nexus-repository-oss) da Sonatype.
- [NuGet Server (Open Source)](https://github.com/svenkle/nuget-server), un'implementazione open source simile a NuGet Server di Inedo
- [NuGet Server](http://nugetserver.net/), un progetto di community di Inedo
- [ProGet](https://inedo.com/proget) di Inedo
- [Sleet](https://github.com/emgarten/sleet), un generatore di feed statico di NuGet V3 open source
- [TeamCity](https://www.jetbrains.com/teamcity/) di JetBrains

Indipendentemente dalla modalità di hosting, i pacchetti diventano accessibili una volta aggiunti all'elenco delle origini disponibili in `NuGet.Config`. Questa operazione può essere eseguita in Visual Studio come descritto nella sezione [Package Sources](../consume-packages/install-use-packages-visual-studio.md#package-sources) (Origini dei pacchetti) o dalla riga di comando tramite [`nuget sources`](../reference/cli-reference/cli-ref-sources.md). Il percorso di un'origine può essere un nome di percorso di una cartella locale, un nome di rete o un URL.
