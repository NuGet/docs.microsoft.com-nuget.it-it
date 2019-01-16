---
title: Metadati del pacchetto, NuGet API
description: L'URL di base di registrazione pacchetto consente il recupero dei metadati sui pacchetti.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 19a1f48164f65f1ff805e036e55abb110247aa72
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324864"
---
# <a name="package-metadata"></a>Metadati del pacchetto

È possibile recuperare i metadati relativi ai pacchetti disponibili in un'origine del pacchetto tramite l'API di NuGet V3. Questi metadati possono essere recuperati tramite il `RegistrationsBaseUrl` trovare la risorsa nella [indice del servizio](service-index.md).

La raccolta dei documenti in `RegistrationsBaseUrl` sono spesso chiamati "registrazioni per" o "registrazione BLOB". Il set di documenti in una singola `RegistrationsBaseUrl` è detto "hive" registrazione". Un hive registrazione contiene tutti i metadati relativi a ogni pacchetto disponibile su un'origine del pacchetto.

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di @type                     | Note
------------------------------- | -----
RegistrationsBaseUrl            | La versione iniziale
RegistrationsBaseUrl/3.0.0-beta | Alias di `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias di `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Risposte compresso con gzip
RegistrationsBaseUrl/3.6.0      | Include i pacchetti di SemVer 2.0.0

Questo rappresenta tre hive distinti registrazione disponibili per le diverse versioni di client.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Queste registrazioni non sono stati compressi (vale a dire usano un implicita `Content-Encoding: identity`). Sono pacchetti di SemVer 2.0.0 **esclusi** da questo hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Queste registrazioni vengono compressi mediante `Content-Encoding: gzip`. Sono pacchetti di SemVer 2.0.0 **esclusi** da questo hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Queste registrazioni vengono compressi mediante `Content-Encoding: gzip`. Sono pacchetti di SemVer 2.0.0 **inclusi** in questo hive.
Per altre informazioni su SemVer 2.0.0, vedere [supporto di SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore della `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valori. Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL disponibili il supporto di risorse di registrazione i metodi HTTP `GET` e `HEAD`.

## <a name="registration-index"></a>Indice di registrazione

I gruppi di risorse di registrazione del pacchetto dei metadati dall'ID del pacchetto. Non è possibile ottenere dati relativi a più di un ID del pacchetto alla volta. Questa risorsa non fornisce alcun modo per individuare gli ID di pacchetto. Invece il client si presuppone che conosce già l'ID pacchetto desiderato. I metadati disponibili relativi a ogni versione del pacchetto dipende dalla implementazione del server. I BLOB di registrazione pacchetto presentano la struttura gerarchica seguente:

- **Indice**: il punto di ingresso per i metadati del pacchetto, condivisi da tutti i pacchetti in un'origine con lo stesso ID di pacchetto.
- **Pagina**: un raggruppamento di versioni del pacchetto. Il numero di versioni del pacchetto in una pagina viene definito dall'implementazione del server.
- **Foglia**: un documento specifico a una versione singolo pacchetto.

L'URL dell'indice di registrazione è prevedibile e può essere determinato mediante il client ha un ID pacchetto e la risorsa di registrazione `@id` valore dall'indice del servizio. Gli URL per le pagine di registrazione e lascia vengono individuati tramite l'analisi dell'indice di registrazione.

### <a name="registration-pages-and-leaves"></a>Lascia e le pagine di registrazione

Sebbene non sia strettamente è obbligatorio per un'implementazione del server archiviare registrazione foglie nei documenti di pagina di registrazione separati, è consigliabile conservare la memoria lato client. Invece di all inlining registrazione lascia in corrispondenza dell'indice o immediatamente l'archiviazione foglie nei documenti di pagina, è consigliabile che l'implementazione del server definire alcune euristica per scegliere tra i due approcci in base al numero di versioni del pacchetto o lascia le dimensioni complessive del pacchetto.

L'archiviazione di tutte le versioni dei pacchetti (foglie) nel Salva indice registrazione sul numero di richieste HTTP necessaria per recuperare i metadati del pacchetto, ma significa che è necessario scaricare un documento più grande e deve essere allocata più memoria del client. D'altra parte, se l'implementazione del server archivia immediatamente registrazione lascia in documenti di una pagina separata, il client deve eseguire più richieste HTTP per ottenere le informazioni che necessarie.

L'euristica che usa nuget.org è come segue: se sono presenti 128 o più versioni di un pacchetto, le foglie di suddivisione in pagine di dimensioni 64. Se sono presenti versioni minore di 128, inline tutti lascia nell'indice della registrazione.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametri della richiesta

nome     | In     | Tipo    | Obbligatorio | Note
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | stringa  | sì      | L'ID del pacchetto minuscola

Il `LOWER_ID` valore è l'ID pacchetto desiderato minuscola usando le regole implementate da. Di NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (metodo).

### <a name="response"></a>Risposta

La risposta è un documento JSON che include un oggetto radice con le proprietà seguenti:

nome  | Tipo             | Obbligatorio | Note
----- | ---------------- | -------- | -----
count | numero intero          | sì      | Il numero di pagine di registrazione nell'indice
elementi | Matrice di oggetti | sì      | Matrice di pagine di registrazione

Ogni elemento dell'oggetto indice `items` matrice è un oggetto JSON che rappresenta una pagina di registrazione.

#### <a name="registration-page-object"></a>Oggetto pagina registrazione

L'oggetto pagina di registrazione trovato in corrispondenza dell'indice registrazione presenta le proprietà seguenti:

nome   | Tipo             | Obbligatorio | Note
------ | ---------------- | -------- | -----
@id    | stringa           | sì      | L'URL alla pagina di registrazione
count  | numero intero          | sì      | Il numero di registrazione lascia nella pagina
elementi  | Matrice di oggetti | No       | Matrice di foglie di registrazione e i relativi metadati associati
inferiore  | stringa           | sì      | La versione di SemVer 2.0.0 più bassa nella pagina (inclusiva)
Elemento padre | stringa           | No       | L'URL per l'indice di registrazione
superiore  | stringa           | sì      | La versione di SemVer 2.0.0 più alto nella pagina (inclusiva)

Il `lower` e `upper` nei limiti dell'oggetto page sono utili quando i metadati per una versione di pagina specifica sono necessari.
Questi limiti possono essere usati per recuperare la pagina di registrazione solo necessita. Le stringhe di versione rispettano [regole della versione di NuGet](../reference/package-versioning.md). Le stringhe di versione vengono normalizzate e non includono i metadati di compilazione. Come con tutte le versioni dell'ecosistema NuGet, confronto delle stringhe di versione viene implementato usando [regole di precedenza versione SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

Il `parent` proprietà verrà visualizzata solo se l'oggetto pagina di registrazione ha il `items` proprietà.

Se il `items` proprietà non è presente nell'oggetto pagina di registrazione, l'URL specificato nella `@id` deve essere usato per recuperare i metadati relativi a versioni dei singoli pacchetti. Il `items` matrice talvolta viene esclusa dall'oggetto pagina come ottimizzazione. Se il numero di versioni di un ID pacchetto singolo è molto grande, il documento di indice di registrazione sarà inutili al processo per un client che può interessare solo su una versione specifica o una gamma ristretta di versioni e di grandi dimensioni.

Si noti che se il `items` proprietà è presente, il `@id` proprietà non è necessario utilizzare, poiché tutti i dati di pagina è già impostato come inline nel `items` proprietà.

Ogni elemento dell'oggetto pagina `items` matrice è un oggetto JSON che rappresenta una foglia di registrazione e sono associati i metadati.

#### <a name="registration-leaf-object-in-a-page"></a>Oggetto di registrazione foglia in una pagina

L'oggetto di foglia registrazione trovato in una pagina di registrazione ha le proprietà seguenti:

nome           | Tipo   | Obbligatorio | Note
-------------- | ------ | -------- | -----
@id            | stringa | sì      | L'URL per la foglia di registrazione
catalogEntry   | object | sì      | La voce di catalogo che contiene i metadati del pacchetto
packageContent | stringa | sì      | L'URL per il contenuto del pacchetto (con estensione nupkg)

Ogni oggetto di registrazione foglia rappresenta i dati associati a una singolo pacchetto versione.

#### <a name="catalog-entry"></a>Voce di catalogo

Il `catalogEntry` proprietà nell'oggetto foglia registrazione presenta le proprietà seguenti:

nome                     | Tipo                       | Obbligatorio | Note
------------------------ | -------------------------- | -------- | -----
@id                      | stringa                     | sì      | L'URL usato per produrre l'oggetto documento
authors                  | stringa o matrice di stringhe | No       | 
dependencyGroups         | Matrice di oggetti           | No       | Le dipendenze del pacchetto, raggruppati per framework di destinazione
Descrizione              | stringa                     | No       | 
iconUrl                  | stringa                     | No       | 
ID                       | stringa                     | sì      | L'ID del pacchetto
licenseUrl               | stringa                     | No       |
licenseExpression        | stringa                     | No       | 
disponibili                   | boolean                    | No       | Deve essere considerata come se assente, elencate
minClientVersion         | stringa                     | No       | 
projectUrl               | stringa                     | No       | 
Pubblicato                | stringa                     | No       | Stringa che contiene un timestamp di ISO 8601 di quando il pacchetto è stato pubblicato
requireLicenseAcceptance | boolean                    | No       | 
summary                  | stringa                     | No       | 
tag                     | stringa o matrice di stringhe  | No       | 
title                    | stringa                     | No       | 
version                  | stringa                     | sì      | La stringa di versione completo dopo la normalizzazione

Il pacchetto `version` proprietà è la stringa di versione completo dopo la normalizzazione. Ciò significa che i dati di compilazione di SemVer 2.0.0 possono essere inclusi di seguito.

Il `dependencyGroups` proprietà è una matrice di oggetti che rappresentano le dipendenze del pacchetto, raggruppati per framework di destinazione. Se il pacchetto non ha dipendenze, il `dependencyGroups` proprietà manca, una matrice vuota, o `dependencies` proprietà di tutti i gruppi è vuoto o mancante.

Il valore della `licenseExpression` è conforme allo [sintassi delle espressioni di NuGet licenza](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Gruppo di dipendenze di pacchetto

Ogni oggetto gruppo dipendenza presenta le proprietà seguenti:

nome            | Tipo             | Obbligatorio | Note
--------------- | ---------------- | -------- | -----
targetFramework | stringa           | No       | Il framework di destinazione che queste dipendenze sono applicabili a
dependencies    | Matrice di oggetti | No       |

Il `targetFramework` stringa utilizza il formato implementato dalla libreria .NET di NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Se nessun `targetFramework` viene specificato, il gruppo di dipendenze si applica a tutti i framework di destinazione.

Il `dependencies` proprietà è una matrice di oggetti, ognuno dei quali rappresenta una dipendenza del pacchetto del pacchetto corrente.

#### <a name="package-dependency"></a>Dipendenza del pacchetto

Ogni dipendenza del pacchetto ha le proprietà seguenti:

nome         | Tipo   | Obbligatorio | Note
------------ | ------ | -------- | -----
ID           | stringa | sì      | L'ID della dipendenza del pacchetto
range        | object | No       | Consentiti [intervallo di versioni](../reference/package-versioning.md#version-ranges-and-wildcards) della dipendenza
registrazione | stringa | No       | L'URL per l'indice di registrazione per questa dipendenza

Se il `range` proprietà è esclusa o una stringa vuota, il client deve essere predefinito per l'intervallo di versioni `(, )`. Vale a dire, è consentita qualsiasi versione della dipendenza.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

In questo caso particolare, l'indice di registrazione ha la pagina di registrazione resa inline in modo che non esistono richieste aggiuntive necessarie per recuperare i metadati relativi a versioni dei pacchetti singoli.

## <a name="registration-page"></a>Pagina di registrazione

La pagina di registrazione contiene le foglie di registrazione. L'URL per recuperare una pagina di registrazione è determinato dal `@id` proprietà nel [oggetto pagina registrazione](#registration-page-object) indicato in precedenza.

Quando la `items` matrice non viene fornita nell'indice di registrazione, una richiesta GET HTTP richiesta del `@id` valore verrà restituito un documento JSON che dispone di un oggetto come elemento principale. L'oggetto presenta le proprietà seguenti:

nome   | Tipo             | Obbligatorio | Note
------ | ---------------- | -------- | -----
@id    | stringa           | sì      | L'URL alla pagina di registrazione
count  | numero intero          | sì      | Il numero di registrazione lascia nella pagina
elementi  | Matrice di oggetti | sì      | Matrice di foglie di registrazione e i relativi metadati associati
inferiore  | stringa           | sì      | La versione di SemVer 2.0.0 più bassa nella pagina (inclusiva)
Elemento padre | stringa           | sì      | L'URL per l'indice di registrazione
superiore  | stringa           | sì      | La versione di SemVer 2.0.0 più alto nella pagina (inclusiva)

La forma degli oggetti foglia registrazione è uguale a quello dell'indice di registrazione [sopra](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Foglia di registrazione

La foglia di registrazione contiene informazioni su un ID di pacchetto specifico e una versione. I metadati sulla versione specifica potrebbero non essere disponibili in questo documento. I metadati del pacchetto devono essere recuperati dal [indice registrazione](#registration-index) o nella [pagina di registrazione](#registration-page) (che viene individuato tramite l'indice di registrazione).

L'URL per recuperare una foglia di registrazione viene ottenuto dal `@id` proprietà di un oggetto foglia di registrazione in un indice di registrazione o pagina di registrazione.

La foglia di registrazione è un documento JSON con un oggetto di primo livello con le proprietà seguenti:

nome           | Tipo    | Obbligatorio | Note
-------------- | ------- | -------- | -----
@id            | stringa  | sì      | L'URL per la foglia di registrazione
catalogEntry   | stringa  | No       | L'URL per la voce di catalogo che ha prodotto questi foglia
disponibili         | boolean | No       | Deve essere considerata come se assente, elencate
packageContent | stringa  | No       | L'URL per il contenuto del pacchetto (con estensione nupkg)
Pubblicato      | stringa  | No       | Stringa che contiene un timestamp di ISO 8601 di quando il pacchetto è stato pubblicato
registrazione   | stringa  | No       | L'URL per l'indice di registrazione

> [!Note]
> In nuget.org, il `published` valore è impostato su anni 1900 quando il pacchetto è incluso nell'elenco.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
