---
title: Tools. JSON per l'individuazione delle versioni di NuGet. exe
description: Endpoint per
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611027"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>Tools. JSON per l'individuazione delle versioni di NuGet. exe

Attualmente, esistono diversi modi per ottenere la versione più recente di NuGet. exe nel computer in modo da poter eseguire lo script. Ad esempio, è possibile scaricare ed estrarre il pacchetto di [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) da NuGet.org. Questa operazione presenta una certa complessità poiché richiede che sia già presente NuGet. exe (per `nuget.exe install`) o che sia necessario decomprimere il file con estensione nupkg usando uno strumento di decompressione di base e trovare il file binario all'interno di.

Se si dispone già di NuGet. exe, è anche possibile utilizzare `nuget.exe update -self`, tuttavia è necessario disporre di una copia esistente di NuGet. exe. Questo approccio consente inoltre di aggiornare la versione più recente. Non consente l'uso di una versione specifica.

L'endpoint `tools.json` è disponibile sia per risolvere il problema di bootstrap che per fornire il controllo della versione di NuGet. exe scaricata. Questo può essere usato negli ambienti CI/CD o negli script personalizzati per individuare e scaricare qualsiasi versione rilasciata di NuGet. exe.

È possibile recuperare l'endpoint `tools.json` usando una richiesta HTTP non autenticata, ad esempio `Invoke-WebRequest` in PowerShell o `wget`. Può essere analizzato usando un deserializzatore JSON e gli URL di download di NuGet. exe successivi possono anche essere recuperati tramite richieste HTTP non autenticate.

L'endpoint può essere recuperato utilizzando il metodo `GET`:

    GET https://dist.nuget.org/tools.json

Lo [schema JSON](https://json-schema.org/) per l'endpoint è disponibile qui:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Risposta

La risposta è un documento JSON contenente tutte le versioni disponibili di NuGet. exe.

L'oggetto JSON radice presenta la proprietà seguente:

Name      | Digitare             | Richiesto
--------- | ---------------- | --------
nuget.exe | matrice di oggetti | sì

Ogni oggetto nella matrice `nuget.exe` presenta le proprietà seguenti:

Name     | Digitare   | Richiesto | Note
-------- | ------ | -------- | -----
version  | string | sì      | Stringa SemVer 2.0.0
url      | string | sì      | URL assoluto per il download di questa versione di NuGet. exe
Fase    | string | sì      | Stringa enum
caricato | string | sì      | Timestamp ISO 8601 approssimativo di quando è stata resa disponibile la versione

Gli elementi nella matrice verranno ordinati in ordine decrescente, SemVer 2.0.0. Questa garanzia è destinata a ridurre il carico di un client interessato al numero di versione più alto. Ciò significa tuttavia che l'elenco non è ordinato in ordine cronologico. Se, ad esempio, una versione principale inferiore viene gestita in una data successiva a una versione principale più elevata, la versione servita non verrà visualizzata nella parte superiore dell'elenco. Se si vuole che la versione più recente rilasciata da *timestamp*, è sufficiente ordinare la matrice in base alla stringa `uploaded`. Questa operazione funziona perché il timestamp del `uploaded` è nel formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , che può essere ordinato in ordine cronologico usando un ordinamento lessicografico, ovvero un ordinamento stringa semplice.

La proprietà `stage` indica il modo in cui la versione dello strumento è stata controllata. 

Fase              | Significato
------------------ | ------
EarlyAccessPreview | Non ancora visibile nella [pagina Web di download](https://www.nuget.org/downloads) e deve essere convalidato dai partner
Rilasciata           | Disponibile nel sito di download, ma non è ancora consigliato per un consumo di ampia diffusione
ReleasedAndBlessed | Disponibile nel sito di download ed è consigliato per l'utilizzo

Un approccio semplice per avere la versione più recente consigliata consiste nell'usare la prima versione dell'elenco con il valore `stage` `ReleasedAndBlessed`. Questa operazione funziona perché le versioni sono ordinate in base all'ordine di SemVer 2.0.0.

Il pacchetto di `NuGet.CommandLine` in nuget.org viene in genere aggiornato solo con `ReleasedAndBlessed` versioni.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [tools-json.json](./_data/tools-json.json)]
