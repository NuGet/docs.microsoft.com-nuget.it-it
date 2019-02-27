---
title: per individuare le versioni nuget.exe Tools.JSON
description: L'endpoint per
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852533"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>per individuare le versioni nuget.exe Tools.JSON

Attualmente, esistono alcuni modi per ottenere la versione più recente di nuget.exe nel computer in modo gestibile tramite script. Ad esempio, è possibile scaricare ed estrarre il [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) pacchetti da nuget.org. Questo ha un livello di complessità perché sia richiede che sia già stato nuget.exe (per `nuget.exe install`) o è necessario decomprimere il pacchetto. nupkg usando uno strumento di decompressione di base e trovare binario interno.

Se hai già nuget.exe, è anche possibile usare `nuget.exe update -self`, ma anche è necessario disporre di una copia esistente di nuget.exe. Questo approccio anche si aggiorna alla versione più recente. Non consente l'uso di una versione specifica.

Il `tools.json` endpoint è disponibile per entrambi è stato risolto l'avvio automatico e di offrire il controllo della versione di nuget.exe scaricato. Ciò è utilizzabile negli ambienti CI/CD o script personalizzati per individuare e scaricare qualsiasi versione rilasciata di nuget.exe.

Il `tools.json` endpoint possono essere recuperate tramite una richiesta HTTP non autenticata (ad esempio `Invoke-WebRequest` in PowerShell o `wget`). Può essere analizzata usando un deserializzatore JSON né autenticate di download successivi nuget.exe che URL può anche essere recuperati tramite richieste HTTP.

L'endpoint può essere recuperato usando la `GET` metodo:

    GET https://dist.nuget.org/tools.json

Il [dello schema JSON](http://json-schema.org/) per l'endpoint è disponibile qui:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Risposta

La risposta è un documento JSON contenente tutte le versioni disponibili di nuget.exe.

L'oggetto JSON radice ha la proprietà seguente:

nome      | Tipo             | Obbligatorio
--------- | ---------------- | --------
nuget.exe | Matrice di oggetti | sì

Ogni oggetto di `nuget.exe` matrice presenta le proprietà seguenti:

nome     | Tipo   | Obbligatorio | Note
-------- | ------ | -------- | -----
version  | string | sì      | Una stringa di SemVer 2.0.0
url      | string | sì      | Un URL assoluto per il download di questa versione di nuget.exe
Fase    | string | sì      | Una stringa di enum
caricato | string | sì      | Un timestamp di ISO 8601 approssimativo di quando è stata resa disponibile la versione

Gli elementi della matrice verranno ordinati in senso decrescente, SemVer 2.0.0. Questa garanzia è progettata per ridurre il carico di lavoro di un client che interessata più alto numero di versione. Tuttavia, ciò significa che l'elenco non verrà ordinato in ordine cronologico. Ad esempio, se una versione principale precedente viene gestita in una data successiva rispetto a una versione principale successiva, questa versione servita non verrà visualizzato nella parte superiore dell'elenco. Se si desidera che la versione più recente rilasciata da *timestamp*, è sufficiente ordinare della matrice in base il `uploaded` stringa. Questo procedimento funziona perché il `uploaded` timestamp è espresso nel [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) formato che può essere ordinato in ordine cronologico con un ordinamento lessicografico (vale a dire un ordinamento semplice stringa).

Il `stage` proprietà indica la versione dello strumento esaminato come è. 

Fase              | Significato
------------------ | ------
EarlyAccessPreview | Non è ancora visibile sulla [pagina web di download](https://www.nuget.org/downloads) e deve essere convalidato dai partner
Rilasciata           | Disponibile nel sito di download, ma non è ancora consigliato per l'utilizzo di diffusa
ReleasedAndBlessed | Disponibile nel sito di download ed è consigliata per l'utilizzo

Un approccio semplice per avere la versione più recente, versione consigliata deve eseguire la prima versione nell'elenco che contiene il `stage` pari a `ReleasedAndBlessed`. Questo procedimento funziona perché le versioni sono ordinate in ordine di SemVer 2.0.0.

Il `NuGet.CommandLine` pacchetto in nuget.org in genere viene aggiornata solo con `ReleasedAndBlessed` versioni.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [tools-json.json](./_data/tools-json.json)]
