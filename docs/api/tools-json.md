---
title: per individuare le versioni nuget.exe Tools.JSON
description: L'endpoint per
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2018
ms.locfileid: "40248355"
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
version  | stringa | sì      | Una stringa di SemVer 2.0.0
url      | stringa | sì      | Un URL assoluto per il download di questa versione di nuget.exe
Fase    | stringa | sì      | Una stringa di enum
caricato | stringa | sì      | Un timestamp di quando è stata resa disponibile la versione approssimativo

Gli elementi della matrice verranno ordinati in senso decrescente, SemVer 2.0.0. Questa garanzia è progettata per semplificare il carico di lavoro in un client cerca la versione più recente. 

Il `stage` proprietà indica la modalità vettect questa versione dello strumento. 

Fase              | Significato
------------------ | ------
EarlyAccessPreview | Non è ancora visibile sulla [pagina web di download](https://www.nuget.org/downloads) e deve essere convalidato dai partner
Rilasciata           | Disponibile nel sito di download, ma non è ancora consigliato per l'utilizzo di diffusa
ReleasedAndBlessed | Disponibile nel sito di download ed è consigliata per l'utilizzo

Un approccio semplice per avere la versione più recente, versione consigliata deve eseguire la prima versione nell'elenco che contiene il `stage` pari a `ReleasedAndBlessed`.

Il `NuGet.CommandLine` pacchetto in nuget.org in genere viene aggiornata solo con `ReleasedAndBlessed` versioni.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [tools-json.json](./_data/tools-json.json)]
