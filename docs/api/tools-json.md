---
title: tools.json per individuare le versioni di nuget.exe
description: Endpoint per
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773824"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>tools.json per individuare le versioni di nuget.exe

Attualmente, esistono diversi modi per ottenere la versione più recente di nuget.exe nel computer in modo da poter eseguire lo script. Ad esempio, è possibile scaricare ed estrarre il [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) pacchetto da NuGet.org. Questa operazione presenta una certa complessità poiché richiede che sia già presente nuget.exe (per `nuget.exe install` ) o che sia necessario decomprimere il file con estensione nupkg usando uno strumento di decompressione di base e trovare il file binario all'interno di.

Se si dispone già di nuget.exe, è anche possibile utilizzare `nuget.exe update -self` , tuttavia è necessario disporre di una copia di nuget.exe esistente. Questo approccio consente inoltre di aggiornare la versione più recente. Non consente l'uso di una versione specifica.

L' `tools.json` endpoint è disponibile sia per risolvere il problema di bootstrap che per consentire il controllo della versione di nuget.exe scaricata. Questo può essere usato negli ambienti CI/CD o negli script personalizzati per individuare e scaricare qualsiasi versione rilasciata di nuget.exe.

L' `tools.json` endpoint può essere recuperato usando una richiesta HTTP non autenticata, ad esempio `Invoke-WebRequest` in PowerShell o `wget` . Può essere analizzato usando un deserializzatore JSON e gli URL di download nuget.exe successivi possono anche essere recuperati tramite richieste HTTP non autenticate.

L'endpoint può essere recuperato utilizzando il `GET` Metodo:

```
GET https://dist.nuget.org/tools.json
```

Lo [schema JSON](https://json-schema.org/) per l'endpoint è disponibile qui:

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>Risposta

La risposta è un documento JSON contenente tutte le versioni disponibili di nuget.exe.

L'oggetto JSON radice presenta la proprietà seguente:

Nome      | Type             | Necessario
--------- | ---------------- | --------
nuget.exe | matrice di oggetti | sì

Ogni oggetto nella `nuget.exe` matrice presenta le proprietà seguenti:

Nome     | Type   | Necessario | Note
-------- | ------ | -------- | -----
version  | string | sì      | Stringa SemVer 2.0.0
url      | string | sì      | URL assoluto per il download di questa versione di nuget.exe
fase    | string | sì      | Stringa enum
caricato | string | sì      | Timestamp ISO 8601 approssimativo di quando è stata resa disponibile la versione

Gli elementi nella matrice verranno ordinati in ordine decrescente, SemVer 2.0.0. Questa garanzia è destinata a ridurre il carico di un client interessato al numero di versione più alto. Ciò significa tuttavia che l'elenco non è ordinato in ordine cronologico. Se, ad esempio, una versione principale inferiore viene gestita in una data successiva a una versione principale più elevata, la versione servita non verrà visualizzata nella parte superiore dell'elenco. Se si vuole che la versione più recente rilasciata da *timestamp*, è sufficiente ordinare la matrice in base alla `uploaded` stringa. Questa operazione funziona perché il `uploaded` timestamp è nel formato [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) , che può essere ordinato in ordine cronologico usando un ordinamento lessicografico, ovvero un ordinamento stringa semplice.

La `stage` proprietà indica il modo in cui la versione dello strumento è stata controllata. 

Fase              | Significato
------------------ | ------
EarlyAccessPreview | Non ancora visibile nella [pagina Web di download](https://www.nuget.org/downloads) e deve essere convalidato dai partner
Rilasciata           | Disponibile nel sito di download, ma non è ancora consigliato per un consumo di ampia diffusione
ReleasedAndBlessed | Disponibile nel sito di download ed è consigliato per l'utilizzo

Un approccio semplice per avere la versione più recente consigliata consiste nell'usare la prima versione dell'elenco con il `stage` valore `ReleasedAndBlessed` . Questa operazione funziona perché le versioni sono ordinate in base all'ordine di SemVer 2.0.0.

Il `NuGet.CommandLine` pacchetto in NuGet.org viene in genere aggiornato solo con le `ReleasedAndBlessed` versioni.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [tools-json.json](./_data/tools-json.json)]
