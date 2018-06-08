---
title: Panoramica dell'hosting dei feed NuGet
description: Panoramica delle opzioni per l'hosting dei feed o delle raccolte di pacchetti NuGet localmente o in remoto.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 48ebddb26aa6c236609691e099a82db80075944e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818425"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hosting dei feed NuGet

Invece di rendere i pacchetti pubblicamente disponibili, potrebbe essere necessario rilasciarli solo per un pubblico limitato, ad esempio un'organizzazione o un gruppo di lavoro. Inoltre, per alcune aziende potrebbe essere necessario limitare le librerie di terze parti utilizzabili dagli sviluppatori, vincolandoli ad attingere a un'origine pacchetto limitata anziché a nuget.org.

Per tutti questi scopi, NuGet supporta l'impostazione di origini pacchetto private secondo le modalità seguenti:

- Feed locale: i pacchetti vengono semplicemente inseriti in una condivisione file di rete appropriata, preferibilmente usando `nuget init` e `nuget add` per creare una struttura di cartelle gerarchica (NuGet 3.3+). Per maggiori dettagli, vedere [Feed locali](../hosting-packages/local-feeds.md).
- NuGet.Server: i pacchetti vengono resi disponibili tramite un server HTTP locale. Per maggiori dettagli, vedere [NuGet.Server](../hosting-packages/nuget-server.md).
- Raccolta NuGet: i pacchetti sono ospitati in un server Internet tramite il [progetto della raccolta NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). La raccolta NuGet fornisce la gestione degli utenti e funzionalità quali un'interfaccia utente Web completa che consente la ricerca e l'esplorazione dei pacchetti dall'interno del browser, analogamente a nuget.org.

Sono inoltre disponibili diversi altri prodotti di hosting NuGet che supportano feed privati remoti, tra cui:

- [Gestione pacchetti di Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish), anche disponibile in Team Foundation Server 2017 e versioni successive.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) di Inedo
- [NuGet Server](http://nugetserver.net/), un progetto di community di Inedo
- [NuGet Server (Open Source)](http://nuget-server.net), un'implementazione open source simile a NuGet Server di Inedo
- [Artifactory](https://www.jfrog.com/artifactory/) di JFrog
- [Nexus](http://www.sonatype.org/nexus/) di Sonatype
- [TeamCity](https://www.jetbrains.com/teamcity/) di JetBrains

Indipendentemente dalla modalità di hosting, i pacchetti diventano accessibili una volta aggiunti all'elenco delle origini disponibili in `NuGet.Config`. Questa operazione può essere eseguita in Visual Studio come descritto nella sezione [Package Sources](../tools/package-manager-ui.md#package-sources) (Origini dei pacchetti) o dalla riga di comando tramite [`nuget sources`](../tools/cli-ref-sources.md). Il percorso di un'origine può essere un nome di percorso di una cartella locale, un nome di rete o un URL.
